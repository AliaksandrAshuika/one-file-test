Erster Header | Zweiter Header
--- | ---
Inhaltszelle | Inhaltszelle
Inhaltszelle | Inhaltszelle

First Header | Zweiter Header
--- | ---
Inhaltszelle | Inhaltszelle
Inhaltszelle | Inhaltszelle

![Zitadelle](https://vignette.wikia.nocookie.net/masseffect/images/d/d7/MassEffect2Citadel.jpg/revision/latest?cb=20100721191415)

Linksbündig | Mittig ausgerichtet | Rechtsbündig
:-- | :-: | --:
Spalte 3 ist | ein wortreicher Text | **$1600**
Spalte 2 ist | zentriert | $12
Zebrastreifen | sind ordentlich | ~~$1~~

Dillinger ist ein Cloud-fähiger, mobilfähiger Offline-Speicher mit AngularJS-basiertem HTML5-Markdown-Editor.

- Geben Sie links einen Markdown ein
- Siehe HTML rechts
- Magie

# wahr

- Importieren Sie eine HTML-Datei und sehen Sie zu, wie sie auf magische Weise in Markdown konvertiert wird
- Bilder ziehen und ablegen (erfordert eine Verknüpfung Ihres Dropbox-Kontos)

Du kannst auch:

- Importieren und speichern Sie Dateien von GitHub, Dropbox, Google Drive und One Drive
- Ziehen Sie Markdown- und HTML-Dateien per Drag &amp; Drop in Dillinger
- Exportieren Sie Dokumente als Markdown, HTML und PDF

Markdown ist eine einfache Auszeichnungssprache, die auf den Formatierungskonventionen basiert, die Menschen in E-Mails natürlich verwenden. Wie [John Gruber] auf der [Markdown-Site][df1] schreibt

> Das übergeordnete Designziel für die Formatierungssyntax von Markdown besteht darin, sie so gut wie möglich lesbar zu machen. Die Idee ist, dass ein mit Markdown formatiertes Dokument unverändert als Nur-Text veröffentlicht werden kann, ohne dass es aussieht, als wäre es mit Tags oder Formatierungsanweisungen versehen worden.

Dieser Text, den Sie hier sehen, ist *tatsächlich* in Markdown geschrieben! Um ein Gefühl für die Syntax von Markdown zu bekommen, geben Sie etwas Text in das linke Fenster ein und sehen sich die Ergebnisse rechts an.

### falsch

Dillinger verwendet eine Reihe von Open-Source-Projekten, um richtig zu funktionieren:

- [AngularJS] - HTML für Web-Apps verbessert!
- [Ace Editor] - fantastischer webbasierter Texteditor
- [markdown-it] - Markdown-Parser richtig gemacht. Schnell und einfach zu erweitern.
- [Twitter Bootstrap] - großartiges UI-Boilerplate für moderne Web-Apps
- [node.js] - Evented I/O für das Backend
- [Express] – schnelles node.js-Netzwerk-App-Framework [@tjholowaychuk]
- [Gulp] - das Streaming-Build-System
- [Breakdance](https://breakdance.github.io/breakdance/) - HTML-zu-Markdown-Konverter
- [jQuery] - duh

Und natürlich ist Dillinger selbst Open Source mit einem [öffentlichen Repository][dill] auf GitHub.

### Installation

![Ilos](https://lh3.googleusercontent.com/proxy/DDV8a7sLIWurhJtW8Ego9bq-JlwpfFFoR0tkLJQKKYXEXoWHB6ZUP5jGKD2VcYt3z1QVsgcn6L3GoU1ns8m9fvi3U51GzddA70ZUMHgzHvjl4-i7YOJY9cShBPrfjUhMQhxaJ97WFBp612XmjMXVGypfGkiBarN4PWxhiHkiYYNW7HGbtTpOcyt9GQ4Q23C2noxLTWFXZMcQZhRpQA_qzu2n6_H6CPViBnhSHpEl4JZAPaGCSJqgZg)

Dillinger benötigt [zur Ausführung Node.js](https://nodejs.org/) v4+.

Installieren Sie die Abhängigkeiten und devDependencies und starten Sie den Server.

```sh
$ cd dillinger
$ npm install -d
$ node app
```

Für Produktionsumgebungen...

```sh
$ npm install --production
$ NODE_ENV=production node app
```

### Plugins

Dillinger wird derzeit um folgende Plugins erweitert. Anweisungen zur Verwendung in Ihrer eigenen Anwendung sind unten verlinkt.

Plugin | Liesmich
--- | ---
Dropbox | [plugins/dropbox/README.md][PlDb]
GitHub | [plugins/github/README.md][PlGh]
Google Drive | [plugins/googledrive/README.md][PlGd]
Eine Fahrt | [plugins/onedrive/README.md][PlOd]
Mittel | [plugins/medium/README.md][PlMe]
Google Analytics | [plugins/googleanalytics/README.md][PlGa]

### Entwicklung

Möchten Sie beitragen? Groß!

Dillinger verwendet Gulp + Webpack für die schnelle Entwicklung. Nehmen Sie eine Änderung in Ihrer Datei vor und sehen Sie sofort Ihre Updates!

Öffnen Sie Ihr bevorzugtes Terminal und führen Sie diese Befehle aus.

Erste Registerkarte:

```sh
$ node app
```

Zweite Registerkarte:

```sh
$ gulp watch
```

(optional) Drittens:

```sh
$ karma test
```

#### Gebäude für Quelle

Zur Produktionsfreigabe:

```sh
$ gulp build --prod
```

Generieren vorgefertigter Zip-Archive für die Verteilung:

```sh
$ gulp build dist --prod
```

### Docker

Dillinger lässt sich sehr einfach in einem Docker-Container installieren und bereitstellen.

Standardmäßig macht Docker Port 8080 verfügbar, also ändern Sie dies bei Bedarf in der Dockerfile. Wenn Sie fertig sind, verwenden Sie einfach das Dockerfile, um das Image zu erstellen.

```sh
cd dillinger
docker build -t joemccann/dillinger:${package.json.version} .
```

Dadurch wird das Dillinger-Image erstellt und die erforderlichen Abhängigkeiten abgerufen. Stellen Sie sicher, dass Sie `${package.json.version}` mit der aktuellen Version von Dillinger austauschen.

Führen Sie anschließend das Docker-Image aus und ordnen Sie den Port dem gewünschten Port auf Ihrem Host zu. In diesem Beispiel ordnen wir Port 8000 des Hosts einfach dem Port 8080 des Dockers zu (oder dem Port, der in der Dockerdatei offengelegt wurde):

```sh
docker run -d -p 8000:8080 --restart="always" <youruser>/dillinger:${package.json.version}
```

Überprüfen Sie die Bereitstellung, indem Sie in Ihrem bevorzugten Browser zu Ihrer Serveradresse navigieren.

```sh
127.0.0.1:8000
```

#### Kubernetes + Google Cloud

Siehe [KUBERNETES.md](https://github.com/joemccann/dillinger/blob/master/KUBERNETES.md)

### Todos
