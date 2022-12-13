# dockerfiles

Dockerfiles for applications not commonly found in package managers.

## Usage

The following steps are optional.
The intent is to simplify the usage of these containerized applications.

You can tweak your keyboard shortcuts to launch the images,
create symlinks or aliases, etc.

### 1) Create an executable. (e.g. my_image)

```bash
#!/bin/sh
docker run \
--rm \
-it \
-v "${HOME}/$1:/root/$1:ro" \
-v "${HOME}/$2:/root/$2:ro" \
my_image
```

### 2) Save the executable in your ~/bin folder.

```bash
export PATH="${HOME}/bin:$PATH"
```

Ideally, appending ~/bin to PATH should be set in .profile

### 3) Test the executable with the arguments given.

```bash
my_image "Documents" "Downloads"
```

## Resources

* https://docs.docker.com/engine/reference/builder/
* https://docs.fedoraproject.org/en-US/iot/build-docker/
* https://docs.podman.io/en/latest/markdown/podman-build.1.html

## Roadmap

* Rootless environment.
* gVisor sandboxing.