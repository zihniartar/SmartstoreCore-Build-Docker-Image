
## Smartstore Docker Image erstellen, übertragen und ausführen

### Erstellen eines Docker Images aus dem Quellcode

- Aus dem Ordner ```\Smartstore\docker``` die Datei ```build.cmd``` ausführen. Diese Datei erstellt mit Hilfe der Datei ```\Smartstore\Dockerfile``` das Smartstore-Projekt, baut ein Docker Image und installiert auch gleichzeitig wkhtmltopdf. Das Image hat den Namen ```smartstore```

###  Docker Image auf einen Server übertragen

- Das Docker Image kann z.B. in ein tar-Archiv gespeichert werden:
     ```bash
	docker save -o d:\smartstore.tar smartstore
   ```
- Das Image ist jetzt in der Datei ```d:\smartstore.tar``` gespeichert und kann beliebig übertragen werden. 
> **Hinweis**: Die Datei ```\Smartstore\docker-compose-yml``` muss mit übertragen werden und im gleichen Zielordner liegen.

###  Docker Image auf einem Server ausführen

**Ausgangszustand:** Die ```smartstore.tar```-Datei und die ```docker-compose.yml```-Datei liegen in demselben Ordner 
> Es ist nicht unbedingt notwendig, dass beide Dateien in demselben Ordner liegen, vereinfacht die Sache aber.

**Voraussetzungen:** ```docker``` und ```docker-compose``` müssen installiert sein.

 **Docker Image laden**:
- Das Docker-Image aus dem tar-Archiv in Docker laden:
   ```bash
	docker load -i ./smartstore.tar 
   ```


**Docker Container erstellen und starten**:

- Einen Docker Container erstellen:
     ```bash
	docker compose up
   ```
Hier wird zusätzlich noch ein mysql Image gestartet, der in der docker-compose.yml deklariert ist.

--------------------prüfen:
- Das Container starten
     ```bash
	docker run --name smartstore smartstore
   ```

> **Hinweis** : In der Datei ```docker-compose.yml``` ist ein Volume mit dem Host-Pfad ```D:/mount/smtenants``` angegeben. Auf einem Linux-Host sollte der Pfad angepasst werden.
