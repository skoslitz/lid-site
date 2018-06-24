+++
id = "?"
autor = "Sebastian Koslitz"
date = "2015-06-15"
title = "LiD-Online Kompendium"
subtitle = "Leitfaden zur Erstellung der Markdown-Inhalte"
description = ""

+++

## Beiträge verfassen

Um eine _Exkursion_ oder einen _Themenbeitrag_ (ffg. auch einfach als _Inhalt_ oder _Beitrag_ zsgf.) der Website hinzuzufügen, stehen derzeit zwei Vorlagedateien zur Verfügung:

### Themenvorlage

Die Themenvorlage finden sie unter `/lid-site/content/themen/78_B_001-themenvorlage.md`.

### Exkursionsvorlage

Die Exkursionsvorlage finden sie unter `/lid-site/content/exkursionen/78_E_001-exkursionsvorlage.md`.

### Generelles

Jeder dieser Beitrag besteht aus _zwei_ Bereichen in _einer_ `.md`-Datei, dem sog. "Frontmatter" und dem "Markdown".

Der **Frontmatter**-Bereich dient zur Angabe von wichtigen Informationen über den _Inhalt_ und ist relevant für das _funktionieren_ der Website. Hierbei ist demnach auf genaueste Schreibweise zu achten. Im Frontmatter könnnen Ganzzahlen ohne `" "` angegeben werden, Wörter sind jedoch zwingend mit `" "`anzugeben. 

Der **Markdown**-Bereich enthält den Inhalt sowie optional diverse Zusatzmodule, sog. "Shortcodes" mit welchen es möglich ist _Bilder_, _Downloads_, _statistische Karten_, _Animationen_, _Videos_ und _Mappetizer_ in einen Beitrag gezielt einzubinden.

## Umgang mit Dateien

### Speicherort von Dateien

