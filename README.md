puremagic
=========

puremagic is a pure python module that will identify a file based off it's
magic numbers.

[![Build Status](https://travis-ci.org/cdgriffith/puremagic.png?branch=master)](https://travis-ci.org/cdgriffith/puremagic)

It is designed to be minimalistic and inherently cross platform
compatible. However this does come at the price of being incomplete.
It is also designed to be a stand in for python-magic, it incorporates the
functions from_file(filename[, mime]) and from_string(string[, mime])
however the magic_file() and magic_string() are more powerful and will also
display confidence and duplicate matches.

Advantages over using a wrapper for 'file' or 'libmagic':

* Faster
* Lightweight
* Cross platform compatible
* No dependencies
    
Disadvantages:

* Does not have as many file types
* No multilingual comments
* Duplications due to small or reused magic numbers

(Help fix the first two disadvantages by contributing!)

### Compatibility:

* Python 2.6+
* Python 3.2+
* Pypy

Using travis-ci to run continuous integration tests on listed platforms.
(Note: Tested on 'Python' I mean 'CPython' implementation specifically, though
it should work on other implementations as well.)


## Install

In either a virtualenv or globally, simply run:

```bash
    $ python setup.py install
```

It has no dependencies (other than the 2.7+ built-in argparse)
        
## Usage

`from_file` will return the most likely file extension. `magic_file` will give
you every possible result it finds, as well as the confidence.

```python
    import puremagic

    filename = "test/resources/images/test.gif"

    ext = puremagic.from_file(filename)
    # '.gif'

    puremagic.magic_file(filename)
    # (2, [['.gif', 'image/gif', 'Graphics interchange format file (GIF87a)', 0.7],
    #      ['.gif', '', 'GIF file', 0.5]])

```

With `magic_file` it gives
you the count of matching items first, then for each match provides:

- possible extension(s)
- mime type
- description
- confidence (All headers have to perfectly match to make the list, however this orders it by longest header, therefore most precise, first)


## Script

*Usage*

```bash
    $ python -m puremagic [options] filename <filename2>...
```

*Examples*

```bash
    $ python -m puremagic test/resources/images/test.gif
    'test/resources/images/test.gif' : .gif

    $ python -m puremagic -m test/resources/images/test.gif test/resources/audio/test.mp3
    'test/resources/images/test.gif' : image/gif
    'test/resources/audio/test.mp3' : audio/mpeg

```

## FAQ

*The file type is actually X but it's showing up as Y with higher confidence?*

This can happen when the file's signature happens
to match a subset of a file standard. The subset signature will be longer,
therefore report with greater confidence, because it will have both the base
file type signature plus the additional subset one.

*Your version isn't as complete as I want it to be, where else should I look?*

Look into python modules that wrap around libmagic or use something like Apache Tika.


## Acknowledgements

Gary C. Kessler

    For use of his File Signature Tables, available at:
    http://www.garykessler.net/library/file_sigs.html

Freedesktop.org

    For use of their shared-mime-info file, available at:
    https://cgit.freedesktop.org/xdg/shared-mime-info/

## License

MIT Licenced, see LICENSE, Copyright (c) 2013-2016 Chris Griffith