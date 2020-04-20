---
output:
  pdf_document: default
  html_document: default
---
#  Unpack deb without installing
1.  Unpack it.
```bash
  dpkg -x package.deb dir
```
2.  Add the path to your path. Done!

# Rotate pdf files from terminal

```bash
pdftk input.pdf cat 1-endeast output output.pdf
```
90^0^ rotate:
```
pdftk input.pdf cat 1-endnorth output output.pdf
```

# Trim white boarders of pdf

```bash
pdftrimwhite in.pdf out.pdf
```


# Select out a page from pdf

```bash
pdftk from.pdf cat PAGE_NUMBER output out.pdf
```

# Disable animations

```bash
gsettings set org.gnome.desktop.interface enable-animations false
```

Can be set to true to revert effects.

# Reduce pdf file size

```bash
gs -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=setting -sOutputFile=output.pdf input.pdf
```
setting is changed into "/screen," the lowest resolution and lowest file size, but fine for viewing on a screen; "/ebook," a mid-point in resolution and file size; "/printer" and "/prepress," high-quality settings used for printing PDFs.
