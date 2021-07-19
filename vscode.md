# Visual Studio Code

## Exclude directories from Python language tools

Create `pyrightconfig.json` file in project/ workspace root:

E.g. to exclude VS Code local history directory:

```json
{
    "exclude": [
        "**/.history"
    ]
}

```

## Shortcuts

- `Alt` + `UP / DOWN` switch line's position with line above / below
- `Shift` + `Alt` + `UP / DOWN` duplicate line above / below current position
