# axis-ming-path

A tool to analyze how objects moves within a scene.  The data is captured by an ACAP called Path that is installed in Axis cameras.  The data is sent over MQTT to an MQTT broker hosted within the tool.  The data is stored in an InfluxDB and a MongoDB also hosted within the toool.

The container includes:
* Node-RED, flows and modules
* Mosquitto MQTT Broker
* Mongo DB
* Influx DB
* Grafan can be easily added by editing the docker-compose.yaml


# pre-requisites
- Linux host with Docker, Docker-compose and GIT installed

# Customization

## docker-compose.yaml
You may want to edit the following in docker-compose.yaml for production systems

```
  nodered:
    environment:
      - TZ=Europe/Stockholm
    ports:
      - '8050:1880'
  mqtt:
    ports:
      - '1883:1883'
  mongodb:
    container_name: axis-ming-path-mongo
    image: mongo:4.4.14
    restart: always
\# Remove \# below to expose mongodb port outside the container
\#    ports:
\#      - 27017:27017
\#    environment:
\#      - MONGO_INITDB_ROOT_USERNAME=user
\#      - MONGO_INITDB_ROOT_PASSWORD=password
  influxdb:
\# Remove # to expose influx db outisde  
\#    ports:
\#      - '8686:8086'  

```

## settings.js
- httpAdminRoot: '/admin',   (Default flows view url http://address:8600/admin)
- ui: { path: "/" },         (Default dashboard url http://address:8600/)
- adminAuth:                 (Default disabled.  It is recommended that you enable admin credentials.  See [Securing Node-RED](https://nodered.org/docs/user-guide/runtime/securing-node-red#editor--admin-api-security))
- httpNodeAuth:              (Default disabled.  It is recommeded to enable credentials to dashboard view. See [Securing Dasboard](https://nodered.org/docs/user-guide/runtime/securing-node-red#http-node-security))
- contextStorage:            (Default enabled.  Contect data will be stored and retained between reboots)
- projects:                  (Default enable.  Allows to revisioning of local projects or import remote repositories)  
- credentialSecret           (Set your own key to encrypt sensative data on host)


# Deployment
```
git clone https://github.com/pandosme/axis-ming
cd axis-ming
git checkout path
docker-compose up -d
```

You need to edit the Axis Node and add user and password to get background images.
