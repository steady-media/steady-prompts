# Steady Prompt-Set

Version 0.2, 5. Oktober 2026. Für Testnutzer:innen des Steady-Connectors.

## Was das ist

Zwölf Fragen zu deinen Mitgliederzahlen, ausgeschrieben als Prompts. Ein Prompt ist der Text, den du einem KI-Assistenten wie Claude oder ChatGPT gibst. Diese Prompts sagen dem Assistenten, wie er deine Steady-Zahlen richtig liest. Ohne sie nennt er dir oft die Gesamtzahl aus dem Dashboard, wo du wissen wolltest, wie viele Menschen zahlen.

Der Assistent liest deine Zahlen nur. Er ändert nichts bei Steady.

## Bevor du anfängst

Verbinde deine Publikation über den Steady-Connector mit deinem Assistenten. Du findest ihn in deinem Steady-Backend unter Integrationen, KI-Assistenten: https://steady.page/backend/publications/default/integrations/ai_assistants

## Drei Wege, diese Datei zu nutzen

1. **Schnell ausprobieren.** Kopiere einen Prompt aus Teil B in einen neuen Chat. Fang mit „Wo fange ich an?“ an.
2. **Mit der ganzen Datei.** Hänge diese Datei an einen neuen Chat an und schreib: „Halte dich an die festen Regeln in dieser Datei und beantworte Frage 1.“
3. **Einmal einrichten.** Lege in Claude oder ChatGPT ein Projekt an. Füge Teil A in die Anweisungen des Projekts ein. Prüfe, ob der Steady-Connector in dem Projekt eingeschaltet ist. Danach reicht die kurze Frage: „Wie läuft’s?“

Der dritte Weg gibt die besten Antworten.

## Alle zwölf Fragen

| Nr. | Frage | Wann |
| --- | --- | --- |
| 1 | Wo fange ich an? | Wenn du Steady zum ersten Mal mit einem KI-Assistenten nutzt. |
| 2 | Wie läuft’s? | Einmal im Monat, als regelmäßige Kontrolle. |
| 3 | Kommen weniger oder gehen mehr? | Wenn deine zahlenden Mitglieder oder dein Umsatz nicht mehr wachsen. |
| 4 | Wann verliere ich Mitglieder? | Vor den Monaten, in denen sich viele Mitgliedschaften verlängern. |
| 5 | Wo stehe ich in einem Jahr? | Wenn du ein Ziel willst oder planen musst. |
| 6 | Was hat die Kampagne gebracht? | Nach einem Mitgliederaufruf, einer Kampagne oder einem Sonderangebot. |
| 7 | Bleiben sie? | Wenn du wissen willst, ob neue Mitglieder nach dem ersten Jahr verlängern. |
| 8 | Ist das viel oder wenig? | Wenn du wissen willst, wie deine Zahlen im Vergleich stehen. |
| 9 | Soll ich meinen Preis ändern? | Bevor du einen Preis erhöhst oder einen Rabatt beendest. |
| 10 | Die Zahlen für Profis | Wenn Steuerberatung, Bank oder ein Beirat nach Kennzahlen fragt. |
| 11 | Das Dashboard | Wenn du alle Grafiken auf einer Seite willst, für ein Treffen oder den Jahresrückblick. |
| 12 | Die volle Analyse | Einmal im Jahr oder vor einer großen Entscheidung. Sie dauert mehrere Minuten und braucht viele Abrufe. |

## Teil A: Feste Regeln

Füge das einmal in die Anweisungen eines Projekts ein. Jede Antwort in dem Projekt hält sich dann an diese Regeln.

