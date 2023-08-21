# imageOpt

> A few scripts to help convert/optimize images.

![][license]

This is a set of image optimizing tools/helpers. Nothing fancy or advanced, but just to make it easier to use. 2 scripts are to create/convert files, and the other ones to optimize images.

I used a GUI tool before, but decided to move over to using these scripts instead. Much easier and more convinient, and I can use the same set of scripts in both GNU/Linux and macOS. You can use them as they are, or perhaps together with other scripts - as helpers.


## Install

Install the files to /usr/local/bin, or to any other location. Just make sure it's added to PATH.

I use `/usr/local/xbin` for these scripts, so...

```bash
$ cd /path/to/imageOpt/files
$ sudo install -v -m755 -o0 -g0 mk* *opt /usr/local/xbin
```

## Dependencies

You'll need to have these programs installed:

- `convert` (ImageMagick), or `magick` (ImageMagick v7),
- `jpegoptim`
- `optipng`
- `gifsicle`

Each scripts will abort if any dependecies are missing.

_Refer to your package manager (pacman, dnf, apt, port, etc), or compile from source._


## Usage

#### mkjpg, mkthumb

Both are using ImageMagick (`magick`(IM7) or `convert`(IM6)), and `sips`(macOS) to create the files.

```bash
$ mkjpg -h
# Usage:
#   mkjpg [ % ] file.png        Default is 100 (%)
#   mkjpg 60 file.png           60%
#   mkjpg **/{more,files}.png   Mulltiple images
#   mkjpg -h                    Show help

$ mkthumb -h
# Usage:
#   mkthumb file.jpg            Result: file_250px.jpg
#   mkthumb 400 file.jpg        Result: file_400px.jpg
#   mkthumb **/{foo,bar}.jpg    Multiple images
#   mkthumb -h                  Show help
```


#### jpgopt

`jpgopt` is using `jpegoptim` and `mkjpg` (above). Use 1 or more files, or even the double star `**` to recursively run it from where you're at.

```bash
$ jpgopt -h
# Usage:
#   jpgopt [ % ] file.jpg       Default is 100 (%)
#   jpgopt 60 file.jpg          60% quality
#   jpgopt **/{more,files}.jpg  More files
#   jpgopt -h                   Show help
```

The line used by `jpegoptim` looks like this:

```bash
jpegoptim -m${_q} -ftPv -s "${_img}";
```

You can also run `jpgopt` on your PNG images, to batch _convert->optimize_ your images in one take. It uses `mkjpg` for that. That saves some time.


#### pngopt

`pngopt` is using `optipng`, and works like `jpgopt`.

```bash
$ pngopt -h
# Usage:
#   pngopt [-v] <file(s)>       1 or more files
#   pngopt -h                   Show help
```

The line used by `optipng` looks like this:

```bash
optipng -strip all -quiet -o7 "${file}" -out "${file}.opt";
```

`-o7` is quite a hard setting, it may take some time on larger files.

If the optimized file doesn't get smaller than the original - it'll keep the original instead.


#### gifopt

`gifopt` is using `gifsicle`. I don't use it that much - just wanted something simular to the 2 ones above.

```bash
$ gifopt -h
# Usage:
#   gifopt [-v] [-c <int>] <file(s)>        1 or more files
#   gifopt -h                               Show help
```

The line used by `optipng` looks like this:

```bash
gifsicle ${C}-O3 "${file}" -o "${file}.opt";
```


## Contributing

1. Fork it (<https://gitlab.com/iefdev/imageOpt/forks/new>)
2. Create your feature branch (`git switch -c feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Merge Request


<!-- Markdown link & img dfn's -->
[license]: https://img.shields.io/badge/License-0BSD-789.svg?style=plastic "BSD Zero Clause License (SPDX: 0BSD)"
[wiki]: https://gitlab.com/iefdev/imageOpt/wikis/
