# Build Configurations

A build configuration (also called a build target) is a collection of project settings that determines how your IDE will build your project.

- The debug configuration is designed to help you debug your program.
- The release configuration is designed to be used when releasing your program to the public.


```diff
+ Best Practice: Use the debug build configuration when developing your programs. Use the release build configuration for finished products.
```

## Bulid parameters

Add `-ggdb` (add debug symbols) to the command line for debug builds and `-O2 -DNDEBUG` (optimization level 2 and do not add debug symbols) for release builds. For GCC and Clang, the `-O#` option is used to control optimization settings.

If using VS Code, the file `tasks.json` contains the `args` key within a JSON object. Above the `“${file}”` line, add a new line (one line per parameter) containing the bulid parameters enlisted before.