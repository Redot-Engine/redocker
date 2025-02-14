# ![Redocker](./logo.svg)

This is a collection of Redot Docker Images for use in CI/CD.

## Images

Image names are constructed from multiple parts.
With Placeholders these Parts would look like:

```sh
ghcr.io/redot-engine/redocker/{actions}/{action-platform}/{type}/{target}-{version}:latest
```

### Action

Is this image for a specifiy CI/CD System?
If no, you can remove the `{actions}` and the sections requiring it.
If it is for a specific CI/CD platform, but `actions` here.

### Action Platforms

Which CI System are you using?
Values for the `{action-platform}`:

| Platform  | Status |
| --------- | ------ |
| `github`  | ❓     |
| `forgejo` | ❓     |
| `gitlab`  | ❓     |

`✅`= verified to work **|** `❓`= unknown status **|** `❌`= known to not be working

### Type

Do you require Mono?
If no use `minimal`

Values for the `{type}`:

| Type      | Status |
| --------- | ------ |
| `minimal` | ✅     |
| `mono`    | ❌     |

`✅`= verified to work **|** `❓`= unknown status **|** `❌`= known to not be working

### Target

Which export templates do you require?

Values for the `{target}`:

| Target    | Status                                                     |
| --------- | ---------------------------------------------------------- |
| `web`     | ✅                                                         |
| `linux`   | ✅                                                         |
| `windows` | ✅                                                         |
| `android` | ⚖️ [#2](https://github.com/Redot-Engine/redocker/issues/2) |
| `macos`   | ⚖️ [#3](https://github.com/Redot-Engine/redocker/issues/3) |
| `ios`     | ⚖️ [#3](https://github.com/Redot-Engine/redocker/issues/3) |

`✅`= verified to work **|** `❓`= unknown status **|** `❌`= known to not be working **|** `⚖️`= Not Possible due to License

### Version

Which version of Redot are you using?

Values for the `{version}`:

| Version | Status |
| ------- | ------ |
| `4.3`   | ✅     |

`✅`= verified to work **|** `❓`= unknown status **|** `❌`= known to not be working

## Example Usage

Bind your Project inside the target container:

```sh
docker run -it --rm -v "$(pwd):/game:Z" ghcr.io/redot-engine/redocker/minimal/linux-4.3:latest sh
```

Go into the Project dir

```sh
cd game
```

Run the Build

```sh
redot --headless --export-release Linux game.elf
```
