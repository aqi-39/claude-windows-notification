# Claude Code Windows 通知功能使用指南

## 功能说明

为 Claude Code 添加 Windows 系统通知功能。当会话停止或收到通知事件时，会自动显示 Windows 通知。

## 设置步骤

### 1. 复制通知脚本到全局配置目录

将项目中的 `windows-notification.ps1` 脚本复制到 Claude Code 全局配置目录：

**目标路径**: `%APPDATA%\claude-code\windows-notification.ps1`

### 2. 配置全局 hooks

将以下配置添加到用户级别的全局配置文件：

**配置文件路径**: `%APPDATA%\claude-code\settings.json`

```json
{
  "hooks": {
    "Stop": [
      {
        "matcher": "*",
        "hooks": [
          {
            "type": "command",
            "command": "powershell -ExecutionPolicy Bypass -File \"$env:APPDATA\\claude-code\\windows-notification.ps1\" -Title 'Claude Code' -Message 'Session stopped'",
            "async": true
          }
        ]
      }
    ],
    "Notification": [
      {
        "matcher": "*",
        "hooks": [
          {
            "type": "command",
            "command": "powershell -ExecutionPolicy Bypass -File \"$env:APPDATA\\claude-code\\windows-notification.ps1\" -Title 'Claude Code' -Message 'Approval Required'",
            "async": true
          }
        ]
      }
    ]
  }
}
```
### 3. 重启

重启 Claude Code 让设置生效. 