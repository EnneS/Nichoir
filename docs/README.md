# Rapport technique
## Initialisation
### Docker-compose
Grâce à docker-compose, l'initialisation a été plutôt rapide.<br>
Une fois les dockers lancés et les droits sur les dossiers accordés, nous avons connecté NodeRed au server MQTT.

### Connection MQTT
Configuration serveur :
```
Connection:
  Server: lns.campusiot.imag.fr
  Port: 8883
  UseTLS: True
  Protocol: MQTT V3.1.1

Security:
  Username: <username_sur_gdoc>
  Password: <password_sur_gdoc>
```

Configuration topic :

```
Topic: application/216/device/+/rx
```

Ici ``216`` correspond à l'id de notre application.<br>
<br>
Ensuite il a fallu connecter NodeRed à InfluxDB

### Connection InfluxDB
Tout d'abord, il faut se connecter une fois à InfluxDB pour créer la base de donnée.<br>
Configuration serveur :
```
Version: 1.8-flux
URL: http://influxdb:8086
Username: <influxdb_username>
Password: <influxdb_password>
```

Configuration database:
```
Database: db0
```

Une fois RedNode connecté à InfluxDB, nous commençons à recevoir des données que nous pouvons afficher. Il faut donc connecter Grafana à InfluxDB.

### Connection Grafana
Chemin d'accès pour ajouter une source InfluxDB
``Configuration``-> ``Data source`` -> ``Add data source`` -> ``InfluxDB``

Configuration Grafana avec InfluxDB
```
URL: http://influxdb:8086
Database: db0
Username: <influxdb_username>
Password: <influxdb_password>
```

C'est tout bon ! Il reste plus qu'à faire un dashboard

### Création d'un dashboard

Lorsque tout est connecté, vous pouvez alors créer un ``dashboard`` et y ajouter des panneaux.
Dans chaque panneau vous pourrez faire des requêtes à partir des données/colonnes présentes dans la base de données.
