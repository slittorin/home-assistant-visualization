# home-assistant-visualization

Configuration of visualizations for my Home Assistant

## Table of content

- [Generic information](https://github.com/slittorin/home-assistant-visualization#generic-information)
- [Governing principles](https://github.com/slittorin/home-assistant-visualization#governing-principles)
- [Dashboard - Home Assistant](https://github.com/slittorin/home-assistant-visualization#dashboard---home-assistant)
  - [Github push](https://github.com/slittorin/home-assistant-visualization#github-push)
  - [Size of recorder database and tables](https://github.com/slittorin/home-assistant-visualization#size-of-recorder-database-and-tables)
  - [min(created) date for tables](https://github.com/slittorin/home-assistant-visualization#mincreated-date-for-tables)
  - [Number of domains and entities](https://github.com/slittorin/home-assistant-visualization#number-of-domains-and-entities).

## Generic information

- [Home Assistant standard Colors](https://github.com/home-assistant/core/blob/dev/homeassistant/util/color.py).
- [Home Assistant standard Graph Colors](https://github.com/home-assistant/frontend/blob/dev/src/common/color/colors.ts).

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

We have the following visual components in an entities card:
- Add Git commit comment.
- Press to trigger script to perform Git push.
- Show status for latest run (last row in the logfile).

### Size of recorder database and tables

![Recorder database and tables](https://github.com/slittorin/home-assistant-visualization/blob/main/images/recorder_database_and_tables.png)

See also [Home Assistant system - Database and tables data configuration](https://github.com/slittorin/home-assistant-configuration#package---home-assistant-system---database-and-tables-data).

We have the following visual components in an history graph card :
- History graph with the following entities:
  - Full recorder database size.
  - Size of the main tables:
    - states
    - events
    - statistics
    - statistics_short_term

### min(created date) for tables

![Min created date](https://github.com/slittorin/home-assistant-visualization/blob/main/images/min_created_date.png)

See also [Home Assistant system - Database and tables data configuration](https://github.com/slittorin/home-assistant-configuration#package---home-assistant-system---database-and-tables-data).

We have the following visual components in an history graph card :
- First created data for the main tables:
  - states
  - events
  - statistics
  - statistics_short_term

### Number of domains and entities

![Domains and sensors](xxx)

See also [Home Assistant system - Domains and entities configuration](https://github.com/slittorin/home-assistant-configuration/blob/main/README.md#package---home-assistant-system---domains-and-entities).

We have the following visual components in an two entities card:
- Entity card 1:
  - List of all domains.
- Entity card 2:
  - Number of all domains.
  - Number of entities.
  - Number of entities per domain.
