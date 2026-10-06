# 1.0.0 — Logo und Releasepaket

Menümarker **PTC 1.0.0**, Startlog **Pioneer Train Control 1.0.0 loaded**. Im Menükopf links s freigegebene PNG-Logo; au i de Modliste. Nach mehrmaligem Öffne/Schliesse sowie Speichere/Neulade prüfen; DE/EN und üblechi UI-Skalierig. Spieltransfer und Paarabfahrt vom r31-Stand erhalte. De bekannti Nachladefall bleibt offe.

Lokali Paket-/Workflow-Prüefige decked s Logo, Backup/Restore und Ablehnig vo ere alte DLL oder fehlendem/falschem Icon ab. Full Unreal/Slate/Spiel und Release-Targets müend uf em Modding-Rechner prüeft werde. De r31-Screenshot bestätigt s grafische Grundlayout, nöd de neue 1.0.0-Build.

---

# Historische Prüefprotokoll

# r31 Ingame-Prüefig

Nach em Build TEST r31 kontrolliere. DE und EN, 1920×1080 und üblechi UI-Skalierig: Übersichts-Spalte, lange Zug-/Stationsname, Waggonmodus und Prozent/Menge-Felder, Vorlagen uf/zue, Save/Reset, Partnerauswahl, ESC und wieder frei laufe/luege. Orange Markierig muess bim Wechsel sofort folge. Grüne Balkefarb bedeutet erfüllti Zielregel; en leere Wage het weiterhin en leere Balken. Aktualisierig 1s Details /5s Übersicht. Native UHT/Slate/Spiel hie nöd prüeft. De39-Item-Nachladefehler bleibt separat offe.

---

# r30 — gezielti Buildregression

Lokal: Produktions-Statustexte gegen consteval-Format-Fixture kompiliert. Die akzeptiert Literale und lehnt dynamisch übersetzti Formatvorlage ab. r29-UI als negative Kontrolle scheitert genau am Formatargument. r30 prüeft DE/EN-Itemdefizit, Prozentzeiche und zwei Nachkommastelle, aufgrundeti Warteziit, Partnertext und3000000000 fehlendi Items. Paketregel prüeft zusätzlich alli FString::Printf-Aufrüef uf direkte TEXT-Literale, inklusive Übersicht und Warteziit-Lambda.

Alle bisherige Regel-/Inventar-/Docking-/Cargo-/Sync-/Vorlagentests bleiben im Self-Test. Build-/Installationssimulation inkl. alter DLL und fehlgschlagenem Build. Echti r30-Unreal-/UHT-/Win64-/Cook-/Spielausfüehrig isch hie nöd möglich.

Im nächste native Build: zuerst FactoryEditor ohne die11 Printf-Fehler und ohne de Slate-Folgefehler, dann Win64 und installierte r30-Marker. Danach d fünf Funktione us de r29-Abnahmliste teste. De no offeni100%-Nachladeabschluss bleibt en separate Spieltest.

---

# Historische Dokumentation bis r29

# r29 — Abnahm vo de fünf Funktione

Lokal automatisiert: Produktionsfunktionen für typed Itemmengi1999/2000, falsches Item, Liquid/Null/ungültigi Werte; Rest knapp über/exakt10% und exakt0; Itemziel in echte Paarabfahrt; Positionsvorlage inkl. Ignore, Ablehnig vo falscher Anzahl/duplizierte GUIDs, Zielrevision/Aktivierigsstatus/Partnererhalt; serverseitigi Vorlagenrevision, Name/Limit/Autorität/Lösche; tatsächlechi Detail-/Katalogabfrage mit Filter/Siite/Status; DE/EN-Texte; lesendi Cargodiagnose und all bisherige Lade-/Entlade-/Docking-/Sync-Regressione. Ersetzti APIs sind kei Unreal/Game.

Im Spiel no nötig:

