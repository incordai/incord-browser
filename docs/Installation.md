## Linux x86_64

```bash
curl -LO https://github.com/incordai/incord-browser/releases/latest/download/incord-browser-x86_64-linux.tar.gz
tar xzf incord-browser-x86_64-linux.tar.gz
./incord-browser --version
```

## Linux ARM64

```bash
curl -LO https://github.com/incordai/incord-browser/releases/latest/download/incord-browser-aarch64-linux.tar.gz
tar xzf incord-browser-aarch64-linux.tar.gz
./incord-browser --version
```

Linux builds target Ubuntu 22.04 and require glibc 2.35+.

## macOS Apple Silicon

```bash
curl -LO https://github.com/incordai/incord-browser/releases/latest/download/incord-browser-aarch64-macos.tar.gz
tar xzf incord-browser-aarch64-macos.tar.gz
./incord-browser --version
```

## macOS Intel

```bash
curl -LO https://github.com/incordai/incord-browser/releases/latest/download/incord-browser-x86_64-macos.tar.gz
tar xzf incord-browser-x86_64-macos.tar.gz
./incord-browser --version
```

## Windows

Download the `.zip` from [Releases](https://github.com/incordai/incord-browser/releases), extract, run `incord-browser.exe --version`.

## Arch Linux (AUR)

```bash
yay -S obscura-browser
```

## Docker

```bash
docker build -t incord-browser .
docker run -d --name incord-browser -p 127.0.0.1:9222:9222 incord-browser
```

Built on `distroless/cc:nonroot`, with no shell or package manager in the runtime image, running as uid 65532. Note the `-p 127.0.0.1:...` above: it publishes the port to host loopback only. A mounted `--storage-dir` must be writable by uid 65532 — see [Run in production at scale](Run-in-production-at-scale.md#the-container-does-not-run-as-root).

Official archives and the Docker image include the rendering engine. Source
builders must pass `--features render`; see [Build from source](Build-from-source.md).

## From source

See [Build from source](Build-from-source.md).

## What's in the archive

- `incord-browser`: CLI and CDP server.
- `incord-browser-worker`: helper for the parallel `scrape` command. Keep both in the same directory.

Archive suffixes identify the feature set: no suffix includes rendering,
`-stealth` includes rendering and stealth, `-no-render` includes neither, and
`-no-render-stealth` includes stealth without rendering.

## Smoke test

```bash
./incord-browser fetch https://example.com --eval "document.title"
./incord-browser fetch https://example.com --screenshot smoke.png
```

Expected output: `"Example Domain"`, followed by a nonempty PNG at `smoke.png`.

## Troubleshooting

`cannot execute binary file`: wrong arch. Check `uname -m`.

`GLIBC_2.35 not found`: distro is older than Ubuntu 22.04. Use Docker or build from source.

macOS Gatekeeper warning: `xattr -d com.apple.quarantine ./incord-browser`.
