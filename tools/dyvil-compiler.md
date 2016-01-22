# The Dyvil Compiler

The Dyvil Compiler is the main tool for converting Dyvil source files to Class Files and Dyvil Object Files.

## Source Files

The following file types can be processed by the Dyvil Compiler:

- `.dyv` or `.dyvil` - Dyvil Classes, compiled to the Java Class File format (`.class` files)
- `.dyh` or `.dyvilh` - Dyvil Headers, compiled to Dyvil Object Files (`.dyo`)
- `.jar` - compiled Java or Dyvil Libraries, container files for `.class` files.

## Compiler Configuration

In order to tell the compiler where to find source files and libraries, there are two options:

### Launch Arguments

When running the compiler via the command line, it is possible to pass space-separated arguments to it, as shown in the below example:

```
dyvilc compile source_dir=src output_dir=bin ...
```

Note that there are four types of arguments that can be passed:

1. Phase Arguments - These simple arguments tell the compiler which work it you want it to do. The following phase arguments are available:
  - `compile` - Performs the usual compilation steps, without any optimizations or constant folding.
  - `optimize` - Performs optimizations, with `1` constant folding iteration
  - `-oN` - Performs optimizations, where `N` is the number of constant folding iterations
  - `jar` - Generates a Jar file from the source files. File names and other versioning information can be set via the corresponding options.
  - `format` - Formats the source files according to the recommended Dyvil code style
  - `clean` - Cleans the output directory before compilation, deleting all binaries
  - `print` - Prints the formatted source files, but does not override them unless `format` is passed as well
  - `test` - runs the Main Type with the specified Main Arguments
2. Debug Arguments
  - `--debug` - enables both `print` and `test`, and enables advanced logging output
3. `@configfile.txt` - loads the Compiler Configuration file from the path after the `@` symbol (relative to the directory from which the compiler was launched)
4. `option=value` - sets the value of the option named `option` to the `value`. Possible options are listed below.

Please note that it is currently not possible to pass list options like `libraries=[libs/,...]` as main arguments. However, it is possible to include multiple libraries into compilation by adding multiple options with the same option name:

```sh
dyvilc libraries=libs/asm.jar libraries=libs/guava.jar
```

### 2. Configuration Files

When passing an argument starting with an `@` symbol when launching the compiler, it will load a configuration file from the path after that symbol:

```sh
dyvilc compile @config.txt
```

This command will load all options from the `config.txt` file, which is resolved relative to the directory from which the compiler has been launched. Note that it is only possible to define options in the configuration file. Other compiler arguments such as `compile`, `jar`, debug arguments and optimization settings have to be passed directly as launch arguments.

The config file has a format like this

```
option = value
listOption = [ value1, value2, ... ]
```

## Available Options

The following options can be passed as launch arguments or in the configuration file:

| Option Name | Type      | Behavior                           | Example / Default Value         |
|-------------|-----------|------------------------------------|---------------------------------|
| jar_name    | String    | The name of the Jar File           | `Dyvil`                         |
| jar_version | String    | The version of the Jar File        | `1.0.0`                         |
| jar_vendor  | String    | The Jar Vendor                     | `Clashsoft`                     |
| jar_format  | String    | The format of the Jar file name    | default: `[name]-[version].jar` |
| log_file    | File Path | The file to which logs are written | default: none / `dyvilc.log`    |
| source_dir  | Dir. Path | The main source file directory     | `src/main/dyvil`                |
| output_dir  | Dir. Path | The main output / binary directory | `bin`                           |
| main_type   | Class Name| The main type, used in the generated Jar file and the compiler test|`dyvil.test.Main` |
| main_args   | String List | The launch arguments for the main type | `[1, 2]` (passed separately as Strings) |
| include     | Path List | Inclusion filter for source files  | default: none (all files in `source_dir`) / `[ compiler, library]` |
| exclude     | Path List | Exclusion filter for source files  | default: none / `[ repl ]`       |
| libraries   | Path List | Additional Jar Libraries           | default: none / `[ libs/asm.jar ]` |

### Important Notes about Options

- The file options `log_file`, `source_dir`, `output_dir` and `libraries` are relative to the parent directory of the configuration file when present in a config file.
- If they are passed as launch arguments, they relative to the launch directory of the compiler. 
- `include` and `exclude` are both relative to the `source_dir`.
- All file names are separated with the file separator of the host system (`/` on Unix / Mac, `\` on Windows).
- The main type is separated with `.`, as usual for Java class names.


