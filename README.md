![Titelblatt_M300](Images/M300_Titelblatt.png)

## Inhaltsverzechnis
1. [Einleitung](#Einleitung)
2. [Grafische Übersicht mit Visio](#Visio)
3. [Ablauf](#Ablauf)
4. [Code im Detail](#Code)
5. [Testen](#testen)
6. [Quellenverzechnis](#Quellen)

## Einleitung <a name="Einleitung"></a>
Am 05.02.2021 durfte die ST18d mit dem neuen Modul "Plattformübergreifende Dienste im Netzwerk integrieren" beginnen. Zu Beginn gab es eine intensive Einführung und dazu haben wir die Toolumgebung aufgesetzt. Dies war die Voraussetzung für die LB2. 

Da wir nun die nötigen Informationen zur LB2 erhalten haben, stand uns grundsätzlich nichts mehr im Wege mit dem Projekt zu starten.

Ich habe mich dafür entschieden, einen Webserver mit Ubuntu zu ertsellen. Das Projekt war nicht allzu kompliziert, jedoch erfüllt es seinen Zweck. Eine VM (Virtualbox) wird nach dem "vagrant up" Befehl gestartet. Danach wird ein Skript erstellt, welches die Systemprozesse anzeigt. Dazu kommt dass die Daten mit Hilfe eines Cronjob immer aktuell bleiben.

## Grafische Übersicht mit Visio <a name="Visio"></a>
![Grafische Übersicht](https://github.com/sergio8585/M300_lb/blob/9f62754186925a6a41e3c6084ae79c1137e1e9d7/Images/LB2_M300_Visio.PNG)

## Ablauf <a name="Ablauf"></a>

- Gitbash öffnen und ins Verzeichnis (/c/repository/M300_lb) gehen. Dort gibt man dann nur noch den Befehl "vagrant up" aus.

- Danach öffnet man z.B. Chrome und gibt in der Suchleiste http://localhost:8080/prozesse ein. 

- Mit "vagrant destroy" wird die Maschine gelöscht.

## Code im Detail <a name="Code"></a>

**Vagrant.configure(2) do |config|**

Konfiguration der Vagrantbox wird gestartet. Die 2 steht für die neuste Version von Vagrant.

**config.vm.box = "ubuntu/xenial64"**

Die VM hat das Betriebssystem Ubuntu/Xenial 64-Bit.

**config.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true**

Dieser Befehl ist für die Portweiterleitung zuständig. Port 80 = VM und Port 8080 = Hostsystem. **auto_correct: true** ist dafür zuständig, dass mögliche Kollisionen automatisch korrigiert werden.

**config.vm.synced_folder ".", "/var/www/html"**

Die Files aus /var/www/html sind auch auf dem Hossystem im Ordner mit dem Vagrantfile gespeichert.

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

**crontab -l | {  cat; echo "* * * * * /cronscript/run-cronjob.sh"; } | crontab -** 

Cronjob ist zuständig für das autmatische Ausführen des Scripts. Aufgrund der 5 Sterne, wird das Skript alle 5 Minuten ausgeführt.

## Testen <a name="testen"></a>

## Quellenverzeichnis <a name="Quellen"></a>

-Template für Vagrantfile

testest