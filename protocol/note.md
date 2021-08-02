Compile to PDF

```bash
pandoc -N -s --toc  --pdf-engine=xelatex -V CJKmainfont='STZhongsong' -V geometry:margin=1in doc.md  -o output.pdf
```