```text
Du hilfst einer Medienmacherin oder einem Medienmacher, die Mitgliederzahlen der eigenen Publikation bei Steady zu verstehen. Die Person macht Journalismus, einen Podcast oder einen Newsletter. Sie ist keine Betriebswirtin. Lies die Zahlen über den Steady-Connector. Ändere nichts bei Steady.

DATENREGELN
1. Zahlende Mitglieder zuerst. Die Gesamtzahl im Steady-Dashboard zählt auch Gäste mit (Menschen, die über die Mitgliedschaft einer anderen Person lesen und selbst nichts zahlen) und Mitglieder aus einem Bundle. Nimm zahlende Mitglieder, Gäste und externe Mitglieder aus total_by_type in get_key_statistics. Schreib „zahlende Mitglieder“, nie nur „Mitglieder“. Erkläre den Unterschied zur Dashboard-Zahl einmal.
2. Die Zeitreihen zählen alle Mitgliedstypen zusammen. Um zahlende Mitglieder von Gästen zu trennen, hol Tageswerte für Mitglieder und für Umsatz über dieselben Tage. An einem Tag, an dem der Umsatz gestiegen ist, sind einige Neuzugänge zahlend: Teile den neuen Monatsumsatz durch 5 Euro und runde. Zähle so viele, aber nie mehr als die Neuzugänge des Tages und nie weniger als einen. Ein einzelner Neuzugang mit 50 Euro oder mehr im Monat ist ein Paket. Ein Tag mit Neuzugängen ohne neuen Umsatz zählt als Gäste. Dieselbe Regel gilt für Kündigungen und verlorenen Umsatz. Für die Zahl der zahlenden Mitglieder an einem früheren Tag rechne von der heutigen Zahl zurück. Sag einmal, dass diese Trennung eine Schätzung ist.
3. Monats- und Jahreswerte für „new“ und „lost“ sind saldiert: Wer im selben Monat kommt und geht, fehlt darin. Für neue Mitglieder und Kündigungen addiere Tageswerte. Nutze Monats- und Jahreswerte nur für Bestände.
4. Frag höchstens 365 Tage Tageswerte pro Abruf ab. Frag nie Daten vor der Gründung der Publikation ab. Ein Abruf mit period=all liefert Jahreswerte und in period.start das Gründungsdatum. Ein Vergleich mit dem Vorjahr braucht zwei Abrufe pro Zeitreihe.
5. Lass den laufenden Monat aus jedem Vergleich heraus, denn er ist nicht abgeschlossen. Bewerte den letzten abgeschlossenen Monat.
6. Die Kündigungsrate aus get_churn_rate zählt alle Mitgliedstypen und ist deshalb für zahlende Mitglieder zu niedrig. Brauchst du die Kündigungsrate der zahlenden Mitglieder, rechne sie mit Regel 2 aus.
7. Beträge kommen in Cent. Zeig Euro.
8. Rechne alles in Code, nicht im Kopf. Widersprechen sich zwei Zahlen, sag das in einem Satz und melde es mit submit_feedback.
9. Sag, was die Daten nicht zeigen: wer die Mitglieder sind, warum sie gehen, woher sie kommen. Rate nicht.
10. Kostenlose Leser:innen stehen in free_members in get_key_statistics. Sie haben sich angemeldet, ohne zu zahlen, und zählen nicht zur Dashboard-Zahl. Die Zahlen für die letzten 30 Tage dort reichen in den laufenden Monat.
11. Nutze so wenige Abrufe, wie die Frage braucht. Rufe get_churn_rate und get_trial_members nur ab, wenn es um die Kündigungsrate oder um Probemitgliedschaften geht.

SO ANTWORTEST DU
– Erster Satz: die Antwort, mit Zahl und Vergleich. Vergleiche mit demselben Monat im Vorjahr. Ist die Publikation jünger, vergleiche mit dem Vormonat.
– Nenne die Richtung in einfachen Worten: aufwärts, abwärts oder gleich.
– Dann eine Grafik, die diesen Satz zeigt.
– Dann drei kurze Teile mit diesen Überschriften: Was ist passiert? Warum? Was kann ich diese Woche tun? Sag unter „Warum?“, was die Zahlen über die Ursache zeigen, zum Beispiel weniger neue Mitglieder oder mehr Kündigungen. Zeigen sie keine Ursache, sag das. Nenne unter der letzten Überschrift eine Handlung, mit Zahl.
– Schluss: „Das sehe ich in deinen Daten nicht: …“ und eine Frage, die sich als nächste lohnt.
– Höchstens eine Bildschirmseite Text.

SPRACHE
– Antworte in der Sprache der Person. Auf Deutsch: du, und gendern mit Doppelpunkt (Leser:innen).
– Schreib wie eine sorgfältige Reporterin: kurze Sätze, Subjekt, Verb, Zahl. Keine Metaphern. Kein Wirtschaftsjargon wie Hebel, Funnel, Treiber, KPI, Insight, Nutzerbasis.
– Nutze den richtigen Fachbegriff und erkläre ihn beim ersten Mal. Beispiele: „Kündigungsrate (der Anteil der zahlenden Mitglieder, deren Mitgliedschaft in einem Monat endete)“, „Monatsumsatz (was alle Mitgliedschaften zusammen pro Monat einbringen)“. Danach nutze den Begriff.
– Bei weniger als 100 zahlenden Mitgliedern kommen Menschen vor Prozenten: „4 deiner 40 zahlenden Mitglieder“.
– Schreib „Medienmacher:innen“, nie „Creator“.
– Lobe und tadle keine Zahl. Nenne die Zahl und womit du sie vergleichst.

GRAFIKEN
– Titel: das Ergebnis als ganzer Satz mit Zahl. Untertitel: was gemessen wird, Einheit, Zeitraum.
– Eine Akzentfarbe, #EC7B68, für das, worum es im Titel geht. Alles andere grau. Keine Legende: Linien und Balken direkt beschriften. Nur waagerechte Hilfslinien. Balken beginnen bei null.
– Verlauf: Säulen bis 13 Zeiträume, darüber eine Linie. Neue Mitglieder gegen Kündigungen: Säulen nach oben und unten von einer Nulllinie. Ein Anteil: 100 Punkte. Weniger als 30 Menschen: ein Punkt pro Mensch. Keine Tortendiagramme.
– Unter der Grafik, klein: „Quelle: Steady, Stand [Datum]“, und ein Hinweis, falls Gäste mitgezählt sind.
– Kannst du in dieser App nicht zeichnen, schreib eine Tabelle mit höchstens fünf Zeilen. Behalte Titel, Untertitel und Quellenzeile.
```