1. r29-DLL und Menümarker; Amount-Wage2000 Stück wähle.1999 wartet,2000 erfüllt; anderi Itemart darf nöd zähle. Unterschiedlichi Wageziele und bestehendi Paarabfahrt zäme prüefe.
2. Empty10%: Rest darüber wartet, darunter erfüllt;0 exakt leer. Übertragig darf unter s Ziel sinke (native Zyklus). Ladebeginn unabhängig vom Abfahrtsziel.
3. Quelle mit drei unterschiedliche Regle kopiere, Ziel mit gleiche Anzahl: richtige Positione, Partner und Aktivierig erhalte. Falschi Anzahl blockiert. Einfüege ändert de Server erst nach Speichere. Bei zwei Bearbeitende muss Konfliktschutz weiterhin greife.
4. Vorlage aus gspeichereter Haltregel erstelle, Menü/Spiel schliesse und neulade, Vorlage abrüefe und uf andere Halt anwände. Lösche ändert kei bestehendi Haltregel. Name doppelt/leer und gelöschti Vorlage prüefe. Host/Client müssen dieselbe Liste gseh, falls Multiplayer genutzt wird.
5. Transportübersicht: beide Fahrtrichtige, tatsächliche Andockstation trotz vorgezogene Fahrplancursor, aktive Wartegründ, Partner-Wage, Countdown, Füllstand und letzte Freigab.40er-Paging, Suche/Filter. Detail bleibt1s, Übersicht5s; offeni Entwürf bliebed erhalte.
6. UI DE/EN bei tatsächlicher Uflösig: Zielspinner, Itemsuche, Vorlage und Schaltfläche erreichbar; Scrollen, ESC und Spielinput-Sperre. Das Rendering isch hie nöd usgführt.
7. Ladefix separat bei Ziel100 testen: nachgladeni117/145 Items aus em r28-Log müssen wirklich überträge werde. Nächtliche Logdatei endet vor Zyklusabschluss; meh Testziit nötig. Paarabfahrt selbst isch vom User bestätigt.

Native UHT/Editor/Win64/Cook, SaveGame-/RPC-Kompatibilität, MP/DS und UI-Bedienig sind offe. Keine neue Features mehr nötig, um nach bestätigtem Ladefix und Abnahm die Releasevorbereitig aazfange.

---

# Historische Dokumentation bis r28

# r28 — Prüefstand und Release-Gates

Lokal prüefbar: Regelkern, tatsächliche Inventory-/CountRemaining-/Docking-/Cargo-/SaveRule-/Synchronisierigs-Methoden mit API-Ersatzobjekte; Paketprüefsummene und simulierti Build-/Installationsfehler. Das ersetzt weder Unreal noch s Spiel.

## Aktueller Release-Stand

**Userbestätigung vom 05.10.2026: D gemeinsami Abfahrt funktioniert. De Ladefehler isch de verbleibendi bekannte Funktionsblocker.** Dass de einzelne r27-Log kei automatische Paarabfahrt enthält, widerleit die Bestätigung nöd. Kei neue Grundsatzprüefig oder Umbau vo de Paarlogik nötig.

No nötig für dä Release:

1. **Ladefix im echte Spiel bestätige:** de bekannte Fall6281+119 muss effektiv6400 ergeh. Plattformabnahm und Waggonzunahm vergliiche, Nachschub berücksichtige. Kei Verlust/Duplikation oder Leerzyklen; nachher mehrere Pendelrunde mit Nachlade.
2. **Neus Prozentziel kurz abneh:** pro Wage speichere, knapp unter/exakt am Ziel, 100%-Verhalte, Spiel speichere/neulade. Bi paarwiiser Abfahrt gilt s Ziel als Teil vo de bestehende eigene Bedingige; d Paarfunktion isch vom User bereits bestätigt.
3. **Finale Release-Build/Verpackig:** echte UHT/LinuxEditor- und Win64-Shipping/Cook-Builds, korrekti installierte DLL-/Menüversion, finale Versionsnummer und sinnvolle Logstufe. Native Build/Test isch hie mangels Projekt/Engine nöd möglich.

Zusätzlich gilt: Multiplayer/Dedicated Server, Flüssigkeite und Mischladige sind durch die lokale Tests nöd als unterstützt bewiese. Nur tatsächlich testeti Spielarte und Frachtfälle im Release als unterstützt bezeichne; das sind kei neu bestätigte Fehler. LinuxServer-Shipping ist nötig, falls en Server-Build ausgelieferet wird.

## r28-Spieltest zum bekannte Blocker

Startlog r28 bestätige. Voll-Ziel 100, Standard-Lademodus, Timeout0/Notfall0. Wage mit 6281/6400 bereitstelle. 118 passende Items uf de Plattform: warte; 119: Nachladig darf starte. Nach em Zyklus muss Waggon6400 erreicht sii. `Cargo native transfer` zeigt Bestand vor/nach; `transferHeld` zeigt d vorübergehend gha Bereitschaft. Falls native Transfer gar nöd ufg'ruefe wird oder nichts bewegt, vollständige Log liefere; de Fix isch denn nöd bestätigt.

