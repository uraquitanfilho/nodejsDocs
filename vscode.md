# VSCODE SETUP

## Font

- Download and install [**FiraCode font**](https://github.com/tonsky/FiraCode)

## Plugins (vscode)

- Color Highlight > show HTML hex color
- Dracula Official > dark style
- vscode-icons > show extension icons
- EditorConfig for VS Code > setup a default config to TEAM
- ESLint > make default sintax to TEAM
- Prettier - Code formatter > Make auto adjust files from ESLint rules

## settings.json (ctrl+shift+p | command+shift+p(MAC))

```json
{
  "typescript.updateImportsOnFileMove.enabled": "always",
  "workbench.colorTheme": "Dracula",
  "editor.fontFamily": "Fira Code",
  "editor.fontLigatures": true,
  "editor.formatOnSave": true,
  "editor.rulers": [80, 120],
  "editor.tabSize": 2,
  "editor.renderLineHighlight": "gutter",
  "terminal.integrated.fontSize": 14,
  "emmet.syntaxProfiles": {
    "javascript": "jsx"
  },
  "emmet.includeLanguages": {
    "javascript": "javascriptreact"
  },
  "javascript.updateImportsOnFileMove.enabled": "never",
  "breadcrumbs.enabled": true,
  "editor.parameterHints.enabled": false,
  "prettier.eslintIntegration": true,
  "eslint.codeAction.disableRuleComment": {
    "enable": true,
    "location": "separateLine"
  },
  "eslint.enable": true,
  "eslint.autoFixOnSave": true, //to auto fix some syntaxe error code
  "eslint.validate": [
    {
      "language": "javascript",
      "autoFix": true
    },
    {
      "language": "javascriptreact",
      "autoFix": true
    },
    {
      "language": "typescript",
      "autoFix": true
    },
    {
      "language": "typescriptreact",
      "autoFix": true
    }
  ],
  "workbench.iconTheme": "vscode-icons"
}
```

<a href="README.md"><img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSJNVZV7wCi99hzuk8g0M21gtKq9bUCEUEhMIsYjYT3HqcoeDx1PA" width="90"></a>