## Teil B: Sechs Kernfragen

Jeder Prompt funktioniert auch allein, ohne Teil A. Ersetze den Text in [eckigen Klammern] durch deinen eigenen.

### 1. Wo fange ich an?

**Wann:** Wenn du Steady zum ersten Mal mit einem KI-Assistenten nutzt.

```text
Nutze den Steady-Connector und gib mir einen ersten Überblick über meine Publikation, auf einer Seite.

Beginne mit der einen Sache, die ich wahrscheinlich noch nicht weiß. Prüfe zuerst das: Mein Steady-Dashboard zählt Gäste, die nichts zahlen, zusammen mit zahlenden Mitgliedern. Sag mir, wie viele heute wirklich zahlen und wie viele vor einem Jahr gezahlt haben.

Zeig dann vier weitere Ergebnisse. Jedes bekommt einen Satz mit Zahl, eine kleine Grafik und die Frage, die ich als nächste stellen sollte:
– meinen Monatsumsatz über die letzten 13 abgeschlossenen Monate
– neue zahlende Mitglieder und Kündigungen in den letzten 12 abgeschlossenen Monaten. Nutze dafür Tageswerte, denn in Monatswerten fehlen alle, die im selben Monat kommen und gehen. Zähle nur zahlende Mitglieder. An einem Tag mit neuem Umsatz: Teile den neuen Monatsumsatz durch 5 Euro und runde. So viele Neuzugänge sind zahlend, aber nie mehr, als an dem Tag dazukamen, und nie weniger als einer. Mach dasselbe für Kündigungen mit dem verlorenen Monatsumsatz. Neuzugänge oder Kündigungen an einem Tag ohne solchen Umsatz sind Gäste, die nichts zahlen.
– die Kalendermonate, in denen der meiste Umsatz begonnen hat. Jahresmitgliedschaften verlängern sich in dem Monat, in dem sie begonnen haben. Das sind also meine Verlängerungsmonate.
– meine kostenlosen Leser:innen und wie viele von ihnen angefangen haben zu zahlen

Gib noch keinen Rat. Schließe mit den drei Fragen, die für meine Zahlen am wichtigsten sind. Erkläre jeden Fachbegriff, wenn du ihn zum ersten Mal benutzt. Schreib kurze, einfache Sätze, ohne Metaphern und ohne Wirtschaftsjargon. Nutze höchstens sechs Abrufe bei Steady.
```

**Du bekommst:** Eine Seite: eine Sache, die du vielleicht nicht wusstest, vier weitere Ergebnisse mit je einer Grafik, und drei Fragen zum Weitermachen.

**Frag danach:** Die der drei Fragen, die dich am meisten interessiert.

### 2. Wie läuft’s?

**Wann:** Einmal im Monat, als regelmäßige Kontrolle.

```text
Nutze den Steady-Connector und sag mir, wie meine Publikation läuft.

Ich will drei Dinge wissen: wie viele Mitglieder wirklich zahlen (die Gesamtzahl in meinem Dashboard zählt auch Gäste, die nichts zahlen), was ich pro Monat einnehme, und wie beides im Vergleich zum Vormonat und zum selben Monat vor einem Jahr steht. Lass den laufenden Monat weg, denn er ist nicht abgeschlossen. Bleib bei diesen drei Dingen; andere Ergebnisse gehören zu den anderen Fragen.

Antworte in dieser Reihenfolge: ein Satz mit der Zahl; eine Grafik meines Monatsumsatzes über die letzten 13 abgeschlossenen Monate; was passiert ist; warum; eine Sache, die ich diese Woche tun kann. Sag mir dann, was meine Daten nicht zeigen und welche Frage ich als nächste stellen sollte. Erkläre jeden Fachbegriff, wenn du ihn zum ersten Mal benutzt. Schreib kurze, einfache Sätze, ohne Metaphern und ohne Wirtschaftsjargon. Bleib bei einer Bildschirmseite.
```

**Du bekommst:** Zahlende Mitglieder, Monatsumsatz, die Richtung und eine Sache, die du tun kannst.

**Frag danach:** „Kommen weniger oder gehen mehr?“, wenn die Zahlen fallen oder stehen bleiben.

### 3. Kommen weniger oder gehen mehr?

**Wann:** Wenn deine zahlenden Mitglieder oder dein Umsatz nicht mehr wachsen.

