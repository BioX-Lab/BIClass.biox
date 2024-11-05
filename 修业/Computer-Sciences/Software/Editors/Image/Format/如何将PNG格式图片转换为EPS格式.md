# 如何将PNG格式图片转换为EPS格式

## 使用在线转换工具

有许多在线图像转换工具可供选择，例如：
- [CloudConvert](https://cloudconvert.com/png-to-eps)：上传你的 PNG 图片，选择输出格式为 EPS，然后进行转换。操作简单方便，但要注意上传的图片可能存在隐私风险。

## 使用图形编辑软件

### GIMP
   - 打开 GIMP。
   - 选择“文件”>“打开”，选择你的 PNG 图片。
   - 选择“文件”>“导出 As”。
   - 在“选择文件类型（按扩展名）”下拉菜单中，选择“Encapsulated PostScript (.eps)”。
   - 点击“导出”并根据需要调整设置，然后再次点击“导出”以创建 EPS 文件。

### Adobe Illustrator
   - 打开 Adobe Illustrator。
   - 选择“文件”>“打开”，找到你的 PNG 图片并打开它。
   - 一旦图片打开，选择“文件”>“存储为”。
   - 在“存储为”对话框中，选择“EPS”作为文件格式，并根据需要调整其他设置。
   - 点击“保存”以创建 EPS 文件。

## 使用命令行工具

### ImageMagick
   - 确保你已经安装了 ImageMagick。
   - 打开命令提示符或终端窗口。
   - 运行以下命令：`convert input.png output.eps`，其中“input.png”是你的 PNG 文件名，“output.eps”是你想要的 EPS 文件名。

#Image #PNG #EPS 