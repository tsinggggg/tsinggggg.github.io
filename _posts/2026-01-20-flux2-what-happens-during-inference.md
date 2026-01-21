---
layout: post
title: "Flux 2: What happens during inference[WIP]"
date: 2026-01-20
tags: [diffusion]
---


This is a brief introduction of Flux 2 at inference time, as an illustration of how modern day image generation AI works.

## Inputs to the inference method

Here is a simple input payload to the inference method of a diffusion model, mainly containing a text prompt.

```python
    prompt = """Realistic macro photograph of a hermit crab using a soda can as its shell, partially emerging from the can, 
    captured with sharp detail and natural colors, on a sunlit beach with soft shadows and a shallow depth of field, 
    with blurred ocean waves in the background. The can has the text `BFL Diffusers` on it and it has a color gradient 
    that start with #FF5733 at the top and transitions to #33FF57 at the bottom."""
    image = pipe(
        prompt=prompt,
        generator=torch.Generator(device=device).manual_seed(42),
        num_inference_steps=1,
        guidance_scale=4,
    )
```

## Text prompt encoding

The first computational heavy step is converting text prompt into numeric representation through a text encoder model.

```python
        prompt_embeds, text_ids = self.encode_prompt(
            prompt=prompt,
            prompt_embeds=prompt_embeds,
            device=device,
            num_images_per_prompt=num_images_per_prompt,
            max_sequence_length=max_sequence_length,
            text_encoder_out_layers=text_encoder_out_layers,
        )
```

It's an interesting change in Flux 2 compared to previous versions or a lot of other diffusion models that the text encoder is 
no longer one or more CLIP style encoders but rather a decoder style LLM. To be specific, here the model used is a Mistral Small 3.1 model.

```python
	# Forward pass through the model
        output = text_encoder(
            input_ids=input_ids,
            attention_mask=attention_mask,
            output_hidden_states=True,
            use_cache=False,
        )
```

First, the text prompt will be tokenized then be forward passed through the layers. Here the hidden states are what creates 
the final text embedding for the prompt. This corresponds to the previous code block where we can see a 
`text_encoder_out_layers` is passed to the `encode_prompt` method. For Flux2, we'll be taking hidden representations from 
layers `10, 20, 30` of the text encoder. Since the hidden representation has a size of 5120 and those from 3 layers will be 
used(concatenated, to be exact),

```python
text_encoder.config.get_text_config().to_dict()['hidden_size']
5120
```

the final prompt embedding will be a tensor of size

```python
prompt_embeds.size()
torch.Size([1, 512, 15360])
```

where `15360 = 3 * 5120`.

Another artifact generated along with the prompt embedding is a tensor `text_ids` of size 

```python
text_ids.size()
torch.Size([1, 512, 4])
```

which will be the "positional embedding" of the prompt tokens. The `4` represents dimensions of time, height, width and 
position in prompt string, where the first 3 dimensions is just 0.

## Size of generated images

By default, the generated images have size of `1024 * 1024`

```python
        height = height or self.default_sample_size * self.vae_scale_factor
        width = width or self.default_sample_size * self.vae_scale_factor
```

where `default_sample_size` is 128 and then scaled 8 times by `vae_scale_factor`. This is because like most diffusion models
since the first version of Stable Diffusion model, diffusion happens at a latent space where latent shape is smaller than 
the shape of the final image generated; and a VAE is responsible for projecting latents back to the space of images. This 
allows diffusion models to operate with a smaller data size so the whole pipeline needs less compute.