# Docker Utility Images

I'm creating Docker utility images for applications that are not in the Docker Hub. Since most of my applications will run on a Raspberry Pi 3, these images will be using armv7.

## Getting Started

These instructions will get your desired utility image up and running

### Prerequisites

What things you need to install the software and how to install them

- Raspberry Pi 3 or other ARM based system
- Docker
- docker-compose

### Installing

A step by step series of examples that tell you how to get a development env running

Navigate to the utility image of your choosing and build from the dockerfile by referencing the Github path

Here's an example of how to build from the Prometheus utility image:

```
$ docker build github.com/etho201/utility-images/prometheus
```