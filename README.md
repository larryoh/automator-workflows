# Tunghsiao Liu’s Automator Workflows

A collection of Automator workflows that speed up your design and development process. Compatible with LaunchBar 6 and 7.

## Installation

Paste the following code at a Terminal prompt:

```shell
bash <(curl -fsSL https://raw.github.com/sparanoid/automator-workflows/go/install)
```

The script explains what it will do and then pauses before it does it. If you don’t trust it, [download zip package](https://github.com/sparanoid/automator-workflows/releases) and manually copy the workflows to `~/Library/Services/`.

## Other Notes

Please note that some workflows are using third-party scripts, the default path of them (for example `imagemagick`) is `/usr/local/bin/imagemagick`. (Installed by [Homebrew](https://brew.sh/)).

## Available Workflows

- [Create App Iconset](#create-app-iconset)
- [Create .icns](#create-icns)
- [Unpack .icns](#unpack-icns)
- [Create `favicon.ico`](#create-faviconico)
- [Create `favicon.ico` (multi-resource)](#create-faviconico-multi-resource)
- [Add `@2x` (`@3x`) Suffix](#add-2x-3x-suffix)
- [Copy & Add `@2x` (`@3x`) Suffix](#copy--add-2x-3x-suffix)
- [Create `@2x` (`@3x`) Image](#create-2x-3x-image)
- [Remove `@2x` (`@3x`) Suffix](#remove-2x-3x-suffix)
- [Convert Image Format](#convert-image-format)
- [Resize Images](#resize-images)
- [Rename Selected Files](#rename-selected-files)
- [Create DMG Image](#create-dmg-image)
- [Open with rmate](#open-with-rmate)
- [Compress Images](#compress-images)
- [Encode Selected Files Using Base64](#encode-selected-files-using-base64)
- [Convert Selected Text to Audio File](#convert-selected-text-to-audio-file)
- [Convert .ass to .srt](#convert-ass-to-srt)

### Create App Iconset

Create the following sizes of icon resources for your OS X app:

Filename | Size of canvas (in pixels)
--- | ---
icon_512x512@2x | 1024×1024
icon_512x512    | 512×512
icon_256x256@2x | 512×512
icon_256x256    | 256×256
icon_128x128@2x | 256×256
icon_128x128    | 128×128
icon_32x32@2x   | 64×64
icon_32x32      | 32×32
icon_16x16@2x   | 32×32
icon_16x16      | 16×16

The icon you created should be 1024×1024 with an sRGB color profile. You can read more about icon design guidelines [here](https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/OSXHIGuidelines/Designing.html).

**Note**: You should always select the original file during the workflow, don’t press any key or click your mouse.

### Create .icns

Create .icns file using `iconutil`. Command Line Tools from Xcode must be installed before using this workflow.

### Unpack .icns

Unpack .icns into .iconset folder. Command Line Tools from Xcode must be installed before using this workflow.

### Create `favicon.ico`

Create a `favicon.ico` from selected PNG image with [ImageMagick](http://www.imagemagick.org/).

**Requires**: `imagemagick`

**Notes**:

1. The generated `favicon.ico` also works on all platforms include high-res devices. The different from “multi-resource” action is only 64x64 (4x) resource is generated, so you'll get smaller file size.
2. Sometimes you'll get `convert: iCCP: extra compressed data` error when process PNGs exported from Photoshop, if you got this error, try to compress exported PNGs to remove extra metadata (for example using [Compress Images](#compress-images) workflow or [ImageOptim](https://imageoptim.com/)).

### Create `favicon.ico` (multi-resource)

Create a multi-resource `favicon.ico` from selected PNG image with [ImageMagick](http://www.imagemagick.org/), 64x64, 32x32, and 16x16 are included.

**Requires**: `imagemagick`

**Notes**:

1. You should only select one image, then multi-resource icos are automatically scaled down.
2. The selected image should be at least 48x48, for best result, use exact 48x48.

### Add `@2x` (`@3x`) Suffix

Add `@2x` or (`@3x`) suffix for retina image assets.

### Copy & Add `@2x` (`@3x`) Suffix

Copy (duplicate) selected images and rename them with `@2x` or (`@3x`)  suffix. Useful when you want to downscale with your own method.

### Create `@2x` (`@3x`) Image

Auto downscale retina images generated by [PNG Express](http://www.pngexpress.com/), or any “@2x” / “@3x” images.

**Notes**:

1. Export your original images in retina size, WITHOUT `@2x` or (`@3x`) suffix.
2. Create `@3x` Image doesn't downscale images properly at the moment. Need a better method to handle it.

### Remove `@2x` (`@3x`) Suffix

Remove `@2x` and (`@3x`) suffix for retina image assets. Useful when you’re doing something wrong and need to recreate downscaled images one more time.

### Convert Image Format

Convert selected images to specific format.

### Resize Images

Resize your images to specific size or by percentage.

### Rename Selected Files

![Rename Finder Items](https://raw.github.com/sparanoid/rsrc/automator-workflows/01-rename-finder-items.png)

What? You just bought [A Better Finder Rename](http://www.publicspace.net/ABetterFinderRename/)?

### Create DMG Image

Create distributable, cross-platform hybrid DMG images using `hdiutil`, select a directory first to use this script. You’ll be prompted to enter a volume name for your image, then Voilà!

**Note**: This script doesn’t create “fancy” DMG for your OS X app.

### Open with rmate

Open selected file with [rmate](https://github.com/textmate/rmate).

**Requires**: `rmate`

### Compress Images

Compress selected images based on file type, `.png`, `.jpg`, and `.svg` are supported. It auto detects the file type of selected images and compress them. [OptiPNG](http://optipng.sourceforge.net/), [Pngcrush](http://pmt.sourceforge.net/pngcrush/), [jpegoptim](https://github.com/tjko/jpegoptim), and [svgo](https://github.com/svg/svgo) are used.

**Requires**:

- `optipng` (bundled)
- `pngcrush` (bundled)
- `jpegoptim`
- `svgo`

**Notes:**

1. The default compress options for each type of images is the same as the individual compress workflow.
2. It’s okay to run this workflow if you only install some of required dependencies, for example, you can just installed `jpegoptim`, but only `.jpg` will be compressed when you run this workflow, all other SVG files you selected will be skipped.
3. The default `optipng` compress option is set to `-o7` (smallest file size and slowest), you may need change that.
4. The default `pngcrush` compress option is set to `-brute -reduce -ow` (try 138 different methods and do lossless color-type or bit-depth reduction), you may need change that.
5. `pngcrush` will take longer time for large images.
6. The default `jpegoptim` compress option is set to `--strip-all --force --all-progressive` (lossless compression, remove comment, Exif and ICC profile, force all outputs to be progressive), You may need change that.

### Encode Selected Files Using Base64

Encode Selected Files using Base64 for [data URI scheme](https://en.wikipedia.org/wiki/Data_URI_scheme).

### Convert Selected Text to Audio File

Convert selected text to audio file (AIFF) in any application

### Convert .ass to .srt

Convert .ass subtitles to .srt subtitles. [sorz/asstosrt](https://github.com/sorz/asstosrt) must be installed before using this workflow.

## Author

**Tunghsiao Liu**

- Twitter: @[tunghsiao](https://twitter.com/tunghsiao)
- GitHub: @[sparanoid](https://github.com/sparanoid)

## License

MIT
