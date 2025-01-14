# (Py)OrthoANI [![Stars](https://img.shields.io/github/stars/althonos/orthoani.svg?style=social&maxAge=3600&label=Star)](https://github.com/althonos/orthoani/stargazers)

*A Python implementation of the [OrthoANI](https://doi.org/10.1099/ijsem.0.000760) algorithm for nucleotide identity measurement.*

[![Actions](https://img.shields.io/github/actions/workflow/status/althonos/orthoani/test.yml?branch=main&logo=github&style=flat-square&maxAge=300)](https://github.com/althonos/orthoani/actions)
[![License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square&maxAge=2678400)](https://choosealicense.com/licenses/mit/)
[![Source](https://img.shields.io/badge/source-GitHub-303030.svg?maxAge=2678400&style=flat-square)](https://github.com/althonos/orthoani/)
[![Coverage](https://img.shields.io/codecov/c/gh/althonos/orthoani?style=flat-square&maxAge=3600)](https://codecov.io/gh/althonos/orthoani/)
[![PyPI](https://img.shields.io/pypi/v/orthoani.svg?style=flat-square&maxAge=600)](https://pypi.org/project/orthoani)
[![Wheel](https://img.shields.io/pypi/wheel/orthoani.svg?style=flat-square&maxAge=3600)](https://pypi.org/project/orthoani/#files)
[![Python Versions](https://img.shields.io/pypi/pyversions/orthoani.svg?style=flat-square&maxAge=600)](https://pypi.org/project/orthoani/#files)
[![Python Implementations](https://img.shields.io/pypi/implementation/orthoani.svg?style=flat-square&maxAge=600)](https://pypi.org/project/orthoani/#files)
[![Source](https://img.shields.io/badge/source-GitHub-303030.svg?maxAge=2678400&style=flat-square)](https://github.com/althonos/orthoani/)
[![GitHub issues](https://img.shields.io/github/issues/althonos/orthoani.svg?style=flat-square&maxAge=600)](https://github.com/althonos/orthoani/issues)
[![Changelog](https://img.shields.io/badge/keep%20a-changelog-8A0707.svg?maxAge=2678400&style=flat-square)](https://github.com/althonos/orthoani/blob/master/CHANGELOG.md)
[![Downloads](https://img.shields.io/pypi/dm/orthoani?style=flat-square&color=303f9f&maxAge=86400&label=downloads)](https://pepy.tech/project/orthoani)


## 🗺️ Overview

OrthoANI is a metric proposed by Lee *et al.*[\[1\]](#ref1)
in 2016 to improve computation of Average Nucleotide Identity. It uses
[BLASTn](https://en.wikipedia.org/wiki/BLAST_(biotechnology)) to find orthologous
blocks in a pair of sequences, and then computes the average identity only
considering alignments of reciprocal orthologs.

![Algorithm](https://www.microbiologyresearch.org/docserver/fulltext/ijsem/66/2/000760-f1.gif)

This project is a reimplementation of the closed-source Java implementation
provided by the authors on [`ezbiocloud.net`](https://www.ezbiocloud.net/sw/oat).
It relies on [Biopython](https://biopython.org/) to handle the I/O, and calls
the BLAST+ binaries using the `subprocess` module of the Python standard 
library.


## 🔧 Installing

Installing with `pip` is the easiest:
```console
$ pip install orthoani
```

`orthoani` also requires the BLAST+ binaries to be installed on your machine
and available somewhere in your `$PATH`.


## 💡 Example

Use Biopython to load two FASTA files, and then `orthoani.orthoani` to compute
the OrthoANI metric between them:
```python
import orthoani
from Bio.SeqIO import read

genome_1 = read("sequence1.fa", "fasta")
genome_2 = read("sequence2.fa", "fasta")

ani = orthoani.orthoani(genome_1, genome_2)
```

`orthoani` can also be used from the CLI using a very simple command-line
interface:
```console
$ orthoani -q sequence1.fa -r sequence2.fa
57.25
```


## 💡 Multiple sequences

run the script orthoani.py in the folder that there are the .fasta archives
remember modify the path to the diretory

```
python orthoani.py 
```


## 🐏 Memory

`orthoani` uses the machine temporary folder to handle BLAST+ input and output
files, which is configurable through
[`tempfile.tempdir`](https://docs.python.org/3/library/tempfile.html#tempfile.tempdir).
On some systems (like ArchLinux), this filesystem can reside in memory, which means
that your computer could have trouble processing very large files. If this
happens, try changing the value of the `tempfile.tempdir` to a directory that
is actually located on physical storage.


## 📏 Precision

Values computed by this package and the original Java implementation may differ
slightly because in Java the authors perform rounding of floating-point values
at the sub-percent level, while this library uses the full values.


## 📜 About

This library is provided under the open-source
[MIT license](https://choosealicense.com/licenses/mit/).

*This project is in no way not affiliated, sponsored, or otherwise endorsed by
the [original OrthoANI authors](http://www.chunlab.com/). It was developed by
[Martin Larralde](https://github.com/althonos/orthoani) during his PhD project
at the [European Molecular Biology Laboratory](https://www.embl.de/) in
the [Zeller team](https://github.com/zellerlab).*

## 📚 References

- <a id="ref1">\[1\]</a> Imchang Lee, Yeong Ouk Kim, Sang-Cheol Park and Jongsik Chun. *OrthoANI: An improved algorithm and software for calculating average nucleotide identity* (2016). International Journal of Systematic and Evolutionary Microbiology. [doi:10.1099/ijsem.0.000760](https://doi.org/10.1099/ijsem.0.000760). [PMID:26585518](https://pubmed.ncbi.nlm.nih.gov/26585518/).
