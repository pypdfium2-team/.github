<!-- SPDX-FileCopyrightText: 2025 geisserml <geisserml@gmail.com> -->
<!-- SPDX-License-Identifier: CC-BY-4.0 -->

# pypdfium2-team

This is the place of development for a liberal-licensed[^1] Python PDF rendering library, powered by PDFium.


### Supported Environment

* [CPython](https://github.com/python/cpython) >= 3.6 [^2]
* `Windows` amd64 / arm64 / win32
* `macOS` x86_64 (10.13+) / arm64 (11.0+)
* `Linux (glibc)` x86_64 / i686 / aarch64 / armv7l
* `Linux (musl)` x86_64 / i686 / aarch64
* `Android` arm64_v8a / armeabi_v7a (+ x86_64 / x86 simulators) (experimental)
* `iOS` arm64 (+ arm64 / x86_64 simulators) (experimental, untested)

These are the platforms supported with pre-built binaries.
In principle, pypdfium2 may run anywhere provided you are able to procure a pdfium build for the platform.[^3]


### Installation

```bash
python3 -m pip install pypdfium2
```


### Example

```python
import pypdfium2 as pdfium

# Load a document
pdf = pdfium.PdfDocument("tests/resources/multipage.pdf")

# Loop over pages and render
for i in range(len(pdf)):
    page = pdf[i]
    image = page.render(scale=4).to_pil()
    image.save(f"output_{i:03d}.jpg")
```


### Advantages

* Liberal license (`BSD-3-Clause`, `Apache-2.0`, plus various other open-source licenses for third-party components of PDFium.)
* Wide range of supported platforms and Python versions.
* No mandatory runtime dependencies.
* Can process encrypted (password-protected) PDFs.
* Fast rendering (probably outperforming [`poppler`](https://gitlab.freedesktop.org/poppler/poppler) and [`ghostscript`](https://github.com/ArtifexSoftware/ghostpdl)). In terms of speed, pypdfium2 can almost reach [`pymupdf`](https://github.com/pymupdf/PyMuPDF).
* Multiple choices for the rendering return type:
    * [`ctypes.c_ubyte`](https://docs.python.org/3/library/ctypes.html#fundamental-data-types) [array](https://docs.python.org/3/library/ctypes.html#arrays)
    * [`PIL.Image.Image`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image)
    * [`numpy.ndarray`](https://numpy.org/doc/stable/reference/generated/numpy.ndarray.html)


### References

* [pypdfium2 repository](https://github.com/pypdfium2-team/pypdfium2) (with [support model code](https://github.com/pypdfium2-team/pypdfium2/tree/main/src/pypdfium2/_helpers))
* [pypdfium2 documentation](https://pypdfium2.readthedocs.io/en/stable/)
* [ctypes documentation](https://docs.python.org/3/library/ctypes.html)
* [pdfium repository](https://pdfium.googlesource.com/pdfium/+/refs/heads/main)
* [pdfium merge requests](https://pdfium-review.googlesource.com/)
* [pdfium bug tracker](https://bugs.chromium.org/p/pdfium/issues/list)
* [pdfium mailing list](https://groups.google.com/g/pdfium)

For pdfium documentation, please look at the comments in its public header files (`public/*.h`).

[^1]: Disclaimer: This is not legal advice. While we hope this project is useful to others, there is ABSOLUTELY NO WARRANTY. It is the embedder's responsibility to check on licensing. See also [GitHub's disclaimer](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository#disclaimer).
[^2]: PyPy might work but is not tested.
[^3]: Other rare operating systems / CPU architectures exist, such as `FreeBSD`, `Illumos`, `Haiku`, `SerenityOS` / `PowerPC`, `s390x`, `LoongArch`, but it is not possible to provide pre-builds for any arbitrary platform under the roof of this project. In particular, we are limited to targets covered by Google's toolchain/sysroots, or native GitHub actions runners, and by the portability of pdfium's code itself (notably, there might be endianness bugs on big-endian platforms, pdfium's Readme acknowledges this). Building/packaging pdfium for other platforms is down to porting experts or technically accomplished end users from the respective projects. Where the host system provides pdfium and standard `ctypes.util.find_library()` means can find it, pypdfium2's setup theoretically should work even on unhandled platforms (if not, please file a bug report). Moreover, on non-covered CPUs of supported OSes (or more generally: any host supported by pdfium's GN build system), the [native sourcebuild](https://github.com/pypdfium2-team/pypdfium2?tab=readme-ov-file#install-source-selfbuilt) should work if system-level dependencies are installed (pypdfium2's `setup.py` will attempt this as a last resort).