```text
Nutze den Steady-Connector. Meine zahlenden Mitglieder oder mein Umsatz wachsen nicht. Finde heraus, was von zwei Dingen sich geändert hat: Kommen weniger Menschen dazu, oder kündigen mehr?

Nutze Tageswerte für Mitglieder und für Umsatz, denn in Monatswerten fehlen alle, die im selben Monat kommen und gehen. Frag ein Jahr Tageswerte pro Abruf ab. Zähle nur zahlende Mitglieder. An einem Tag mit neuem Umsatz: Teile den neuen Monatsumsatz durch 5 Euro und runde. So viele Neuzugänge sind zahlend, aber nie mehr, als an dem Tag dazukamen, und nie weniger als einer. Mach dasselbe für Kündigungen mit dem verlorenen Monatsumsatz. Neuzugänge oder Kündigungen an einem Tag ohne solchen Umsatz sind Gäste, die nichts zahlen. Vergleiche die letzten 12 abgeschlossenen Monate mit den 12 Monaten davor. Habe ich 100 oder mehr zahlende Mitglieder, zeig es auch Monat für Monat.

Beginne mit einem Satz, der die Seite nennt, die sich geändert hat, mit beiden Zahlen für beide Zeiträume. Zeichne eine Grafik: neue zahlende Mitglieder nach oben, Kündigungen nach unten. Nenne dann eine Sache, die ich diese Woche tun kann. Sag mir, was meine Daten nicht zeigen. Erkläre jeden Fachbegriff, wenn du ihn zum ersten Mal benutzt. Schreib kurze, einfache Sätze, ohne Metaphern und ohne Wirtschaftsjargon. Bleib bei einer Bildschirmseite.
```

**Du bekommst:** Welche der beiden Seiten sich geändert hat, mit den Zahlen für dieses Jahr und das Jahr davor.

**Frag danach:** „Wann verliere ich Mitglieder?“, wenn mehr kündigen. „Was hat die Kampagne gebracht?“, wenn weniger kommen.

### 4. Wann verliere ich Mitglieder?

**Wann:** Vor den Monaten, in denen sich viele Mitgliedschaften verlängern.

```text
Nutze den Steady-Connector. In welchen Monaten kündigen die meisten meiner zahlenden Mitglieder, und welche Termine in den nächsten 12 Monaten sind für meinen Umsatz wichtig?

Nutze Tageswerte für Mitglieder und für Umsatz über meine ganze Geschichte, ein Jahr pro Abruf. Zähle nur zahlende Mitglieder. An einem Tag mit neuem Umsatz: Teile den neuen Monatsumsatz durch 5 Euro und runde. So viele Neuzugänge sind zahlend, aber nie mehr, als an dem Tag dazukamen, und nie weniger als einer. Mach dasselbe für Kündigungen mit dem verlorenen Monatsumsatz. Neuzugänge oder Kündigungen an einem Tag ohne solchen Umsatz sind Gäste, die nichts zahlen. Addiere die Kündigungen nach Kalendermonat über die letzten 24 abgeschlossenen Monate. Prüfe für jeden Monat mit vielen Kündigungen, ob im selben Kalendermonat eines früheren Jahres viel Umsatz begonnen hat. Jahresmitgliedschaften verlängern sich in dem Monat, in dem sie begonnen haben, und dann kündigen Menschen.

Suche außerdem nach einer einzelnen Mitgliedschaft oder einem Paket, das allein 10 Prozent oder mehr meines Monatsumsatzes bringt. Sag mir, wann es begonnen hat und wann es sich wahrscheinlich verlängert.

Beginne mit einem Satz. Zeichne zwölf Säulen, Januar bis Dezember, und einen Zeitstrahl der Termine, die vor mir liegen. Nenne dann eine Sache, die ich vier Wochen vor dem nächsten Termin tun kann. Sag mir, was meine Daten nicht zeigen. Erkläre jeden Fachbegriff, wenn du ihn zum ersten Mal benutzt. Schreib kurze, einfache Sätze, ohne Metaphern und ohne Wirtschaftsjargon. Bleib bei einer Bildschirmseite.
```

**Du bekommst:** Die Monate mit vielen Kündigungen, den Grund, falls die Daten einen zeigen, und die Termine, die vor dir liegen.

**Frag danach:** „Wo stehe ich in einem Jahr?“

### 5. Wo stehe ich in einem Jahr?

**Wann:** Wenn du ein Ziel willst oder planen musst.

```text
Nutze den Steady-Connector. Wenn sich nichts ändert: Wie viele zahlende Mitglieder habe ich in einem Jahr?

Nimm die letzten sechs abgeschlossenen Monate aus Tageswerten: die durchschnittliche Zahl neuer zahlender Mitglieder pro Monat und den Anteil der zahlenden Mitglieder, die pro Monat kündigen. Zähle nur zahlende Mitglieder. An einem Tag mit neuem Umsatz: Teile den neuen Monatsumsatz durch 5 Euro und runde. So viele Neuzugänge sind zahlend, aber nie mehr, als an dem Tag dazukamen, und nie weniger als einer. Mach dasselbe für Kündigungen mit dem verlorenen Monatsumsatz. Neuzugänge oder Kündigungen an einem Tag ohne solchen Umsatz sind Gäste, die nichts zahlen. Schreib beides zwölf Monate fort. Nenne das Ergebnis eine Hochrechnung, keine Prognose: Es ist eine Rechnung und weiß nichts von Kampagnen, Preisänderungen oder Jahreszeiten. Gib eine Spanne an. Sag mir auch die Zahl, bei der gleich viele Menschen kommen wie gehen.

Mein Ziel sind [Zahl] zahlende Mitglieder in zwölf Monaten. Sag mir, wie viele neue zahlende Mitglieder ich dafür pro Monat brauche und wie viele das mehr sind als heute. Habe ich keine Zahl genannt, frag mich danach.

Beginne mit einem Satz. Zeichne eine Linie: die Vergangenheit durchgezogen, die Hochrechnung gestrichelt. Erkläre jeden Fachbegriff, wenn du ihn zum ersten Mal benutzt. Schreib kurze, einfache Sätze, ohne Metaphern und ohne Wirtschaftsjargon. Bleib bei einer Bildschirmseite.
```

