# Master PDF Editor 4.3.89

## Requirements

* Docker.
* Linux with X11.

## Build

```bash
# cd ~/oci_masterpdfeditor4
docker build -t masterpdfeditor4 .
```

Optional arguments can be passed to the build command,
overriding the default username:

```bash
docker build --build-arg=user="$(whoami)" -t masterpdfeditor4 .
```

## Run

```bash
docker run -it --rm \
  --net=host \
  -e DISPLAY="${DISPLAY}" \
  -v "${HOME}/.Xauthority:/home/user/.Xauthority:ro" \
  -v "${HOME}/Documents:/home/user/Documents:ro" \
  masterpdfeditor4
```

If the optional argument was passed,
replace "user" in the '-v' argument with your given username.

Optional: symlink the provided executable:

```bash
mkdir -p "$HOME/bin"
cp ./masterpdfeditor4 "$HOME/bin"
ln -sf "$HOME/bin" "/usr/bin/masterpdfeditor4"
```

## License

Refer to the licenses of Docker & Code Industry respectively.
