# quickjs-libraries

Native shared libraries built from [quickjs-ng/quickjs](https://github.com/quickjs-ng/quickjs) for use with C# P/Invoke.

## Supported Platforms

| Platform   | Architecture | Runtime Identifier |
|------------|-------------|-------------------|
| Windows    | x64         | `win-x64`         |
| Windows    | x86         | `win-x86`         |
| Windows    | arm64       | `win-arm64`       |
| Linux      | x64         | `linux-x64`       |
| Linux      | arm64       | `linux-arm64`     |
| macOS      | arm64       | `osx-arm64`       |

## Library Files

| Platform | File           |
|----------|----------------|
| Windows  | `quickjs.dll`  |
| Linux    | `libquickjs.so`|
| macOS    | `libquickjs.dylib` |

## Usage in C#

```csharp
using System.Runtime.InteropServices;

internal static class QuickJS
{
    private const string LibName = "quickjs";

    [DllImport(LibName, CallingConvention = CallingConvention.Cdecl)]
    public static extern nint JS_NewRuntime();

    [DllImport(LibName, CallingConvention = CallingConvention.Cdecl)]
    public static extern void JS_FreeRuntime(nint rt);

    // Add more P/Invoke declarations as needed
}
```

## Building

The libraries are built automatically via GitHub Actions on every push to `main` and on version tags.

To trigger a release, push a tag matching `v*` (e.g. `v1.0.0`).

Artifacts for each platform are uploaded as GitHub Actions artifacts on every build,
and attached as release assets when a version tag is pushed.

## Local Build

Requirements: CMake 3.10+, a C compiler (MSVC/GCC/Clang)

```sh
git clone --depth=1 https://github.com/quickjs-ng/quickjs.git quickjs-src
cmake -S quickjs-src -B build -DCMAKE_BUILD_TYPE=Release -DBUILD_SHARED_LIBS=ON -DQJS_ENABLE_INSTALL=OFF
cmake --build build --target qjs
```
