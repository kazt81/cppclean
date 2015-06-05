CppClean attempts to find problems in C++ source that slow development particularly in large code bases.  It is similar to lint; however, CppClean focuses on finding global inter-module problems rather than local problems similar to other static analysis tools.

The goal is to find problems that slow development in large code bases that are modified over time leaving unused code.  This code can come in many forms from unused functions, methods, data members, types, etc to unnecessary `#include` directives.  Unnecessary `#include`s can cause considerable extra compiles increasing the edit-compile-run cycle.

## Features ##

  * Find and print C++ language constructs: classes, methods, functions, etc.
  * Find classes with virtual methods, no virtual destructor, and no bases
  * Find global/static data that are potential problems when using threads
  * Unnecessary forward class declarations
  * Unnecessary function declarations
  * Undeclared function definitions
  * (planned) Find unnecessary header files #included
    * No direct reference to anything in the header
    * Header is unnecessary if classes were forward declared instead
  * (planned) Source files that reference headers not directly `#include`d, ie, files that rely on a transitive #include from another header
  * (planned) Unused members (private, protected, & public) methods and data
  * (planned) Store AST in a SQL database so relationships can be queried

## How to Run ##

For all examples, it is assumed that CppClean resides in a directory called `/cppclean`.

To print warnings for classes with virtual methods, no virtual destructor and no base classes:
```
      /cppclean/run.sh nonvirtual_dtors.py file1.h file2.h file3.cc ...
```

To print all the functions defined in header file(s):
```
      /cppclean/run.sh functions.py file1.h file2.h ...
```

Note: if you have too many files to fit on the command line, store a list of all the files in a file, e.g., all-files.txt, then do:
```
      cat all-files.txt | xargs /cppclean/run.sh functions.py
```

All the commands take multiple files on the command line.  Other programs include: find\_warnings, headers, methods, and types.  Some other programs are available, but used primarily for debugging.

run.sh is a simple wrapper that sets `PYTHONPATH` to `/cppclean` and then runs the program in `/cppclean/cpp/PROGRAM`.  There is currently no equivalent for Windows.  Contributions for a `run.bat` file would be greatly appreciated.

## Internals ##

For information about how CppClean works and how to modify it, see the InternalDesign.