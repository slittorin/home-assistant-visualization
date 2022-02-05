# home-assistant-visualization

Configuration of visualizations for my Home Assistant

## Table of content

- [Generic information](https://github.com/slittorin/home-assistant-setup#generic-information)
- [Governing principles](https://github.com/slittorin/home-assistant-setup#generic-information)
- [Dashboard - Home Assistant](https://github.com/slittorin/home-assistant-setup#generic-information)

## Generic information

- Home Assistant standard [Colors}(https://github.com/home-assistant/core/blob/dev/homeassistant/util/color.py).

## Governing principles

#### Generic

- We want to run the Dashboard-setup in UI mode, but be able to push the configuration files to Github. This to keep the setup as standard as possible, but obtain the possibility to store the dashboards in Github.
  - As the lovelace files are by default stored in the `/config/.storage` directory that is by default ignored in `/config/.gitignore`.
    - We need to add the yaml-files for the dashboard manually as whitelisted in `/config/.gitignore`.

## Dashboard - Home Assistant

#### Design and logic

We want to be able to have the following components:
- 
