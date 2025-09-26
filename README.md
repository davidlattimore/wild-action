# Wild GitHub action

Depend on this action to use Wild when building rust code.

See the main [wild repo](https://github.com/davidlattimore/wild) for more details about wild.

Example:

```yml
name: ci
on: [push, pull_request]

jobs:
  ci:
    name: CI
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: dtolnay/rust-toolchain@stable
      - uses: davidlattimore/wild-action@latest
      - run: cargo test
```

The above workflow will use the latest version of wild. If you'd like to pin to a specific version,
you can instead do:

```yml
      - uses: davidlattimore/wild-action@0.6.0
```

This action writes the following to `~/.cargo/config.toml`:

```toml
[target.${target_arch}-unknown-linux-gnu]
linker = "clang"
rustflags = ["-Clink-arg=--ld-path=${{ github.action_path }}/wild"]
```

If you specify `rustflags` via a `.cargo/config.toml` in your repository or by setting `RUSTFLAGS`,
then that will override the effect of this action.
