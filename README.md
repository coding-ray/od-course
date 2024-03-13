# Lecture Materials of the Optimum Design Course

The lecture materials of the course [Optimum Design](https://class-qry.acad.ncku.edu.tw/crm/course_map/course.php?dept=NE&cono=RB51801&lang=en) ([最佳化設計](https://class-qry.acad.ncku.edu.tw/crm/course_map/course.php?dept=NE&cono=RB51801))\* in the graduate school of the [PEHL (體健所)](https://pehl.ncku.edu.tw/)\*\* in the [NCKU](https://www.ncku.edu.tw/) ([國立成功大學](https://www.ncku.edu.tw/?Lang=zh-tw))\*\*\*, Tainan, Taiwan.

\* Optimum Design: Theories and Applications to Sports Industry and Engineering (最佳化設計：理論與運動產業及工程之應用)

\*\* Institute of Physical Education, Health &Leisure Studies (體育健康與休閒研究所)

\*\*\* National Cheng Kung University (國立成功大學)

## Getting Handouts

If you just need the handouts, please check the [latest release](https://github.com/coding-ray/od-course/releases/latest).

## Getting Started to Edit and Compile Handouts

### Install Docker

1. If you want to set up a working and fast LaTeX environment, you may want to skip this section. Otherwise, for building the handouts once or to isolate LaTeX environments, follow the instructions here.

1. Install Docker Engine by following the [official instructions](https://docs.docker.com/engine/install/).

1. Skip the next section.

### Install Dependencies Locally

1.  If you've set up Docker, you could skip this sections, for the Docker image [rays2/gt-handout-env](https://hub.docker.com/r/rays2/gt-handout-env) handles all the LaTeX-related dependencies.

1.  Install a TeX distribution which provides the [pdfTeX](https://tug.org/applications/pdftex/) engine.

    > [!TIP]
    > You could install either [TeX Live](https://www.tug.org/texlive/) or [MikTeX](https://miktex.org/download).
    >
    > Some Linux distributions also provide TeX Live packages from the default package manager (like `apt install texlive` or `pacman -S texlive-bin`).

1.  Install the following packages with your TeX distribution.

    <!--
    When building a Docker image as the environment, the script accesses this package list, so make sure this list covers all required packages to build handouts in a Docker container.

    Also, make sure the div tag is at three lines before the single-line package list.
    -->

    <div id="package-list"></div>

    ```
    mathabx babel tools datetime2 geometry mathtools pgfplots subfiles xcolor multirow caption cleveref ragged2e preprint
    ```

    > [!TIP]
    > With TeX Live, you could use `tlmgr install <packages>`, where `<packages>` is the package list above.
    >
    > Replace the package `tools` with `latex-tools` in MikTeX.

1.  (Optional) Install an editor you prefer.
    <details>
    <summary>Some editors with LaTeX syntax highlighting (click to expand/hide):</summary>

    Terminal:

    1. [Emacs with AUCTeX](https://tex.stackexchange.com/a/356)
    1. [Vim/gVim](https://www.vim.org/), [Neovim](https://neovim.io/), [MacVim](https://macvim.org/) (macOS) with [vim-latex](https://vim-latex.sourceforge.net/)
    1. [Nano](https://www.nano-editor.org/)
    1. [Sublime Text](https://www.sublimetext.com/)

    Simple GUI:

    1. [Notepadqq](https://notepadqq.com/s/)
    1. [Notepad++](https://notepad-plus-plus.org/)

    Comprehensive GUI, IDE:

    1. [Visual Studio Code](https://code.visualstudio.com/) (VS Code), [VSCodium](https://vscodium.com/)
    1. [TexMaker](https://www.xm1math.net/texmaker/)
    1. [TeXstudio](https://www.texstudio.org/)
    1. [TeXworks](https://tug.org/texworks/)
    </details>

### Compilation of TeX Files

<div id="docker-handout"></div>

1.  With Docker, you could compile the main handout `src/handouts/main.tex` in a Docker container.

    ```bash
    # Linux
    cd src/build-handouts
    ./build-handouts.sh
    ```

    ```bat
    rem Windows, in Command Prompt (CMD)
    cd src\build-handouts
    .\build-handouts-windows.bat
    ```

1.  Without using Docker, you can also compile the main handout in `src/handouts`. Note that you may need to run `pdflatex` command three or more times to have correct referencing.

    ```bash
    # with files clustering in the working directory
    pdflatex main.tex

    # put all compiled files in build/
    # ..\..\build in Windows
    mkdir ../../build
    pdflatex -output-directory="../../build" -file-line-error main.tex

    # see only error messages in Linux
    # exit code 1 means no error
    pdflatex -output-directory="../../build" \
        -file-line-error \
        main.tex 2>&1 | \
        grep '^!.*' -A200 --color=always
    ```
