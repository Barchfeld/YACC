[![C/C++ CI](https://github.com/glvi/json_parser/actions/workflows/c-cpp.yml/badge.svg)](https://github.com/glvi/json_parser/actions/workflows/c-cpp.yml)
# json_parser

Parser for JSON

I started this project for educational purposes.
I wanted to show-case how to write a parser using GNU bison.
And writing a JSON parser seemed like a good idea at the time.

**References**:
- GNU Bison, <https://www.gnu.org/software/bison/>.
- Bray, T., Ed., "The JavaScript Object Notation (JSON) Data Interchange Format", STD 90, RFC 8259, DOI 10.17487/RFC8259, December 2017, <https://www.rfc-editor.org/info/rfc8259>.
- Ecma International, "The JSON Data Interchange Format", Standard ECMA-404, <http://www.ecma-international.org/publications/standards/Ecma-404.htm>.
- See also: https://json.org/.

**On Compilers**:
- Stanford's course in the practical and theoretical aspects of compiler construction (CS143 Compilers) web page: <https://web.stanford.edu/class/archive/cs/cs143/cs143.1128/>.

# Dependencies

## Operating system(s)

Tested on macOS 13.3.1 with support from [Homebrew](https://brew.sh/)

## Compiler(s)

Tested with LLVM 16.0 Clang and GNU G++ 13.1

```ShellSession
$ brew install llvm # or
$ brew install gcc # or both
```

## Parser and scanner generators

Tested with GNU Bison 3.8.2 and GNU Flex 2.6.4

```ShellSession
$ brew install bison # and
$ brew install flex
```

## Build tool

Tested with GNU Make 4.4.1.

```ShellSession
$ brew install make
```

# Contents

The parser is in `json_parser.yy`.

The scanner is in `json_scanner.ll`.

The glue is in `json.cc/.hh`.

The executable is `json`.

The project is built using GNU Autotools.

# Building

To initialize the build system
```ShellSession
$ autoreconf -i -s
```

To create the build configuration
```ShellSession
$ mkdir -p build
$ cd build
$ export YACC=/usr/local/opt/bison/bin/bison # use GNU Bison parser generator from Homebrew installation
$ export CXX=/usr/local/opt/gcc/bin/g++-13   # use GNU C++ compiler from Homebrew installation
$ ../configure
```

To build
```ShellSession
$ cd build
$ gmake -j
```

To test
```ShellSession
$ cd build
$ gmake check
```

# Usage

The parser reads data from the standard input.

If the parser accepts the input as JSON, it presents what it has understood to the standard output.

Errors, warnings, and other messages are reported to standard error.

```ShellSession
$ ./json < FILE
```

# Examples
For this input (`test1.json`):

```JavaScript
[null, true, false, 123, 123.456, "Fnord!\nHail\tEris!"]
```

this will happen:

```ShellSession
$ ./json < test1.json
I found JSON: [null, true, false, 123, 123.456, "Fnord!
Hail	Eris!"]
```
