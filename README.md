# Sensu Go Elasticsearch metric handler plugin
[![Bonsai Asset Badge](https://img.shields.io/badge/CHANGEME-Download%20Me-brightgreen.svg?colorB=89C967&logo=sensu)](https://bonsai.sensu.io/assets/CHANGEME/CHANGEME) [![TravisCI Build Status](https://travis-ci.org/CHANGEME/sensu-go-elasticsearch.svg?branch=master)](https://travis-ci.org/CHANGEME/sensu-go-elasticsearch)

sensu-go-elasticsearch is a sensu go handler for pushing metric data and full
event bodies into elasticsearch for visualization in kibana.

## Installation

Download the latest version of the sensu-go-elasticsearch from [releases][1],
or create an executable script from this source.

From the local path of the sensu-go-elasticsearch repository:

```
go build -o /usr/local/bin/sensu-go-elasticsearch main.go
```

## Configuration

Example Sensu Go definition for metric handling:

Define an asset:
```json
{
  "type": "Asset",
  "api_version": "core/v2",
  "metadata": {
    "name": "sensu-go-elasticsearch",
    "namespace": "nbo_development",
    "labels": {},
    "annotations": {}
  },
  "spec": {
    "url": "https://github.com/jkerry/sensu-go-elasticsearch/releases/download/0.0.4/sensu-go-elasticsearch_0.0.4_linux_amd64.tar.gz",
    "sha512": "66e580e43b1babba0622d7df2a2d1482cfb4454e9fc050af60ff7b9bdd1a44874b485566d34f5291505c498703f7457221590dcdcdb9d75f5d5b8d80c9eeb901"
  }
}
```

Add a handler:
```json
{
  "type": "Handler",
  "api_version": "core/v2",
  "metadata": {
    "name": "elasticsearch",
    "namespace": "CHANGEME"
  },
  "spec": {
    "type": "pipe",
    "command": "sensu-go-elasticsearch -i metric_index_name -d",
    "env_vars": [
      "ELASTICSEARCH_URL=https://USERNAME:PASSWORD@URL_TO_ELASTICSEARCH:9243"
    ],
    "runtime_assets": [
      "elasticsearch"
    ],
    "filters": [
      "has_metrics"
    ]
  }
}
```

## Usage Examples

Help:

```
The Sensu Go handler for metric and event logging in elasticsearch
Required:  Set the ELASTICSEARCH_URL env var with an appropriate connection url (https://user:pass@hostname:port)

Usage:
  sensu-go-elasticsearch [flags]

Flags:
  -d, --dated_index    Should the index have the current date postfixed? ie: metric_data-2019-06-27
  -h, --help           help for sensu-go-elasticsearch
  -i, --index string   metric_data
```

## Contributing

See https://github.com/sensu/sensu-go/blob/master/CONTRIBUTING.md

[1]: https://github.com/jkerry/sensu-go-elasticsearch/releases