Sämtliche Medien und Dateianlagen werden im Ordner `lid-site/static`abgelegt. Für jede Medienart gibt es im `/static` Ordner entsprechende Unterordner. **Hinweis zum `img` Ordner**: Bilder werden nach Bandnummer und Beitrags-Id abgelegt. Es gilt folgendes Schema:
<pre>
  Schema:   /static/img/bandnr/beitrags_id/beitrags_id-`bildname.jpg`
  Beispiel: /static/img/78/78_B_103/78_B_103-abb1.jpg`
</pre>

Bei der Einbindung von _Abbildungen_ über (a) den Shortcode "bild" (siehe unten) oder (b) via Frontmatter erfolgt **nur** über den `bildnamen`-Teil (siehe Schema), d.h. Angabe des Dateinamens ohne die `beitrags_id` und ohne die `bandnr`. Um diese nicht immer und immer wieder angeben zu müssen führen wir eine `id` im Frontmatter eines jeden Beitrags.

Alle Dateien die in einem Beitrag mittels Download-Shortcode (siehe utnen) referenziert werden solle müssen (ebenso wie Abbildungen) in dem entsprechenden Beitragsordner unterhalb von `/static/img/` abgelegt werden. Zur Einbindung von Download-Dateien muss dem Dateinamen ebenfalls das `Band-Nr_Beitrags-Nr`-Schema vorangestellt sein (dieses enthalten).

Beispiel: 
78_B_001-meine-tabelle-zum-download.csv

Hinterlegen: Anstatt eine (Microsoft spezifische) `.xlxs` (oder ähnliches) Tabelle zum Download anzubieten bitte einfach kurz die Exportfunktion von MS EXEL nutzen und die Tabelle mit der Dateiendung `.csv` abspeichern. Optionen für den Export sind `Tabulator` getrennte Spalten, Kodierung `UTF-8`.


### Bildformate

Fotos und Grafiken die für die Darstellung auf der Website aufbereitet werden müssen aufbereitet werden und dabei die beiden folgenden, mit dem Web-Design abgestimmten Maße einhalten:

- _Vorschaubild_<br/>
  Breite: 280px<br/>
  Höhe: entsprechend bzw. angemessen (nicht unbedingt viel höher als 280px)
- _Titelbild + Bild im Text_<br/>
  Breite: 1000px<br/>
  Höhe: entsprechend bzw. angemessen (nicht unbedingt viel höher als 1000px)

Außerdem ist zu beachten das die Dateiendungen (JPG, PNG, SVG, GIF) stets klein geschrieben (.jpg, .gif, .png, .svg) werden müssen.

Alle Fotos und Grafiken erhalten die `Beitrags-Id` im Dateinamen: `78_B_107-bildname.jpg`. Zur Einbindung von Bild-Dateien finden sich einige Beispiele unter Shortcode > Bilder.

### Titelbild und Vorschaubild

_Exkursionen_ bekommen ihr Titelbild stets direkt von Mapbox.com auf Basis der "centroid"-Angabe im Markdown (o.a. Frontmatter).

In den Markdown-Vorlagen für _Regionen_ und _Beiträge_ ermöglichen uns die Angabe der folgenden Zeilen ein Titelbild sowie ein Vorschaubild für den Inhalt feszulegen.

Wichtig ist, damit die Bilder vom System korrekt für einen Beitrag geladen werden können, das im Frontmatter des Beitrags sets die korrekte <code>id</code> gesetzt ist.

<pre>
  id = "78_B_135"
  # Speicherort des Titelbildes: /static/img/78/78_B_135/78_B_135-titelbild.jpg 
  titelbild = "titelbild.jpg"
  titelbild_titel = "Titel des Bildes, ein Text für Blinde sowie Text unterm Mauszeiger"
  titelbild_quelle = "Bildunterschrift, üblicherweise name des Urhebers inkl. Lizenzhinweis"
</pre>

Vorschaubilder werden bei _Auflistung_ von mehreren Inhalten in einem Bereich oder in einer Rubrik herangezogen. Folgendermaßen wird ein Vorschaubild für einen Beitrag, eine Exkursion oder eine Region im Frontmatter hinterlegt.

<pre>
  vorschaubild = "preview.jpg"
  vorschaubild_titel = "Ansichtskarte, IfL: PKL-Mus.V.054"
</pre>

{{% kommentar text="Hinweis:" %}}
**Bitte die Originalbilder (deren Breite größer als 1000px ist) unberührt lassen und ebenfalls in dem Bilder-Ordner des Beitrags hinterlegen.**


---



## Frontmatter - Metadaten eines Beitrags

Die Frontmatter Markup Sprache ist [TOML](https://github.com/toml-lang/toml). Alle Frontmatter Inhalte müssen somit valides TOML sein. Im Frontmatter könnnen Ganzzahlen ohne `" "` angegeben werden, Wörter sind jedoch zwingend mit `" "`anzugeben und es ist auf genaueste Schreibweise zu achten.

Egal ob ein _Themenbeitrag_ oder eine _Exkursion_ erstellt wird, in jedem Fall benötigen wir die folgenden Angaben im Frontmatter: `ID, Title, Autor, Date`, sowie `rubriken` bzw. `exkursionstyp`.

### ID, Title

Themenbeiträge und Exkursionen benötigen in jedem Fall eine <code>id</code> Angabe im Frontmatter, diese wird benötigt damit die Bilddateien geladen werden können.

Eine ID setzt sich nach dem Schema `{{</* BandNr-[B|E]-BeitragsNr */>}}` zusammen, wobei `B` einen Themenbeitrag und `E` eine Exkursion identifiziert.

Beispiel:<br/>
<code>id = "78_B_135"</code>

Dazu benötigt jeder Beitrag einen Titel.

<code>title = "Name des Beitrags"</code><br/>

### Datumsangabe

Datumsangaben können in verschiedenen Formaten gemacht werden, aber in jedem Fall innerhalb von zwei Anführungszeichen:

Hier zwei Beispiele:<br/>
<code>date = "2015-02-28"</code><br/>
<code>date = "2015-03-17T14:55:18+01:00"</code><br/>

**Bitte beachten das die Datumsangabe mindestens das Jahr, den Monat und den Tag enthalten muss.**

### Autor_Innen

Der Name der Autor*Innen ist ebenfalls innerhalb von zwei Anführungszeichen und bei mehreren ggf. von einem Kommata getrennt, wie folgt im Frontmatter des Beitrags anzugeben:

<code>autor = "Cletus Spuckler, Harry Krüger"</code><br/>

### Taxonomie: Rubriken und Exkursionstypen

_Exkursionen_ sowie _Beiträge_ können aktuell folgendermaßen mit einem oder mehreren der folgenden Begriffe "verschlagwortet" werden. Neben der "Verwandte Artikel"-Sektion unterhalb eines Themenbeitrags lassen sich z.B.: auch die Filteroptionen in der Übersichtsseiten durch den gezielten Einsatz dieser Taxonomien steuern.

Die folgenden Begriffe sind fix:<br/>

<pre>
  rubriken = [ "Wirtschaft & Verkehr", "Natur & Landschaft", "Vergangenheit & Erinnerung", "Kultur & Soziales", "Siedlung & Bevölkerung"]
</pre>

_Exkursionen_ können aktuell zusätzlich noch mit den folgenden Begriffen ausgezeichnet werden:
<pre>
  exkursionstypen = [ "Fuß", "Fahrrad" ]
</pre>

_Exkursionen_ müssen dazu (neuerdings) die Angabe `fremdexkursion="ja/nein" gesetzt haben. Hier ein Beispiel:
<pre>
fremdexkursion = "nein"
</pre>

