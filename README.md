# Ramekin Hello World example

A Go program that prints "Hello World", packaged with [Ramekin](https://github.com/ascension-association/ramekin) for a gokrazy device using a persistent overlay. This is the project from Ramekin's quick start.

- `main.go` is the program. It prints its greeting and keeps running until the device stops it.
- `ramekin.yaml` is the Ramekin project in overlay mode: the wolfi-base image, plus whatever `ramekin shell` adds to `overlay.img`, running `/usr/bin/hello`. It publishes to this repository's [releases](https://github.com/ascension-association/ramekin-hello-world-example/releases); `hello-world/stable.json` on this branch is the signed channel pointer devices poll.
- Release `hello-world-1` prints "Hello"; `hello-world-2` prints "Hello World".

`overlay.img` isn't committed (it's large and binary), so recreate it:

```sh
git clone https://github.com/ascension-association/ramekin-hello-world-example && cd ramekin-hello-world-example
ramekin keys generate
ramekin overlay init
CGO_ENABLED=0 GOOS=linux GOARCH=arm64 go build -o hello .
echo 'cp hello /usr/bin/hello' | ramekin shell
ramekin build
```

To publish your own releases, point `releases.github` in `ramekin.yaml` at a repository of yours.
