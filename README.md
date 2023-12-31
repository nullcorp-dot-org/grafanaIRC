# grafanaIRC
IRC bot that sends grafana alerts to IRC
Planned Features:

Bot stuff
- [X] connect to IRC (SASL preferred)
- IRC commands:
  - [X] `alert rate [alertname] [duration]`	: set a rate limit on an alert
  - [X] `alert mute alertname [duration]` : mute an alert for a certain period of time
  	 	  [ ] default value for mute duration?
  - [X] `alert unmute alertname` : unmute a currently muted alert (same as `alert mute alertname 0m`)
  - [ ] `alert list` list alerts which are muted
  - [X] `alert info alertname` : report current [mute, last seen, rate limit] record
  
  - [X] join / part channel, defaults to current channel if none given
  - [X] quit command

- [ ] IRC command to temporarily mute bot for a period of time.
- [X] possible format request: 10h10m30s etc (supported up to hours. Days+ not supported)
- [ ] Authentication based on who has +o, +a, etc
- [X] Autojoin channels
- [X] reports firing alerts on channel

Graphana stuff
- [X] Host simple web endpoint to receive JSON post requests ( to receive an alert from grafana )
- [X] JSON parsing of alerts
- [X] Rate Limiting: Determine if the alert has been reported within configurable time window. If not, report to IRC.
- [X] Rate Limiting duration configurable per alert.
- [ ] default, global rate limit


Other
- [ ] connect to postgresQL to store IRC bot settings(blacklist)
- [X] take startup configs (IRC server, username, password) from a yaml file
- [ ] Dockerize


Notes:
Alerts should have:
- Alert_name
- Rate_limit ( eg, report only every 15m )
- Mute_until: timestamp, stored as unix timestamp.
- Last_seen : last time we observed this alert
- Last_reported : last time we reported ( subject to mute / rate limits )
  