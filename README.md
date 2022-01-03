# Jay's Home Assistant Add-ons: InfluxDB2

![HA Ingress Support][ingressSupport]
![Local Build][influxdb2-local-build]

[![GitHub Release][releases-shield]][releases]
![Project Stage][project-stage-shield]
[![License][license-shield]](LICENSE.md)

![Supports aarch64 Architecture][aarch64-shield]
![Supports amd64 Architecture][amd64-shield]
![Supports armhf Architecture][armhf-shield]
![Supports armv7 Architecture][armv7-shield]
![Supports i386 Architecture][i386-shield]

![Project Maintenance][maintenance-shield]
[![GitHub Activity][commits-shield]][commits]


Scalable datastore for metrics, events, and real-time analytics.

## About

InfluxDB2 is an open source time series database optimized for high-write-volume.
It's useful for recording metrics, sensor data, events,
and performing analytics. It exposes an HTTP API for client interaction and is
often used in combination with Grafana to visualize the data.

This add-on is built on the InfluxDB v2.x build. \
If you're after the InfluxDB V1.x build - check out this other add-on [Here][Influxdbv1]

[:books: Read the full add-on documentation][docs]

## FAQ
- Why make another add-on and why not just upgrade the current [InfluxDB v1.x Community Add-on][Influxdbv1]?
  - The upgrade path from V1.x to V2.x requires access to the command line and isn't a very user friendly process. So I decided to create a new add-on and start from there.
- This doesn't support Home Assistant Ingress web interface - why not?
  - Unfortunately the way the ingress works requires the application to support a Base URL rewrite of some form and the InfluxDB2 project currently doesn't.
- Are kapacitor and chronograf both still avaliable in this build?
  - No, neither are included as InfluxDB2 now includes a UI and most features from these other packages.

## Support

Got questions?

You have several options to get them answered:

- Try the [discussion page][githubDiscussions] here on GitHub
- The [Home Assistant Discord chat server][discord-ha] for general Home
  Assistant discussions and questions.
- The Home Assistant [Community Forum][forum].
- Join the [Reddit subreddit][reddit] in [/r/homeassistant][reddit]

You could also [open an issue here][issue] on GitHub.

## Contributing

This is an active open-source project. We are always open to people who want to
use the code or contribute to it.

Thank you for being involved! :heart_eyes:

## Authors & contributors

The original setup of this repository is by [Jay Antoney][jantoney]. \
However I used the InfluxDB v1.x add-on from [Franck Nijhof][frenck] for some inspiration.

For a full list of all authors and contributors,
check [the contributor's page][contributors].

## Want more Add-ons?

Expand your Home Assistant instance with more apps, features, and widgits!

As I write more Add-on's, you can find them [here][repositoryMe]. \
Otherwise, check out the external [Home Assistant Community Add-on GitHub Repository][repositoryCommunity]

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


[influxdb2-local-build]: https://img.shields.io/badge/Home%20Assistant%20--%20local%20build-YES-orange.svg
[releases]: https://github.com/Jays-Home-Assistant-Add-ons/j-addon-influxdb2/releases
[releases-shield]: https://img.shields.io/github/release/Jays-Home-Assistant-Add-ons/j-addon-influxdb2.svg
[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[amd64-shield]: https://img.shields.io/badge/amd64-yes-green.svg
[armhf-shield]: https://img.shields.io/badge/armhf-no-red.svg
[armv7-shield]: https://img.shields.io/badge/armv7-yes-green.svg
[i386-shield]: https://img.shields.io/badge/i386-yes-green.svg
[commits-shield]: https://img.shields.io/github/commit-activity/y/Jays-Home-Assistant-Add-ons/j-addon-influxdb2.svg
[commits]: https://github.com/Jays-Home-Assistant-Add-ons/j-addon-influxdb2/commits/main
[contributors]: https://github.com/Jays-Home-Assistant-Add-ons/j-addon-influxdb2/graphs/contributors
[docs]: https://github.com/Jays-Home-Assistant-Add-ons/j-addon-influxdb2/blob/main/influxdb2/DOCS.md
[frenck]: https://github.com/frenck
[jantoney]: https://github.com/jantoney
[issue]: https://github.com/Jays-Home-Assistant-Add-ons/j-addon-influxdb2/issues
[license-shield]: https://img.shields.io/github/license/Jays-Home-Assistant-Add-ons/j-addon-influxdb2.svg
[maintenance-shield]: https://img.shields.io/maintenance/yes/2022.svg
[project-stage-shield]: https://img.shields.io/badge/project%20stage-production%20ready-brightgreen.svg
[reddit]: https://reddit.com/r/homeassistant
[repositoryMe]: https://github.com/Jays-Home-Assistant-Add-ons/repository
[Influxdbv1]: https://github.com/hassio-addons/addon-influxdb
[githubDiscussions]: https://github.com/hassio-addons/addon-influxdb/discussions
[repositoryCommunity]: https://github.com/hassio-addons/repository
[ingressSupport]: https://img.shields.io/badge/Home%20Assistant%20--%20ingress%20support-NO-red
