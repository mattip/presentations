# Python Perfomance Seminar - Matti Picus
tinyurl https://tinyurl.com/matti-summit
## Who am I?
- Now working for UC Berkeley on NumPy, 6 months into a 2 year contract
- PyPy volunteer since 2011, part of a great team
- Implemented much of the C-API compatability layer in PyPy
- Brought the PyPy alternative NumPy to 95% feature compatibility, (it is a rewrite of NumPy in RPython that is JIT friendly).
  - It used to have a graph feature that would delay calculating output until needed, like Dask, but needs reviving

## ~~TurboPython~~ PyPy
- Mature Python interpreter with tracing JIT and generational mark-sweep GC
- Is often 2-5x faster than CPython (and can be up to 100x, for highly algorithmic code)
- Based on RPython, a restricted Python dialect that can be translated to C (other backends existed - Java, C#)
- Framework used for [other interpreters](https://rpython.readthedocs.io/en/latest/examples.html) as well (in addition to Python 2.7 and Python 3.5, soon python 3.6)
- Supports C-Extensions via a compatibility layer
- Supports Linux/x86, Linux/ARMv7, MacOS X/x86, FreeBSD/x86, Windows/x86, Linux/PPC64, Linux/s390x and other linux variants on x86, ARMv7
- Way underfunded
  - [Proposal](https://drive.google.com/open?id=1p3NnO-zrB3SL6SIXx5m37k5WZxfr9qyg) to improve performance of C-extensions
  - Proposal to [remove the GIL](https://morepypy.blogspot.com/2017/08/lets-remove-global-interpreter-lock.html) for ~$100,000
  - Recently received funding to [support ARM64](https://morepypy.blogspot.com/2018/11/hello-everyone-at-pypy-we-are-trying-to.html)
  - No funding for Windows 64 bit
- Used in industry because it is faster
- Spawned CFFI, [vmprof](https://vmprof.readthedocs.io/en/latest/vmprof.html) (also underfunded) and extended the Python benchmark suite from Unladen Swallow

## C-API
- Mixing metaphors causes problems.
- Enables you to write Python in C (Cython), which totally confuses a VM not based on C.
- [Explanation](https://morepypy.blogspot.com/2018/09/inside-cpyext-why-emulating-cpython-c.html) of what PyPy does and why it is slow
- Is Python-only, restricts interop with other languages
- The direction of Cython is a step forward, it still allows introspection of code

## Way forward
- Write a shared object with a C interface and use CFFI, or a C++ interface and use CPPYY (or pybind11)
- Just write in Python and use a JITting virtual machine like PyPy, Numba, numexpr, ... and improve these JITs if necessary
- Continue with Cython-like tools
- **benchmarking is critical** and should be a higher priority

## Not the way forward
- Developing a new VM from scratch
  - unless you have a several year runway and serious funding (compare with the size of JS VM teams, and Javascript is a much simpler language than Python!)
  - without involving people versed in the details of the language and JIT technology
  - without interviewing (or hiring) people who have worked on similar projects
- Splitting the community
- Doing something without wide community backing

