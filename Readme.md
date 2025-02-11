# ![Redocker](./logo.svg)

This is a collection of Redot Docker Images for use in CI/CD.

## Images

Image names are constructed from multiple parts.
With Placeholders these Parts would look like:

```sh
ghcr.io/redot-engine/redocker/{actions}/{action-platform}/{type}/{target}-{version}:latest
```

| placeholder         | description                                                                                               |
| ------------------- | --------------------------------------------------------------------------------------------------------- |
| `{actions}`         | Is the Image for actions? if yes, put `action` here, if no, remove this segment                           |
| `{action-platform}` | This requires `{actions}` to be present. This can either be: `github` or `forgejo`                        |
| `{type}`            | Do you Require Mono? if no, use `minimal` if yes use `mono`                                               |
| `{target}`          | Which export templates to you require, choose one of `web`, `linux`, `windows`, `android`, `macos`, `ios` |
| `{version}`         | Which version of Redot are you using?                                                                     |

### Action Platforms

Values for the `{action-platform}`:
| Platform | Status |
|-----------|--------|
| `github` | ❓ |
| `forgejo` | ❓ |

`✅`= verified to work **|** `❓`= unknown status **|** `❌`= known to not be working

### Type

Values for the `{type}`:
| Type | Status |
|-----------|--------|
| `minimal` | ✅ |
| `mono` | ❌ |

`✅`= verified to work **|** `❓`= unknown status **|** `❌`= known to not be working

### Target

Values for the `{target}`:
| Target | Status |
|-----------|--------|
| `web` | ✅ |
| `linux` | ✅ |
| `windows` | ✅ |
| `android` | ❌ |
| `macos` | ❌ |
| `ios` | ❌ |

`✅`= verified to work **|** `❓`= unknown status **|** `❌`= known to not be working

### Version

Values for the `{version}`:
| Version | Status |
| `4.3` | ✅ |

`✅`= verified to work **|** `❓`= unknown status **|** `❌`= known to not be working

## Example Usage

Bind your Project inside the target container:

```sh
docker run -it --rm -v "$(pwd):/home/runner/game:Z" ghcr.io/redot-engine/redocker/minimal/linux-4.3:latest sh
```

Go into the Project dir

```sh
cd game
```

Run the Build

```sh
redot --headless --export-release Linux game.elf
```
