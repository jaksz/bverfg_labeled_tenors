# Teaser
Wie gut kann man mit künstlicher Intelligenz vorhersagen, wie eine Verfassungsbeschwerde beschieden wird?

# Einleitung
Dieses Repository enthält einen Datensatz von ca. 1800 Entscheidungen des Bundesverfassungsgerichts (jeweils nur Sachverhalt) über Verfassungsbeschwerden, gelabelt nach Obsiegen/Niederlage

*Ziel*: KI-Modelle trainieren, die ausschließlich anhand des Tatbestandes versuchen vorherzusagen, ob eine Verfassungsbeschwerde Erfolg haben wird oder nicht.

# Beschreibung der Datenstruktur
1. Spalte: Nummerierung
2. Spalte: Obsiegen ("ja") oder Niederlage ("nein"). Zum Thema, wie des ermittelt wurde, siehe weiter unten.
3. Spalte: Tenor der Entscheidung

# Hintergrund
## aus juristischer Sicht
Wenn das Bundesverfassungsgericht über eine Verfassungsbeschwerde entscheidet, besteht diese Entscheidung aus folgenden Teilen:
1. **Tenor**: Sehr kurzer und präziser Abschnitt, aus dem sich ergibt, wie in der Sache entschieden wurde, d.h. ob die Verfassungsbeschwerde Erfolg hatte oder nicht, z.B. "Die Verfassungsbeschwerde ist unzulässig".
2. **Tatbestand**: "Objektive" (siehe unten bei "Problem") Zusammenfassung des tatsächlichen Geschehens, was zu einer Verfassungsbeschwerde geführt hat, Beispiel: "Die Beschwerdeführerin ist eine Partei, die eine Versammlung angemeldet hatte, welche jedoch von der Versammlungsbehörde verboten wurde, [...]".
3. **Entscheidungsgründe**: Erwägungen der Richter, warum sie aus dem *Tatbestand* zum *Tenor* gekommen sind.

## aus technischer Sicht
Es existieren Algorithmen der "künstlichen Intelligenz" (z.B. https://github.com/facebookresearch/fastText), welche Texte "clustern" können, d.h. einer Gruppe zuordner, z.B. über einen Zeitungsartikel sagen können, ob er zum Sportteil, zum Finanzteil, etc. gehört. Man trainiert ein Modell, indem man es mit Beispieltexten füttert, bei dem die zugehörige Gruppe bekannt ist (z.B. "Der BVB hat gestern gewonnen" -> Sportteil). Danach kann man das Modell abfragen, indem man einen Text eingibt ("Die Aktie der Firma XY ist abgestürzt") und das Modell im Idealfall dann ausspuckt: "Finanzteil".

# Idee
Was wäre, wenn man ein Modell mit wie folgt trainieren würde: Man nimmt Verfassungsbeschwerden, die bereits entschieden wurden (d.h. der Ausgang ist bekannt, z.B. die Formulierung "wird abgewiesen" heißt, die Verfassungsbeschwerde war nicht erfolgreich). Hiervon nimmt man den Tatbestand, der ja bloß objektiv die Ereignisse beschreibt, und nimmt dazu den Tenor, der beschreibt, ob diese Ereignisse aus dem Tatbestand einen Verstoß gegen die Verfassung darstellen (und die Verfassungsbeschwerde somit Erfolg hat). Die rechtliche Würdigung (Entscheidungsgründe) lassen wir einmal weg.

# Problem (aus meiner Sicht)
Die Richter verfassen die Tatbestände nicht am Anfang der Verfahrens (bzw nach dem Schluss der mündlichen Verhandlung), jedenfalls bevor sie eine Entscheidung treffen, sondern erst NACHDEM sie (im Kopf) eine Entscheidung getroffen haben. Das Urteil wird also am Stück abgefasst, also Tenor, Tatbestand und Entscheidungsgründe in unmittelbarem zeitlichen Zusammenhang. Dies wird sicherlich dazu führen, dass die Richter dazu neigen, (auch unbewusst) bestimmte Formulierungen zu bevorzugen, wenn die Verfassungsbeschwerde Erfolg hat, als wenn sie abgewiesen wird, und das sogar beim Verfassen des "objektiven" Tatbestandes. 

Daher ist es gut möglich, dass ein solcher Datensatz untauglich ist, um damit Vorhersagen zu treffen. Vielmehr müsste man Zugriff auf die ursprünglichen Schriftsätze der Anwälte haben. Natürlich schrieben Anwälte parteiisch, aber die gegensätzlichen Betrachtungsweisen heben sich bei gegenüberstellender Betrachtung hoffentlich auf. Letzendlich entscheidet das Gericht ja auf dieser Basis (natürlich evtl noch weitere Dokumente, Urkunden, Protokolle der mündlichen Verhandlungen). Jedenfalls ist es zum jetzigen Zeitpunkt unmöglich, an diese Dokumente in Masse zu kommen, sodass man sich für den Moment mit dem vorliegenden Datensatz abfinden muss :)