**Du bekommst:** Eine Hochrechnung für zwölf Monate und wie viele neue zahlende Mitglieder pro Monat dein Ziel braucht.

**Frag danach:** „Wie läuft’s?“ in einem Monat, um die Zahl zu prüfen.

### 6. Was hat die Kampagne gebracht?

**Wann:** Nach einem Mitgliederaufruf, einer Kampagne oder einem Sonderangebot.

```text
Nutze den Steady-Connector. Ich habe vom [Datum] bis zum [Datum] [eine Kampagne / einen Mitgliederaufruf / ein Angebot] gemacht. Was hat das gebracht?

Nutze Tageswerte für Mitglieder und für Umsatz von 14 Tagen vor dem Start bis 14 Tage nach dem Ende. Zähle neue zahlende Mitglieder pro Tag. Zähle nur zahlende Mitglieder. An einem Tag mit neuem Umsatz: Teile den neuen Monatsumsatz durch 5 Euro und runde. So viele Neuzugänge sind zahlend, aber nie mehr, als an dem Tag dazukamen, und nie weniger als einer. Mach dasselbe für Kündigungen mit dem verlorenen Monatsumsatz. Neuzugänge oder Kündigungen an einem Tag ohne solchen Umsatz sind Gäste, die nichts zahlen. Vergleiche die Kampagnentage mit der üblichen Zahl pro Tag. Biete ich Probemitgliedschaften an, zeig, wie viele begonnen haben und wie viele zu zahlenden Mitgliedern wurden. Probemitgliedschaften, die noch laufen, können noch nicht umgewandelt sein. Sag also, welche Zahlen noch offen sind. Zeig auch, wie viele kostenlose Leser:innen sich angemeldet haben.

Beginne mit einem Satz: wie viele zahlende Mitglieder mehr dazugekommen sind als in einem normalen Zeitraum gleicher Länge. Zeichne neue zahlende Mitglieder pro Tag, die Kampagnentage markiert. Sag mir, was meine Daten nicht zeigen, zum Beispiel, ob diese Mitglieder bleiben. Erkläre jeden Fachbegriff, wenn du ihn zum ersten Mal benutzt. Schreib kurze, einfache Sätze, ohne Metaphern und ohne Wirtschaftsjargon. Bleib bei einer Bildschirmseite.
```

**Du bekommst:** Was die Kampagne über einen normalen Zeitraum hinaus gebracht hat.

**Frag danach:** „Wo stehe ich in einem Jahr?“

## Teil C: Sechs weitere Fragen

Diese sind neuer und weniger erprobt als Teil B. Die Fragen 7 und 8 stoßen heute an die Grenzen der Daten: Die Prompts sagen das und zeigen das Nächstliegende.

### 7. Bleiben sie?

**Wann:** Wenn du wissen willst, ob neue Mitglieder nach dem ersten Jahr verlängern.

```text
Nutze den Steady-Connector. Ich will wissen, ob meine neuen zahlenden Mitglieder bleiben: Von 100, die angefangen haben, wie viele zahlen nach einem Jahr noch?

Prüfe zuerst, ob der Connector ein Werkzeug hat, das Mitglieder nach ihrem Startmonat verfolgt. Wenn ja: Sag mir, wie viele von 100 zahlenden Mitgliedern eines Startmonats nach 3, 12 und 13 Monaten noch gezahlt haben, getrennt für Mitglieder, die jährlich zahlen, und Mitglieder, die monatlich zahlen. Nutze nur Startmonate, die mindestens 13 Monate alt sind. Vergleiche die 12 jüngsten dieser Monate mit den 12 davor.

Wenn der Connector kein solches Werkzeug hat: Sag das in zwei Sätzen und schätze keine Zahl. Zeig mir stattdessen das Nächstliegende: in welchen Kalendermonaten der meiste Umsatz begonnen hat und in welchen der meiste verloren ging, über meine ganze Geschichte. Jahresmitgliedschaften verlängern sich in dem Monat, in dem sie begonnen haben.

Beginne mit einem Satz. Erkläre jeden Fachbegriff, wenn du ihn zum ersten Mal benutzt. Schreib kurze, einfache Sätze, ohne Metaphern und ohne Wirtschaftsjargon. Bleib bei einer Bildschirmseite.
```

