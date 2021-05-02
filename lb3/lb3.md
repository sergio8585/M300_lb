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

-     **version: "2"**

Mit Version 2 wird die Version des Files festgelegt.

-     **networks:**
-     **v_net:**
-     **ipam:**
-     **driver: default**
-     **config:**
-     **- subnet: 192.168.60.0/24**

Nun haben wir das Subnetz **192.168.60.0/24** definiert.

-     **services:**

Nun werden die services (2) im Container dokumentiert und beschrieben.

-     **db:**
-     **image: mariadb**
-     **environment:**
-     **- MYSQL_ROOT_PASSWORD=root**
-     **- MYSQL_DATABASE=LB*_DB**
-     **volumes:**
-     **- ./database:/var/lib/mysql**
-     **networks:**
-     **v_net:**
-     **ipv4_address: 192.168.60.100**

Nun definieren wir den DB-Service. Das Passwort und der Name der Datenbank werden hier angegeben. In volumes werden gesyncte Ordner definiert. Zum Schluss werden wir die IP-Adresse definieren.

>  phpmyadmin:
>     image: phpmyadmin/phpmyadmin
>     container_name: phpmyadmin
>     environment:
>         - PMA_HOST=db
>     restart: always
>     ports:
>         - 8080:80
>     volumes:
>         - /sessions
>     links:
>         - db
>     networks:
>       v_net:
>           ipv4_address: 192.168.60.101-

Nun definieren wir den phpMyAdmin service. Die Variable PMA_HOST ist für das Festlegen des db-Service zuständig. Mit Ports: wird die Portweiterleitung von 80 auf 8080 definiert. Zum Schluss haben wir noch im v_net die IP-Adresse (192.168.60.101) angegeben. 

## Testing <a name="testen"></a>

| Nummer | Eingabe                                      | Resultat                          |
| ------ |:--------------------------------------------:| ---------------------------------:|
| 1      | Befehl: docker-compose up                    | Container startet                 |
| 2      | Im Browser http:/localhost:8080 eingeben     | Loginfenster erscheint            |
| 3      | Passwort (root) und Username (root) eingeben | Login erfolgreich                 |
| 4      | Mit docker-compose down den Container löschen| Docker werden tatsächlich gelöscht|

## Quellenverzeichnis <a name="Quellen"></a>

- Docker Compose: (https://docs.docker.com/compose/gettingstarted/)

- Markdown basic Syntax: (https://www.markdownguide.org/basic-syntax/)