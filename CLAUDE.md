# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a University of Aveiro (UA) thesis template running in a WebLaTeX environment on GitHub Codespaces. It combines:
- **UA Thesis Template**: Professional thesis/dissertation template with department-specific formatting
- **WebLaTeX Environment**: LaTeX editor with full Git integration, GitHub Copilot, Grammarly support, and live collaboration features

The project is built on top of the `sanjibsen/weblatex:latest` Docker image with additional dependencies for the UA template (pygments, biber, Portuguese language support, linting tools, etc.).

## Build and Compilation

### Generating PDFs

**Method 1: Auto-save (Quick Iterations)**
- PDFs are automatically generated on file save (Ctrl+S) to the `./build/` directory
- Output directory: `./build/` (contains both PDFs and auxiliary files)
- First-time preview: Initial PDF preview takes 20-30 seconds to load, subsequent previews are instant
- Auxiliary files: Cleaned automatically after build

**Method 2: Makefile (Advanced Features)**
```bash
make build        # Build thesis (default)
make preview      # Continuous watch mode (auto-rebuild on changes)
make print        # Generate print-optimized PDF with color simplification
make ebook        # Generate e-book optimized PDF
make lint         # Lint LaTeX files for common errors
make clean        # Clean auxiliary files
make cleanall     # Clean everything including PDFs
```

**Main Documents to Compile:**
- `matter.tex` - Complete thesis document (includes cover.tex)
- `cover.tex` - Cover pages only (compiled separately by Makefile)

### Compiler Selection

**Default Configuration**: The template uses `pdflatex` with `--shell-escape` flag (required for minted package)

To use a different TeX program (e.g., LuaLaTeX, XeLaTeX), add this magic comment at the top of your main .tex file:

```tex
%!TEX program = lualatex
```

Supported programs: `pdflatex`, `lualatex`, `xelatex`, etc.

**Note**: `--shell-escape` is automatically enabled for all compilation methods to support the minted package for syntax-highlighted code listings.

### Viewing Compilation Logs

- **VS Code Output panel**: Terminal > Output > "LaTeX Compiler"
- **LaTeX Workshop sidebar**: Shows error logs and compilation status
- **Troubleshooting**: If PDF preview fails, reload the browser (Ctrl+R)

## Project Architecture

### Key Configuration Files

**Environment Configuration:**
- **`.devcontainer/devcontainer.json`**: Primary configuration for the dev container, extensions, LaTeX Workshop settings, and Grammarly integration
- **`.vscode/settings.json`**: Mirrors LaTeX Workshop settings from devcontainer (for local development compatibility)
- **`Makefile`**: Build automation with advanced features (print/ebook optimization, linting, continuous preview)
- **`requirements.txt`**: Python dependencies (pygments, proselint)

**Thesis Template Files:**
- **`matter.tex`**: Main thesis document (compile this)
- **`cover.tex`**: Thesis cover pages
- **`glossary.tex`**: Acronyms and glossary definitions
- **`custom-theme.tex`**: Optional custom chapter/section styling (currently not loaded)
- **`uaThesisTemplate.sty`**: UA-specific style package with cover generation, department colors, and formatting

**Content Organization:**
- **`chapters/`**: Thesis chapters and appendices
- **`bib/`**: Bibliography files (references.bib, rfc.bib, 3gpp.bib)
- **`figs/`**: Figures and images (includes required UA logos)
- **`build/`**: Compilation output directory (PDFs and auxiliary files)
- **`scripts/`**: Utility scripts (simplify-colors.sh for print optimization)

### LaTeX Workshop Configuration

