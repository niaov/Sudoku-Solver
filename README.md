# Sudoku Solver in C++

## 项目描述

这个项目是一个用 C++ 实现的数独求解器，用于中山大学24/9/30面向对象课程作业，包含以下功能：

- 字符串输入解析
- 数独棋盘推理
- 为每个单元格生成候选值
- 对象创建、初始化、克隆和序列化
- 比较和位集合管理（行、列和子网格）
- 深度优先搜索多组解

## 类定义

### 类 Grid

- **描述**: 表示数独棋盘的基本网格，支持序列化、反序列化、获取和设置单元格值、以及对棋盘行列值进行操作。

- **主要方法**:
  - `oserialize()`: 将数独网格序列化为字符串。
  - `odeserialize(const string& data)`: 从字符串反序列化为数独网格。
  - `ogetRowValues(int rowId)`: 获取某行的所有数值。
  - `ogetColValues(int colId)`: 获取某列的所有数值。
  - `ogetBlockValue(int rowId, int colId)`: 获取某个单元格的数值。
  - `osetBlockValue(int rowId, int colId, int val)`: 设置某个单元格的数值。
  - `ooperator==`: 比较两个数独棋盘是否相等。

### 类 Sudoku

- **描述**: 表示一个数独问题，继承自 Grid，支持数独求解、序列化和反序列化等功能。

- **主要方法**:
  - `osolve(bool ifOutputAns = true, int rowId = 0, int colId = 0)`: 使用深度优先搜索算法求解数独，其中 `ifOutputAns` 代表是否打印每个解。最多搜索 101 个解。
  - `oprintBoard()`: 打印当前数独棋盘。
  - `ooperator==`: 比较两个数独对象是否相等。
  - `ogetSolution_count`: 计算有多少数独解的数量（不打印每一个解）。
  - Sudoku 的序列化依赖于 Grid 的序列化。
  - Sudoku 的反序列化需要先判断是否为 81 位的字符串再调用 Grid 的反序列化函数。
  - Sudoku 的类构造函数方案为对给定字符串反序列化，若给出的字符串长度超过 81，则截断多余部分；若不足 81，则缺失部分补 0。

## 测试代码  test.cpp

### 描述

测试代码用于测试数独的求解功能是否正确，以及测试序列化、反序列化、深拷贝功能。

### 测试用例

1. **唯一解示例**: `017903600000080000900000507072010430000402070064370250701000065000030000005601720`
2. **多解示例**: `006000200100700090000006075008002030020000060070400500640300000090004001002000400` （8 个解）
3. **无解示例**: `530071000600050000098000060800600003400803001700020006000000080060000195000281000`
4. **非法示例**: `ABCDE0179036000000900000507072010430000402070064370250701000065000030000005601720` （含字母）
5. **全 0 示例**: `000000000000000000000000000000000000000000000000000000000000000000000000000000000`
6. **长度不足示例**: `123456789`
7. **长度过大示例**: `0000000000000000000000000000000000000000000000000000000000000000000000000000000000000`
8. **用户自定义输入**: 对其进行序列化、反序列化、深拷贝等操作，验证最后得到的新对象与原先一致，并给出所有可能的答案（不超过 101）。

