# vue-laser-doc
Maybe I should use an organization account: [Transferring a repository - GitHub Docs](https://docs.github.com/en/github/administering-a-repository/managing-repository-settings/transferring-a-repository)
## Main Repo
- [vue-laser-backend](https://github.com/crosstyan/vue-laser-backend) Back
- [vue-laser](https://github.com/crosstyan/vue-laser) Front
## Docs Organization
- `api` Backend API
- `fig` Figures used
- `manual` User Manual
- `protocol` Communication protocol for LoRa/Chirpstack to our backend server
  - `tables` Useful tables of protocol

## Compile to PDF
You need to use [Pandoc](https://pandoc.org/) and [TeX Live](https://www.tug.org/texlive/)

```bash
pandoc -N -s --toc  --pdf-engine=xelatex -V CJKmainfont='STZhongsong' -V geometry:margin=1in protocol/README.md  -o target/protocol.pdf
pandoc -N -s --toc  --pdf-engine=xelatex -V CJKmainfont='STZhongsong' -V geometry:margin=1in manual/README.md  -o target/manual.pdf
```