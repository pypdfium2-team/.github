<!-- SPDX-FileCopyrightText: 2022 geisserml <geisserml@gmail.com> -->
<!-- SPDX-License-Identifier: CC-BY-4.0 -->

# pypdfium2-team

This is the place of development for a liberal-licensed Python PDF rendering library suitable for inclusion in non-copyleft projects, powered by PDFium.


### Supported Environment

* [CPython](https://github.com/python/cpython) >= 3.6 [^1]
* `Windows` amd64 / arm64 / win32
* `macOS` x86_64 (10.13+) / arm64 (11.0+)
* `Linux (glibc 2.26+)` x86_64 / i686 / aarch64 / armv7l
* `Linux (musl 1.2+)` x86_64 / i686


### Installation

```bash
python3 -m pip install pypdfium2
```


### Example

```python
import pypdfium2 as pdfium

# Load a document
filepath = "tests/resources/multipage.pdf"
pdf = pdfium.PdfDocument(filepath)

# render a single page to a PIL image (in this case: the first one)
page = pdf.get_page(0)
pil_image = page.render_to(pdfium.BitmapConv.pil_image)
pil_image.save("output.jpg")
page.close()

# concurrently render multiple pages to PIL images (in this case: all)
page_indices = [i for i in range(len(pdf))]
renderer = pdf.render_to(
    pdfium.BitmapConv.pil_image,
    page_indices = page_indices,
)
for image, index in zip(renderer, page_indices):
    image.save("output_%02d.jpg" % index)
    image.close()

pdf.close()
```


### Advantages

* Liberal license: `Apache-2.0` or `BSD-3-Clause` (at your choice), and various similar licenses for external components of PDFium.
* Wide range of supported platforms and Python versions.
* No mandatory runtime dependencies.
* Can process encrypted (password-protected) PDFs.
* Rendering is fast, outperforming [`ghostscript`](https://github.com/ArtifexSoftware/ghostpdl) and [`poppler`](https://gitlab.freedesktop.org/poppler/poppler). In terms of speed, pypdfium2 can almost reach [`pymupdf`](https://github.com/pymupdf/PyMuPDF).
* Multiple choices for the rendering return type:
    * [`ctypes.c_ubyte`](https://docs.python.org/3/library/ctypes.html#fundamental-data-types) [array](https://docs.python.org/3/library/ctypes.html#arrays)
    * [`bytes`](https://docs.python.org/3/library/stdtypes.html#bytes)
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

For pdfium documentation, please look at the comments in its public header files (`public/*.h`). [^2]

[^1]: PyPy might work but is not tested. Similarly, pypdfium2 might still be compatible with Python 3.5 / 3.4, but this is not tested either.

[^2]: There are still some [outdated Foxit HTML docs](https://developers.foxit.com/resources/pdf-sdk/c_api_reference_pdfium/group___f_p_d_f_i_u_m.html), but using them is strongly discouraged.
