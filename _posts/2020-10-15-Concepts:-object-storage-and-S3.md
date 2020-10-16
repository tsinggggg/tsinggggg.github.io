---
layout: post
title: "Concepts: Object storage and S3"
date: 2020-10-15
css: foo
tags: [storage, s3]
---

# Object storage vs File storage vs Block storage
## File storage
> File storage, also called file-level or file-based storage, is exactly what you think it might be: Data is stored as a single piece of information inside a folder, just like you’d organize pieces of paper inside a manila folder. When you need to access that piece of data, your computer needs to know the path to find it. (Beware—It can be a long, winding path.) Data stored in files is organized and retrieved using a limited amount of metadata that tells the computer exactly where the file itself is kept. It’s like a library card catalog for data files.
> 
> Think of a closet full of file cabinets. Every document is arranged in some type of logical hierarchy—by cabinet, by drawer, by folder, then by piece of paper. This is where the term hierarchical storage comes from, and this is file storage. It is the oldest and most widely used data storage system for direct and network-attached storage systems, and it’s one that you’ve probably been using for decades. Any time you access documents saved in files on your personal computer, you use file storage. File storage has broad capabilities and can store just about anything. It’s great for storing an array of complex files and is fairly fast for users to navigate.
> 
> The problem is, just like with your filing cabinet, that virtual drawer can only open so far. File-based storage systems must scale out by adding more systems, rather than scale up by adding more capacity.
Block storage chops data into blocks—get it?—and stores them as separate pieces. Each block of data is given a unique identifier, which allows a storage system to place the smaller pieces of data wherever is most convenient. That means that some data can be stored in a Linux® environment and some can be stored in a Windows unit.

## Block storage
> Block storage is often configured to decouple the data from the user’s environment and spread it across multiple environments that can better serve the data. And then, when data is requested, the underlying storage software reassembles the blocks of data from these environments and presents them back to the user. It is usually deployed in storage-area network (SAN) environments and must be tied to a functioning server.
> 
> Because block storage doesn’t rely on a single path to data—like file storage does—it can be retrieved quickly. Each block lives on its own and can be partitioned so it can be accessed in a different operating system, which gives the user complete freedom to configure their data. It’s an efficient and reliable way to store data and is easy to use and manage. It works well with enterprises performing big transactions and those that deploy huge databases, meaning the more data you need to store, the better off you’ll be with block storage.
> 
> There are some downsides, though. Block storage can be expensive. It has limited capability to handle metadata, which means it needs to be dealt with in the application or database level—adding another thing for a developer or systems administrator to worry about.

## Object storage
> Object storage, also known as object-based storage, is a flat structure in which files are broken into pieces and spread out among hardware. In object storage, the data is broken into discrete units called objects and is kept in a single repository, instead of being kept as files in folders or as blocks on servers.
> 
> Object storage volumes work as modular units: each is a self-contained repository that owns the data, a unique identifier that allows the object to be found over a distributed system, and the metadata that describes the data. That metadata is important and includes details like age, privacies/securities, and access contingencies. Object storage metadata can also be extremely detailed, and is capable of storing information on where a video was shot, what camera was used, and what actors are featured in each frame. To retrieve the data, the storage operating system uses the metadata and identifiers, which distributes the load better and lets administrators apply policies that perform more robust searches.
> 
> Object storage requires a simple HTTP application programming interface (API), which is used by most clients in all languages. Object storage is cost efficient: you only pay for what you use. It can scale easily, making it a great choice for public cloud storage. It’s a storage system well suited for static data, and its agility and flat nature means it can scale to extremely large quantities of data. The objects have enough information for an application to find the data quickly and are good at storing unstructured data.
> 
> There are drawbacks, to be sure. Objects can’t be modified—you have to write the object completely at once. Object storage also doesn’t work well with traditional databases, because writing objects is a slow process and writing an app to use an object storage API isn’t as simple as using file storage.

[https://www.redhat.com/en/topics/data-storage/file-block-object-storage](https://www.redhat.com/en/topics/data-storage/file-block-object-storage)

# AWS S3 or S3 API

> Object storage is the underlying technology for a S3 compliant storage. S3 compliant storage is built on the S3 API allowing data storage as well as manage and retrieve object stores. Applications which comply with the S3 API can communicate easily with any S3 compliant storage. 

[https://backup.ninja/news/how-build-your-own-object-storage-using-minio](https://backup.ninja/news/how-build-your-own-object-storage-using-minio)

> [MinIO](https://docs.min.io/docs/minio-quickstart-guide.html) is a High Performance Object Storage released under Apache License v2.0. It is API compatible with Amazon S3 cloud storage service. Use MinIO to build high performance infrastructure for machine learning, analytics and application data workloads.

[https://docs.min.io/docs/minio-quickstart-guide.html](https://docs.min.io/docs/minio-quickstart-guide.html)