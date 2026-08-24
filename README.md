# frpc-for-iOS

**frpc** — compiled as an **iOS** standalone binary forked from the upstream [frp](https://github.com/fatedier/frp) project.

> This repository is a fork of the upstream [gofrp/frp](https://github.com/fatedier/frp) project. It has been adapted and built specifically to produce an **iOS** executable of **frpc** (the frp client). No server-side binary (**frps**) is provided.

---

## What is frpc?

[frpc](https://gofrp.org) is the client component of [frp](https://github.com/fatedier/frp), a fast reverse proxy for exposing local services behind NAT or a firewall to the public internet. It supports TCP, UDP, HTTP, HTTPS, and P2P communication.

This fork builds **only the client**, targeting **iOS (arm64)**, so you can run a lightweight `frpc` binary directly on iOS devices.

## What's included / not included

| Component | Description | Provided |
|-----------|-------------|----------|
| `frpc` | The frp **client** | ✅ iOS build |
| `frps` | The frp **server** | ❌ Not provided |

- Only the **iOS client (`frpc`)** source and build pipeline are maintained here.
- The server (`frps`) and the general-purpose desktop/mobile builds from the upstream project are intentionally out of scope.

## Building frpc for iOS

The iOS binary is compiled on a macOS runner with cgo enabled (see [`.github/workflows/build.yml`](.github/workflows/build.yml)):

```bash
GOOS=ios GOARCH=arm64 CGO_ENABLED=1 go build -trimpath -ldflags="-s -w" -o frpc ./cmd/frpc
```

The resulting `frpc` iOS artifact can be downloaded from the **Actions** tab of this repository.

## Requirements

- [Go](https://go.dev/dl/) `1.25.0` or newer (see [`go.mod`](go.mod))
- macOS host / runner to produce the iOS binary (cgo linking required for `ios/arm64`)

## Note on source layout

The code under `cmd/`, `client/`, `server/`, `pkg/`, and `web/` is lifted from the upstream frp project. The upstream `frps` (server) pieces remain in the tree for upstream parity but are **not** built, shipped, or supported by this fork.

---

## Upstream & License

This project is a fork of [gofrp/frp](https://github.com/fatedier/frp). All credit for the underlying frp project goes to its authors and contributors.

Licensed under the [Apache License 2.0](LICENSE).
