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