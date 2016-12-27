fips-nfd
=========

[![Build Status](https://travis-ci.org/fungos/fips-nfd.svg?branch=travis-ci)](https://travis-ci.org/fungos/fips-nfd)

fipsified nativefiledialog (https://github.com/mlabbe/nativefiledialog)

fips build system: https://github.com/floooh/fips

To use nfd you need just to add it to your `fips.yml`:

```cmake
imports:
     fips-nfd:
         git: https://github.com/fungos/fips-nfd.git
```

And them add a dependency to your project using `fips_deps(nfd)`.