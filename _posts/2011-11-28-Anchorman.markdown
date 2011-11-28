---
layout: post
title: Anchorman
---
Wer den [Datenschorle Podcast](http://datenschorle.de) verfolgt wird vermutlich die langen Linklisten, die als Shownotes zu jeder Folge erscheinen, kennen und im Idealfall sogar mögen. Diese Listen werden von mir nach jeder Aufnahme und vor der Veröffentlichung erstellt. Der Aufwand hierfür ist nicht gerade gering, daher war der Wunsch nach einem hilfreichen Tool für die Aufgabe groß.

Die ersten Shownotes habe ich noch mit vim erstellt. Dabei habe ich im Browser die entsprechenden Links zusammengesucht und als Liste kombiniert mit einem hübschen Titel in vim zusammengetragen. Ein simples Macro hat danach die Liste umgewandelt in eine Linkliste mit HTML anchor-Tags, mit denen ich den Wordpress Eintrag füttern konnte.

Das ging ganz gut, aber das Wechseln zwischen Editor und Browser konnte bisweilen zu einer hektischen Angelegenheit werden, da ich möglichst selten den Podcast während des Erstellens der Notes pausieren wollte.

Etwa bei Folge 6 stieg ich dann auf Sublime Text 2 um. Der Workflow war dort allerdings noch der selbe - Sublime unterstützte ab diesem Zeitpunkt vim Macros.

Die Idee
--------
Da die Arbeit im Browser zu 95% darin bestand, den Link zum Thema zu ergooglen, war die Idee: Warum nicht die Suchmaschine in den Texteditor integrieren? Geboren war die Idee zu Anchorman. Mit Hilfe der Plugin API von Sublime Text 2 war schnell der Grundstein für die gewünschte Funktionalität gelegt.

Die Idee bestand darin, den Suchquery in Sublime zu markieren und auf Knopfdruck eine Liste mit möglichen Seiten zu bekommen. Wenn man eine auswählt, wird ein Link daraus gebastelt.

Die passende Suchmaschine
-------------------------
Initial war der Plan, google als Suchbackend zu verwenden. Leider stellte sich heraus, dass google dem geneigten Entwickler absurde Limits für API-Zugriffe in den Weg legt. Also musste eine Alternative her.

Plan 1: Den HTML Response von google parsen und die Titel und Links extrahieren
Diesen Plan verwarf ich sehr schnell wieder aus mehreren Gründen:
* Google checkt bei Requests den User-Agent und wirft ein "Forbidden" zurück, sollte es keinen Browser vermuten. Man könnte zwar den User-Agent faken (dazu später mehr), aber das wollte ich dann nicht als priorisierte Lösung durchgehen lassen.
* Sollte Google sein Markup ändern, muss der Code nachgepflegt werden
* Es ist wesentlich langsamer und fehleranfälliger als der Zugriff auf eine definierte API

Plan 2: [duckduckgo](http://duckduckgo.com/)
Diese Suchmaschine ist frei, hat eine kostenlose API und bietet im Webinterface annehmbare Ergebnisse. Selbiges ist leider nicht vom API Zugriff zu sagen. Die Ergebnisse dort waren schlichtweg unbrauchbar. Schade

Plan 3: Bing
Why not Zoidberg .. äh .. Microsoft. Es stellte sich heraus, dass Bing zwar eine grauenvoll dokumentierte API hat, alle anderen Faktoren aber wirklich brauchbar erschienen. Unlimitierter Zugriff, saubere JSON-Respone, flexibel und schnell.

Und somit hat tatsächlich Microsoft den Zuschlag erhalten und Bing ist nun das Rückrat von Anchorman.

Die Funktionalität
------------------
Anchorman hat momentan drei Funktionalitäten:

* Get Link - Text markieren und auf mit dem ersten gefundenen Link bespaßen (quasi ein "I feel lucky")
* Get Link (multiple choice) - Dropdown mit Suchergebnissen, aus denen sich der User eins auswählen kann
* Make Link from URL - Sollte man bereits eine URL haben, kann man diese hiermit in einen Link umwandeln. Anchorman versucht dabei, den Titel der Seite herauszufinden und setzt diesen als Linktitel

Außerdem beinhaltet das Plugin noch ein Snippet zum manuellen Linkerstellen.

![Anchorman in Aktion](/img/anchorman.png)

Tests
-----
Kürzlich habe ich angefangen, das Fundament für Unit Tests zu legen. Hierfür muss man große Teile der Sublime API mocken, da im Testfall außerhalb des Editors (oder sogar innerhalb mit dem Buildsystem) das sublime Modul nicht zur Verfügung steht. Das Mock-Setup habe ich hierbei ausgelagert, sodass es sich eventuell mal in ein Modul verwandelt, das man allgemein für Tests von Sublime Plugins verwenden kann.

Der User-Agent
--------------
Ich erwähnte bei der Suche nach der passenden Suchmaschine, dass ich keinen User-Agent faken wollte. Nun könnte man im Code über folgende Zeichenfolge stolpern und denken "aha! hater er DOCH!":

{% highlight python %}
user_agent = "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/535.2 (KHTML, like Gecko) Chrome/15.0.874.106 Safari/535.2"
headers = {'User-Agent': user_agent}
request = Request(url, None, headers)
{% endhighlight %}

Das mache ich im Kontext der dritten beschriebenen Funktionalität, da ich das Herausfinden des Titels gerne bestmöglich absichern wollte und sicherlich nicht nur Google da einen Riegel vor Requests schiebt, die nicht von einem Browser kommen.
Den User-Agent habe ich aus dem aktuellen Chrome unter Linux gefischt.

Download
--------
Für das WANT-Gefühl darf ich auf die [Projektseite von Anchorman](http://bestform.github.com/anchorman/) oder direkt auf das [github Repository](https://github.com/bestform/anchorman) verweisen.
Das Plugin ist weiterhin in einem Zustand aktiver Weiterentwicklung - daher lohnt es sich wohl am ehesten, das Repository direkt in den Packages-Folder von Sublime Text 2 zu clonen und von Zeit zu Zeit ein git pull draufzuschmeißen.

Die Lizenz
----------
[Beerware](http://de.wikipedia.org/wiki/Beerware) - 'nough said.
OK, eigentlich ist darüber noch nicht alles gesagt, aber das ist ein anderes Thema.


