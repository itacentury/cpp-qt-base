# cpp-qt-base

A minimal C++/Qt6 base project using CMake. Intended as a starting point for new Qt Widgets applications.

## Requirements

- CMake >= 3.19
- A C++17 compiler (tested with GCC 14.2.1 and Clang 19.1.7 on Linux x86_64)
- Qt6 development libraries

On Fedora: `sudo dnf install cmake gcc-c++`

## Build

```sh
cmake -B build -S .
cmake --build build
```

Run the resulting binary:

```sh
./build/CppQtBase
```

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
