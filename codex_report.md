# Dependency Check Failure

`moon check` fails in dependency `rami3l/js-ffi`.

I first ran `moon check`. The check downloaded `rami3l/js-ffi@0.3.1` and failed while checking files under:

`./.mooncakes/rami3l/js-ffi/src/js/`

The primary error is:

```text
extern "js" is unsupported in wasm-gc backend.
```

The failing command emitted by `moon check` targets `wasm-gc`:

```text
moonc check ... -pkg rami3l/js-ffi/js ... -target wasm-gc ...
```

Following the requested dependency remediation flow, I then ran:

```bash
moon add rami3l/js-ffi
```

This updated the direct dependency to `rami3l/js-ffi@0.4.0`, but `moon check` still fails with the same dependency-side issue. The second check reports 42 errors, still from `./.mooncakes/rami3l/js-ffi/src/js/`, including many instances of:

```text
extern "js" is unsupported in wasm-gc backend.
```

There are also secondary type errors in `rami3l/js-ffi` such as:

```text
Type Object has no method inner.
```

Because the remaining errors are from the dependency package rather than this repository's source files, I stopped here per the requested workflow.
