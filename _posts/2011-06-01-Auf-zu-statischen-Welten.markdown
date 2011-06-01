---
layout: post
title: Auf zu statischen Welten
---

Web 0.1 ist das neue Web2.0. Das weiß auch schon der [Schockwellenreiter](http://www.schockwellenreiter.de/), der gerne über seine Ausflüge in die Welt der statisch generierten Website berichtet.

Der Vorteil derartiger Seiten liegt auf der Hand: Performance. Ein Webserver, wie beispielsweise der Apache, kann sehr gut mit statischen Dateien umgehen. Er kann sie gezielt cachen und fix ausliefern, ohne auf dynamische Zusammenstellung oder Datenbankzugriffe warten zu müssen.

Natürlich gibt es Bereiche, bei denen ein kompletter Verzicht auf dynamische Inhalte hinderlich ist. Da wären in erster Linie Kommentare, für die sich eine Datenbank durchaus eignen würde. Auch eine Suche gestaltet sich ganz offensichtlich einfacher auf einer Datenbank.

Dennoch: das Generieren statischer Seiten hat seinen Reiz und so dachte ich mir, ich probiere derartiges einmal aus.

Dieses Blog ist ein Beispiel, wie es gehen kann. In kurzer Zeit zusammengehack basiert es auf [jekyll](https://github.com/mojombo/jekyll), einem in Ruby geschriebenen Tool, das es erlaubt, aus statischen Files elegant Seiten zusammenzubauen, und dabei in den Genuss von Templates zu kommen, um Duplizierung von Code zu vermeiden. Desweiteren erstellt es hübsche URLs, und zwar nicht etwa über .htaccess Files mit Rewrite-Rules, sondern ganz einfach über die Verzeichnisstruktur, die es beim Erstellen der Seite anlegt.

Doch das ist nicht das Ende der Sexyness. Deployed wird der ganze Spaß nämlich per push in mein persönliches [github Repository](https://github.com/bestform/bestform.github.com). Von da aus jagt es github durch jekyll und heraus kommt das, was ihr hier lest. Versioniertes, verteiltes Blogsystem mit automatischem Deployment. *Awesomesauce*!

Ich werde hier erst mal noch ein wenig basteln - soll heißen, hier ist alles noch Baustelle. Ich bin allerdings schon fast mit der Portierung meiner Tonstube aus Django in einen statischen Container fertig. Darüber werde ich hier dann noch genauer berichten, wenn ich damit fertig bin.
