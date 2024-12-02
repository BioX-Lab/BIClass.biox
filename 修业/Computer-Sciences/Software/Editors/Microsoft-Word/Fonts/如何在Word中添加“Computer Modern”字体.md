# 如何在Word中添加“Computer Modern”字体

[QLNU/SJ/20241201]

`Computer Modern`是LaTeX排版系统中的默认字体，而非Word的默认字体，Word中一般没有直接提供Computer Modern字体的安装包，可以通过以下几种方法来获取并在Word中使用该字体。

## 寻找第三方字体库
- **搜索可靠的字体资源网站**：一些知名的字体资源网站，如DaFont (https://www.dafont.com/)等，可能会有用户上传的Computer Modern字体的Word版本。
- **筛选并下载合适的字体文件**：在网站上搜索“Computer Modern”，从搜索结果中找到适合Word使用的字体文件格式，如.ttf等，然后下载到本地.
- **安装字体**：在Windows系统下，将找到的字体文件复制到“C:\Windows\Fonts”文件夹中；在Mac系统下，双击字体文件，然后点击“安装字体”按钮来安装。

## 从LaTeX发行版中提取字体文件并安装到系统
- **下载LaTeX发行版**：例如TeX Live或MiKTeX等，TeX Live可从其官网 [https://www.tug.org/texlive/](https://www.tug.org/texlive/) 下载，MiKTeX可从 [https://miktex.org/download](https://miktex.org/download) 下载。
- **找到字体文件**：在安装好的LaTeX发行版中找到Computer Modern字体文件，通常在类似于“texmf-dist/fonts/opentype/public/cm”或“texmf-dist/fonts/type1/public/cm”这样的路径下，字体文件格式一般为.otf或.pfb等。
- **安装字体到系统**：将下载的字体文件安装到系统中，具体方法如前文所述。

## 使用在线字体转换工具
- **选择可靠的在线转换工具**：如Font Squirrel (https://www.fontsquirrel.com/tools/webfont-generator)等在线字体转换网站。
- **上传Computer Modern字体文件**：如果已经有该字体文件，可直接上传到转换工具网站；如果没有则需先通过”从LaTeX发行版中提取字体文件并安装到系统“中的步骤找到字体文件再上传 。
- **进行转换并下载**：按照网站的提示进行操作，将Computer Modern字体转换为可在Word中使用的字体格式，如TrueType（.ttf）等，然后下载转换后的字体文件，并按照上述安装字体到系统的方法进行安装.

安装好字体后，打开Word文档，在字体选择下拉菜单中就可以找到并使用Computer Modern字体来编辑文档了 。