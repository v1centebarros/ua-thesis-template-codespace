<div align="center">

# University of Aveiro Thesis Template + WebLaTeX

![WebLaTeX](https://user-images.githubusercontent.com/54777542/224550592-657a2f4e-bd46-4f11-85af-e9b299650434.jpg)

[![GitHub license](https://img.shields.io/github/license/sanjib-sen/WebLaTex?style=for-the-badge)](https://github.com/sanjib-sen/WebLaTex/blob/main/LICENSE)

> A complete University of Aveiro thesis template powered by WebLaTeX with VSCode + Web + Git Integration + GitHub Copilot + Grammarly + Live Collaboration Support

</div>

## Overview

This project combines the **University of Aveiro Thesis Template** with **WebLaTeX**, providing a professional LaTeX thesis environment that runs entirely in your browser via GitHub Codespaces. No local installation required!

**UA Thesis Template Features:**
- Complies with University of Aveiro's thesis guidelines
- Supports multiple departments and schools
- Professional cover page generation
- Portuguese and English language support
- Comprehensive bibliography management with biber
- Code syntax highlighting with minted

**WebLaTeX Environment Features:**
- Full VSCode editor in your browser
- Automatic PDF generation on save
- Git version control built-in
- GitHub Copilot AI assistance
- Grammarly/LanguageTool integration
- Real-time collaboration support
- Dark mode PDF viewer

This template was developed by professors and students. We will try to keep up to date with thesis requirements but some discrepancies may exist. Feel free to open issues and pull requests with new options, packages and fixes.

## Why Use This?

### Beyond Overleaf

Traditional LaTeX platforms like Overleaf have limitations:
- Limited Git integration (requires $40/month subscription)
- Restricted collaboration (only 1 collaborator on free plan)
- No VSCode extensions or customization
- No GitHub Copilot or advanced AI assistance
- Limited dark mode support

### With This Template You Get:

✅ **Full Git Integration** - Complete version control, branches, commits, and history
✅ **VSCode Power** - All your favorite extensions, themes, and keybindings
✅ **AI Assistance** - GitHub Copilot suggests LaTeX commands and content
✅ **Grammar Checking** - Built-in Grammarly or LanguageTool support
✅ **Real-time Collaboration** - Unlimited collaborators with Live Share
✅ **Mobile Access** - Edit your thesis from any device, including tablets
✅ **Automatic Builds** - PDF generated on every save (Ctrl+S)
✅ **No Installation** - Runs entirely in the browser

## Installation Instructions

<a href="https://github.com/v1centebarros/ua-thesis-template-codespace/generate" target="_blank"> ![get-started](https://user-images.githubusercontent.com/54777542/224549654-6f2dc0ad-54e0-4827-b316-ebe264dbf007.svg)</a>

1. **Login to GitHub** - [Sign up](https://github.com/signup) or [login](https://github.com/login)

2. **Create Your Repository**
   - **Use as Template (Recommended):** Click `Use this template` → `Create a new repository`
   - Or **Fork:** Fork this repository to your account

3. **Launch Codespace**
   - Click `<> Code` → `Codespaces` → `Create codespace on main`
   - **First launch takes ~2 minutes** to install dependencies
   - Subsequent launches take only 2-3 seconds

4. **Start Writing!**
   - Edit `matter.tex` or files in `chapters/`
   - Press `Ctrl+S` to save and auto-generate PDF
   - View PDF in the `build/` directory

![tutorial](https://user-images.githubusercontent.com/54777542/224550678-32a949ae-3a9b-4e8d-a0f1-ad30ec429908.gif)

## Quick Start

### Where is my PDF?

Generated PDFs are saved to the **`build/`** directory:
- `build/matter.pdf` - Your complete thesis
- `build/cover.pdf` - Just the cover pages

### Editor Instructions

1. **Save & Build** - Press `Ctrl+S` to save and automatically generate PDF
2. **View PDF** - Click the PDF file in `build/` folder
   - ⚠️ **First preview takes 20-30 seconds** - be patient!
   - After that, previews are instant
3. **Auto-save** - Your document auto-saves and rebuilds on changes
4. **View Logs** - Check `Terminal` → `Output` → `LaTeX Compiler` for errors
5. **Troubleshooting** - If PDF preview fails, reload browser (`Ctrl+R`)

### Basic Workflow

**Starting a new chapter:**
```bash
# 1. Create chapter file
chapters/chapter1.tex

# 2. Add to matter.tex
\include{chapters/chapter1}

# 3. Write content and save (Ctrl+S)
```

**Adding bibliography entries:**
```bash
# 1. Add entries to bib/references.bib
# 2. Cite in text: \cite{key}
# 3. Biber processes automatically on build
```

**Adding figures:**
```latex
% 1. Place image in figs/ directory
% 2. Include in document:
\includegraphics[width=0.8\textwidth]{figs/myimage.png}
```

## Building Your Thesis

### Method 1: Auto-Save (Recommended for Quick Iterations)

Press `Ctrl+S` to save your file, and PDF is automatically generated to `build/` directory.

### Method 2: Makefile (Advanced Features)

```bash
make build        # Build thesis (default)
make preview      # Continuous watch mode (auto-rebuild on changes)
make print        # Generate print-optimized PDF with color simplification
make ebook        # Generate e-book optimized PDF
make lint         # Lint LaTeX files for common errors
make clean        # Clean auxiliary files
make cleanall     # Clean everything including PDFs
```

**Main documents to compile:**
- `matter.tex` - Complete thesis document (includes cover)
- `cover.tex` - Cover pages only (compiled separately by Makefile)

### Choosing Your TeX Compiler

**Default:** The template uses `pdflatex` with `--shell-escape` (required for minted package)

To use a different compiler (e.g., LuaLaTeX, XeLaTeX), add this magic comment at the top of your .tex file:

```tex
%!TEX program = lualatex
```

Supported programs: `pdflatex`, `lualatex`, `xelatex`

## Advanced Features

### GitHub Copilot

![copilot](https://user-images.githubusercontent.com/54777542/224550711-9927d67f-e63e-445e-9ff0-db7674d7acef.gif)

[GitHub Copilot](https://github.com/features/copilot) suggests LaTeX commands, completes sentences, and even writes paragraphs based on your context!

**To disable:** Remove/comment `"GitHub.copilot"` from `.devcontainer/devcontainer.json`:
```json
"extensions": [
  // "GitHub.copilot",
]
```

### Grammarly Integration

Built-in [Grammarly](https://www.grammarly.com/) support checks grammar and spelling in `.tex` files automatically.

**Use Premium Account:** Press `Ctrl+Shift+P` → `Grammarly: Login / Connect your account`

**Check Other Files:** Press `Ctrl+Shift+P` → `Grammarly: Check text`

**Configure File Types:** Edit `.devcontainer/devcontainer.json`:
```json
"grammarly.files.include": ["*.md", "*.tex"],
"grammarly.files.exclude": ["*.bib"]
```

**To disable:** Remove/comment `"znck.grammarly"` from extensions list

### LanguageTool (Open-Source Alternative)

[LanguageTool](https://languagetool.org) supports LaTeX, BibTeX, Markdown, and more - **disabled by default**.

**To enable:** Uncomment in `.devcontainer/devcontainer.json`:
```json
"extensions": [
  "valentjn.vscode-ltex",  // Uncomment this
  // "znck.grammarly",     // Comment this out
]
```

### Live Collaboration

Real-time collaborative editing powered by [Visual Studio Live Share](https://visualstudio.microsoft.com/services/live-share/).

1. Click **Live Share** in the sidebar
2. Share the link with collaborators
3. Edit together in real-time!

![collaborate](https://user-images.githubusercontent.com/54777542/224550768-48997ac9-8747-425b-b7b4-05473f3ba944.png)

**To disable:** Remove/comment `"ms-vsliveshare.vsliveshare"` from extensions

### PDF Viewer Dark Mode

PDF viewer uses dark mode automatically when your OS is in dark mode.

**To disable dark mode:** Remove these lines from `.devcontainer/devcontainer.json`:
```json
"latex-workshop.view.pdf.color.dark.pageColorsBackground":"#171717",
"latex-workshop.view.pdf.color.dark.pageColorsForeground":"#FFFFFF",
"latex-workshop.view.pdf.color.dark.backgroundColor":"#171717",
```

## UA Thesis Template Specifics

### Document Structure

**Key Files:**
- `matter.tex` - Main thesis document (compile this)
- `cover.tex` - Thesis cover pages
- `glossary.tex` - Acronyms and glossary definitions
- `uaThesisTemplate.sty` - UA-specific style package
- `chapters/` - Your thesis chapters and appendices
- `bib/` - Bibliography files
- `figs/` - Figures and images (includes UA logos)

### Configuring Your Thesis

Edit the configuration variables in `matter.tex` (lines 1-24):

```latex
\def\mtitle{Your Thesis Title}
\def\msubtitle{Subtitle if any}
\def\mauthorfirst{First Name}
\def\mauthorsecond{Last Name}
\def\mdegree{Master/Doctor}
\def\msupervisors{Supervisor Name\\Prof. Title, University}
\def\mdate{\monthyeardate\today}
\def\mdocument{thesis} % or dissertation, proposal
```

### Department Selection

Configure your department/school in `matter.tex` preamble. Supported departments:

**Engineering:** deti, dao, dbio, dcspt, deca, degeit, de, demac, decivil, dem
**Sciences:** dfis, dmat, dq, dbio
**Humanities:** dlc
**Other:** dcm, dgeo

**Or use school-wide colors:** arts, sciences, education, economy, engineering, humanities, health

### Code Listings with Minted

Syntax-highlighted code blocks using the `minted` package:

```latex
\begin{minted}{python}
def hello_world():
    print("Hello, World!")
\end{minted}
```

Supported languages: python, java, c, cpp, javascript, latex, bash, and 200+ more

### Bibliography Management

Uses `biblatex` with biber backend (IEEE style):

```latex
\cite{key}           % [1]
\parencite{key}      % (Author, Year)
\textcite{key}       % Author (Year)
```

Add entries to `bib/references.bib`, `bib/rfc.bib`, or `bib/3gpp.bib`

### Acronyms

Define acronyms in `glossary.tex`:

```latex
\acro{API}{Application Programming Interface}
```

Use in text:
```latex
\ac{API}   % First use: Application Programming Interface (API)
\ac{API}   % Subsequent: API
\acp{API}  % Plural: APIs
```

### Print Optimization

Generate print-friendly PDFs with reduced color pages:

```bash
make print  # Creates build/matter-print.pdf and matter-print-final.pdf
```

The `scripts/simplify-colors.sh` script converts grayscale pages to true gray colorspace, significantly reducing printing costs.

### Linting Your Thesis

Check for errors and style issues:

```bash
make lint                       # Lint all LaTeX files
make lint texfile=chapter1.tex  # Lint specific file
```

**Linting tools:** lacheck, chktex, proselint, pandoc

## Using the Template (Traditional Setup)

For local/traditional usage without WebLaTeX:

### Option 1: Use as GitHub Template
[Click here](https://github.com/detiuaveiro/ua-thesis-template/generate) to create a repository from this template

### Option 2: Fork
Fork this repository to your account

### Option 3: Git Subtree (Most Flexible)
```bash
mkdir mythesis
cd mythesis
git init
git commit --allow-empty -m "Initial commit"
git subtree add --prefix document https://github.com/detiuaveiro/ua-thesis-template.git master --squash
# Later, to pull updates:
git subtree pull --prefix document https://github.com/detiuaveiro/ua-thesis-template.git master --squash
```

### Local Dependencies

**Required:**
- TeX Live or MacTeX (full installation recommended)
- pygments (for minted): `pip install -r requirements.txt`
- biber

**Optional (for advanced features):**
- ghostscript (for `make print`, `make ebook`)
- pandoc (for `make lint`)
- imagemagick and poppler (for color simplification)

**Ubuntu/Debian packages:**
```bash
sudo apt install texlive-full biber texlive-bibtex-extra texlive-latex-extra texlive-science
```

**Auto-setup on Debian/Ubuntu:**
```bash
make setup
```

## Configuration

### Change Output Directory

Edit both `.devcontainer/devcontainer.json` and `.vscode/settings.json`:

```json
"latex-workshop.latex.outDir": "./YourDirectoryName",
"latex-workshop.latex.magic.args": [
  "-output-directory=YourDirectoryName",
  "-shell-escape"
]
```

Also update `OUTDIR` in `Makefile` if using make commands.

### LaTeX Workshop Settings

The project uses [LaTeX Workshop](https://github.com/James-Yu/LaTeX-Workshop) with:
- Auto-build: Disabled (use Ctrl+S to compile)
- Auto-clean: Runs after build
- PDF viewer: Opens in VS Code tab
- Dark mode: Enabled by default
- Output directory: `./build/`
- Shell escape: Enabled (required for minted)

## Additional Features

- **Intellisense:** Auto-completion for citations and references
- **Snippets:** LaTeX command shortcuts
- **Code Folding:** Supported for sections and environments
- **SyncTeX:** Forward/inverse search between source and PDF
- **Format on Save:** Automatically format LaTeX code

For more features, see the [LaTeX Workshop Wiki](https://github.com/James-Yu/LaTeX-Workshop/wiki)

## Important Notes

- **Do not delete** `.devcontainer/devcontainer.json` - essential for environment
- **Remote user:** Must remain `root` (do not change)
- **First startup:** Takes ~2 minutes to install dependencies
- **PDF Preview:** First preview takes 20-30 seconds, then instant
- **Git integration:** Full git functionality (unlike Overleaf)

## Credits & Authors

**UA Thesis Template:**
- Tomás Oliveira e Silva - [Original template](http://sweet.ua.pt/tos/TeX/ua_thesis.tgz)
- João Paulo Barraca - [Improved and maintained](http://code.ua.pt//projects/latex-ua/repository)
- Fábio Maia and Ricardo Jesus - Further improvements and workflow

**WebLaTeX Environment:**
- [@James-Yu](https://github.com/James-Yu) - [LaTeX Workshop](https://github.com/James-Yu/LaTeX-Workshop)
- [@sanjib-sen](https://github.com/sanjib-sen) - [WebLaTeX](https://github.com/sanjib-sen/WebLaTex)
- [dante-ev](https://github.com/dante-ev/docker-texlive) - TeXLive Docker image
- [@znck](https://github.com/znck) - Grammarly extension
- [@thodson-hugs](https://github.com/thodson-hugs) - GitHub Copilot integration

## Contributing

Contributions are welcome! Please:
- Open an issue for feature requests or bug reports
- Submit pull requests with improvements
- Help keep the template up-to-date with UA requirements