**Du bekommst:** Heute: ein ehrliches „noch nicht sichtbar“ und deine Verlängerungsmonate. Später, sobald Steady die Daten liefert: wie viele von 100 bleiben.

**Frag danach:** „Wann verliere ich Mitglieder?“

### 8. Ist das viel oder wenig?

**Wann:** Wenn du wissen willst, wie deine Zahlen im Vergleich stehen.

```text
Nutze den Steady-Connector. Ich will wissen, ob meine Zahlen normal sind.

Prüfe zuerst, ob der Connector ein Werkzeug mit Vergleichswerten ähnlicher Steady-Publikationen hat. Wenn ja: Stell meine Zahlen neben die von Publikationen meiner Größe und sag mir, bei welcher Zahl ich am weitesten zurückliege.

Wenn es kein solches Werkzeug gibt: Sag in einem Satz, dass es einen Vergleich mit anderen Publikationen noch nicht gibt. Nenne keine Zahlen anderer Unternehmen oder aus Studien, denn sie sind nicht vergleichbar. Vergleiche mich mit mir selbst: Gib für diese fünf Zahlen die letzten 12 abgeschlossenen Monate und die 12 Monate davor an, und nenne die Zahl, die sich am stärksten verschlechtert hat:
– neue zahlende Mitglieder pro Monat
– Kündigungen zahlender Mitglieder pro Monat
– Monatsumsatz
– Umsatz pro zahlendem Mitglied
– der Anteil der Mitglieder, die einmal im Jahr zahlen (nur heute)

Nutze Tageswerte für neue Mitglieder und Kündigungen, ein Jahr pro Abruf. Zähle nur zahlende Mitglieder. An einem Tag mit neuem Umsatz: Teile den neuen Monatsumsatz durch 5 Euro und runde. So viele Neuzugänge sind zahlend, aber nie mehr, als an dem Tag dazukamen, und nie weniger als einer. Mach dasselbe für Kündigungen mit dem verlorenen Monatsumsatz. Neuzugänge oder Kündigungen an einem Tag ohne solchen Umsatz sind Gäste, die nichts zahlen.

Beginne mit einem Satz. Zeichne eine Grafik mit den fünf Zahlen. Erkläre jeden Fachbegriff, wenn du ihn zum ersten Mal benutzt. Schreib kurze, einfache Sätze, ohne Metaphern und ohne Wirtschaftsjargon. Bleib bei einer Bildschirmseite.
```

**Du bekommst:** Heute: ein Vergleich mit deinem eigenen Vorjahr. Später: ein Vergleich mit ähnlichen Publikationen.

**Frag danach:** Die Frage, die zu deiner schwächsten Zahl passt.

### 9. Soll ich meinen Preis ändern?

**Wann:** Bevor du einen Preis erhöhst oder einen Rabatt beendest.

```text
Nutze den Steady-Connector. Ich überlege, meinen Preis um [Prozent] zu erhöhen. Empfiehl mir keinen Preis. Zeig mir, was ich für meine Entscheidung brauche.

Rechne die Schwelle aus: Steigt der Preis um p Prozent, dürfen höchstens 1 − 1 ÷ (1 + p) der betroffenen Mitglieder kündigen, bevor ich weniger einnehme als heute. Bei 20 Prozent sind das etwa 17 von 100. Habe ich keinen Prozentwert genannt, rechne es für 10, 20 und 50 Prozent.

Stell daneben, wie viele von 100 zahlenden Mitgliedern in einem normalen Monat kündigen. Nimm das aus Tageswerten der letzten 12 abgeschlossenen Monate. Zähle nur zahlende Mitglieder. An einem Tag mit neuem Umsatz: Teile den neuen Monatsumsatz durch 5 Euro und runde. So viele Neuzugänge sind zahlend, aber nie mehr, als an dem Tag dazukamen, und nie weniger als einer. Mach dasselbe für Kündigungen mit dem verlorenen Monatsumsatz. Neuzugänge oder Kündigungen an einem Tag ohne solchen Umsatz sind Gäste, die nichts zahlen.

Zeig meinen Monatsumsatz heute und nach der Erhöhung, falls niemand kündigt. Der Connector zeigt meine Pakete und Preise nicht, und er kann nicht zeigen, was eine frühere Preisänderung bewirkt hat. Sag das.

Beginne mit einem Satz. Zeichne zwei Balken für den Umsatz und einen Punkt pro zahlendem Mitglied, mit markierter Schwelle. Sag mir, was meine Daten nicht zeigen: wie viele wegen einer Erhöhung gehen würden. Erkläre jeden Fachbegriff, wenn du ihn zum ersten Mal benutzt. Schreib kurze, einfache Sätze, ohne Metaphern und ohne Wirtschaftsjargon. Bleib bei einer Bildschirmseite.
```

**Du bekommst:** Wie viele Mitglieder kündigen dürfen, bevor ein höherer Preis weniger einbringt. Keine Preisempfehlung.

**Frag danach:** „Wo stehe ich in einem Jahr?“

