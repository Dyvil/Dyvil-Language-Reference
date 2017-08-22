---
dyvil: v0.34.0
---

# The Dyvil Compiler

The Dyvil Compiler is the main tool for converting Dyvil source files to Class Files and Dyvil Object Files.

## Source Files

The following file types can be processed by the Dyvil Compiler:

* `.dyv` or `.dyvil` - Dyvil Classes, compiled to the Java Class File format \(`.class` files\)
* `.dyh` or `.dyvilh` - Dyvil Headers, compiled to Dyvil Object Files \(`.dyo`\)
* `.jar` - compiled Java or Dyvil Libraries, container files for `.class` files.

## Compiler Configuration

In order to tell the compiler where to find source files and libraries, there are two options:

### Launch Arguments

When running the compiler via the command line, it is possible to pass space-separated arguments to it, as shown in the below example:

```
dyvilc compile source_dir=src output_dir=bin ...
```

Note that there are four types of arguments that can be passed:

1. Phase Arguments - These simple arguments tell the compiler which work it you want it to do. The following phase arguments are available:
   * `compile` - Performs the usual compilation steps, without any optimisations or constant folding.
   * `optimise` - Performs optimisations, with `1` constant folding iteration
   * `-oN` - Performs optimisations, where `N` is the number of constant folding iterations
   * `jar` - Generates a Jar file from the source files. File names and other versioning information can be set via the corresponding options.
   * `format` - Formats the source files according to the recommended Dyvil code style
   * `clean` - Cleans the output directory before compilation, deleting all binaries
   * `print` - Prints the formatted source files, but does not override them unless `format` is passed as well
   * `test` - runs the Main Type with the specified Main Arguments
2. Debug Arguments
   * `--debug` - enables both `print` and `test`, and enables advanced logging output
3. `@configfile.txt` - loads the Compiler Configuration file from the path after the `@` symbol \(relative to the directory from which the compiler was launched\)
4. `option=value` - sets the value of the option named `option` to the `value`. Possible options are listed below.

Please note that it is currently not possible to pass list options like `libraries=[libs/,...]` as main arguments. However, it is possible to include multiple libraries into compilation by adding more arguments:

```sh
dyvilc libraries=libs/asm.jar libraries=libs/guava.jar
```

### 2. Configuration Files

A command line argument starting with `@` is treated by the compiler as the path for a configuration file.

```sh
dyvilc compile @config.dyc
```

This command will load all options from the `config.dyc` file, which is resolved relative to the directory from which the compiler has been launched. Note that it is only possible to define options in the configuration file. Other compiler arguments such as `compile`, `jar`, debug arguments and optimisation settings have to be passed directly as launch arguments.

The config file has a format like this

```
option = value
listOption = [ value1, value2, ... ]
```

By convention, the file should use the `.dyc` extension \(read `Dyvil Config`\). Other file extensions like `.txt` are also accepted by the compiler.

## Available Options

The following options can be passed as launch arguments or in the configuration file:

| Option Name | Type | Behavior | Example / Default Value | Default Value |
| --- | --- | --- | --- | --- |
| jar\_name | String | The name of the Jar File | `Dyvil` |  |
| jar\_version | String | The version of the Jar File | `1.0.0` |  |
| jar\_vendor | String | The Jar Vendor | `Clashsoft` |  |
| jar\_format | String | The format of the Jar file name |  | `[name]-[version].jar` |
| log\_file | File Path | The file to which logs are written | `dyvilc.log` | no log file |
| source\_dir | Dir. Path | The main source file directory | `src/main/dyvil` |  |
| source\_dirs | List of Dir. Paths | The main source file directories | `[ src/main/dyvil, gen/main/dyvil ]` |  |
| output\_dir | Dir. Path | The main output / binary directory | `bin` |  |
| main\_type | Class Name | The main type, used in the generated Jar file and the compiler test | `dyvil.test.Main` |  |
| main\_args | List of Strings | The launch arguments for the main type, passed separately as Strings | `[1, 2]` |  |
| include | List of Ant File Patterns | Inclusion filter for source files | `[ compiler, library]` | none \(includes all files in `source_dir`\) |
| exclude | List of Ant File Patterns | Exclusion filter for source files | `[ repl ]` | none |
| libraries | List of Paths | Additional Jar Libraries | `[ libs/asm.jar ]` | none |

### Important Notes about Options

- The file options `log_file`, `source_dir`, `source_dirs`, `output_dir` and `libraries` are relative to the launch directory of the compiler.
- The `include` and `exclude` options are both relative to the source directory roots.
- All file names are separated with `/`, but the file separator of the host system (e.g. `\` on Windows) is also supported.
- The main type is separated with `.`, as usual for Dyvil and Java class names.



