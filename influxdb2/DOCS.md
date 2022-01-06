# Home Assistant Community Add-on: InfluxDB2

InfluxDB is an open source time series database optimized for high-write-volume.
It's useful for recording metrics, sensor data, events,
and performing analytics. It exposes an HTTP API for client interaction and is
often used in combination with Grafana to visualize the data.

This add-on runs the InfluxDB v2.x build channel. \
For InfluxDB v1.x build channel, remove this add-on and install https://github.com/hassio-addons/addon-influxdb


## Installation

This add-on doesn't come from the commmunity store and needs to be added from a GitHub repository. Don't worry - the process isn't too hard!

1. Within Home Assistant, navigate to **Configuration** > ** Add-ons, Backups & Supervisor** 
1. Click **ADD-ON STORE** > **Menu** (3 dot elipsis, top right) > **Repositories**
1. Add the following Repository: https://github.com/Jays-Home-Assistant-Add-ons/repository
1. Install the InfluxDB2 add-on
1. After install, click **Start**
1. Check the logs tab to see if everything went well.
1. Navigate to the interface using
   - No-SSL: http://homeassistant.local:8086/
   - SSL: https://homeassistant.local:8086/


## First Run

When running the web UI provided by this add-on for the first time, you'll need to setup an account.
Navigate to the interface using the link above and create your first user

**Note**: _If you're planning on pushing Home Assistant data into InfluxDB using the Home Assistant Intergration, then set your first bucket name to be **home_asssistant**_ \
_Refer to **Integrating into Home Assistant** later in this document_


## Configuration

**Note**: _Remember to restart the add-on when the configuration is changed._

Example add-on configuration:

```yaml
reporting: true
ssl: true
certfile: fullchain.pem
keyfile: privkey.pem
envvars:
  - name: INFLUXD_LOG_LEVEL
    value: "info"
```

**Note**: _This is just an example, don't copy and paste it! Create your own!_


### Option: `log_level`

The `log_level` option controls the level of log output by the addon and can
be changed to be more or less verbose, which might be useful when you are
dealing with an unknown issue. Possible values are:

- `trace`: Show every detail, like all called internal functions.
- `debug`: Shows detailed debug information.
- `info`: Normal (usually) interesting events.
- `warning`: Exceptional occurrences that are not errors.
- `error`: Runtime errors that do not require immediate action.
- `fatal`: Something went terribly wrong. Add-on becomes unusable.

Please note that each level automatically includes log messages from a
more severe level, e.g., `debug` also shows `info` messages. By default,
the `log_level` is set to `info`, which is the recommended setting unless
you are troubleshooting.

The logging level set here doesn't change the logging level of InfluxDB. Use **envvars** for that.

### Option: `reporting`

This option allows you to disable the reporting of usage data to InfluxData.

**Note**: _No data from user databases is ever transmitted!_

### Option: `ssl`

Enables/Disables SSL (HTTPS) on the web interface.
Set it `true` to enable it, `false` otherwise.

**Note**: _This does NOT activate SSL for InfluxDB, just the web interface_

### Option: `certfile`

The certificate file to use for SSL.

**Note**: _The file MUST be stored in `/ssl/`, which is the default_

### Option: `keyfile`

The private key file to use for SSL.

**Note**: _The file MUST be stored in `/ssl/`, which is the default_

### Option: `envvars`

This allows the setting of Environment Variables to control InfluxDB
configuration as documented at:

<https://docs.influxdata.com/influxdb/v2.1/reference/config-options>

A common one might be to change the logging level of InfluxDB2. For example:

```yaml
envvars:
  - name: INFLUXD_LOG_LEVEL
    value: "info"
```
_Log levels include: debug, info, error_

**Note**: _Changing these options can possibly cause issues with you instance.
USE AT YOUR OWN RISK!_

These are case sensitive.

#### Sub-option: `name`

The name of the environment variable to set which must start with `INFLUXDB_`

#### Sub-option: `value`

The value of the environment variable to set, set the Influx documentation for
full details. Values should always be entered as a string (even true/false values).

### Option: `leave_front_door_open`

