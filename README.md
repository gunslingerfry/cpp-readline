cpp-readline
============

This is a very simple library that wraps GNU readline into a C++ reusable class,
hiding all the global state of the readline library. It is meant to help you
interface really easily with your programs, while waiting for a more powerful
solution (or improving this library itself for your needs).

Features
========

The main features of this library are:

- Easy adding of custom commands
- Automatic completion of commands and filenames.
- Can run files containing lists of commands automatically.
- Multiple separate Consoles can be run at the same time, bypassing the readline
  library global state.
- Currently NOT thread-safe.
- Can be installed into system libraries and linked against by import name cpp-readline::cpp-readline
- Can be linked against in a hierarchy
- Uses modern cmake patterns

Requirements
============

The library currently requires support for C++11, and, of course, the readline
library.

Building
========

To build the project using CMake, just do the following in the project root directory:

    mkdir build && cd build && cmake .. && make

Usage
=====

This library's usage can easily be seen in the file `example/main.cpp`.
