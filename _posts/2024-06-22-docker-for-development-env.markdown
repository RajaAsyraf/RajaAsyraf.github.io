---
layout: post
title:  "Using Docker for development environment"
date:   2024-06-22 23:03:00 +0800
categories: docker
---

I still remember a few years back when it took me quite some time to really understand and have that "ah-ha" moment when adopting Docker into my workflow. I am fortunate enough that my workplace has adopted Docker for our development and production environments. I took advantage of this and got my hands dirty by exploring and using Docker for my personal side projects. In this post, I want to share my personal experience and explain why we should consider using Docker as the development environment across all of our projects.

![docker-containers](/assets/docker-containers.png)

### The Conventional Way
Previously, when we wanted to start working with a new tech stack, we would begin by installing a couple of packages, programs, or tools to ensure it could be executed on our local machine. This process could sometimes be tedious and easily overwhelming. Spending more time debugging unexpected errors and outcomes can really slow us down and cause frustration.

Cleaning up and removing those installed tools can also be very troublesome and requires a lot of mental energy to ensure your local machine remains clean. Upgrading the versions of these tools is also not straightforward, especially when they depend heavily on other tools.

For instance, I wanted to install Jekyll (a static website generator) on my local machine. I followed the guide from the official website and, for some reason, encountered an error (related to incompatible Ruby versions, I guess?). This was really unexpected and quite annoying. I didn't want to spend my time diving deep into that problem just to get it running locally; I wanted to make progress.

### The Docker Way
So I turned to Google to search for something that could help me provide an environment with Jekyll within a Docker container. The result was that I found a perfect solution for my situation. This open-source repository [BretFisher/jekyll-serve](https://github.com/BretFisher/jekyll-serve) comes with very helpful documentation. By simply executing `docker run -p 4000:4000 -v $(pwd):/site bretfisher/jekyll-serve` in our Jekyll project directory, I could already serve my static website in a container.

The author also provides additional help by allowing us to use the [docker-compose.yml](https://github.com/BretFisher/jekyll-serve/blob/main/docker-compose.yml) and place it in the root directory of our project. With that, we can simplify our command by running `docker compose up -d` to spin up the container.

### Conclusion
This saves me a lot of time, and by using Docker containers for my development environment, I don't have to worry about upgrading the Jekyll version with its dependencies in the future. I can do that in the `docker-compose.yml` file. I can also ensure my local machine is clean from unwanted programs that might take up space. There are many Docker images available on Docker Hub that we can utilize for most programs. In fact, the community is very helpful in maintaining those images and keeping them updated. We really appreciate the efforts in making these tools accessible to everyone!