---
title: Windows Portable 提权
weight: 49
---

在Windows下，Portable程序没有管理员权限，这会导致以下问题：

* 当UAC（用户账户控制）窗口弹出时，画面无法传输。
* 当弹出被提权的窗口（如任务管理器）时，鼠标操作不响应。

通过提权, RustDesk在启动时或会话过程中可以创建一个具有管理员权限的进程，用于截屏和鼠标操作，从而避免了上述问题。

## 启动时提权

这种方式，连接时不需要再请求提升。有两种方法：

* 方法一：更改portable程序的名称，名称中需包含`-qs-`（1.2.0，1.2.1，1.2.2版本以`qs.exe`结尾）。鼠标左键点击运行，并在UAC窗口点击允许。

* 方法二: 右键以管理员权限运行。

## 被控端主动提权

被控端可以在对方发起连接时，直接点击`接受并提权`，或在已经连接的情况下点击`提权`。

|                   正在连接                   |                   已连接                    |
| :--------------------------------------: | :--------------------------------------: |
| ![](/docs/en/client/windows/windows-portable-elevation/images/cm_unauth.jpg) | ![](/docs/en/client/windows/windows-portable-elevation/images/cm_auth.jpg) |

## 控制端主动提权

在点击动作菜单中的`请求提权`后，将弹出下面的对话框。如果选择`请求远程用户授权`，则无需输入用户名和密码，但需要电脑对面的用户具有管理员权限。如果选择`发送管理员用户的账号和密码`，则只需要对面用户在UAC窗口点击确认。发送请求后，请等待对面用户确认UAC窗口, 然后将提示成功。需要注意的是，这两种方式**都需要被控端有人在UAC窗口点击确认**。因此，如果对面没有人，则被控端不应该主动请求提权。

|                    菜单                    |                   对话框                    |
| :--------------------------------------: | :--------------------------------------: |
| ![](/docs/en/client/windows/windows-portable-elevation/images/menu.png) | ![](/docs/en/client/windows/windows-portable-elevation/images/dialog.png) |
|                  **等待**                  |                  **成功**                  |
| ![](/docs/en/client/windows/windows-portable-elevation/images/wait.png) | ![](/docs/en/client/windows/windows-portable-elevation/images/success.png) |

## 如何选择

|                情形                |             方式             |
| :------------------------------: | :------------------------: |
|              无需处理提权              |            安装程序            |
|              被控端没有人              |     重命名<br>或右键以管理员权限运行     |
| 被控端有人<br/>且通过点击确认连接<br/>且连接时立即提权 |     被控端接收连接时点击`接受并提权`      |
|        被控端有人<br/>且仅必要时提权         | 被控端通过连接管理窗口提权<br/>或主控端请求提权 |