### 10. Die Zahlen für Profis

**Wann:** Wenn Steuerberatung, Bank oder ein Beirat nach Kennzahlen fragt.

```text
Nutze den Steady-Connector und gib mir eine Tabelle mit Kennzahlen, die ich an Steuerberatung, Bank oder Beirat weitergeben kann.

Eine Zeile pro Kennzahl. Spalten: der letzte abgeschlossene Monat, derselbe Monat im Vorjahr, der Durchschnitt der letzten 12 abgeschlossenen Monate, und ein Satz, der die Kennzahl erklärt. Die Kennzahlen:
– Monatsumsatz (MRR) und MRR mal 12 (ARR)
– zahlende Mitglieder
– neue zahlende Mitglieder und Kündigungen pro Monat
– die Kündigungsrate der zahlenden Mitglieder, und daneben die Kündigungsrate, die Steady für alle Mitgliedstypen meldet
– durchschnittliche Dauer einer Mitgliedschaft: 1 ÷ Kündigungsrate der zahlenden Mitglieder
– Umsatz pro zahlendem Mitglied (ARPU)
– Lifetime Value: ARPU mal durchschnittliche Dauer einer Mitgliedschaft
– Quick Ratio: neuer Umsatz ÷ verlorener Umsatz über 12 Monate
– der Anteil der Mitglieder, die einmal im Jahr zahlen

Nutze Tageswerte für neue Mitglieder und Kündigungen, ein Jahr pro Abruf, denn Monatswerte sind saldiert. An einem Tag mit neuem Umsatz: Teile den neuen Monatsumsatz durch 5 Euro und runde. So viele Neuzugänge sind zahlend, aber nie mehr, als an dem Tag dazukamen, und nie weniger als einer. Mach dasselbe für Kündigungen mit dem verlorenen Monatsumsatz. Neuzugänge oder Kündigungen an einem Tag ohne solchen Umsatz sind Gäste, die nichts zahlen. Lass den laufenden Monat weg. Beschrifte jede Zeile mit „zahlende Mitglieder“ oder „alle Mitgliedstypen“ und mische die beiden nie. Neuer Umsatz enthält Upgrades, verlorener Umsatz enthält Downgrades. Sag, dass sich das nicht trennen lässt.

Beginne mit einem Satz zur wichtigsten Veränderung. Schließe mit drei Sätzen zu dem, was am meisten zählt. Gib keine Empfehlung, denn diese Tabelle wird weitergereicht.
```

**Du bekommst:** Eine Tabelle mit den üblichen Kennzahlen des Abo-Geschäfts, jede in einem Satz erklärt.

**Frag danach:** „Zeig mir das Dashboard.“

### 11. Das Dashboard

**Wann:** Wenn du alle Grafiken auf einer Seite willst, für ein Treffen oder den Jahresrückblick.

```text
Nutze den Steady-Connector und bau ein Dashboard meiner Publikation auf einer Seite. Kann diese App eine interaktive Seite erstellen, nutze das.

Über den Grafiken: die Lage in einem Satz und die drei Zahlen dahinter. Dann höchstens zwölf Grafiken, eine pro Zeile:
1. die Dashboard-Zahl, geteilt in zahlende Mitglieder und Gäste
2. Monatsumsatz, letzte 36 abgeschlossene Monate
3. neue zahlende Mitglieder und Kündigungen pro Monat, letzte 24 Monate
4. zahlende Mitglieder im Zeitverlauf
5. die Kündigungsrate pro Monat, beschriftet mit „alle Mitgliedstypen“
6. neue zahlende Mitglieder nach Kalendermonat
7. Kündigungen nach Kalendermonat
8. neue zahlende Mitglieder nach Wochentag
9. Mitglieder, die jährlich zahlen, gegen Mitglieder, die monatlich zahlen
10. Umsatz pro zahlendem Mitglied, letzte 24 Monate
11. Probemitgliedschaften und wie viele zu zahlenden Mitgliedern wurden, nur wenn ich welche anbiete
12. eine Hochrechnung für die nächsten 12 Monate, falls sich nichts ändert

Nutze Tageswerte für Mitglieder und für Umsatz, ein Jahr pro Abruf. Zähle nur zahlende Mitglieder. An einem Tag mit neuem Umsatz: Teile den neuen Monatsumsatz durch 5 Euro und runde. So viele Neuzugänge sind zahlend, aber nie mehr, als an dem Tag dazukamen, und nie weniger als einer. Mach dasselbe für Kündigungen mit dem verlorenen Monatsumsatz. Neuzugänge oder Kündigungen an einem Tag ohne solchen Umsatz sind Gäste, die nichts zahlen. Lass den laufenden Monat weg.

Jede Grafik bekommt einen Titel, der ihr Ergebnis als Satz mit Zahl nennt, und einen Untertitel mit dem, was gemessen wird, Einheit und Zeitraum. Eine Akzentfarbe, alles andere grau. Keine Legenden: Linien und Balken direkt beschriften. Nur waagerechte Hilfslinien. Unter jeder Grafik eine kleine graue Quellenzeile mit Datum.

Schreib im Chat fünf Sätze: die fünf wichtigsten Titel. Erkläre jeden Fachbegriff, wenn du ihn zum ersten Mal benutzt. Schreib kurze, einfache Sätze, ohne Metaphern und ohne Wirtschaftsjargon.
```

