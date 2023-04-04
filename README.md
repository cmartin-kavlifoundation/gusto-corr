# README for the gusto-corr repository

Omnisys correlator prototype software

A series of Python 3 scripts is included to initialize, calibrate, and read data from a correlator.

Optionally, C code for `corrspec` to watch for lag files delivered by NFS or TFTP and FFT's of the lags done for spectra output.  This relies on either inotify or fswatch.

## Prerequisites:
### libiT Information Theory C library
Provides a C library for access to the inverse error function erfinv( ) which takes the Hi and Lo count values as inputs to the P_I and P_Q power scaling factors along with the DAC Voltage settings.

libit.sourceforge.net/index.html

Installation of the library  is to download libit-0.2.3 from sourceforge and install where the FFT of the lags will be done.

Fix some things

1) in src/convcode.c:53, fls=>fls2, as well as name changed through.  Todo: make a patch for this, or even better fix it and use the one in strings.h if possible.

To install on OS X:
```
./configure --target=x86_64 --prefix=/opt/local
make
make install
```
Assuming you've installed libit in a local library directory, add that to the corrspec Makefile.

### fftw-3
FFTW is used to perform the FFT of lags to spectra.  Installation from either a debian or Macports repository is adequate.
Mac:
```
sudo port install fftw-3
```

### Optional: inotify is not available in OS X, so fswatch is complied as an option to corrspec

Getting fswatch
---------------

A regular user may be able to fetch `fswatch` from the package manager of your
OS or a third-party one.  If you are looking for `fswatch` for macOS, you can
install it using either [MacPorts] or [Homebrew]:

```
# MacPorts
$ port install fswatch

# Homebrew
$ brew install fswatch
```

On FreeBSD, `fswatch` can be installed using [pkg]:

```console
# pkg install fswatch-mon
```

### corrspec
To compile `corrspec`

```
make dict
make corrspec
```
