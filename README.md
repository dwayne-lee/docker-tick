# Docker TICK Stack

### To monitor localhost:
Edit the ./etc/telegraf.conf file and add the hostname to 'hostname = ""',
otherwise it will use the cotainer name which is not ideal.

### To monitor additional hosts:
Install Telegraf from https://docs.influxdata.com/telegraf/v1.9/introduction/installation/
Copy ./etc/telegraf.conf to additional hosts(/etc/telegraf/telegraf.conf),
edit the hostname and the inputs.procstat section, and start/enable telegraf.


### Deploy the TICK stack
```
$ sudo docker-compose up -d
```


### Test InfluxDB
```
$ curl http://localhost:8086/ping
```


### Check that Telegraf works and that telegraf DB was created
```
$ sudo docker-compose run influxdb-cli
> show databases
> exit
```


### Check that Chronograf works
http://localhost:8888


### Check that Kapacitor works
```
$ curl http://localhost:9092/kapacitor/v1/ping
```

```
$ sudo docker-compose run kapacitor-cli
$ kapacitor list tasks
```

```
$ sudo docker-compose run influxdb-cli
> show subscriptions
> exit
```


### Remove an old host from the Influx DB
```
$ sudo docker-compose run influxdb-cli
> DROP SERIES WHERE "host" = '8c9f36dc3030'
> DELETE FROM cpu,disk,diskio,mem,swap,system WHERE "host" = '8c9f36dc3030'
> exit
```


### Bring down the whole stack
```
$ sudo docker-compose down
```

