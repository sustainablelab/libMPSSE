I'd like to just use this downloaded pre-built binary, but no
luck. I'm giving up on this path for now.

# FTDI link

This is part of FTDI `LibMPSSE DLL` [downloaded from
FTDI](https://www.ftdichip.com/old2020/Support/SoftwareExamples/MPSSE/LibMPSSE-I2C.htm)
on Mon, Jan  9, 2023.

I wrote this README and the `.gitignore`. Everything else is from
FTDI.

For compiling on MinGW, I had to:

```c
#include <Windows.h>    // defines stuff like PVOID
#include "ftd2xx.h"
```

But I still get linker errors. I need to build the libMPSSE
binary myself. Linker complains the 32-bit `.dll` is an
incompatible type.

# No samples or visualstudio

The FTDI link above includes two folders I ignore in the
`.gitignore`:

- `samples/`
- `lib/windows/visualstudio/`

I build my projects for Windows with MinGW and for Linux, so I
keep this repo small by excluding all the other stuff.

# Why make this a GitHub repo

I created this for personal use so I can build my projects that
depend on this library. I keep this repo public so that
my project collaborators have access.

My projects add this repo as a [git
submodule](https://git-scm.com/docs/git-submodule). This lets me
get the FTDI dependencies with a simple `git submodule update
--init` instead of manually downloading from the FTDI website
each time I clone my project repo.

# Library binaries

The pre-compiled libraries are in the `lib` folder:

- dynamic library: `.so` (Linux) and `.dll` (Windows)
- static library: `.a` (Linux and Windows)

See [this YouTube video about static and dynamic linking](https://www.youtube.com/watch?v=UdMRcJwvWIY&t=141s).

I would like to keep life simple and static link the library. The
libMPSSE.a is only 44KB on Windows and 40KB on Linux:

```
$ du -sh lib/windows/mingw/i386/libMPSSE.a
44K     lib/windows/mingw/i386/libMPSSE.a

$ du -sh lib/linux/i386/libMPSSE.a
40K     lib/linux/i386/libMPSSE.a
```

But I don't know how to static link just this library and dynamic
link other libraries.

Whether static or dynamic, these are the Windows linker flags:

```
-Llib/windows/mingw/i386 -lMPSSE
```

Unfortunately, this `i386` pre-compiled binary doesn't work on
64-bit Windows. The linker tried both the `.a` and `.dll` and
rejected them both as incompatible types.
