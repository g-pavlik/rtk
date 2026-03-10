# rtk — Nix flake fork

This fork exists solely to maintain a [Nix flake](https://nix.dev/concepts/flakes) for **[rtk (Rust Token Killer)](https://github.com/rtk-ai/rtk)**, a high-performance CLI proxy that reduces LLM token consumption by 60-90%.

For documentation, issues, and general usage, see the **[upstream repository](https://github.com/rtk-ai/rtk)**.

## Installation (Nix)

### Run directly

```bash
nix run github:g-pavlik/rtk
```

### Build

```bash
nix build github:g-pavlik/rtk
./result/bin/rtk --version
```

### Development shell

Provides `rustc`, `cargo`, `rust-analyzer`, `clippy`, and `rustfmt`:

```bash
nix develop github:g-pavlik/rtk
```

### NixOS module

Add this flake as an input and enable the module:

```nix
{
  inputs.rtk.url = "github:g-pavlik/rtk";

  # In your NixOS configuration:
  nixosModules = [ rtk.nixosModules.default ];
}
```

Then in your system configuration:

```nix
{
  programs.rtk.enable = true;
}
```

## What the flake provides

- **Default package** — builds rtk with `rustPlatform.buildRustPackage` using the committed `Cargo.lock`
- **Dev shell** — Rust toolchain with `rust-analyzer`, `clippy`, and `rustfmt`
- **NixOS module** — `programs.rtk.enable` option for system-wide installation
- macOS frameworks (`Security`, `SystemConfiguration`) included conditionally
- `RUSQLITE_USE_PKG_CONFIG=0` to let rusqlite use its bundled SQLite

## License

MIT — see [LICENSE](LICENSE) for details.
