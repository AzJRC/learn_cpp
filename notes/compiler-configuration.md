# Compiler Configuration

## C++ Standard Compliance

The C++ standard defines rules about how programs should behave in specific circumstances. And in most cases, compilers will follow these rules. However, some compilers may implement their own changes to the language. These compiler-specific behaviors are called **compiler extensions**.

Unfortunately, compiler extensions are often enabled by default. This could cause new learners to think some behavior that works is part of official C++ standard and make the code not portable to other systems and compilers without those extensions.

```diff
+ Best practice: Disable compiler extensions to ensure your programs remain compliant with C++ standards.
```

### Disabling Compiler Extensions

This process is IDE specific. But for VS Code, the following steps are advised:

1. Open the `tasks.json` file, find `"args"`, and then locate the line `"${file}"` within that section.
2. Above the `"${file}"` line, add a new line containing the following command: `"-pedantic-errors",`

Additionally, VS Code does not automatically add a newline to the end of code files that are missing it (which is somewhat a requirement as stated in the C++ standard). To automatically add a final newline to a code file, you can enable the function following these steps:

1. Open VS Code and go to `File > Preferences > Settings`. This will open a settings dialog.
2. Enter `insert final newline` into the search bar.
3. In both the `Workspace Settings` and `User Settings` tabs, ensure the checkbox labeled `Files: Insert Final Newline` is checked.

## Warning and Errors

When you write your programs, the compiler will check to ensure you’ve followed the rules of the C++ language (assuming you’ve turned off compiler extensions). When the compiler encounters some kind of issue, it will emit diagnostic message. The C++ standard does not present any categories of diagnostics messages, but modern compilers have conventionally adopted the following:

1. A **diagnostic error** (error for short) means the compiler has decided to halt compilation, because it either cannot proceed or deems the error serious enough to stop.
2. A **diagnostic warning** (warning for short) means the compiler has decided not to halt compilation. In such cases, the issue is simply ignored, and compilation proceeds.

Diagnostic messages typically contain both the filename and line number where the compiler found the issue.

```diff
+ Best Practice: Don’t let warnings pile up. Resolve them as you encounter them (as if they were errors).
```

### Configure verbose diagnostic messages

Most compilers will only generate warnings about the most obvious issues. However, you can request your compiler be more assertive about providing warnings.

For GCC, the following parameters are often used to include most warning messages when compiling a program.

```Bash
gcc -Wall -Weffc++ -Wextra -Wconversion -Wsign-conversion file.cpp
```

You can add the same parameters to a VS Code `tasks.json` in the `“args”` key, above the line where `“${file}”` appears. Add each flag on a new line.

### Treat warnings as errors

If you need a more restrictive compiler, you can convert all warnings into error-like diagnostic messages. Using GCC you can add the flag `-Werror`. In VS Code, that flag can be added in the `tasks.json` file.

## Language standard

There are several standards for the C++ language, and often some compilers use by default a deprecated or non-recent C++ language standard (like C++14).

The conventional names for language standards (e.g. C++20) are based on the year the language standard was published (or expected to be published). For example, in 2020, C++20 (formal name: SO/IEC 14882:2020). Some conventional names may vary a year with the formal name though.

In professional environments, it’s common to choose a language standard that is one or two versions back from the latest finalized standard (e.g. if C++20 were the latest finalized version, that means C++14 or C++17). On the other hand, for personal projects and while learning, we recommend choosing the latest finalized standard.

Remember that when changing your language standard (or any other project setting), make the change to all build configurations.

### Configuring language standard

For GCC/G++/Clang, you can use compiler options `-std=<conventional-name>`, like `-std=c++14`, `-std=c++17`, `-std=c++20`, or `-std=c++23`.

For VS Code, we place the appropriate language standard flag (including the double quotes and comma) in the `tasks.json` configuration file, in the `"args"` section. We may also want to configure Intellisense to use the same language standard. For C++20, in `settings.json`, change or add the following setting on its own line: `"C_Cpp.default.cppStandard": "c++20"`.

### Determine your current language standard

The following program is designed to print the name of the language standard your compiler is currently using.

```CPP
// This program prints the C++ language standard your compiler is currently using
// Freely redistributable, courtesy of learncpp.com (https://www.learncpp.com/cpp-tutorial/what-language-standard-is-my-compiler-using/)

#include <iostream>

const int numStandards = 7;
// The C++26 stdCode is a placeholder since the exact code won't be determined until the standard is finalized
const long stdCode[numStandards] = { 199711L, 201103L, 201402L, 201703L, 202002L, 202302L, 202612L};
const char* stdName[numStandards] = { "Pre-C++11", "C++11", "C++14", "C++17", "C++20", "C++23", "C++26" };

long getCPPStandard()
{
    // Visual Studio is non-conforming in support for __cplusplus (unless you set a specific compiler flag, which you probably haven't)
    // In Visual Studio 2015 or newer we can use _MSVC_LANG instead
    // See https://devblogs.microsoft.com/cppblog/msvc-now-correctly-reports-__cplusplus/
#if defined (_MSVC_LANG)
    return _MSVC_LANG;
#elif defined (_MSC_VER)
    // If we're using an older version of Visual Studio, bail out
    return -1;
#else
    // __cplusplus is the intended way to query the language standard code (as defined by the language standards)
    return __cplusplus;
#endif
}

int main()
{
    long standard = getCPPStandard();

    if (standard == -1)
    {
        std::cout << "Error: Unable to determine your language standard.  Sorry.\n";
        return 0;
    }

    for (int i = 0; i < numStandards; ++i)
    {
        // If the reported version is one of the finalized standard codes
        // then we know exactly what version the compiler is running
        if (standard == stdCode[i])
        {
            std::cout << "Your compiler is using " << stdName[i]
                << " (language standard code " << standard << "L)\n";
            break;
        }

        // If the reported version is between two finalized standard codes,
        // this must be a preview / experimental support for the next upcoming version.
        if (standard < stdCode[i])
        {
            std::cout << "Your compiler is using a preview/pre-release of " << stdName[i]
                << " (language standard code " << standard << "L)\n";
            break;
        }
    }

    return 0;
}
```

