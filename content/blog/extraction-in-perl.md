---
title: "Text Extraction in Perl"
date: 2025-03-14T00:00:00+00:00
description: "Discussion about text extraction from image in Perl."
type: post
image: images/blog/extraction-in-perl.png
author: Mohammad Sajid Anwar
tags: ["Perl"]
---

#### **DISCLAIMER:** Image is generated using `FREE` version of `ChatGPT`.
***

<br>

<div class="container">
    <div class="row">
        <div class="col-12 col-sm mb-4 p-2 text-center">
            <a href="/blog/slurp-in-perl" title="Slurp in Perl">
                <img src="/images/blog/slurp-mini.png" class="img-fluid">
            </a>
        </div>
        <div class="col-12 col-sm mb-4 p-2 text-center">
            <a href="/blog/scientist-in-perl" title="Scientist in Perl">
                <img src="/images/blog/scientist-in-perl-mini.png" class="img-fluid">
            </a>
        </div>
        <div class="col-12 col-sm mb-4 p-2 text-center">
            <a href="/blog/extraction-in-perl" title="Text Extraction in Perl">
                <img src="/images/blog/subroutine-signatures-mini.png" class="img-fluid">
            </a>
        </div>
        <div class="col-12 col-sm mb-4 p-2 text-center">
            <a href="/blog/random-in-perl" title="Random in Perl">
                <img src="/images/blog/random-in-perl-mini.png" class="img-fluid">
            </a>
        </div>
        <div class="col-12 col-sm mb-4 p-2 text-center">
            <a href="/blog/perl-regex" title="Perl Regex">
                <img src="/images/blog/perl-regex-mini.png" class="img-fluid rounded-3 border border-3">
            </a>
        </div>
        <div class="col-12 col-sm mb-4 p-2 text-center">
            <a href="/blog/read-large-file" title="Read Large File">
                <img src="/images/blog/read-large-file-mini.png" class="img-fluid">
            </a>
        </div>
        <div class="col-12 col-sm mb-4 p-2 text-center">
            <a href="/blog/welcome-to-perl" title="Welcome to Perl">
                <img src="/images/blog/welcome-to-perl-mini.png" class="img-fluid">
            </a>
        </div>
    </div>
</div>

<br>

## Text Extraction in Perl
***

I have always been fascinated about image processing but never got my head around it.

Even today, I barely know anything about it.

Text extraction from image is something, I always wanted to try but never managed to do it successfully.

I tried first in `Perl` but when I failed in my attempt then I tried in `Python`.

None worked for me, I would partially blame it on my local development environment.

Now I have a rather stable environment i.e. `Ubuntu 24.04.1 LTS` running on `WSL2`.

The first task is to find a suitable `OCR Engine` that is easy to install in my local environment.

Luckily, it didn't take long to find one, i.e. [**Tesseract OCR**](https://github.com/tesseract-ocr/tesseract).

Time to install the `Ubuntu` package for the `OCR Engine`.

<br>

    $ sudo apt install tesseract-ocr

<br>

Let's verify if everything installed properly, first thing:

<br>

    $ tesseract -v
    tesseract 5.3.4

<br>

Having done the hard bit, now we want `Perl` interface to the `Tesseract OCR Engine`.

The good old friend `CPAN` came handy as always.

Quick search and I found this module [**Image::OCR::Tesseract**](https://metacpan.org/dist/Image-OCR-Tesseract).

Let's quickly install the module using my favourite tool `cpanm`.

<br>

    $ cpanm -vS Image::OCR::Tesseract

<br>

Having prepared the ground, now time for some fun.

The `Perl` programmer inside me, quickly jumped and wrote this cute little script `extract-text.pl`:

<br>

```perl
#!/usr/bin/env perl

use v5.38;
use Image::OCR::Tesseract qw/get_ocr/;
say get_ocr($ARGV[0]);
```

<br>

For this, I need a simple image with some text in it.

I created a very basic image, `tesseract.png` using `Paint` app.

<br>

<div class="container">
    <div class="row">
        <div class="col-12 col-sm mb-4 p-2 text-center">
            <img src="/images/blog/tesseract.png" class="img-fluid">
        </div>
    </div>
</div>

<br>

Now time for some action, fingers crossed:

<br>

    $ perl extract-text.pl tesseract.png
    Hello World from Perl

<br>

Having done this, I thought why bother with script and came up with this one-liner instead.

<br>

    $ perl -MImage::OCR::Tesseract=get_ocr -E 'say get_ocr($ARGV[0])' tesseract.png
    Hello World from Perl

<br>

Still not happy, too much typing.

Finally checked the documentation of the `CPAN` module [**Image::OCR::Tesseract**](https://metacpan.org/dist/Image-OCR-Tesseract) and noticed it comes with a cute little program `ocr`.

Now you can't beat this, can you?

<br>

    $ ocr tesseract.png
    Hello World from Perl

<br>

***

Happy Hacking !!!
