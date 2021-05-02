![Titelblatt_M300_LB3](https://github.com/sergio8585/M300_lb/blob/e9d4f2d62ac85496e9f8bc512d98e3c51415527a/Images/M300_LB3_Titelblatt.png)

## Inhaltsverzechnis
1. [Einleitung](#Einleitung)
2. [Tutorial](#Tutorial)
3. [Code im Detail](#Code)
5. [Testing](#testen)
6. [Quellenverzechnis](#Quellen)

## Einleitung <a name="Einleitung"></a>

Da wir nun die LB2 erfolgreich durchgeführt haben, kam die LB3 an die Reihe. Das Thema DOcker war für mich noch etwas anspruchsvoller wie das Vorherige. Jedoch habe ich mir so viel Mühe gegeben, wie nur möglich.

Da ich etwas Mühe mit der Themenwahl hatte, hat mir Herr Berger das Thema vorgegeben und zwar MariaDB.

Die LB3 beinhaltet im Container 2 VMs, eine Maria Datenbank und das phpMyAdmin, welches für die Verwaltung zuständig ist.

## Tutorial <a name="Tutorial"></a>

- Gitbash öffnen und ins Verzeichnis (/c/repository/M300_lb/lb3) gehen. 

- Danach gibt man den Befehl "docker-compose up" ein.

- Danach öffnet man z.B. Chrome und gibt in der Suchleiste http://localhost:8080 ein. 

- Username: root
  Passwort: root

- Zum Schluss kann man den Befehl "docker-compose down" eingeben um den Container herunterzufahren

## Code im Detail <a name="Code"></a>

**version: "2"**

Mit Version 2 wird die Version des Files festgelegt.

**networks:**
      **v_net:**
          **ipam:**
              **driver: default**
              **config:**
                  **- subnet: 192.168.60.0/24**

Nun haben wir das Subnetz **192.168.60.0/24** definiert.

**services:**

Nun werden die services (2) im Container dokumentiert und beschrieben.

**db:**
         **image: mariadb**
         **environment:**
              **- MYSQL_ROOT_PASSWORD=root**
              **- MYSQL_DATABASE=defaultdb**
         **volumes:**
              **- ./database:/var/lib/mysql**
         **networks:**
          **v_net:**
              **ipv4_address: 192.168.60.100**

Nun definieren wir den DB-Service. Das Passwort und der Name der Datenbank werden hier angegeben.

**config.vm.provider "virtualbox" do |vb|**

Hypervisor wird definiert (Virtualbox). Konfiguration in Virtualbox wird gestaret.

**vb.memory = "512"**

RAM wird festgelegt (512MB).

**config.vm.provision "shell", inline: <<-SHELL**

Konfiguration wird in der Linuxkonsole gestartet.

**sudo apt-get update**
**sudo apt-get -y install apache2**

Übliche Befehle in Linux. Appkatalog wird zuerst aktualisiert und danach Apache installiert.

**cd /**
**mkdir bashscripts**
**cd bashscripts**

Mit dem ersten Befehl wird ins Root-Verzeichnis geweschselt. Danach den Ordner "bashscripts." Mit dem dritten Befehl wechselt man ins Verzechnis.

**touch dateproc.sh**

Ein neues Shell-Script wird ertsellt.

**echo "env TZ=CET-1 date > /var/www/html/prozesse" > dateproc.sh**

Die aktuelle Zeit wird in Zentraleuropäischerzeit in das File "Prozesse" geschrieben. Vorheriger Inhalt wird überschrieben.

**echo "ps aux >> /var/www/html/prozesse" >> dateproc.sh**

Die Systemprozesse werden in "Prozesse" übernommen.

**chmod +x /bashscripts/dateproc.sh**

Rechte auf das Script. (Executable-Rechte)

**./dateproc.sh**

Script wird ausgeführt und Ergebnisse direkt herausgegeben.

**crontab -l | { cat; echo "*/ * * * * /bashscripts/dateproc.sh"; } | crontab -**

Cronjob ist zuständig für das automatische Ausführen des Scripts. Aufgrund der 5 Sterne, wird das Skript alle 5 Minuten ausgeführt.

## Testing <a name="testen"></a>

Zuerst öffnen Sie Gitbash und gehen ins gewünschte Verzechnis (/c/repository/M300_lb). Danach Befehl "Vagrant Up" eingeben:

![Testing_1](https://github.com/sergio8585/M300_lb/blob/f92e956773e8938aa67d30476bd7f8e704c67b93/Images/Testing_1.PNG)

Danach geben Sie den Link im Browser ein und öffnen die Seite. 

![Testing_2](https://github.com/sergio8585/M300_lb/blob/faa9e85a81b288701bb66d5c5799b9ebf0743845/Images/Testing_2.PNG)

Nach erneutem Laden sieht man, dass sich die Zeit geändert hat.

![Testing_2](https://github.com/sergio8585/M300_lb/blob/be67b1eddfdee61e5f70379bdf29ed79cb5d669f/Images/Testing_3.PNG)

## Quellenverzeichnis <a name="Quellen"></a>

- M300 Web-Template link: (https://github.com/mc-b/M300/tree/master/vagrant/web)

- Markdown Basic Syntax Link: (https://www.markdownguide.org/basic-syntax/)

- Cronjob Link: (https://stackoverflow.com/questions/878600/how-to-create-a-cron-job-using-bash-automatically-without-the-interactive-editor)

- Zeitzonen Command Link: (https://unix.stackexchange.com/questions/48101/how-can-i-have-date-output-the-time-from-a-different-timezone)