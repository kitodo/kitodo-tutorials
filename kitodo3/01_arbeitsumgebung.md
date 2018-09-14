[kitodo-tutorials](../README.md) » [kitodo3](README.md) » 01_arbeitsumgebung.md

# Arbeitsumgebung für Kitodo 3.x

Zum Zeitpunkt des Workshops (September 2018) sind die folgenden Versionen von Kitodo aktuell:

* Kitodo.Production: [2.1.0](https://www.kitodo.org/news/2017/05/23/release-kitodoproduction-210/)
* Kitodo.Presentation: [2.2.0](https://www.kitodo.org/news/2017/12/27/kitodopresentation-220/)

Wir werden mit einer **Entwicklerversion von Kitodo.Production 3.x** arbeiten, um uns vor dem offiziellen Beta-Release einen Eindruck von den neuen Funktionalitäten und dem neuen Design verschaffen zu können.

## Installation des Webservers

Wir werden in diesem Tutorial Kitodo.Production auf einem Linux-Webserver installieren. Um den Linux-Webserver bereitzustellen, werden im Folgenden zwei Möglichkeiten beschrieben:

1. **Installation einer virtuellen Maschine mit der Software VirtualBox** (hierzu benötigen Sie Administrationsrechte auf Ihrem PC, 4 GB freien Arbeitsspeicher, 20 GB freien Festplattenspeicher und einen aktuellen Prozessor mit Baujahr etwa ab 2011)
2. **Installation einer virtuellen Maschine bei einem Cloud-Hoster** (erfordert eine Registrierung bei einem Hoster, dauerhafte Nutzung kostet etwa 20 Dollar pro Monat; ein etwa zweiwöchiger Test im Rahmen dieses Tutorials lässt sich über das Empfehlungsprogramm von Digital Ocean kostenfrei realisieren, Sie müssen dafür aber eine Kreditkarte hinterlegen)

### Variante 1: Installation mit VirtualBox

Laden Sie die Software [VirtualBox](https://www.virtualbox.org/wiki/Downloads) herunter und installieren Sie diese auf Ihrem Betriebssystem. Die Software ist erhältlich für Windows, Mac (OS X) und Linux.

Laden Sie außerdem das Installationsmedium (ISO-Datei) der Linux-Distribution Debian in der Version 9.4 herunter: https://cdimage.debian.org/cdimage/archive/9.4.0/amd64/iso-cd/debian-9.4.0-amd64-netinst.iso (291 MB).

#### Neue virtuelle Maschine erstellen:

- Name: `kitodo 3.0.0-alpha.2`
- Type: `Linux`
- Version: `Debian (64-bit)`
- Memory size: `4096 MB`
- Hard disk: `VDI` / `dynamically allocated` / `20 GB`

#### **Einstellungen der virtuellen Maschine anpassen (Empfehlungen):**

- General/Advanced/Shared clipboard: `Bidirectional`
- System/Processor/Processor(s): `2` 
- System/Processor/Extended Features: `Enable PAE/NX`
- Display/Screen/Video Memory: `128 MB`
- Network/Adapter 1/Advanced/Port Forwarding/+
  - Host Port: `8080`
  - Guest Port: `8080`

#### Start der virtuellen Maschine:

Wählen Sie die zuvor heruntergeladene Installationsdatei aus (`debian-9.4.0-amd64-netinst.iso`) und machen Sie im Installationsprozess folgende Angaben:

- Select `Graphical install`
- Language: `English`
- Location: `United States`
- Keyboard: `German`
- Hostname: `kitodo`
- Domain: `` (blank)
- Root password: `kitodo`
- Full name: `kitodo`
- User name: `kitodo`
- User password: `Workshop20180910`
- Time zone: `Eastern`
- Partioning method: `Guided - use entire disk`
- Partioning scheme: `All files in one partition`
- Mirror: `Germany/ftp.de.debian.org`
- Proxy: `` (blank)
- Software: deselect `print server`

#### VirtualBox Gasterweiterungen installieren

Nach erfolgreicher Installation des Betriebssystems müssen noch Erweiterungen der Software VirtualBox installiert werden, damit die Zwischenablage funktioniert. Außerdem erleichtert es uns die weitere Installation, wenn wir das Paket `sudo` installieren, damit der Nutzer `kitodo` mit Administrationsrechten arbeiten kann.

Öffnen Sie das Programm `Terminal` und geben Sie dort folgenden Befehl ein (das System startet nach der Installation automatisch neu):

```
su -c 'echo "deb http://ftp.debian.org/debian stretch-backports main contrib" > /etc/apt/sources.list.d/stretch-backports.list && apt update && apt install -y virtualbox-guest-dkms virtualbox-guest-x11 linux-headers-$(uname -r) sudo && adduser $USER sudo && echo \"Defaults timestamp_timeout=300\" >> /etc/sudoers.d/timeout && reboot'
```

### Variante 2: Installation bei einem Cloud-Hoster (am Beispiel von Digital Ocean)

Eine kostengünstige Möglichkeit ist die Registrierung beim Anbieter Digital Ocean. Sie erhalten 10 Dollar Startguthaben, sofern Sie sich über folgenden Link anmelden: https://m.do.co/c/22f45ed23fdd

*Disclaimer: Der Autor dieses Tutorials erhält von Digital Ocean 25 Dollar Guthaben, sofern Sie Digital Ocean weiter nutzen und dort mindestens 25 Dollar ausgeben, vgl. [Empfehlungsprogramm](https://www.digitalocean.com/docs/accounts/settings/referral-program/)*.

#### Droplet erstellen

* Image: Distributions / Debian / 9.5 x64
* Size: 4 GB, 2 vCPUs, 80GB, 4TB
* Datacenter region: Frankfurt

#### Login via SSH

Per E-Mail wird die IP-Adresse und ein Einmalpasswort zugestellt. Verbinden Sie sich über SSH mit dem Server. Unter Windows können Sie den kostenlosen SSH-Client [putty.exe](https://the.earth.li/~sgtatham/putty/latest/w32/putty.exe) verwenden, der ohne Administrationsrechte ausgeführt werden kann. Unter Mac OS X und Linux ist eine SSH-Funktionalität integriert und kann direkt vom Terminal aufgerufen werden. Beispiel:

```
ssh root@46.101.132.29
```

Sobald Sie mit dem Einmalpasswort eingeloggt sind, müssen Sie ein neues Passwort für den Root-Account vergeben. Als erstes sollten wir danach Sicherheitsupdates installieren:

```
apt update && apt upgrade
```

Legen Sie anschließend einen neuen Account mit Administrationsrechten an. Im Workshop verwenden wir das Passwort `Workshop20180910`. Fehlermeldungen wie `sent invalidate(passwd) request, exiting` können Sie ignorieren (Hintergründe in der Doku von DigitalOcean [Initial Server Setup with Debian 9](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-debian-9)).

```
adduser kitodo
```

```
usermod -a -G sudo kitodo
```

Melden SIe sich dann mit dem neuen Account via SSH an. Beispiel:

```
exit
ssh kitodo@46.101.132.29
```

#### Firewall einrichten

Zum Schutz vor unberechtigten Zugriffen installieren wir abschließend eine Firewall und lassen nur Verbindungen über SSH sowie über den Port 8080 (für den Tomcat Webserver, der später installiert wird) zu:

```
sudo apt install ufw
```

```
sudo ufw allow OpenSSH
sudo ufw allow 80
sudo ufw allow 8080
sudo ufw enable
```

## Installation von Kitodo.Production

Die folgende Installationsanleitung entspricht der [offiziellen Anleitung zur Erstellung einer aktuellen Entwicklerversion](https://github.com/kitodo/kitodo-production/blob/master/docs/gettingstarted/development-version.md) (Stand September 2018). Wir nutzen für den Workshop den Entwicklungsstand vom 7. September zuzüglich der zu diesem Zeitpunkt noch nicht germergten Pull Requests 1748, 1753, 1755 und 1758. Dieser Stand ist in folgendem GitHub-Branch verfügbar: [felixlohmeier/kitodo-production/tree/workshop20180910](felixlohmeier/kitodo-production/tree/workshop20180910).

Anders gesagt: Es handelt sich um unfertige Software, die nicht für den Produktivbetrieb freigegeben ist. Bitte beachten Sie auch, dass die folgende Anleitung für eine Testinstallation gedacht ist und unsichere Passwörter enthält.

### mysql.com 5.7 als Paketquelle ergänzen

```
sudo apt install -y dirmngr
```

```
sudo apt-key adv --keyserver pgp.mit.edu --recv-keys 5072E1F5 && echo "deb http://repo.mysql.com/apt/debian/ stretch mysql-5.7" | sudo tee -a /etc/apt/sources.list.d/mysql-5.7.list
```

### Pakete openjdk-8, maven, mysql-community-server und zip installieren

```
sudo debconf-set-selections <<< "mysql-community-server mysql-community-server/root-pass password "
sudo debconf-set-selections <<< "mysql-community-server mysql-community-server/re-root-pass password "
sudo apt update && sudo apt install -y openjdk-8-jdk maven mysql-community-server zip
```

### Java Sicherheitseinstellungen für Nutzung in Cloud-Umgebungen anpassen

```
sudo sed -i 's/securerandom.source=file:\/dev\/random/securerandom.source=file:\/dev\/urandom/' /etc/java-8-openjdk/security/java.security
```

### Entwicklerversion basierend auf dem GitHub branch [felixlohmeier/kitodo-production/tree/workshop20180910](https://github.com/felixlohmeier/kitodo-production/tree/workshop20180910) bauen

```
wget https://github.com/felixlohmeier/kitodo-production/archive/workshop20180910.zip
unzip workshop20180910.zip && rm workshop20180910.zip
mv kitodo-production-workshop20180910 kitodo-production-master
(cd kitodo-production-master/ && mvn clean package '-P!development')
zip -j kitodo-3-modules.zip kitodo-production-master/Kitodo/modules/*.jar
mv kitodo-production-master/Kitodo/target/kitodo-3*.war kitodo-3.war
```

### MySQL Datenbank und Nutzer anlegen

```
sudo mysql -e "create database kitodo;grant all privileges on kitodo.* to kitodo@localhost identified by 'kitodo';flush privileges;"
```

### Beispieldaten laden und in Kitodo 3.x Datenbankformat transformieren

```
cat kitodo-production-master/Kitodo/setup/schema.sql | mysql -u kitodo -D kitodo --password=kitodo
cat kitodo-production-master/Kitodo/setup/default.sql | mysql -u kitodo -D kitodo --password=kitodo
(cd kitodo-production-master/Kitodo-DataManagement && mvn flyway:baseline -Pflyway && mvn flyway:migrate -Pflyway)
mysqldump -u kitodo --password=kitodo kitodo > kitodo-3.sql
```

### Zip-Archiv mit Verzeichnisstruktur und Konfigurationsdateien erstellen

```
mkdir zip zip/config zip/debug zip/import zip/logs zip/messages zip/metadata zip/plugins zip/plugins/command zip/plugins/import zip/plugins/opac zip/plugins/step zip/plugins/validation zip/rulesets zip/scripts zip/swap zip/temp zip/users zip/xslt zip/diagrams
install -m 444 kitodo-production-master/Kitodo/src/main/resources/kitodo_*.xml zip/config/
install -m 444 kitodo-production-master/Kitodo/src/main/resources/modules.xml zip/config/
install -m 444 kitodo-production-master/Kitodo/src/main/resources/docket*.xsl zip/xslt/
install -m 444 kitodo-production-master/Kitodo/rulesets/*.xml zip/rulesets/
install -m 444 kitodo-production-master/Kitodo/diagrams/*.xml zip/diagrams/
install -m 554 kitodo-production-master/Kitodo/scripts/*.sh zip/scripts/
chmod -w zip/config zip/import zip/messages zip/plugins zip/plugins/command zip/plugins/import zip/plugins/opac zip/plugins/step zip/plugins/validation zip/rulesets zip/scripts zip/xslt
(cd zip && zip -r ../kitodo-3-config.zip *)
```

### Elasticsearch 5.x als Paketquelle ergänzen

```
sudo apt install -y apt-transport-https
```

```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add - && echo "deb https://artifacts.elastic.co/packages/5.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-5.x.list
```

### Pakete tomcat8, elasticsearch und curl installieren

```
sudo apt update && sudo apt install -y tomcat8 elasticsearch curl
```

### Tomcat konfigurieren

```
sudo sed -i 's/JAVA_OPTS="-Djava.awt.headless=true/JAVA_OPTS="-Djava.awt.headless=true -Xmx1920m/' /etc/default/tomcat8
```

### MySQL konfigurieren

```
sudo sh -c "echo '[mysqld] innodb_file_per_table' >> /etc/mysql/my.cnf"
sudo service mysql restart
```

### Elasticsearch konfigurieren

```
sudo sed -i 's/#path.data: \/path\/to\/data/path.data: \/var\/lib\/elasticsearch/' /etc/elasticsearch/elasticsearch.yml
sudo sed -i 's/#path.logs: \/path\/to\/logs/path.logs: \/var\/log\/elasticsearch/' /etc/elasticsearch/elasticsearch.yml
sudo sed -i 's/#cluster.name: my-application/cluster.name: kitodo/' /etc/elasticsearch/elasticsearch.yml
sudo sed -i 's/#node.name: node-1/node.name: kitodo-1/' /etc/elasticsearch/elasticsearch.yml
sudo /bin/systemctl daemon-reload
sudo /bin/systemctl enable elasticsearch.service
sudo systemctl start elasticsearch.service
until curl -s -X GET "localhost:9200/kitodo" | grep -q -o "kitodo" ; do sleep 1; done
curl -X PUT "localhost:9200/kitodo"
```

### Verzeichnisse für Kitodo anlegen und Berechtigungen setzen

```
sudo mkdir /usr/local/kitodo
sudo unzip kitodo-3-config.zip -d /usr/local/kitodo
sudo chown -R tomcat8:tomcat8 /usr/local/kitodo
```

### Kitodo Module installieren

```
sudo mkdir /usr/local/kitodo/modules
sudo unzip kitodo-3-modules.zip -d /usr/local/kitodo/modules
sudo chown -R tomcat8:tomcat8 /usr/local/kitodo/modules
```

### Die oben gebaute Entwicklerversion in den Tomcat Webserver laden

```
sudo chown tomcat8:tomcat8 kitodo-3.war
sudo mv kitodo-3.war /var/lib/tomcat8/webapps/kitodo.war
until curl -s GET "localhost:8080/kitodo/pages/login.jsf" | grep -q -o "KITODO.PRODUCTION" ; do sleep 1; done
```

### Plugins installieren

```
sudo ln -s /var/lib/tomcat8/webapps/kitodo/plugins/opac/OpacPica-Plugin-1.0-SNAPSHOT.jar /usr/local/kitodo/plugins/opac/
```

### Anmeldung

Die Webseite sollte jetzt unter localhost (Variante 1 VirtualBox) oder der IP-Adresse (Variante 2 Cloud-Hoster) erreichbar sein. Beispiele:

<http://localhost:8080/kitodo/> bzw. <http://46.101.132.29:8080/kitodo/>

- user: testAdmin
- pass: test

### Beispieldaten in Elasticsearch indexieren

Menü System aufrufen. Beispiel Direktlink: <http://46.101.132.29:8080/kitodo/pages/system.jsf>

- ElasticSearch Index löschen
- ElasticSearch Mapping erzeugen
- Gesamter Index / Indexierung starten


## Fehlerbehebung

### Nach Neustart Kitodo Weboberfläche nicht erreichbar

Sporadisch tritt nach einem Neustart ein Fehler beim Deployment der Kitodo-Applikation (kitodo.war) auf, so dass die Weboberfläche von Kitodo nicht sofort erreichbar ist. Dann erscheint in der Logdatei `/var/lib/tomcat8/logs/catalina.out` folgende Fehlermeldung:

> Caused by: java.lang.IllegalStateException: Unable to complete the scan for annotations for web application [/kitodo] due to a StackOverflowError.

Ein Löschen der Arbeitsverzeichnisse und des Cache hilft in diesem Fall. Geben Sie dazu folgende Befehle ein:

```
sudo service tomcat8 stop
```

```
sudo rm -rf /var/cache/tomcat8/*
sudo rm -rf /var/lib/tomcat8/work/*
sudo rm -rf /var/lib/tomcat8/webapps/kitodo
sudo service tomcat8 start
```

Den Status können Sie in der Logdatei verfolgen:

```
sudo tail -f /var/lib/tomcat8/logs/catalina.out
```



------

<p align="center">Vorige Seite: <a href="README.md">Startseite</a> | Nächste Seite: <a href="02_projekt-anlegen.md">2. Projekt anlegen</a></p>