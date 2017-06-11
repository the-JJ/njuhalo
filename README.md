new(/njuː/)halo
===========
[![Go Report Card](https://goreportcard.com/badge/github.com/lpredova/njuhalo)](https://goreportcard.com/report/github.com/lpredova/njuhalo)


![Njuh njuh](https://68.media.tumblr.com/1da155f441f0c4030225c3811e0c32cd/tumblr_o6ngw4Ve1t1rt6u7do1_500.gif)


Njuhalo is watcher written in Go. 
It watches popular online store [Njuškalo.hr](https://www.njuskalo.hr) and
notifies owner for new occurrences of wanted items that match filters in config.
That way you can

## Usage

```
NAME:
   njuhalo - Watch Njuskalo better than anyone

USAGE:
   njuhalo [global options] command [command options] [arguments...]

VERSION:
   1.0.0

COMMANDS:
     init, initialize, i  initialize configuration and database file in home dir
     start, serve, s      start monitoring njuskalo for items
     add, query, a        adds query to watch to config
     print, p             Prints currently active config file
     help, h              Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --config value, --con value  PATH to config file (default: "$HOME/.njuhalo/config.json")
   --help, -h                   show help
   --version, -v                print the version
```


You need to configure your watcher how often do you want to run it.
Supported alerting channels are email and slack.

You can customize queries and filters so as intervals between fetching each page, because you don't want to send too many requests and act as an idiot.


### Configuration

Configuration file looks like this:

```
{
	"runIntervalMinutes": 1,
	"sleepIntervalSeconds": 2,
	"queries": [{
		"baseQueryPath": "iznajmljivanje-stanova/zagreb",
		"filters": {
			"locationId": "2619",
			"price[max]": "260",
			"mainArea[max]": "50"
		}
	}],
	"slack" : true,
	"slackToken": "",
	"slackChannelId" : "",
	"slackNotificationColor": "#fdcd00",
	"mail": true,
	"to": "myemail@gmail.com",
	"mailgunDomain":"",
	"mailgunAPIKey":"",
	"mailgunPublicKey":""
}

```
It can be found in:
``
{$HOME}/.njuhalo
``

If there is no such file you can create it manually or just run:
``
/.njuhalo i
``

### Adding queries
Adding queries can be pain in the ass so you can simply paste it like this 

``
/.njuhalo a http://www.njuskalo.hr/path?query=1&query=2
``

That will parse query and save it to the default config file.

Number of queries is not limited and you can add as much as you want.

## Development

Location of all njuhalo config and db is in your home folder

``
{$HOME}/.njuhalo
``

To build binary from scratch:

``
go build
``

---
MIT License

Copyright (c) **Lovro Predovan**
2017