---
title: 未在本地计算机上注册Microsoft.Jet.OLEDB.4.0如何解决
categories:
  - 笔记
  - windows
tags:
  - 笔记
comments: true
toc: true
donate: true
share: true
date: 2024-10-08 10:49:08
source: https://learn.microsoft.com/en-us/answers/questions/1658052/download-link-for-microsoft-ace-oledb-12-0
---



# Microsoft.ACE.OLEDB.12.0 的下载链接 - Microsoft Q&A

> ## Excerpt
> We need the Microsoft.ACE.OLEDB.12.0 32 bit install, can someone please provide a link. We need the functionality to import excel files in via SSMS so the 32 bit driver is required

---
![](data:image/svg+xml, %3Csvg xmlns='http://www.w3.org/2000/svg' height='64' class='font-weight-bold' style='font: 600 30.11764705882353px "SegoeUI", Arial' width='64'%3E%3Ccircle fill='hsl(128, 68%, 22%)' cx='32' cy='32' r='32' /%3E%3Ctext x='50%25' y='55%25' dominant-baseline='middle' text-anchor='middle' fill='%23FFF' %3ETD%3C/text%3E%3C/svg%3E)

4月 19， 2024， 10：09 下午

我们需要 Microsoft.ACE.OLEDB.12.0 32 位安装，有人可以提供一个链接吗。我们需要通过 SSMS 导入 excel 文件的功能，因此需要 32 位驱动程序

1.  ![](https://techprofile.blob.core.windows.net/images/J-cKqdzNMkWeJv8idBgCcQ.png?8DC812)
    
    4月 22， 2024， 9：51 上午
    

## 3 个补充答案

1.  ![](data:image/svg+xml, %3Csvg xmlns='http://www.w3.org/2000/svg' height='64' class='font-weight-bold' style='font: 600 30.11764705882353px "SegoeUI", Arial' width='64'%3E%3Ccircle fill='hsl(96, 26%, 19%)' cx='32' cy='32' r='32' /%3E%3Ctext x='50%25' y='55%25' dominant-baseline='middle' text-anchor='middle' fill='%23FFF' %3EYK%3C/text%3E%3C/svg%3E)
    
    4月 20， 2024， 12：05 上午
    
2.  ![](data:image/svg+xml, %3Csvg xmlns='http://www.w3.org/2000/svg' height='64' class='font-weight-bold' style='font: 600 30.11764705882353px "SegoeUI", Arial' width='64'%3E%3Ccircle fill='hsl(198.4, 28.000000000000004%, 29%)' cx='32' cy='32' r='32' /%3E%3Ctext x='50%25' y='55%25' dominant-baseline='middle' text-anchor='middle' fill='%23FFF' %3EJL%3C/text%3E%3C/svg%3E)
    
    5月 20， 2024， 3：14 上午
    
    这个答案听起来可能有点扭曲。ACE OLE DB 12 仍可与 SSIS 2019 配合使用。使用 ACE OLE DB 12 或更早版本通过 Visual Studio 2019 构建的包不再受支持，并且还进行了重大更改 （ACE OLE DB 16），不再可用（或受支持）。这里暗示的是，构建对应于 MS Access，它现在位于支持 Office 365 的新版本下。发生这种情况后，我的 ACE OLE DB 16 更新开始在我的 SSIS 包上失败，我能够恢复到 ACE OLE DB 12 并保持它们运行。如果 Microsoft 允许我们下载较旧的副本，那就太好了，但它们似乎已被销毁。这可能是正确的，但对于我们这些生活在没有开放端口的 NAT 后面的人来说，系统仍然可以安全地在旧文件上运行。我的两分钱。
    

[登录以回答](https://learn.microsoft.com/en-us/answers/questions/1658052/download-link-for-microsoft-ace-oledb-12-0#)

### 问题活动

### Additional resources

___

文档

-   [适用于 Jet 和 ODBC 驱动程序的 OLE DB 提供程序仅为 32 位版本 - Microsoft 365 应用](https://learn.microsoft.com/en-us/office/troubleshoot/access/jet-odbc-driver-available-32-bit-version?source=recommendations)
    
    描述没有 64 位版本的 Microsoft OLE DB Provider for Jet 或 Jet ODBC 驱动程序。
    
-   [Access 使用的 SQL Server Native Client 驱动程序 - Microsoft 365 应用程序](https://learn.microsoft.com/en-us/office/troubleshoot/access/sql-server-native-client-drivers?source=recommendations)
    
    提供有关 Access 中某些功能使用的 SQL Server Native Client 驱动程序的下载信息。
    
-   [下载适用于 SQL Server 的 Microsoft OLE DB 驱动程序 - 适用于 SQL Server 的 OLE DB 驱动程序](https://learn.microsoft.com/en-us/sql/connect/oledb/download-oledb-driver-for-sql-server?source=recommendations)
    
    下载适用于 SQL Server 的 Microsoft OLE DB 驱动程序，以开发连接到 SQL Server 和 Azure SQL 数据库的本机 Windows 应用程序。
