<!-- SPDX-FileCopyrightText: 2022 geisserml <geisserml@gmail.com> -->
<!-- SPDX-License-Identifier: CC-BY-4.0 -->

# pypdfium2-team

This is the place of development for a liberal-licensed Python PDF rendering library suitable for inclusion in non-copyleft projects, powered by PDFium.


### Supported Environment

* Python >= 3.6 [^1] ([CPython](https://github.com/python/cpython) or [PyPy](https://foss.heptapod.net/pypy/pypy))
* `Windows` amd64 / arm64 / win32
* `macOS` x86_64 (10.11+) / arm64 (11.0+)
* `Linux (glibc 2.17+)` x86_64 / i686 / aarch64 / armv7l
* `Linux (musl 1.2+)` x86_64 / i686


### Installation

```bash
python3 -m pip install pypdfium2
```


### Example

```python3
import pypdfium2 as pdfium

pdffile = 'path/to/your_doc.pdf'

# render a single page (in this case: the first one)
with pdfium.PdfContext(pdffile) as pdf:
    image = pdfium.render_page_topil(pdf, 0)
    image.save('output.jpg')

# render multiple pages concurrently (in this case: all)
for image, suffix in pdfium.render_pdf_topil(pdffile):
    image.save('output_%s.jpg' % suffix)
```


### Advantages

* Liberal license: Apache 2.0 or BSD-3-Clause (at your choice), and various similar licenses for external components of PDFium.
* Wide range of supported platforms and Python versions.
* Minimal runtime dependencies.
* Rendering is fast, outperforming `ghostscript` and `poppler`. In terms of speed, pypdfium2 can almost reach `pymupdf`.
* Multiple choices for the rendering return type:
    * [`PIL.Image.Image`](https://pillow.readthedocs.io/en/stable/reference/Image.html#PIL.Image.Image)
    * [`bytes`](https://docs.python.org/3/library/stdtypes.html#bytes)
    * ctypes ubyte array
* Can process encrypted (password-protected) PDFs.
* State-of-the-art setup infrastructure (PEP [517](https://peps.python.org/pep-0517/)/[518](https://peps.python.org/pep-0518/) compliant).


### References

* [pypdfium2 repository](https://github.com/pypdfium2-team/pypdfium2) (with [support model code](https://github.com/pypdfium2-team/pypdfium2/tree/main/src/pypdfium2/_helpers) and [examples](https://github.com/pypdfium2-team/pypdfium2/tree/main/examples))
* [pypdfium2 documentation](https://pypdfium2.readthedocs.io/en/stable/)
* [ctypes documentation](https://docs.python.org/3/library/ctypes.html)
* [pdfium repository](https://pdfium.googlesource.com/pdfium/+/refs/heads/main)
* [pdfium documentation](https://developers.foxit.com/resources/pdf-sdk/c_api_reference_pdfium/group___f_p_d_f_i_u_m.html)
* [pdfium merge requests](https://pdfium-review.googlesource.com/)
* [pdfium bug tracker](https://bugs.chromium.org/p/pdfium/issues/list)
* [pdfium mailing list](https://groups.google.com/g/pdfium)


[^1]: Older versions might work but are not tested.