Sogenannte "Fremdexkursionen" haben dazu zwei besondere Frontmatter-Zeilen, hier mit fiktiven:
<pre>
exkursions_anbieter = "Stadt Leipzig, Amt X"
exkursions_url = "http://leipzig.de/exkursion/1  (WWW zieladresse der exkursion)
</pre>

{{% kommentar text="Hinweis:" %}}
**Bitte bei Verwendung dieser Begriffe stets genauestens auf eine exakte und über alle Inhalte gleichbleibende Schreibweise achten.**

### Literaturangaben

`Literaturangaben` zum jeweiligen Beitrag im Frontmatter angegeben werden.

Hier ein Beispiel:<br/>
...

### VG Wort Bildmarke

Um eine VG Wort Zählmarke einem Beitrag zuzuordnen, wird im Frontmatter der folgende Parameter gesetzt:

<code>vg_wort_code = "723a6487b2364e"</code><br/>
**Der Code ist der Tabelle "20150520_VGWORT_Zuordnung.xlsx" auf Laufwerk P zu entnehmen. Verwendet wird der öffentliche Code.**


### DOI

Jeder Beitrag erhält (eine URN? oder) einen Digital Object Identifier, kurz DOI bzw. URN. Die DOIs erhalten sie auf Nachfrage bei Frau Moser.

<code>doi = "doi:.."</code><br/>

### Exkursionen

Der Ausschnitt des Titelbildes einer Exkursion wird durch den Parameter `centroid` definiert. Die Zoomstufe der Karte ist bereits voreingestellt (Stufe 15). Falls eine andere Zoomstufe gewünscht ist, muss der Parameter `zoomstufe` gesetzt werden.

Der Exkursionsverlauf wird als Pfad in der Karte dargestellt.