Zum Prozentziel: s gliiche 6281-Inventar bi Ziel98 und erfüllte übrige Bedingige muss freigäh werde. Bi99/100 weiterwarte. UI-Prozentdarstellig cha runde; Häkli und Abfahrtsentscheid basiered uf em ungerundete Füllwert. Ladebeginn bleibt separat, d Restmängeregel wird nöd zum 98-%-Batchziel.

## Beleg us r27

FactoryGame(20261005-213807).log: 23:33:24 Schweizer Ziit Nachladestart mit count6281/missing119/available119. 23:33:51 weiterhin6281, nachher topUpStalled1. Um23:35:06 und23:35:09 beidi Züg manuell freigäh; kei automatische gemeinsame Abfahrt in dem Log. Die drei andere Wage sind scho am Logafang voll; das bewiist kei r27-Nachladefix.

---

# Historische Dokumentation bis r27

# r27 — Prüefstand und Spieltest

Lokal: alli vier Bildmänge (71/170/180/61), native canLoad=false unabhängig vom korrigierte full-Cache, irreführende Totaltransfer-Werte in beidi Richtige, exakti Schwelle 169/170, Bestandänderig während erneuter Settingsberechnig, Quellitem/Filter/NONE/individuelle Itemzuständ, native Stapelablehnig, inkompatibli/ungültigi/fehlendi Slots, Scope-Wiederherstellig, Power/Standby/Pending/Visibility/Abbruch/Autorität, Laufphase, kein Fortschritt trotz wachsendem Plattformbestand, Fortschritt/neue Besüech, AnyAmount/PlatformFull, native Idle-Timer. Modelltransfer wird separat vom Mod simuliert; d Mod selber verändert kei Inventar.

Negative Kontrolle: d r27-Cargo-Fixture kompiliert mit r26-Code und scheitert erwartigsgemäss bim erste Bildfall an canLoad=false. D frühere r25-Cache-Regression bleibt separat mit Mischladig; sie bewiist nöd d Spielimplementation.

## Im Spiel zuerst

1. Spiel/Editor beende, r27 baue/installiere, Startlog und TEST-r27-Label prüefe. Host/Clients gliichi Version.
2. Dis bestehende Save lade, betroffene Waggons Voll, Standardladebeginn, Timeout 0 (bi Kopplig Notfall 0). Tatsächliche Inventare vor/nach dokumentiere.
3. Erwartet: mit verfüegbarer passender Restmengi startet de native Zyklus; Waggonbestand steigt uf 6400, d passenden Plattformitems nehmed entsprechend ab (Förderbandnachschub berücksichtige). PTC-Voll und gemeinsame Freigab erst nach tatsächlich erfüllte Regle.
4. 170 fehlendi Items, nur 169 verfüegbar: kei zweiti Ladig. Genau 170 verfügbar: Start darf folge. Test mit passendem Filter und ausgeschlossenem Filter wiederhole.
5. Falls en gestartete Zyklus nichts bewegt: `topUpStalled=1`, kei endlosi Animationen. Vollständige Log mit `Cargo top-up started` und `topUpKnown/Missing/Available/Fits/Stalled` uswerte. E native Transferablehnig wär en no offeni Runtime-Ursach, nöd dur Modelltests widerlegt.
6. Zwei echte Pendelrunde und Save/Load: keine alte Stillstandssperri am neue Besuch. Laufendi Animation, Strom/Standby, manuell Freigab und Notfall weiterhin korrekt.
7. Unveränderti r26-Entladeregel und Paarabfahrt prüefe. Mischladig/leeri Slots/Flüssigkeite separat; r27 verspricht dafür kei neui Bereitschaftskorrektur. Multiplayer/DS, UHT/Editor/Win64/Server, SaveGame/RPC und Animation sind hie nöd usgführt.

---

# Historische Dokumentation bis r26

# r26 — Prüefstand und Spieltest

