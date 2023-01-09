# FTDI link

This is part of FTDI `LibMPSSE DLL` [downloaded from
FTDI](https://www.ftdichip.com/old2020/Support/SoftwareExamples/MPSSE/LibMPSSE-I2C.htm)
on Mon, Jan  9, 2023.

I wrote this README and the `.gitignore`. Everything else is from
FTDI.

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
