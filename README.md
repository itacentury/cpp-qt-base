# cpp-qt-base

A minimal C++/Qt6 base project using CMake. Intended as a starting point for new Qt Widgets applications.

## Requirements

- CMake >= 3.19
- A C++17 compiler (tested with GCC 14.2.1 and Clang 19.1.7 on Linux x86_64)
- Qt6 development libraries

On Fedora: `sudo dnf install cmake gcc-c++`

## Qt location

This project expects the environment variable `QT_PREFIX_PATH` to point at the Qt toolchain directory, for example:

```sh
export QT_PREFIX_PATH="$HOME/Qt/6.11.0/gcc_64"
```

Add that line to your shell rc (`~/.zshrc`, `~/.bashrc`, …) so it persists.

## Build

The project ships with three CMake presets. Each one lives in its own build directory (`build/debug`, `build/release`, `build/asan`), so you can switch between them without reconfiguring.

```sh
cmake --preset <debug|release|asan>
cmake --build --preset <debug|release|asan>
./build/<preset>/CppQtBase
```

### Which preset should I use?

| Preset    | Flags                                  | Use it for                                                      |
| --------- | -------------------------------------- | --------------------------------------------------------------- |
| `debug`   | `-O0 -g`                               | Day-to-day development and stepping through code in a debugger. |
| `release` | `-O3 -DNDEBUG`, LTO via `ENABLE_IPO`   | Shipping, installing, and performance measurements.             |
| `asan`    | Debug + `-fsanitize=address,undefined` | Hunting memory bugs, UB, heap corruption, or sporadic crashes.  |

Rule of thumb: `debug` for development, `release` for the outside world, `asan` when something blows up. Run `asan` once before cutting a release — if it stays silent, the release build is far less likely to hide undefined behavior.

## Using this template

1. Create a new repository from this one (or clone and re-init git).
2. Change the project name in `CMakeLists.txt`:
   ```cmake
   project(YourAppName LANGUAGES CXX)
   ```
   The executable target is derived from `${PROJECT_NAME}`, so nothing else needs to be renamed.
3. Start adding your sources under `src/` and list them in the `qt_add_executable(...)` call.

## Tooling

- **Formatting**: `clang-format -i src/*.cpp src/*.h`
- **Linting**: `clang-tidy -p build src/*.cpp`
- **IDE support**: `compile_commands.json` is generated automatically in `build/` and picked up by `clangd`.
