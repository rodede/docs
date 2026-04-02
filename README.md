# docs

- [CV Dan Dinicescu](CVDanDinicescu.md)
- [To remember](utils.md)

## Tools

Install the required tools for converting a .md file to a clean .pdf (LaTeX engine)

```bash
brew install pandoc
brew install --cask mactex-no-gui
```

## Build CV PDF manually

```bash
pandoc CVDanDinicescu.md -o /Users/rodede/Desktop/perso/CVDanDinicescu.pdf \
  --pdf-engine=xelatex \
  -V mainfont="Arial" \
  -V geometry:margin=1in \
  -V fontsize=11pt \
  -V linestretch=1.2 \
  --metadata colorlinks=true --metadata urlcolor=black --metadata linkcolor=black
```

## Pre-push automation

`.git/hooks/pre-push` runs the same `pandoc` command on every `git push`.

- Input: `CVDanDinicescu.md` (from this repo)
- Output: `/Users/rodede/Desktop/perso/CVDanDinicescu.pdf`