Stationsinformationen (Koordinaten der Suchpunkte sowie die jeweilige Stationsnummer werden nach den allgemeinen Exkursionsangaben jeweils unter `[[exkursion]]` im Frontmatter angegeben.

Für eine Exkursion stellt sich der Frontmatter wie folgt zusammen:

**Syntax** Frontmatter
<pre>
  id = "78_E_501"
  title = "Exkursionstitel"
  date = "2015-03-12"
  centroid = [51.331295, 12.374468]
  # zoomstufe ist optional
  zoomstufe = 13
  exkursionstyp = [ "Fahrrad", "Fuß"]
  exkursionsstart = "Anfang" 
  exkursionsende = "Ende"
  exkursionsstationen = 16
  exkursionslaenge = 12
  vorschaubild = "vorschaubild.jpg"
  # oepnv_start = " "
  # oepnv_ende = " "
  [[exkursion]]
    nr = 1
    lat = 53.1233
    lon = 12.3454
  [[exkursion]]
    nr = 2
    lat = 53.2133
    lon = 12.4254
</pre>

Um Inhalte wie Text und Bild den einzelnen Stationen zuweisen zu können müssen Sie den Shortcode `stationstitel` im Content-Bereich (Markdown-Format) einsetzen.

### Kommentare

Jede Zeile eines Kommentares beginnt im _Frontmatter_ mit einer `#`.
<pre>  # Dies ist ein gültiger Kommentar</pre>

Mit dem Einsatz von Kommentaren im Frontmatter können für einzelne Beiträge auch einzelne Bereiche wie z.B.: "Quellen und weiterführende Literatur" ausgeblendet werden.

### Slideshow

Wenn der Beitrag eine Slideshow enthalten soll, so werden alle benötigten Informationen im Frontmatter angegeben

**Syntax** Frontmatter
<pre>
[[slideshow]]
  bild = "slideshow-abb1.jpg"
  titel = "Titel des ersten Bildes"
  untertitel = "Untertitel / Quellenhinweise zum ersten Bild"
[[slideshow]]
  bild = "slideshow-abb2.jpg"
  titel = "Titel des zweiten Bildes"
  untertitel = "Untertitel / Quellenhinweise zum zweiten Bild"
</pre>

### Mappetizer

Wenn der Beitrag einen Mappetizer beinhalten soll, ist die Angabe der `id` im Frontmatter nötig. Die `id` leitet sich aus dem Speicherort des Mappetizers ab `/static/mappetizer/id/`. Der Titel des Mappetizers wird mit dem Parameter `mappetizer_titel` angegeben.

**Syntax** Frontmatter
<pre>
  # Dieser Mappetizer liegt im Ordner /static/mappetizer/78_B_101/
  mappetizer = "78_B_101"
  mappetizer_titel = "Wohnungsleerstand in Leipzig"
</pre>

### Visualisierungen (D3, Flash)

Visualisierungen werden analog dem Schema für Mappetizer Anwendungen eingebunden. Je nach Art der Visualisierung (Flash oder JavaScript (D3.js) basiert) wird eine `id` (abgeleitet aus dem Speicherort) und ein `titel` vergeben. Optional ist die Angabe einer Höhe `height` für das Seitenlayout.

**Syntax** Frontmatter D3 (statistische Karten)
<pre>
  # Anwendung liegt im Ordner /static/D3/78_B_107
  karte_statistik = "78_B_107"
  karte_statistik_titel = "Wohnungsleerstand in Leipzig 2011"
  karte_statistik_height = "800"
</pre> 

**Syntax** Frontmatter Flash Animation
<pre>
  # Anwendung liegt im Ordner /static/flash/78_B_152
  flash_animation = "78_B_152"
  flash_animation_titel = "Ausbreitung der Türkentaube"
  flash_animation_height = "800"
</pre> 


### Videos

Wenn der Beitrag ein oder mehrere Videos enthalten soll, so werden alle benötigten Informationen im Frontmatter angegeben.

**Syntax** Frontmatter
<pre>
[[video]]
  id = "Vimeo_id_des_Videos"
  titel = "Blühende Landschaften"
  untertitel = "Eine Reise durch ..."
  beschreibung = "Hier kommt die Beschreibung rein"
  quelle = "Wer hat's erfunden?"
  laenge = "55 Minuten"
  [[video.sprungmarke]]
    seek = 200
    label = "Sprungmarke 1"
  [[video.sprungmarke]]
    seek = 300
    label = "Sprungmarke 2"
  [[video.sprungmarke]]
    seek = 500
    label = "Titel von und zu Sprungmarke"
</pre>

Die Eintragung von beliebig vielen `[[video.sprungmarke]]`-Zeilen ist dabei optional, macht sich aber gut da diese unseren Nutzer_Innen eine Art (inhaltliche) Kapitel-Steurung ermöglicht.


### Sonstiges

Zu den <i>optionalen Angaben</i> für jeden Beitrag im Frontmatter gehören:

<code>subtitle = "TODO"</code><br/>
<code>description = "TODO"</code><br/>
<code>draft = true</code>(Falls "true", wird der Inhalt nicht "mit-veröffentlicht" (bei der nächsten Aktualisierung der Seiten-Inhalte))<br/>
<code>...</code><br/>


---




## Markdown - Inhalt eines Beitrags

Im folgenden eine kurze Einführung in die sog. Markdown Syntax in welche alle Inhalte der Website verfasst werden.

### Überschriften
Es stehen fünf Überschriftsebenen zur Verfügung. H1 (Header 1) und H2 sind jedoch bereits durch das Seitenlayout belegt.
Somit stehen im Contentbereich der Beiträge nur die Überschriftsgrößen H3 - H5 zur Verfügung

**Syntax:** Ein Rautenzeichen `#` leitet eine Überschrift ein. H3 erhält drei `###` usw.

### Hervorhebungen
Es sind *kursive* und **fette** Hervorhebungen möglich.

**Syntax:** kursiv `*text*`

**Syntax:** fett `**text**`

### Listen
Listen dienen der besseren Ansicht von Aufzählungen. Es kann dabei zwischen unsortierten und sortierten Aufzählungen unterschieden werden.

**Syntax:** unsortierte Liste
<pre>+ Punkt 1
+ Punkt 2</pre>

**Syntax:** unsortierte Liste
<pre>
 1. Punkt 1
 2. Punkt 2
 3. Punkt 3
 	+ Unterpunkt zur Punkt 3</pre>

### Links (Querverweis)
**Syntax:** Link
<pre>`[Bezeichnung des Links](Adresse des Links)`</pre>

### Sonderzeichen

Sonderzeichen (wie z.B: łaziti) werden dank UTF-8 Kodierung korrekt in Markdown dargestellt. Beinhaltet der Zeichensatz jedoch ein Markdownsteuerzeichen (z.B: ein \*), so muß diesem zwingend ein Backslash \ vorangestellt werden.

**Syntax:** Sonderzeichen mit Markdownsteuerzeichen:

`\*Sukołazy` wird zu *Sukołazy

**Sonderzeichen:** Gedankenstrich

Ein Gedankenstrich wird in Markdown in UTF-8 Kodierung dargestellt:

**Syntax:** Gedankenstrich:

Windows: `alt + 0150`

Mac OS: `alt + -`

### Tabellen

Tabellen sind mit Hilfe des folgenden [Links](http://www.tablesgenerator.com/markdown_tables) zu erstellen und über die Kopie der Zwischenablage dann in den Contentbereich der Markdown einzufügen.

In der Zeile oberhalb einer Tabelle können wir mittels des Shortcdoes `tabellentitel` nun Tabellen betiteln:

<pre>{{%/* tabellentitel text="Wichtige Kläranlagen im Entsorgungsgebiet KWL 2012c" */%}}</pre>

Um dieses Hilfswerkzeug verwenden zu können (eine Tabelle hochzuladen) müssen sie ihren Tabelle ggf. erst aus MS Word zu MS Exel überführen um diese dann von dort aus als einfache .CSV Text-Datei exportieren zu können. Hintergund: Das Hilfswerkzeug nimmt nur .CSV-Dateien entgegen.

Bitte beachten sie auch die folgende Entscheidung bzgl. des Umgangs mit Tabellen:<br/>
Mehrseitige, komplexe Tabellen sollten nicht unbedingt als Teil des Markdown Contents umgesetzt werden sondern für Besucher*Innen von LiD-Online nützlich gemacht werden:

Nützlich werden größere, komplexere Tabellen für Besucher_Innen unserer Website:

- sofern die Tabelle in Exel vorliegt bzw. einfach aus Word nach Exel überführt werden kann als .CSV-Datei (Exportfunktion, TAB separiert, UTF-8 kodiert)
- nur im Notfall ist die Tabelle in ein IfL-Basislayout zu bringen um dann als .PDF-Export anzubieten da dies jegl. eine einfach weiterführende Nutzung, wie z.B.: Filterung der Daten verhindert

Für die Einbindung größerer Tabellendaten in einen Beitrag nutz bitte den Download-Shortcode (siehe unten).

---



## Shortcodes

Diese dienen der Erweiterung der Markdown-Syntax und erlauben es Autor*Innen die folgenden "Zusatzmodule" in den Inhalts-Bereich eines Beitrag zu laden.

### Bilder

Über das Zusatzmodule "bild" können Bild-Dateien und Grafiken eingebunden werden.

<pre>{{%/* bild pfad="abb1-01.jpg" titel="Ansicht 1" quellenangaben="Foto: Müller Lüdenscheidt, 1967" */%}}</pre>

Beispiel für zwei Abbildung in einer Zeile mit max. 300px, Text umfließend und vergößerbar (klickbar mit Pop-up):
<pre>
{{%/* bild pfad="abbildung1.jpg" flow="preview" clickable="true" titel="Hauptstraße von Probstheida, Ansichtskarte um 1927" quellenangaben="IfL: PKL-Prob022"  */%}}
{{%/* bild pfad="abbildung2.jpg" flow="preview" clickable="true" titel="Luftbild von Probstheida, um 1927" quellenangaben="IfL: Eu68Wa-0071"  */%}}
</pre>

Falls ein Bild als Teil der Slideshows des Beitrags auftauchen soll, aber nicht im Text, nutzt bitte die Attribute von "clickable" und "hidden" in Kombination. Beispiel:

<pre>
{{%/* bild pfad="abbildung1.jpg" flow="preview" clickable="true" hidden="true" titel="Hauptstraße von Probstheida, Ansichtskarte um 1927" quellenangaben="IfL: PKL-Prob022"  */%}}
</pre>

Beispiel für eine Abbildung mit max. 1000px, Text umfließend und nicht klickbar:
<pre>
{{%/* bild pfad="abbildung1.jpg" flow="around" titel="Hauptstraße von Probstheida, Ansichtskarte um 1927" quellenangaben="IfL: PKL-Prob022"  */%}}
</pre>

### Absatz erzwingen

Mithilfe des `clear`-Shortcodes können seit kurzem neue Absätze erzwungen und somit auch das "umfließen" (der Bilder durch nachfolgende Inhalte) unterbrochen werden.

<pre>
{{%/* clear */%}}
</pre>

Der Clear-Code findet aktuell bereits Anwendung in **E_534** (Station 5 und 11), sowie in einem Absatz in Beitrag **B_109**.

### Stationen von Exkursionen

Um verschiedene Inhaltsbereiche im Markdown als Stationen von Exkursionen auszuzeichnen gibt es das Zusatzmodul "stationstitel".

Die Überschrift der jeweiligen Stationsbeschreibung erfolgt über den Einsatz dieses Shortcodes im Contentbereich (Markdown, nicht Frontmatter). Neben dem Titel der Station muss zwingend die Stationsnummer übergeben werden:

_Syntax_ Shortcode
<pre>
{{%/* stationstitel titel="Die Lauer" nummer="1" */%}}
</pre>
	
### Kommentar

<pre>{{%/* kommentar text="Hinweis: muss überarbeitet werden" */%}}</pre>

### Querverlinkung

Für die Linkadresse ist folgender Shortcode gültig:
<pre>{{</* relref "themen/78_B_159-urbane-natur.md" */>}}</pre>

Somit setzt sich ein [Querverweis]({{< relref "themen/78_B_159-urbane-natur.md" >}}) im markdown Bereich wie folgt zusammen:
<pre>\[Linktitel\]({{</* relref "themen/78_B_159-urbane-natur.md" */>}})</pre>


### Download

Ein Shortcode um `.pdf`, `.csv` oder sonstige Dokumente in einer Download-Sektion im Inhaltsbereich eines Beitrag einzubinden. Bitte beachten Sie das dieser Shortcode eine eigenständige/besonderer Erweiterung der Markdown-Syntax ist und nicht mit der normalen Hyperlink-Syntax zu kombinieren ist.

<pre>
  {{%/* download pfad="mitte.csv" lizenz="CC-BY" titel="Häufigste Vornamen - Bezirk Berlin Mitte" stand="31.12 2014" format="csv" size="0.04" */%}}
</pre>

Die Dateien die zum Download angeboten werden sollen müssen in demselben `static`-Ordner wie die Bilder zu dem jew. Beitrag hinterlegt werden und können dann einfach über ihren Dateinamen eingebunden/referenziert werden.

### Interaktive Zusatzmaterialien

Ein Shortcode um interaktive Diagramme und ähnliches innerhalb des markdown Inhaltsbereiches einzubinden.

<pre>
  {{%/* karte_statistik karte_statistik="78_B_139" karte_statistik_titel="Temperatur 1862-2012 im 30-jährigen Mittel" karte_statistik_height="400" karte_statistik_file="temp_vergleich" */%}}
</pre>

Die Parameter <code>"karte_statistik_height"</code> sowie <code>"karte_statistik_file"</code> sind optional und steuern die Höhe des Elementes sowie dessen Dateinamen als Einstiegspunkt.

### Mappetizer

Ein Shortcode um Mappetizeranwendungen innerhalb des markdown Inhaltsbereiches einzubinden.

<pre>
  {{%/* mappetizer mappetizer="78_B_139" mappetizer_titel="Einwohner" mappetizer_height="400" */%}}
</pre>
