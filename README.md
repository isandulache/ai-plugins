# ai-plugins

Skills and plugins ready to use with Claude Code or other compatible platforms.
Developed by Julien SANDULACHE.

## TOC

- [ai-plugins](#ai-plugins)
  - [TOC](#toc)
  - [Available Plugins](#available-plugins)
  - [Install in Claude Code](#install-in-claude-code)
  - [Install in ChatGPT](#install-in-chatgpt)
  - [Adding a plugin](#adding-a-plugin)
  - [Licence](#licence)

## Available Plugins

Here is a list of available plugins:

| Plugin                                      |                           Description                                 |
|:--------------------------------------------|:----------------------------------------------------------------------|
| [menus-familiaux](plugins/menus-familiaux)  | FR: Assistant personnel pour choisir des plats du répertoire <br> familial et planifier les menus de la semaine selon la saison, <br> le temps disponible et les présences. |  

## Install in Claude Code

For more information and instructions for using the plugins with Claude Code please refer to the [README](README_Claude.md).

## Install in ChatGPT

Information and instructions for using the plugins with ChatGPT please refer to the [README](README_ChatGPT.md).

## Adding a plugin

1. create a folder `plugins/<name>/` (kebab-case) :

```shell
   plugins/<name>/
   ├── .claude-plugin/plugin.json
   ├── skills/<skill>/SKILL.md
   └── README.md
   ```

2. Declare the entry in `.claude-plugin/marketplace.json` :

```json
{
    "name": "<name>",
    "source": "./plugins/<name>",
    "description": "...",
    "version": "0.1.0"
}
   ```

3. Validate: `claude plugin validate .`
4. Add a line to the "Plugins" table.

## Licence

MIT
