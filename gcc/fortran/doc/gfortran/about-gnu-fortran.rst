..
  Copyright 1988-2022 Free Software Foundation, Inc.
  This is part of the GCC manual.
  For copying conditions, see the copyright.rst file.

.. _about-gnu-fortran:

About GNU Fortran
*****************

The GNU Fortran compiler is the successor to :command:`g77`, the
Fortran 77 front end included in GCC prior to version 4 (released in
2005).  While it is backward-compatible with most :command:`g77`
extensions and command-line options, :command:`gfortran` is a completely new
implemention designed to support more modern dialects of Fortran.
GNU Fortran implements the Fortran 77, 90 and 95 standards
completely, most of the Fortran 2003 and 2008 standards, and some
features from the 2018 standard.  It also implements several extensions
including OpenMP and OpenACC support for parallel programming.

The GNU Fortran compiler passes the
`NIST Fortran 77 Test Suite <http://www.fortran-2000.com/ArnaudRecipes/fcvs21_f95.html>`_, and produces acceptable results on the
`LAPACK Test Suite <https://www.netlib.org/lapack/faq.html>`_.
It also provides respectable performance on
the `Polyhedron Fortran compiler benchmarks <https://polyhedron.com/?page_id=175>`_ and the
`Livermore Fortran Kernels test <https://www.netlib.org/benchmark/livermore>`_.  It has been used to compile a number of
large real-world programs, including
`the HARMONIE and HIRLAM weather forecasting code <http://hirlam.org/>`_ and
`the Tonto quantum chemistry package <https://github.com/dylan-jayatilaka/tonto>`_; see
https://gcc.gnu.org/wiki/GfortranApps for an extended list.

GNU Fortran provides the following functionality:

* Read a program, stored in a file and containing :dfn:`source code`
  instructions written in Fortran 77.

* Translate the program into instructions a computer
  can carry out more quickly than it takes to translate the
  original Fortran instructions.
  The result after compilation of a program is
  :dfn:`machine code`,
  which is efficiently translated and processed
  by a machine such as your computer.
  Humans usually are not as good writing machine code
  as they are at writing Fortran (or C++, Ada, or Java),
  because it is easy to make tiny mistakes writing machine code.

* Provide information about the reasons why
  the compiler may be unable to create a binary from the source code,
  for example if the source code is flawed.
  The Fortran language standards require that the compiler can point out
  mistakes in your code.
  An incorrect usage of the language causes an :dfn:`error message`.

  The compiler also attempts to diagnose cases where your
  program contains a correct usage of the language,
  but instructs the computer to do something questionable.
  This kind of diagnostic message is called a :dfn:`warning message`.

* Provide optional information about the translation passes
  from the source code to machine code.
  This can help you to find the cause of
  certain bugs which may not be obvious in the source code,
  but may be more easily found at a lower level compiler output.
  It also helps developers to find bugs in the compiler itself.

* Provide information in the generated machine code that can
  make it easier to find bugs in the program (using a debugging tool,
  called a :dfn:`debugger`, such as the GNU Debugger :command:`gdb`).

* Locate and gather machine code already generated to
  perform actions requested by statements in the program.
  This machine code is organized into :dfn:`modules` and is located
  and :dfn:`linked` to the user program.

The GNU Fortran compiler consists of several components:

* A version of the :command:`gcc` command
  (which also might be installed as the system's :command:`cc` command)
  that also understands and accepts Fortran source code.
  The :command:`gcc` command is the :dfn:`driver` program for
  all the languages in the GNU Compiler Collection (GCC);
  With :command:`gcc`,
  you can compile the source code of any language for
  which a front end is available in GCC.

* The :command:`gfortran` command itself,
  which also might be installed as the
  system's :command:`f95` command.
  :command:`gfortran` is just another driver program,
  but specifically for the Fortran compiler only.
  The primary difference between the :command:`gcc` and :command:`gfortran`
  commands is that the latter automatically links the correct libraries
  to your program.

* A collection of run-time libraries.
  These libraries contain the machine code needed to support
  capabilities of the Fortran language that are not directly
  provided by the machine code generated by the
  :command:`gfortran` compilation phase,
  such as intrinsic functions and subroutines,
  and routines for interaction with files and the operating system.

  .. and mechanisms to spawn,

  .. unleash and pause threads in parallelized code.

* The Fortran compiler itself, (:command:`f951`).
  This is the GNU Fortran parser and code generator,
  linked to and interfaced with the GCC backend library.
  :command:`f951` 'translates' the source code to
  assembler code.  You would typically not use this
  program directly;
  instead, the :command:`gcc` or :command:`gfortran` driver
  programs call it for you.
