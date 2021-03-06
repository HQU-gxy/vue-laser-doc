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
# resource-path should be the path of file in here
pandoc -N -s --toc  --pdf-engine=xelatex -V CJKmainfont='STZhongsong' -V geometry:margin=1in protocol/README.md  -o target/protocol.pdf --resource-path protocol/
pandoc -N -s --toc  --pdf-engine=xelatex -V CJKmainfont='STZhongsong' -V geometry:margin=1in manual/README.md  -o target/manual.pdf --resource-path manual/
```

The pre-compiled file should be found in [Releases](https://github.com/crosstyan/vue-laser-doc/releases) of the repo. 

See [Relative images are relative to working directory, not file · Issue #3752 · jgm/pandoc](https://github.com/jgm/pandoc/issues/3752)