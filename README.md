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

## Testen <a name="testen"></a>

## Quellenverzeichnis <a name="Quellen"></a>

-Template für Vagrantfile