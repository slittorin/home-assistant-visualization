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
    - We need to add to `/config/.gitignore` so that all lovelace-files are added to Github (see also [Github Push in Configuration](https://github.com/slittorin/home-assistant-configuration/blob/main/README.md#github-push).

## Dashboard - Home Assistant

### Setup

1. Create dashboard in the UI with:
   - `Title`: Home Assistant
   - `Icon`: mdi:home-assistant
   - `URL`: home-assistant

All the below is included in the [Lovelace UI config file for dashboard: Home Assistant](https://github.com/slittorin/home-assistant-config/blob/master/.storage/lovelace.home_assistant).

### Github push.

![Github push](https://github.com/slittorin/home-assistant-visualization/blob/main/images/push_to_github.png)

See also [Github Push configuration](https://github.com/slittorin/home-assistant-configuration#github-push).

We have the following visual components:
- Add Git commit comment.
- Press to trigger script to perform Git push.
- Show status for latest run (last row in the logfile).
