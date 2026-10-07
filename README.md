# LaTeX Résumé

Use `master/` as the source of truth for résumé content. The current LaTeX
build uses the repository-root `main.tex` and generates `main.pdf`.

## Folder and filename conventions

Follow these conventions for future résumé updates:

| Folder | Purpose | Filename rules |
| --- | --- | --- |
| `master/` | Always contains the newest complete version; this is the source of truth. | **Do not put dates in any filenames.** Keep stable names so the current master is easy to find. |
| `general/` | Holds the current general 1–2 page internship résumé. | Date exported versions using `YYYY-MM-DD` so each résumé sent out can be identified. |
| `applications/` | Contains one folder per actual position, such as `applications/<company>-<position>/`. | Keep the résumé tailored to that specific position in its own folder. |

Update the complete master first, then adapt the general résumé or the
version for an individual application. Keep dated general exports as records
of what was shared, for example `Hongrui_Zhang_Resume_2026-10-07.pdf`.

## Requirements

- A LaTeX distribution that provides `pdflatex`, such as BasicTeX (macOS),
  TeX Live, or MiKTeX (Windows).
- The packages used by `main.tex`: `geometry`, `graphicx`, `tabularx`, `url`,
  `enumitem`, `palatino`, `fontawesome`, `fontenc`, `inputenc`, `xcolor`,
  `hyperref`, and `fancyhdr`, including their required fonts.
- Optional: CMake 3.13 or newer for the CMake commands below.

`pdflatex` is supplied by a LaTeX distribution. The
[`pdflatex` package on PyPI](https://pypi.org/project/pdflatex/) is a Python
wrapper and does **not** install the compiler; Python and pip are not needed
to build this résumé.

### Install on macOS

For this résumé, use
[BasicTeX](https://formulae.brew.sh/cask/basictex), a small TeX distribution,
and add the required packages. If you have Homebrew:

```sh
brew install --cask basictex
```

After installation, open a new terminal. To use the compiler immediately in
your current Bash or Zsh session, add the TeX executable directory:

```sh
export PATH="/Library/TeX/texbin:$PATH"
```

Install the additional packages and fonts used by `main.tex` with TeX Live's
package manager (these commands may ask for your macOS administrator password):

```sh
sudo /Library/TeX/texbin/tlmgr update --self
sudo /Library/TeX/texbin/tlmgr install enumitem fontawesome psnfss palatino
```

`enumitem` controls the lists, `fontawesome` supplies the social icons, and
`psnfss` plus `palatino` provide the Palatino font support and font files.
The other required packages are included in BasicTeX's standard installation.

Make sure `pdflatex` is available in your terminal:

```sh
pdflatex --version
```

The larger alternative is
[MacTeX without GUI applications](https://formulae.brew.sh/cask/mactex-no-gui),
installed with `brew install --cask mactex-no-gui`. It includes the full TeX
Live distribution: thousands of packages, fonts, typesetting engines, and
documentation, which account for its several-gigabyte size. BasicTeX installs
a smaller subset and lets you add packages as needed. Choose one distribution;
Homebrew marks the BasicTeX and MacTeX casks as conflicting. If you already
have full MacTeX installed, you can use it and skip the BasicTeX setup.

## Compile directly

Run these commands from the repository root:

```sh
pdflatex -interaction=nonstopmode -halt-on-error -file-line-error main.tex
pdflatex -interaction=nonstopmode -halt-on-error -file-line-error main.tex
```

Run both passes so LaTeX can resolve references and PDF links. The output is
`main.pdf` in the repository root. Auxiliary files such as `main.aux`,
`main.log`, and `main.out` are created alongside it.

## Compile with CMake

From the repository root:

```sh
cmake -S . -B build
cmake --build build --target pdf
```

The `pdf` target runs `pdflatex` twice. With the current `CMakeLists.txt`, the
generated `main.pdf` and LaTeX auxiliary files are in the repository root,
while CMake's build files are in `build/`. After editing `main.tex`, rerun the
build command.

Neither method automatically updates the checked-in `Hongrui_Resume.pdf`.
To update that file, review `main.pdf`, then save a copy with that filename.

## Troubleshooting

- **Installed `pdflatex` with pip:** Remove the unnecessary Python wrapper
  with `python -m pip uninstall pdflatex` in the same Python environment.
  If pip also downgraded `attrs`, restore its previous version shown in the
  installation log, then run `python -m pip check` to check dependencies.
  Install the actual LaTeX compiler using the instructions above.
- **`pdflatex` is not found:** Install a LaTeX distribution and ensure its
  executable directory is on your `PATH`, then reopen your terminal. If using
  CMake, rerun the configure command afterward.
- **A `.sty` file or font is missing:** Install the corresponding package or
  font using your LaTeX distribution's package manager. For example,
  `fontawesome.sty` requires the `fontawesome` package.
- **Compilation fails:** Check the first error in the terminal output or
  `main.log`; `-file-line-error` includes the source location when available.
