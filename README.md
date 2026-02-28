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
pandoc CVDanDinicescu.md -o CVDanDinicescu.pdf \
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
- The hook stops push on build errors (`set -euo pipefail`), so missing `pandoc`/`xelatex` or invalid Markdown/LaTeX blocks the push.
- `SKIP_CV_HOOK=1 git push` bypasses the PDF build if needed.

How it works with the manual command above:

- The manual command is for local testing and one-off generation in the repo.
- The hook enforces the same rendering settings automatically before each push and writes the final PDF to the Desktop target path.
