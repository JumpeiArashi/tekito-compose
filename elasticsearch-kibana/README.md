# ElasticSearch + fluentd + kibana

handle any log files roughly to analyze with kibana

## Starting Up Containers

```sh
docker-coompose up --build
```

## Stopping Containers

```sh
docker-compose stop
```

or ctrl+c haha!

## Removing Containers

**Warning**

Please don't forget rebuilding container after replace each container files. (I've left rebuilding containers many many time. :-( )

```sh
docker-compose rm --all
```

## Changing target log files

### 1. Mounting host side log directory to container

replace following volumes section to mount your log directory

```
# in docker-compose.yaml
services:
  fluentd:
    volumes:
      - YOUR_LOGFILE_DIRECTORY:/home/fluent/logs
```

### 2. Replace target log file name on fluent.conf

replace `path /home/fluent/logs/access.log` on fluentd/fluent.conf

## Datetime format

default datetime format is ISO8601. You can change this in fluentd/fluent.conf at `time_format`.

## Log file format

default log format is json. If your logs isn't formated, you should use `none` format.

```
# in fluentd/fluent.conf
<source>
..snip..
  format none
..snip..
</source>
```

## Trouble Shooting

### Fluent says `pattern not match`

This error occurrs when time_format or a line of logs format is invalid. For example, invalid json type, or datetime format isn't ISO8691.
You can debug with `date` command at invalid datetime format case.

```sh
$ date +%Y-%m-%dT%H:%M:%S%:z
1986-12-02T00:00:00+00:00
```
