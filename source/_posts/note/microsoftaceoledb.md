---
title: 未在本地计算机上注册Microsoft.Jet.OLEDB.4.0
categories:
  - 笔记
tags:
  - 系统
comments: true
toc: true
donate: true
share: true
date: 2024-10-10 13:32:08
source: https://learn.microsoft.com/en-us/answers/questions/1658052/download-link-for-microsoft-ace-oledb-12-0
---

未在本地计算机上注册Microsoft.Jet.OLEDB.4.0”这个错误通常出现在使用OLE DB连接到Access数据库或其他数据源时。这个问题的根源通常是因为你的系统上没有安装Microsoft Jet OLE DB Provider。以下是一些解决方法：

1. **使用Microsoft Access Database Engine**：
   - Microsoft Jet OLE DB Provider仅适用于32位系统，而在64位系统上则需要使用Microsoft Access Database Engine。
   - 你可以下载并安装Microsoft Access Database Engine Redistributable。确保选择与所用的应用程序位数相对应的版本（32位或64位）。

2. **修改应用程序的目标平台**：
   - 如果你在开发者环境中（例如 Visual Studio），可以尝试将目标平台更改为x86，以便你的应用程序使用32位的Jet OLE DB Provider。
   - 在解决方案资源管理器中，右键单击项目 -> 属性 -> 构建 -> 平台目标，选择x86。

3. **检查连接字符串**：
   - 确保你的连接字符串是正确的。如果你已经安装了Access Database Engine，可以使用ACE.OLEDB.12.0或ACE.OLEDB.16.0来替代Jet OLE DB，比如：
     ```
     Provider=Microsoft.ACE.OLEDB.12.0;Data Source=你的数据库路径;
     ```

4. **系统兼容性**：
   - Ensure that your application compatibility matches the 32-bit or 64-bit version of the OLE DB provider you are trying to use. If your application is 64-bit, you must ensure the provider is also 64-bit.

通过上述步骤，通常可以解决这个问题。如果问题仍然存在，请确保您已按照 Microsoft 的要求安装了所有必要的组件。

目前微软的[Microsoft Access Database Engine Redistributable](https://www.microsoft.com/en-us/download/details.aspx?id=13255)链接已失效,找了很多篇帖子和网站均没有提供可用的安装文件或是改x86,遇到没有源码的改不了x86的就尴尬了,以下是安装2010和2016下载安装文件,如果觉得对你有用,可以收藏一下
# 解决方案如下:
# 1. Chocolatey

此内容来自 Chocolatey，但可从以下链接直接下载：

- [32 位](https://web.archive.org/web/20240214170634if_/https://download.microsoft.com/download/2/4/3/24375141-E08D-4803-AB0E-10F2E3A07AAA/AccessDatabaseEngine.exe)
- [64 位](https://web.archive.org/web/20240214170634if_/https://download.microsoft.com/download/2/4/3/24375141-E08D-4803-AB0E-10F2E3A07AAA/AccessDatabaseEngine_X64.exe)

巧克力包装供参考：[Chocolatey Package](https://community.chocolatey.org/packages/made2010#files)

# 2. Microsoft.ACE.OLEDB.16.0

这是 [Microsoft.ACE.OLEDB.16.0 的下载链接](https://www.microsoft.com/en-us/download/details.aspx?id=54920)。

可以按照本文中的步骤在 SSMS 中导入 Excel 文件：[导入 Excel 数据到 SQL](https://learn.microsoft.com/en-us/sql/relational-databases/import-export/import-data-from-excel-to-sql?view=sql-server-ver16#wiz)。


