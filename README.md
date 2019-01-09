# docker-ruby
Yet another docker base images for ruby apps

## Motivation

- Build upon tiny ubuntu:18.04 image
- Compiles ruby with [jemalloc garbage collector](http://jemalloc.net/). why?, it [saves memory and increases perfomance](https://medium.com/rubyinside/how-we-halved-our-memory-consumption-in-rails-with-jemalloc-86afa4e54aa3)
- Stores ruby version and (travis) build id in docker label to easy blacklist container based on this image