Adding this option to the add-on configuration allows you to disable
authentication on the Web Terminal by setting it to `true` and leaving the
username and password empty.

**Note**: _We STRONGLY suggest, not to use this, even if this add-on is
only exposed to your internal network. USE AT YOUR OWN RISK!_



## Integrating into Home Assistant

The `influxdb` integration of Home Assistant makes it possible to transfer all
state changes to an InfluxDB database.

You need to do the following steps in order to get this working:

- Navigate to the InfluxDB2 UI using the link under the **Installation** section of this document.
- On the left menu click on InfluxDB icon at the top.
- Navigate to **Load Data** > **API Tokens** > **+ Generate API Token** >> **Read/Write API Token**
- Set the decription to **Home Assistant InfluxDB Intergration API Token**
- Select the **home_assistant** bucket for both **Read** & **Write**  << IMPORTANT!!
- Click **Save**
- Click on the name of the newly created token
- Click **Copy to Clipboard** ->> This will be required in the yaml below

Now we need to get your organisation ID
- Looking at the URL in your browser, the organisation ID is the 16 digit text between the two slashs just to the right of the **orgs** text
- **fc08dc2f07e50755** is the organization you'll need to use in the yaml configuration based on this URL: http://homeassistant.local:8086/orgs/fc08dc2f07e50755/load-data/tokens

Next, add the following snippet to your Home Assistant
`configuration.yaml` file.

```yaml
influxdb:
  host: localhost
  port: 8086
  api_version: 2
  max_retries: 3
  default_measurement: state
  token: _YOUR_TOKEN_GOES_HERE_
  organization: _YOUR_ORG_ID_GOES_HERE_
  bucket: home_assistant
  ssl: false
  veryify_ssl: false
```

If you have implimented SSL, you may need to make the following changes to the above configuration:
```yaml
influxdb:
  host: _CHANGE_TO_YOUR_CERTIFICATE_HOSTNAME_
  ssl: true
  veryify_ssl: true
```

Restart Home Assistant.

You should now see the data flowing into InfluxDB by visiting the web-interface
and using the Data Explorer.

Full details of the Home Assistant integration can be found here:

<https://www.home-assistant.io/components/influxdb/>


## Known issues and limitations

- InfluxDB2 only supports x64 architecture


## Changelog & Releases

This repository keeps a change log using [GitHub's releases][releases]
functionality.

Releases are based on [Semantic Versioning][semver], and use the format
of `MAJOR.MINOR.PATCH`. In a nutshell, the version will be incremented
based on the following:

- `MAJOR`: Incompatible or major changes.
- `MINOR`: Backwards-compatible new features and enhancements.
- `PATCH`: Backwards-compatible bugfixes and package updates.

## Support

Got questions?

You have several options to get them answered:

- Start a discussion [On GitHub Here][discussion]
- The [Home Assistant Discord chat server][discord-ha] for general Home
  Assistant discussions and questions.
- The Home Assistant [Community Forum][forum].
- Join the [Reddit subreddit][reddit] in [/r/homeassistant][reddit]

You could also [open an issue here][issue] GitHub.

## Authors & contributors

The original setup of this repository is by [Jay Antoney][jantoney] \
The original InfluxDB v1.x add-on that this was based on is by [Franck Nijhof][frenck]

For a full list of all authors and contributors,
check [the contributor's page][contributors].

## License

MIT License

Copyright (c) 2022 Jay Antoney

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

[contributors]: https://github.com/Jays-Home-Assistant-Add-ons/j-addon-influxdb2/graphs/contributors
[discord-ha]: https://discord.gg/c5DvZ4e
[frenck]: https://github.com/frenck
[issue]: https://github.com/Jays-Home-Assistant-Add-ons/j-addon-influxdb2/issues
[reddit]: https://reddit.com/r/homeassistant
[releases]: https://github.com/Jays-Home-Assistant-Add-ons/j-addon-influxdb2/releases
[semver]: http://semver.org/spec/v2.0.0.htm
[discussion]: https://github.com/Jays-Home-Assistant-Add-ons/j-addon-influxdb2/discussions
[jantoney]: https://github.com/jantoney