The project uses [LaTeX Workshop](https://github.com/James-Yu/LaTeX-Workshop) extension with custom configuration:

- **Auto-build**: Disabled by default (`latex-workshop.latex.autoBuild.run: "never"`) - use Ctrl+S to compile
- **Auto-clean**: Runs on build completion (`latex-workshop.latex.autoClean.run: "onBuilt"`)
- **PDF viewer**: Opens in VS Code tab (`latex-workshop.view.pdf.viewer: "tab"`)
- **Dark mode**: PDF viewer uses dark mode by default (configurable via `latex-workshop.view.pdf.color.dark.*` settings)
- **Output directory**: `./build/` for all PDFs and auxiliary files
- **Compilation flags**: `-output-directory=build` and `-shell-escape` (required for minted)
- **Bibliography backend**: biber (configured in recipes)

**Available Compilation Recipes:**
1. `latexmk (UA thesis)` - Uses latexmk with shell-escape (recommended)
2. `pdflatex ➞ biber ➞ pdflatex × 2` - Manual recipe for bibliography compilation

### Extensions Architecture

The environment includes several integrated extensions (configured in `.devcontainer/devcontainer.json`):

1. **James-Yu.latex-workshop**: Core LaTeX editing and compilation
2. **GitHub.copilot**: AI-powered code completion for LaTeX commands and content
3. **ms-vsliveshare.vsliveshare**: Real-time collaboration support
4. **znck.grammarly**: Grammar/spelling checking for .tex files (alternative: valentjn.vscode-ltex for LanguageTool)

To disable an extension, comment it out in `.devcontainer/devcontainer.json` extensions array.

## Grammarly vs LanguageTool

- **Grammarly** (enabled by default): Checks only `.tex` files, excludes `.md` files
- **LanguageTool** (disabled by default): Open-source alternative supporting BibTeX, ConTeXt, LaTeX, Markdown, Org, reStructuredText, R Sweave, and XHTML

To switch from Grammarly to LanguageTool:
1. Uncomment `"valentjn.vscode-ltex"` in `.devcontainer/devcontainer.json`
2. Comment out `"znck.grammarly"` in the same file

## Output Directory Configuration

**Current Setup**: PDFs are generated in `./build/` directory

To change the output directory, update both locations:

1. `.devcontainer/devcontainer.json`:
   - `"latex-workshop.latex.outDir": "./YourDirectoryName"`
   - `"latex-workshop.latex.magic.args": ["-output-directory=YourDirectoryName", "-shell-escape", ...]`
   - Update tool args in `latex-workshop.latex.tools` (latexmk `-auxdir` and `-outdir` flags)

2. `.vscode/settings.json`: Same properties as above

3. `Makefile`: Update `OUTDIR` variable if using Makefile build system

## Important Notes

- **Do not delete** `.devcontainer/devcontainer.json` - it's essential for the environment
- **Remote user**: Must remain as `root` (do not change `"remoteUser"` property)
- **First startup**: Initial environment setup takes approximately 2 minutes
- **Git integration**: Full git functionality is available (unlike Overleaf's limited git support)
- **Format on save**: Enabled by default (`editor.formatOnSave: true`)

## Additional Features

- **Intellisense**: Citations and references auto-completion
- **Snippets**: LaTeX command shortcuts (see LaTeX Workshop wiki)
- **Code folding**: Supported for sections and environments
- **SyncTeX**: Forward/inverse search between source and PDF enabled
- **Linting**: LaTeX linting via lacheck, chktex, and proselint (run `make lint`)

## UA Thesis Template Specifics

### Document Class and Style

**Base Class**: `memoir` (11pt, a4paper, oneside, onecolumn)

**Custom Style Package**: `uaThesisTemplate.sty` provides:
- University of Aveiro branding and formatting
- Automatic cover page generation via `\MakeCover` command
- Department-specific color schemes (7 schools, 16+ departments supported)
- Jury member formatting
- Abstract pages (Portuguese and English)
- Grant acknowledgment support
- AI tool acknowledgment support
- MAP doctoral program support (multi-university)

### Department Options

Configure your department in `matter.tex` preamble. Supported departments:
- **Engineering**: deti, dao, dbio, dcspt, deca, degeit, de, demac, decivil, dem
- **Sciences**: dfis, dmat, dq, dbio
- **Humanities**: dlc
- **Other**: dcm, dgeo

**School Area Colors** (alternative to department-specific):
- arts, sciences, education, economy, engineering, humanities, health

### Key LaTeX Packages Used

**Code Listings:**
- `minted` - Syntax highlighting (requires pygments Python package)
- Configure with: `\begin{minted}{language}...` or `\inputminted{language}{file}`

**Bibliography:**
- `biblatex` with biber backend
- Style: IEEE
- Bibliography files: `bib/references.bib`, `bib/rfc.bib`, `bib/3gpp.bib`
- Usage: `\cite{key}`, `\parencite{key}`, `\textcite{key}`

**Language Support:**
- `babel` with Portuguese (default) and English
- Switch language: `\selectlanguage{english}` or `\selectlanguage{portuguese}`

**Mathematics & Science:**
- `amsmath`, `amssymb` - Math environments and symbols
- `siunitx` - SI units with weight detection

**Acronyms:**
- `acronym` package (printonlyused mode)
- Define in `glossary.tex`, use with `\ac{acronym}`, `\acp{plural}`

### Thesis Configuration in matter.tex

Key configuration variables (lines 1-24 in matter.tex):

```latex
\def\mtitle{Your Thesis Title}
\def\msubtitle{Subtitle if any}
\def\mauthorfirst{First Name}
\def\mauthorsecond{Last Name}
\def\mdegree{Master/Doctor}
\def\msupervisors{Supervisor Name\\Prof. Title, University}
\def\mdate{\monthyeardate\today}
\def\mlocal{Universidade de Aveiro}
\def\mdocument{thesis} % or dissertation, proposal
```

**Cover Page Generation:**
- `\MakeCover` command automatically generates cover pages
- Included via pdfpages in matter.tex
- Separate compilation: `make build` compiles both cover.tex and matter.tex

### Overleaf Compatibility

To use on Overleaf:
1. Set `\def\useoverleaf{1}` in matter.tex (line 25)
2. Add `fc-portuges.def` file to project
3. Note: Some features unavailable (pdfcomment, shell-escape features)

**Recommendation**: Use GitHub Codespaces instead for full feature support

### Print Optimization

The template includes scripts for print cost reduction:

```bash
make print  # Generate print-optimized PDF with Ghostscript compression
```

The `scripts/simplify-colors.sh` script converts grayscale pages to true gray colorspace, significantly reducing color printing costs.

**Print Output Files:**
- `build/thesis-print.pdf` - Compressed version
- `build/thesis-print-final.pdf` - Color-optimized version

### Linting Your Thesis

```bash
make lint              # Lint all LaTeX files
make lint texfile=chapter1.tex  # Lint specific file
```

**Linting Tools Used:**
- `lacheck` - LaTeX syntax checker
- `chktex` - LaTeX semantic checker
- `proselint` - Prose style linter
- `pandoc` - Document converter validation

### Common Workflows

**Starting a New Chapter:**
1. Create `chapters/chapterN.tex`
2. Add `\include{chapters/chapterN}` to matter.tex
3. Write content, save (Ctrl+S) to auto-compile

**Adding Bibliography Entries:**
1. Add entries to `bib/references.bib`
2. Cite in text: `\cite{key}`
3. Biber automatically processes on compilation

**Adding Figures:**
1. Place images in `figs/` directory
2. Use: `\includegraphics[options]{figs/filename}`
3. Supported formats: PDF, PNG, JPG

**Using Code Listings with Minted:**
```latex
\begin{minted}{python}
def hello():
    print("Hello, World!")
\end{minted}
```

Supported languages: python, java, c, cpp, javascript, latex, bash, and 200+ more
