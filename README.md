# home-assistant-visualization

Configuration of visualizations for my Home Assistant

## Table of content

- [Generic information](https://github.com/slittorin/home-assistant-visualization#generic-information)
- [Governing principles](https://github.com/slittorin/home-assistant-visualization#governing-principles)
- [Dashboard - Home Assistant](https://github.com/slittorin/home-assistant-visualization#dashboard---home-assistant)

## Generic information

- Home Assistant standard [Colors](https://github.com/home-assistant/core/blob/dev/homeassistant/util/color.py).

## Governing principles

#### Generic

- We want to run the Dashboard-setup in UI mode, but be able to push the configuration files to Github. This to keep the setup as standard as possible, but obtain the possibility to store the dashboards in Github.
  - As the lovelace files are by default stored in the `/config/.storage` directory that is by default ignored in `/config/.gitignore`.
    - We need to add the yaml-files for the dashboard manually as whitelisted in `/config/.gitignore`.

## Dashboard - Home Assistant

#### Setup

1. Create dashboard in the UI with:
   - `Title`: Home Assistant
   - `Icon`: mdi:home-assistant
   - `URL`: home-assistant
2. Through terminal, isolate the name of the lovelace-file in `/config/.storage`.
3. To file [/config/.gitignore](https://github.com/slittorin/home-assistant-config/blob/master/.gitignore), add the the whitelisted file as: `!.storage/lovelace.home_assistant`

#### Design and logic

We want to be able to have the following components:
- Be able to perform Github push, with possibility to add comment and show the latest status (last line in the log-file for [/config/scripts/github_push.sh](https://github.com/slittorin/home-assistant-config/blob/master/scripts/github_push.sh).
  - Through the `File Editor` add-on, edit the file [/config/configuration.yaml](https://github.com/slittorin/home-assistant-config/blob/master/configuration.yaml) and add (do not add `shell_command` if already present):
    ```yaml
    shell_command:
       github_push: /config/scripts/github_push.sh "{{ value }}"
    ```
  - 
- Be able to


