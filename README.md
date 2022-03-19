# home-assistant-visualization

Configuration of visualizations for my Home Assistant

## Table of content

- [Generic information](https://github.com/slittorin/home-assistant-visualization#generic-information)
- [Governing principles](https://github.com/slittorin/home-assistant-visualization#governing-principles)
- [Dashboard - Home Assistant](https://github.com/slittorin/home-assistant-visualization#dashboard---home-assistant)
  - [Github push](https://github.com/slittorin/home-assistant-visualization#github-push)
  - [Git for Grafana](https://github.com/slittorin/home-assistant-visualization#git-for-grafana)
  - [Size of recorder database and tables](https://github.com/slittorin/home-assistant-visualization#size-of-recorder-database-and-tables)
  - [min(created) date for tables](https://github.com/slittorin/home-assistant-visualization#mincreated-date-for-tables)
  - [Number of domains and entities](https://github.com/slittorin/home-assistant-visualization#number-of-domains-and-entities).

## Generic information

- [Home Assistant standard Colors](https://github.com/home-assistant/core/blob/dev/homeassistant/util/color.py).
- [Home Assistant standard Graph Colors](https://github.com/home-assistant/frontend/blob/dev/src/common/color/colors.ts).
  - Used in index order by HA.
- For Grafana (Inspire from [from Dummy labs](https://dummylabs.com/post/2019-01-13-influxdb-part1/) and others):
  - Light theme add `&theme=light` to Grafana url.
  - Refresh interval add `&refresh=1m` to Grafana url ([time range controls](https://grafana.com/docs/grafana/latest/dashboards/time-range-controls/)).
  - Time intervals `&from=now-8h&to=now` to Grafana url (remember to set Override relative time).
  - For Dashboards. Kiosk mode `&kiosk=tv` to Grafana url.
  - For Bar charts in Grafana, [Convert time series to string](https://community.grafana.com/t/grafana-8-bar-chart-not-working-with-time-base-labels/50062).
- For Grafana and InfluxDB 2 flux language:
  - Vaulable information here [InfluxDB Flux language advanced features](https://www.sqlpac.com/en/documents/influxdb-flux-language-advanced-features.html).
  - Get sum over time:
    ```flux
    from(bucket: "ha")
      |> range(start: v.timeRangeStart, stop: v.timeRangeStop)
      |> filter(fn: (r) => r["entity_id"] == "electrical_consumption_intake_cost_hour")
      |> filter(fn: (r) => r["_field"] == "value")
      |> cumulativeSum()
    ```
  - Get max value over time, with aggregated data over 1h (min and mean can also be used):
    ```flux
    from(bucket: "ha")
      |> range(start: v.timeRangeStart, stop: v.timeRangeStop)
      |> filter(fn: (r) => r["entity_id"] == "electrical_consumption_intake_cost_hour")
      |> filter(fn: (r) => r["_field"] == "value")
      |> aggregateWindow(every: 1h, fn: sum)
      |> max()
    ```
  - Got sum values over time, with field-name and aggregated data in 2h intervals, and span empty data:
    ```flux
    from(bucket: "ha")
      |> range(start: v.timeRangeStart, stop: v.timeRangeStop)
      |> filter(fn: (r) => r["entity_id"] == "electrical_consumption_intake_cost_hour")
      |> filter(fn: (r) => r["_field"] == "value")
      |> map(fn: (r) => ({
          _value: r._value,
          _time: r._time,
          _field: "Kostnad",
      }))
      |> aggregateWindow(every: 2h, fn: sum, createEmpty: true)
    ```
- Heights for card can be set with Card Mod:
  ```yaml
  card_mod:
    style: |
    ha-card {
      height:256px !important;
    }
  ```

## Governing principles

#### Generic

- See [Govering principles in Setup](https://github.com/slittorin/home-assistant-setup#governing-principles) for the capabilities setup for databases, retention and visualization. 
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

### Copy to server1

![Github copy files to server1](https://github.com/slittorin/home-assistant-visualization/blob/main/images/copy_backup.png)

See also [Github Copy files to server1 configuration](https://github.com/slittorin/home-assistant-configuration#copy-backup-files-to-server1).

We have the following visual components in an entities card:
- Press to trigger script to perform copy of files.
- Show status for latest run (last row in the logfile).

### Git for Grafana

![Grafana Github push](https://github.com/slittorin/home-assistant-visualization/blob/main/images/grafana_github_push.png)

See also [Git for Grafana configuration](https://github.com/slittorin/home-assistant-setup#git-for-grafanah).

We have the following visual components in an entities card:
- Add Git commit comment.
- Press to trigger script to perform Git push.
- Show status for latest run (last row in the logfile).

### Size of recorder database and tables

![Recorder database and tables](https://github.com/slittorin/home-assistant-visualization/blob/main/images/recorder_database_and_tables.png)

See also [Home Assistant system - Database and tables data configuration](https://github.com/slittorin/home-assistant-configuration#package---home-assistant-system---database-and-tables-data).

We have the following visual components in an history graph card:
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

![Domains used](https://github.com/slittorin/home-assistant-visualization/blob/main/images/domains_used.png)
![Domains and entities](https://github.com/slittorin/home-assistant-visualization/blob/main/images/domains_entities.png)

See also [Home Assistant system - Domains and entities configuration](https://github.com/slittorin/home-assistant-configuration/blob/main/README.md#package---home-assistant-system---domains-and-entities).

Note that we need to add senors manually for domains that are not present, see [Regular maintenance - Add domain sensors](https://github.com/slittorin/home-assistant-maintenance#add-domain-sensors).

We have the following visual components in an two entities card:
- Entity card 1:
  - List of all current domains.
- Entity card 2:
  - Number of all current domains.
  - Number of current entities.
  - Number of entities per domain.

### InfluxDB database size

![Domains and entities](https://github.com/slittorin/home-assistant-visualization/blob/main/images/domains_entities.png)

See also [Home Assistant system - InfluxDB size configuration](https://github.com/slittorin/home-assistant-configuration#package---home-assistant-system---influxdb-size).


We have the following visual components in an two entities card:
- Entity card 1:
  - List of all current domains.
- Entity card 2:
  - Number of all current domains.
  - Number of current entities.
  - Number of entities per domain.