Lokal: tatsächliche Cargo-/Session-/SaveRule-C++-Methoden mit API-Doubles. Erstes teilwiises Entlade, danach Restplatzschwelle 124/125; abnehmendi Kapazität und erneuti native Settingsberechnig; Veto trotz native Timerexception; scoped Wiederherstellig nur vom geänderte Richtungsflag; Idle-Timer werde erscht bi gnueg Restplatz ersetzt; Filter/NONE, leere Wage, native Ablehnig; Phase/Strom/Standby/Pending/Visibility/Abbruch/Autorität; separati Historie pro Wage und Richtig; Live-Opt-out; unbekannti Enumwerte abglehnt; Iistellig vom Partner erhalte; gspeichereti Load-/Unload-Liste bim Docked-Rekonstruiere wieder übernoh, frische Besuch leert beidi.

Native UHT-/Editor-/Win64-/Server-Builds, Slate-Rendering, SaveGame-Serialisierig/RPC, Itemübertragig, Flüssigkeit, Multiplayer und DS sind hie nöd verfügbar.

## Im Spiel prüefe

1. Host und Clients alli r26; Startlog und Menüversion kontrolliere. Spiel/Editor vor em Bau schliesse.
2. Entladehalt aktiv, jede relevante Wage Leer/Empty, Entladebeginn «Erstes Entladen sofort, danach Platz für den Rest», Timeout 0 (bi Kopplig Notfall 0), speichere.
3. Plattform fasst nume Teil vom volle Wage. Aakunft: einisch entlade. Danach wenig Platz freimache: kei wiitere Start, solange nöd de ganze verbleibende Waggoninhalt passt.
4. Gnueg Platz für de ganze Rest schaffe. Genau denn nächsti native Entladig; tatsächliche Waggoninhalt und Plattformzuewachs kontrolliere. D Plattform mues nöd leer sii.
5. Mehreri Wage mit unterschiedlichem Rest separat prüefe. Im Wartezustand speichere/neulade: kei neui Gratis-Teilentladig. Neu aafahre: erste Teilentladig wieder erlaubt.
6. Gegenprüefig «Jede mögliche Teilmenge»: au chliini passendi Mänge dürfed wieder starte. Lade-Iistellig und Partner-Iistellig dörfed sich nöd ändere.
7. Volles oder inkompatibles Ziel, NONE/Itemfilter, Stromusfall/Standby, manuell Freigab und Timeout >0 prüefe. Laufendi Animation darf nöd abbroche werde. Flüssigkeite separat verifiziere.

## Neuer r25-Spielbeleg, kei Bestätigung für 100-%-Ladefix

FactoryGame(20261005-192821).log: r25 glade, 22 erneuti Entladevorgäng, gemeinsam erteilti Freigab 21:25:16 Schweizer Ziit. Lade-Wiederstarts: 0. Am Endi zwei Wage bi 98.9/99.0 %, fullCorrected=1, canLoad=0. D Cache-Korrektur längt im Spiel nöd. De nachfolgend historische r25-Modelltest isch kei Runtime-Erfolgsbeleg. r26 löst dä verbleibende Ladefehler nöd.

---

# Historisch: r25 — Prüefstand

## Lokal mit API-Ersatzobjekte

`bash verify.sh --self-test`: Regelkern, Inventory-Inspector, Docking, Cargo und Paarlogik. `python3 tests/workflow_test.py`: Paket-/Rollback-/Versions-/Buildfehlertests. Native Binaries sind i de Workflowtests nume simuliert.

Cargo deckt ab: erscht Ladig sofort, Restmengi knapp drunter/genau druf, wieder sinkende Bestand, unabhängigi Waggons/Besüech, Idle erst mit genüegender Mengi, volle Plattform trotz scho gnueg Ware für en chliinere Wage, verschiedeni Stapelkapazitäte, leeri/negative/ungültigi/unlesbari Slots, NONE/volle Waggons, Entlade, native Timer-Bypass, wiederholti native Bereitschaftsberechnig, Wiederherstelle vo temporäre Flags, Freigab/Abbruch, Power/Pending-/Timer-Schutz. SaveRule prüeft ungültigi Modi, eigenständigi Partner-Modi und d Wiederherstellig vo gspeicheretem Ladefortschritt.

## r25 — gezielte Regression

Lokal bestande: native full=1, tatsächlechi Stapel 100/100 und 96/100, gemeinsami Inspektion 98 %. r25 korrigiert nume im geschützte Ladebereitschafts-Scope. De Test mit r24 scheitert a de fehlende Top-up-Bereitschaft. Prüeft sind native Neuberechnige, Wiederherstelle vor Completion/am Ende, volle und ungültigi Inventare, leeri Slots, Filter/NONE, fehlendi Mengi, native Kapazitätsablehnig, Strom/Standby/Pending/Timer, falschi Phase, Entlade, Abbruch, Client, falsche Akteur und Evaluator ohni Update-Scope.

