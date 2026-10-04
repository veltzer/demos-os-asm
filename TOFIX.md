# TOFIX

Findings from a code scan on 2026-10-04.

## Medium

- `rsconstruct.toml` - neither boot sector is ever assembled by the build: only taplo, actionlint, rumdl and shellcheck run, so a syntax error in `Part1/src/main.asm` or `Part2/src/main.asm` stays green. Add `[processor.make]` over `Part1` and `Part2` (their Makefiles already produce `build/main_floppy.img`) and declare `nasm` under `[dependencies] system`.

## Low

- `Part2/src/main.asm:37,39,46` - trailing whitespace (after `pop si`, and on two blank lines), violating the fleet `.editorconfig` `trim_trailing_whitespace = true`.
- `Part1/Makefile:16`, `Part2/Makefile:16` - `mkdir -p build` and `clean`'s `rm -rf build` (`:22`) hardcode the directory instead of using `$(BUILD_DIR)` defined at `:3`; use the variable.
- `README.md:8` - does not say what `Part1` (a halting boot sector) and `Part2` (BIOS hello-world) are, nor how to run them (`make` then `./run.sh` in each part; needs `nasm` and `qemu-system-i386`).