**Du bekommst:** Eine Seite mit bis zu zwölf Grafiken. Wer nur die Titel liest, kennt die Lage.

**Frag danach:** „Gib mir die volle Analyse.“

### 12. Die volle Analyse

**Wann:** Einmal im Jahr oder vor einer großen Entscheidung. Sie dauert mehrere Minuten und braucht viele Abrufe.

```text
Nutze den Steady-Connector und analysiere die ganze Geschichte meiner Publikation. Das braucht viele Abrufe. Arbeite in vier Schritten und zeig mir nach jedem Schritt ein kurzes Ergebnis, bevor du weitermachst.

Schritt 1, Daten holen: die Zahlen von heute; Jahreswerte; Monatswerte seit dem Start; Tageswerte für Mitglieder und für Umsatz für jedes Jahr, ein Jahr pro Abruf. Prüfe, ob die Tageswerte zu den Beständen passen, und sag mir, wo nicht.

Schritt 2, rechnen: zahlende Mitglieder und Gäste für jeden Tag der Geschichte. An einem Tag mit neuem Umsatz: Teile den neuen Monatsumsatz durch 5 Euro und runde. So viele Neuzugänge sind zahlend, aber nie mehr, als an dem Tag dazukamen, und nie weniger als einer. Mach dasselbe für Kündigungen mit dem verlorenen Monatsumsatz. Neuzugänge oder Kündigungen an einem Tag ohne solchen Umsatz sind Gäste, die nichts zahlen. Dann Monatsumsatz, neue zahlende Mitglieder und Kündigungen pro Monat, die Kündigungsrate der zahlenden Mitglieder, Umsatz pro zahlendem Mitglied, und die Tage, an denen ich 100, 250, 500 und 1.000 zahlende Mitglieder erreicht habe.

Schritt 3, Muster suchen: Kalendermonate und Wochentage mit vielen Neuzugängen oder vielen Kündigungen; einzelne Tage mit ungewöhnlich vielen Neuzugängen oder einer großen Zahlung, mit Datum; was von jedem solchen Ausschlag nach drei, sechs und zwölf Monaten geblieben ist.

Schritt 4, zwölf Monate hochrechnen: falls sich nichts ändert; mit 20 Prozent mehr neuen zahlenden Mitgliedern; mit einer Kündigungsrate, die einen Prozentpunkt niedriger liegt.

Schreib dann ein Memo: die Diagnose in drei Sätzen, jeder mit Zahl; höchstens zehn Ergebnisse, nach Wichtigkeit sortiert, jedes mit Zahl und Grafik; die Entscheidungen, die ich treffen muss, jede mit ihrer Wirkung in Mitgliedern und in Euro und mit einem Termin. Kann diese App Dateien erstellen, füge eine Tabelle mit den Daten und den Rechnungen hinzu. Sag mir, was die Daten nicht zeigen. Erkläre jeden Fachbegriff, wenn du ihn zum ersten Mal benutzt. Schreib kurze, einfache Sätze, ohne Metaphern und ohne Wirtschaftsjargon.
```

**Du bekommst:** Ein Memo mit Diagnose, bis zu zehn Ergebnissen und den offenen Entscheidungen; wo die App es kann, eine Tabelle.

**Frag danach:** „Wie läuft’s?“ jeden Monat, um zu sehen, ob die Entscheidungen wirken.

## Wenn eine Antwort falsch aussieht

Schreib an support@steadyhq.com. Diese vier Angaben helfen am meisten:

– welche Frage du gestellt hast, und die Version oben in dieser Datei
– welchen Assistenten du benutzt hast (Claude oder ChatGPT)
– was du erwartet hast und was du bekommen hast
– ein Screenshot der Antwort

Drei Dinge solltest du wissen:

– Die Trennung von zahlenden Mitgliedern und Gästen im Zeitverlauf ist eine Schätzung. Die Zahlen von heute sind exakt.
– Der Assistent sieht nicht, wer deine Mitglieder sind, warum sie gehen oder woher sie kommen.
– Grafiken hängen vom Assistenten ab. Kann er nicht zeichnen, schreibt er eine kleine Tabelle.

## Änderungen

– 0.2, 5. Oktober 2026: sechs weitere Fragen (Teil C). Eine Übersichtstabelle. Jeder Prompt verlangt jetzt einfache Sätze.
– 0.1, 2. Oktober 2026: erste Version für Testnutzer:innen.

## Lizenz

© 2026 Steady Media GmbH. Diese Prompts stehen unter der Lizenz [Creative Commons Namensnennung 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/deed.de). Du darfst sie kopieren, ändern und weitergeben, auch kommerziell, wenn du Steady als Quelle nennst.
