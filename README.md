# Dockerized-Jmeter-Influx-Grafana-Telegraf
Automated dockerized module with connected Influx &amp; Grafana with Jmeter out of box.



### Default auth for Grafana &amp; InfluxDB:

user: admin 

pass: admin123

### Default ports:

Grafana - 3000

InfluxDB - 8086

Chronograph - 8888

# Setup &amp; run the container
```
docker-compose up -d
```


# Running Jmeter test with an example script
```
./run-jmeter.sh
```
