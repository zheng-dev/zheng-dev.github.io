settings.json
---
```json
{
    "editor.fontSize": 17,
    "editor.wordWrap": "on",
    "editor.formatOnSave": true,
    "github.copilot.enable": {
        "*": false,
        "plaintext": false,
        "markdown": false,
        "scminput": false,
        "rust": false
    },
    "workbench.secondarySideBar.defaultVisibility": "hidden",
    "workbench.editor.wrapTabs": true,
    "workbench.editor.enablePreview": false,
    "workbench.editor.revealIfOpen": true,
    "markdown-preview-enhanced.revealjsTheme": "beige.css",
    "markdown-preview-enhanced.codeBlockTheme": "vue.css",
    "markdown-preview-enhanced.enablePreviewZenMode": true,
    "editor.mouseWheelZoom": true,
    "markdown.preview.fontSize": 26,
    "chat.viewSessions.orientation": "stacked",
    "liveServer.settings.donotShowInfoMsg": true,
    "[json]": {
        "editor.quickSuggestions": {
            "strings": true
        },
        "editor.suggest.insertMode": "replace"
    },
    "diffEditor.ignoreTrimWhitespace": false,
    "rust-analyzer.server.path": "C:\\Users\\Administrator\\.cargo\\bin\\rust-analyzer.exe",
    "go.toolsManagement.autoUpdate": true,
    "terminal.integrated.defaultProfile.windows": "pwsh7",
    "terminal.integrated.tabs.title": "${sequence}",
    "terminal.integrated.commandsToSkipShell": [
        "workbench.action.terminal.newWithProfile"
    ],
    "terminal.integrated.profiles.windows": {
        "pwsh7": {
            "path": "pwsh.exe",
            "icon": "terminal-powershell"
        },
        "Codex": {
            "path": "pwsh.exe",
            "args": [
                "-Command",
                "codex"
            ],
            "icon": "terminal-powershell"
        },
    },
    "git.openRepositoryInParentFolders": "never"
}
```

tasks.json
---
```json
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "cc",
            "type": "shell",
            "command": [
                "cd web;npm run build;cd .. ;",
                "powershell -NoProfile -ExecutionPolicy Bypass -File .vscode/increment-yk-version.ps1 ;",
                "$version = (Get-Content -Raw npm/package.json | ConvertFrom-Json).version; go build -trimpath -ldflags ('-s -X main.version=' + $version) -o cc-connect.exe ./cmd/cc-connect/ ;",
                "xcopy cc-connect.exe C:\\Users\\Administrator\\AppData\\Roaming\\npm\\node_modules\\yk-connect\\bin\\yk-connect.exe /Y /F;",
            ],
            "problemMatcher": []
        },
        {
            "label": "cc-publish",
            "type": "shell",
            "dependsOn": "cc",
            "dependsOrder": "sequence",
            "command": [
                "upx --best cc-connect.exe ;",
                "xcopy cc-connect.exe .\\npm\\bin\\yk-connect.exe /Y /F;",
                "npm publish .\\npm\\"
            ],
            "problemMatcher": []
        }
    ]
}
```