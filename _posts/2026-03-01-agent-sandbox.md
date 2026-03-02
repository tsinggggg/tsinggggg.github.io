---
layout: post
title: "Agent Sandbox"
date: 2026-03-01
tags: [agent]
---


This is a list of available sandbox applications for agents.

## [Boxlite](https://github.com/boxlite-ai/boxlite)

Boxes retain packages, files, and environment across stop/restart. No rebuilding on every interaction.


## [opensandbox](https://github.com/alibaba/OpenSandbox)

OpenSandbox Kubernetes Controller is a Kubernetes operator that manages sandbox environments through custom resources. It provides automated sandbox lifecycle management, resource pooling for fast provisioning, batch sandbox creation, and optional task orchestration capabilities in Kubernetes clusters.

## [Pydantic's Monty](https://github.com/pydantic/monty)
Pros:
- Be snapshotted to bytes at external function calls, meaning you can store the interpreter state in a file or database, and resume later
- Startup extremely fast (<1μs to go from code to execution result), and has runtime performance that is similar to CPython (generally between 5x faster and 5x slower)
- Collect stdout and stderr and return it to the caller

Cons:
- Run a reasonable subset of Python code

## [docker sandbox](https://www.docker.com/products/docker-sandboxes/)

references:
- https://www.docker.com/blog/docker-sandboxes-run-claude-code-and-other-coding-agents-unsupervised-but-safely/

Features:

- Each agent runs inside a dedicated microVM
- Only your project workspace is mounted into the sandbox
- Agents can install system packages, run services, and modify files

## [modal](https://modal.com/)

reference: https://modal.com/products/sandboxes

- Modal’s container stack spins up sandboxes in less than a second.
- Instantly autoscale to 50,000+ sandboxes during peak demand.

## [runloop](https://runloop.ai/)

reference: https://docs.runloop.ai/docs/devboxes/overview

- Super fast execute times: Startup to running your first command takes a few seconds.
- Stateful or stateless: For short-running tasks, you can start a Devbox in seconds, perform arbitrary work and then throw away the box. For long-running tasks, take advantage of snapshot, suspend and resume operations to control the lifecycle of your devbox using simple API calls.

## [daytona](https://www.daytona.io)
- Daytona lets you spin up sandboxes in milliseconds and shut them down just as fast.
- Sandboxes run on isolated, customer-managed compute, in your cloud or on-prem. Daytona provides the control plane. No shared compute. No cross-tenant risk.

## [cloudflare sandbox](https://developers.cloudflare.com/sandbox/)
- streaming output support
- Read, write, and manipulate files in the sandbox filesystem
- Expose HTTP services running in your sandbox with automatically generated preview URLs
- Execute Python and JavaScript code with rich outputs including charts, tables, and images. Maintain persistent state between executions for AI-generated code and interactive workflows.


## [e2b sandbox](https://e2b.dev/)

- The E2B Sandboxes in the same region as the client start in 80 ms.
- E2B works anywhere you do. In your AWS, GCP, or Azure account, or your VPC.

## [fly machines](https://fly.io/machines)
- Lightweight VMs that start and stop in milliseconds
- Autoscaling and pay-as-you-go pricing

## [vercel sandbox](https://vercel.com/docs/vercel-sandbox)

## [firecracker microvm](https://firecracker-microvm.github.io/)

## [anthropic sandbox runtime](https://github.com/anthropic-experimental/sandbox-runtime)

## [gVisor](https://gvisor.dev/docs/)

## other references

- [2 sandbox patterns supported in langchain](https://x.com/hwchase17/status/2021261552222158955?s=20)

- [Palantir's AIP agent platform](https://x.com/PalantirTech/status/2014360213692854657?s=20)

- [claude code docs](https://platform.claude.com/docs/en/agent-sdk/hosting)