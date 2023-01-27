# axis-ming:mongo
Common Node-RED configuration when scripting cameras with a local mongo database container.

# pre-requisites
- Linux host with Docker, Docker-compose and GIT installed

# Node-RED Configuration
You may want to alter the following default settings

## docker-compose.yaml
- Port = 8610
- Timezone = Europe/Stockholm
- container_name (if you paln to have multiple instance of Node-RED containers)


## settings.js
- httpAdminRoot: '/admin',   (Default flows view url http://address:8600/admin)
- ui: { path: "/" },         (Default dashboard url http://address:8600/)
- adminAuth:                 (Default disabled.  It is recommended that you enable admin credentials.  See [Securing Node-RED](https://nodered.org/docs/user-guide/runtime/securing-node-red#editor--admin-api-security))
- httpNodeAuth:              (Default disabled.  It is recommeded to enable credentials to dashboard view. See [Securing Dasboard](https://nodered.org/docs/user-guide/runtime/securing-node-red#http-node-security))
- contextStorage:            (Default enabled.  Contect data will be stored and retained between reboots)
- projects:                  (Default enable.  Allows to revisioning of local projects or import remote repositories)  
- credentialSecret           (Set your own key to encrypt sensative data on host)

# Deployment
Clone repository (e.g. from /home/user/ )
```
git clone https://github.com/pandosme/axis-common-node-red.git
cd axis-common-node-red
git checkout mongodb
```
Update containers
```
sudo docker-compose pull
```
Install npm packages. 
The following additional packages will be installed
- [Dashboard](https://flows.nodered.org/node/node-red-dashboard)
- [UI Table](https://flows.nodered.org/node/node-red-node-ui-table)
- [Axis device & Axis Camera](https://flows.nodered.org/node/node-red-contrib-axis-device)
- [Axis ACAP](https://flows.nodered.org/node/node-red-contrib-axis-acap)
- [Axis Security](https://flows.nodered.org/node/node-red-contrib-axis-security)
- [MongoDB](https://flows.nodered.org/node/node-red-node-mongodb)
- [InfluxDB](https://flows.nodered.org/node/node-red-contrib-influxdb)

If nodejs and npm is installed on your system run,
```
npm install
```
If nodejs and npm is not installed run
```
sudo docker-compose up -d
sudo docker exec -it axis-common-node-red bash
cd /data
npm install
exit
sudo docker-compose down
```
Optional edit docker-compose and settings.js (see above)
```
nano docker-compose.yaml
nano settings.js
```
Start container
```
sudo docker-compose up -d
```
Access Node-RED with a browser
```
Flows http://address:8600/admin
Dashboard http://address:8600
```
When entering flows view and you don't plan using projects, just click "Not right now"