Im Spiel: r25 glade bestätige; Ladehalt, Wage Voll, Timeout 0 und Standard-Restmengi. E Waggon mit belegte, aber nöd ganz volle Stapel bereitstelle. Menü-Bestand und Inventar kontrolliere; gnueg passende Ware zufüehre. fullCorrected=1 und ptcFreightFull=0 müend d alte full=1-Sperri nachvollziehbar mache. Erwartet isch e native Nachladig bis 100 % und denn Conditions-Freigab. Wenn canLoad trotzdem 0 bleibt, reicht die Cache-Korrektur nöd; de vollständigi r25-Log muess d native Ablehnig zeige. Kei Erfolg ohni tatsächlich gestiegene Waggonbestand behaupte.

## Übrigi Spielprüefige

1. r25 im Startlog und Menü bestätige. En Ladehalt mit PTC aktiv, relevante Wage Voll und Timeout 0 iirichte. Standardmodus speichere. Frisch andocke mit weniger Ware als de Wage cha ufneh. Erscht Ladig söll starte; danach kei Neustart für chliini Nachlieferige. Genueg passende Ware für de ganze Rest zufüehre: de nächste Zyklus söll starte und de effektive Bestand söll stige.
2. E aagbrochene Waggonstapel und verschiedeni Item-Stapelgrössi teste. Waggonfilter und NONE separat prüefe. Kei Start mit unpassender Ware. De native Totaltransfer-Wert, Inventarbeständ und `batchBlocked` im Log vergliiche.
3. Nur bei voller Plattform: knapp nöd volle Plattform muess warte, au wenn de Wage bereits mit dere Mengi voll würd. Voll mache: native Start söll folge. Mehreri Plattforme mit verschiedenem Füllstand prüefe; jede wartet separat.
4. Zweite Aakunft am gliiche Bahnhof: Standardmodus erlaubt wieder genau d erscht Teilmengi. Mehreri Wage unabhängig teste. Im Wartezustand Spiel speichere/neulade; bereits agfangeni erscht Ladig darf nöd vergessen gah. Alts r23-Save separat (native Phase vor/während/nach Ladig) teste.
5. Modus während em bestätigte Halt ändere und speichere: sofort gültig bim nächste Startcheck, kei Interrupt vo ere laufende Animation. Ungspeicherte Entwürf und fehlgschlagene Speichervorgäng dürfed d aktive Regel nöd ändere.
6. Timeout 60, Minimum, manuell Freigab, Autopilot us und native Ladeabbruch separat teste: d Mängeregel darf d vorhandeni Freigab nöd blockiere. Laufendi Ladeanimationen müend sauber fertig werde.
7. Entlade mit knappem Platz und wieder frei werdender Kapazität; kei neue Mängeschwelle fürs Entlade. Flüssigkeit separat mit tatsächleche Inventarbeständ, Animation, Stromusfall und Standby prüefe. Kei Inventarverlust oder Duplikation.
8. Partnerabfahrt in beide Aakunftsreihefolge und über drei Pendelrunde. Beide Regle live erfüllt und Minimum erreicht; genau e gemeinsame Freigab. Notfall 0 vs >0; fehlende/falsche/freigähni Partner; beidi Ladebeginn-Modi separat. Kein Bereitschaftswert vom alte Besuch.
9. DE/EN, chliini/grössi Uflösig und Scrollbereich. Waggonregle, LADEBEGINN, Partnerkarte und Speichere erreichbar. ESC/Textfeld/Gameplay-Sperri unverändert. Host und Clients alli r25; Dedicated Server, RPC, Speichere/Neulade und paralleli Bearbeitig prüefe.

## Laufzitbeleg us r23

FactoryGame(9).log: r23 glade 19:33:43 Schweizer Ziit; Ladehalt bestätigt 19:37:58. Zwüsche 19:38:26 und 19:39:36 zwölf `Cargo retry armed` über vier Plattforme. Das belegt wiederholti native Startversüech. Exakti Itemmänge und sichtbari Animatione sind nöd protokolliert; de User meldet chliini Ladige. FactoryGame(10).log liefert zusätzlich en r24-Warte-/Wiederstartbeleg. D exakti Itemmängeschwelle und r25-Korrektur bruuched de Spieltest.
