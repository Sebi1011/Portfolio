# Woche 1

**Inhalt:** Ein LLM erzeugt Text, indem es Stück für Stück das wahrscheinlichste nächste Token vorhersagt. Tokens sind Wortteile; Preise und Limits werden in Input- und Output-Tokens gemessen. Das Kontextfenster ist alles, was das Modell bei einem Aufruf sieht. Es hat kein eigenes Gedächtnis zwischen Aufrufen, deshalb muss der Verlauf jedes Mal mitgeschickt werden. Die Temperatur steuert, wie zufällig die Antworten sind. Halluzinationen entstehen, weil das Modell plausible statt geprüfte Antworten erzeugt. Große Modelle lösen komplexe Aufgaben besser, kleine sind schneller und günstiger.

**Kernbegriffe:** Token, Kontextfenster, Temperatur, Halluzination, Modellgröße

**Übung:** Dieselbe Aufgabe per API an ein großes und ein kleines Modell schicken und Token-Verbrauch, Kosten und Qualität vergleichen.

Aufgabe: 
Erstelle einen Ernährungsplan für KW 42 (Post-Race Recovery & Re-Integration). Der Fokus liegt auf der Regeneration nach einem Halbmarathon. Vorgaben: • Kalorien & Makros: Erhaltungsniveau bei 1.800–2.000 kcal/Tag, hohe Proteinzufuhr für die Muskelreparatur, antientzündliche Fette und ausgewogene Kohlenhydrate. • Küche & Zubereitung: Sehr unkompliziert halten (One-Pot oder Prep-Friendly) aufgrund Arbeit im Home-Office und damit erforderlicher Zeiteffizienz.

1. Model: Claude Haiku 5.5 (Token Verbrauch: Output: 3500, Input: 241, Total: 3741):
- Vollständiger Ernährungsplan für KW42, reine Textform. 
- Zutaten + Zubereitung.
- Wiederkehrende Rezepte über die Woche. Frühstück, Mittag, Abend,
- Tipps zur Regeneration
- kurze Einkaufliste (3 Zeilen)
- Rückfrage zu Allergien / Ernährungspräferenzen

2. Model Claude Opus 5.5 (Token Verbrauch: Output: 12,914, Input: 248, Total: 13,162):
- Output in Form von Claude Docs in md
- Überblick & Prinzipien der Woche --> Einblick & Erklärungen der Ernährungsplanung
- Fokus auf Zufuhr von Proteine, Kohlenhydrate, Fette & Omega-3 -> roter Faden für gesamte Ernährungsplanung KW42   
- Zutaten + Zubereitung.
- Wiederkehrende Rezepte über die Woche. Frühstück, Mittag, Abend
- Tipps zur Regeneration, aber deutlich faktenbasierter und genauere Tipps
- längere, deutlich detailliertere Einkaufliste

Erkenntnisse:
Haiku war nicht wirklich geeignet für diese Aufgabe. 
Aufgabe wurde zwar gelöst und das Ergebnis sieht schlüssig aus, ist jedoch im Detail wenig nachvollziehbar & enthält wenig Tiefe.
Output in Form des Textes für Anwenudungsfall wenig praktikabel.
-> kleines Model = schneller, kostengünstiger & einfacher Output. Wenig inhaltliche Tiefe, daher nicht für komplexe Aufgaben geeignet.
Fazit: Für gezielten Output mit inhatlicher Tiefe -> Höherer Aufwand durch klarere Anweisungen / Regelbestimmung im Prompting nötig.

Opus erreicht mit demselben Prompt eine deutlich umfangreichere Analyse und Planung. 
Ergebnis enthält deutlich mehr Tiefe, aber auch potenziell mehr für den Nutzer irrelevante Details / Informationen.
--> mehr Aufwand bei der Informationsfilterung. 
Output in Form der Markdown etwas praktikabler und geeignet für Ablage eines Dokuments.

-> großes Model = höherer Aufwand, die bereitgestellten Informationen für den eigenen Nutzen zu filtern 
Fazit: Für gezielten Output mit inhaltlicher Tiefe -> mehr Guardrails & Filter nötig


Haiku ist wie ein schneller, effizienter Mitarbeiter, der seine Leistung am besten abrufen kann, wenn er dahin geführt wird. 
Opus ist wie ein Fachexperte, der in seinem Themengebiet sehr viele Informationen bereitstellen kann, aber nicht weiß, welche davon tatsächlich gebraucht werden und daher durch gezielte Einschränkungen zum Ergebnis geführt werden muss.


Aktuelle API-Listenpreise (18.10.2026):
Haiku 5.5: 
- 0,10 $ pro Million Input-Tokens
- 0,50 $ pro Million Output-Tokens
Opus 5.5:
- 4 $ pro Million Input-Tokens
- 20 $ pro Million Output-Tokens

|	 | Haiku 5.5	| Opus 5.5 |
| --- | --- | --- |
| Input |	241 Tokens	| 248 Tokens |
| Output |	3.500 Tokens |	12.914 Tokens |
| Kosten pro Plan	| ca. 0,0018 $ |	ca. 0,26 $ |
| Hochgerechnet auf 1.000 Pläne |	ca. 1,80 $ | ca. 260 $ |

Opus war für diese Aufgabe also rund 146-mal so teuer. Das liegt an zwei Faktoren, die sich multiplizieren: Opus hat 3,7-mal so viel Output geschrieben, und Output kostet bei Opus 40-mal so viel wie bei Haiku.

Der Output treibt die Kosten. Über 99 % der Kosten entfallen auf Output-Tokens, der Prompt selbst kostet praktisch nichts. Damit wird die Erkenntnis „Opus braucht mehr Leitplanken“ doppelt wertvoll: Ein Längenlimit oder ein festes Format macht die Antwort nicht nur relevanter, sondern senkt auch direkt die Kosten.

Für einmalige Aufgaben sind beide Beträge vernachlässigbar. In einem Unternehmen mit tausenden Anfragen pro Tag entscheidet genau diese Rechnung, welches Modell wofür eingesetzt wird. 
---> Neben Qualität auch die Output-Tokens messen
