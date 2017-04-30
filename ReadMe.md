# imageOpt

> A few scripts to help convert/optimize images.

![''][license]

This is a set of image optimizing tools/helpers. Nothing fancy or advanced, just to make it easier to use. 2 scripts are to create/convert files, and the other ones to optimize images.

I used a GUI tool before, but decided to move over to using these scripts instead. Much easier and more convinient. You can use them as they are, or perhaps together with other scripts - as helpers.


## Install

Install it to `/usr/local/bin`, or in another location. Just make sure it's added to PATH.

I use `/usr/local/xbin` for these scripts, so...

```bash
$ cd /path/to/imageOpt/files
$ sudo install -bv -m755 -o0 -g0 mk* *opt /usr/local/xbin
```


## Usage

_For more examples and usage, please refer to the [Wiki][wiki]._

Before you use these scripts, you'll need: `jpegoptim`, `optipng` and `gifsicle`, if not already installed. Each scripts will abort if any dependecies are missing.


#### mkjpg, mkthumb

Both are using ImageMagick (`magick`(IM7) or `convert`(IM6)), and `sips`(macOS) to create the files.

```bash
$ mkjpg file.png [<procent>]    # Default is 100 (%)

$ mkthumb file.jpg              # Result: file_250px.jpg
$ mkthumb file.jpg 400          # Result: file_400px.jpg
                                # Max-size is 500
```


#### jpgopt

`jpgopt` is using `jpegoptim` and `mkjpg` (above). Use 1 or more files, or even the double star `**` to recursively run it from where you're at.

```bash
$ jpgopt /path/to/file.jpg
$ jpgopt /path/to/{more,files}.jpg
$ jpgopt [<procent>] files.jpg  # Default is 80 (%)
```
```bash
$ cd /some/image/folder
$ jpgopt ./**/*.jpg
```

> The line used by `jpegoptim` looks like this:

> ```bash
> jpegoptim -m${_q} -ftPv -s "${_img}";
> ```

You can also run `jpgopt` on your PNG images, to batch _convert->optimize_ your images in one take. It uses `mkjpg` for that. That saves some time.


#### pngopt

`pngopt` is using `optipng`, and works much like `jpgopt`.

```bash
$ pngopt /path/to/file.png
$ pngopt /path/to/{more,files}.png
$ pngopt ./**/*.png
```

> The line used by `optipng` looks like this:

> ```bash
> optipng -strip all -quiet -o7 "${file}" -out "${file}.opt";
> ```
> 
> `-o7` is quite a hard setting, it may take some time on larger files.

If the optimized file doesn't get smaller than the original - it'll keep the original instead.


#### gifopt

`gifopt` is using `gifsicle`. I don't use it that much - just wanted something simular to the 2 ones above.

```bash
$ gifopt [-v] [-c <int>] <file(s)>
$ gifopt <file(s)>
$ gifopt -c 256 <file(s)>
```
`-c 256` is for 256 colors.

> The line used by `optipng` looks like this:
>
> ```bash
> gifsicle ${C}-O3 "${file}" -o "${file}.opt";
> ```


## @todo

- [ ] Invoke `jpgopt`/`pngopt` into `mkthumb`, to save a 2'nd run.


## Contributing

1. Fork it (<https://github.com/iEFdev/imageOpt/fork>)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request


<!-- Markdown link & img dfn's -->
[license]: https://img.shields.io/badge/License-WTFPL-778899.svg?style=plastic
[wiki]: https://github.com/iEFdev/imageOpt/wiki
