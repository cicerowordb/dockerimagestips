# Docker Image Do's and Don'ts

A list of simple tips for producing optimized and secure images.

[https://github.com/cicerowordb/dockerimagestips](https://github.com/cicerowordb/dockerimagestips)

## Tip 1: Handle everything in the same layer.

Each layer of a Docker image acts like a different file system, and these layers are independent of one another [cite: 1]. Consequently, if you create a file in one layer and delete it in another, the file remains present in the original layer [cite: 1]. Even if the file is inaccessible in the final image as planned, it continues to occupy space, making your container larger than necessary [cite: 1]. Larger containers take longer to load and consume unnecessary space, among other issues that should be avoided [cite: 1].

*Compare and explain Examples 1 and 2.*

## Tip 2: Properly manage the sequence of layers.

Layers are cached and reused as long as the preceding layers have not been modified [cite: 1]. If a layer changes, its cache and the cache of all subsequent layers will be discarded [cite: 1]. Therefore, it is essential to organize your Dockerfile so that layers changing less frequently are placed at the beginning, while layers that change often are placed at the end [cite: 1]. While it can be difficult to predict exactly which layers will change—as this depends on project demands—being assertive with this order results in faster image builds [cite: 1].

*Compare and explain Examples 3 and 4.*

*Compare and explain Examples 5 and 6.*

## Tip 3: Use .dockerignore to prevent leaks.

The `.dockerignore` file is a configuration file used during the creation of Docker images to specify which files and directories should be ignored during the build process [cite: 1]. Similar to a `.gitignore` file in Git repositories, `.dockerignore` helps reduce image size and build time by avoiding the inclusion of unnecessary files like logs, temporary files, and development directories [cite: 1]. It also serves to ensure that sensitive files used during development are never included inside the final image [cite: 1].

*Explain Example 7.*

## Tip 4: Use base images.

Simply put, a base image is an image used to create another [cite: 1]. While we have used Debian 12 to create our images so far, imagine you want to create your own base image [cite: 1]. If you find yourself installing the same applications every time you use Debian 12 for a specific context, you can create a base image with those applications already installed [cite: 1]. This allows you to reuse it without reinstalling everything every time you build a new image [cite: 1]. In the provided example, a Python image is used to run a small shift cipher application [cite: 1].

*Explain Examples 8 and 9.*

## Tip 5: How to handle sensitive information.

Sensitive information should never be included in your Dockerfile or your image [cite: 1]. There are several strategies for this depending on your needs, but two key methods should always be remembered: using **build args** and using **volumes** [cite: 1]. Build args are environment variables present only during the build process and differ from standard environment variables (`ENV`) [cite: 1]. Volumes allow you to include sensitive files in the container only at runtime [cite: 1].

*Explain Example 10.*
