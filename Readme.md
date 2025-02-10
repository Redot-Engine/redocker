# ![Redocker](./logo.svg)

This is a collection of Redot Docker Images for use in CI/CD.

## Status
`✅`= verified to work  **|**  `❓`= unknown status  **|**  `❌`= known to not be working

### Redocker
| Target | Status |
|-----------|-----|
| `linux`   | ✅  |
| `windows` | ❓  |
| `web`     | ✅  |
| `android` | ❌  |
| `macos`   | ❌  |
| `ios`     | ❓  |

### Redocker Mono

> [!NOTE]
> There are Currently are no Mono based Images available

## Example Usage

Bind your Project inside the target container:
```sh
docker run -it --rm -v "$(pwd):/home/runner/game:Z" ghcr.io/redot-engine/redocker/linux-4.3:latest sh
```
Go into the Project dir
```sh
cd game
```
Run the Build
```sh
redot --headless --export-release Linux game.elf
```

