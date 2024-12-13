# 使用openpyxl库生成包含多个sheet的Excel文件

当前开发环境中（如`BIClass_py310`），如果没有安装`openpyxl`库，可以使用`pip`安装。
``` bash
#安装默认版本openpyxl即可
pip install openpyxl
```
如果使用Jupyter进行开发可以在代码块中添加`!pip install openpyxl`。
## 示例程序
``` python
# 导入openpyxl
from openpyxl import Workbook

# 创建一个新的工作簿
wb = Workbook()

# 删除默认的 "Sheet" 工作表
wb.remove(wb.active)

# 定义要写入的数据（根据个人情况调整）
data_sheets = {
    "Sheet1": [
        ["Name", "Age", "City"],
        ["Alice", 30, "New York"],
        ["Bob", 25, "Los Angeles"]
    ],
    "Sheet2": [
        ["Product", "Price", "Quantity"],
        ["Apple", 1.2, 10],
        ["Banana", 0.8, 20]
    ],
    "Sheet3": [
        ["Employee", "Department", "Salary"],
        ["Charlie", "HR", 50000],
        ["David", "Engineering", 60000]
    ]
}

# 依次写入不同的 sheet
for sheet_name, data in data_sheets.items():
    ws = wb.create_sheet(title=sheet_name)
    for row in data:
        ws.append(row)

# 保存工作簿到文件
output_filename = "output.xlsx"
wb.save(output_filename)

print(f"Excel file '{output_filename}' created successfully with multiple sheets.")
```

#Python #Excel #openpyxl