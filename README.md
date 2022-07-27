# Monitoring instructions

### Setup config for prometheus
```shell
scp prometheus.yml root@IP_ADDRESS:/prometheus.yml
```
### Go to virtual machine: 
```shell 
ssh root@IP_ADDRESS
```
### Install and start node_exporter:
```shell
cd /
git clone https://github.com/prometheus/node_exporter.git
cd node_exporter
apt install make
apt-get purge golang*
add-apt-repository ppa:longsleep/golang-backports
apt-get update
apt-get install golang-go
apt install golang-go
make build
./node_exporter --collector.systemd --collector.processes
```
Note: to restart/stop node exporter: 
`systemctl stop prometheus-node-exporter.service`


### Install and start prometheus
```shell
apt install prometheus
systemctl stop prometheus
prometheus --config.file=/prometheus.yml
```
### Install and start grafana
```shell
apt-get install -y apt-transport-https
apt-get install -y software-properties-common wget
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
apt-get update
apt-get install grafana
systemctl start grafana-server
```
### Go to IP_ADDRESS:3000 and set up username then password  
### Add datasource
1) Go to IP_ADDRESS:3000/datasources
2) Select Prometheus
3) Give url IP_ADDRESS:9090
4) Press Save and test in the bottom of form

### Add dashboard
1) Go to https://grafana.com/grafana/dashboards/ to find interesting one (e.g. https://grafana.com/grafana/dashboards/1860),
2) Remember its id (e.g. 1860)
3) Go to IP_ADDRESS:3000/dashboard/import and specify this id
4) Provide Prometheus datasource
5) Save dashboard
