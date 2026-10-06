# r31 UI

Nur PTCWidget.cpp/.h und Versionsmarker verändert. Theme besitzt d Brushes für d ganzi Widget-Lebensduur. ShowTemplates isch lokaler Menü-Zuestand, wird nöd gspeicheret oder repliziert. De Live-Füllstand und Matches sind bestehendi reine Leseabfrage. Kei neue Server-/Cargo-Hooks.

---

# r30 — begrenzti Korrektur vo de Textformatierig

PTCWidget.cpp formatiert DE/EN-Nachricht einzeln mit direkte TEXT-Literale, denn wählt Tr die Spielsprach. Prozentpräzision, Ganzezahlmänge und Rundig bliebed erhalten. UHT-Datenmodelle, RCOs und sämtliche Cargo-/Abfahrts-/Vorlagenlogik sind bytegleich zu r29. Native Start-/Transferverhalte wird mit dem Buildfix nöd verändert.

---

# Historische Dokumentation bis r29

# r29 — Regle, Diagnose, Vorlage und Übersicht

EPTCMode ergänzt Amount am Endi (0/1/2 bliebed stabil). FPTCWagonRule: additives MaximumRemainingPercent=0, Item-Descriptor-Klasse, MinimumItemCount=1000. Matches ist gemeinsame Logik für echte Abfahrt, Partnerbedingige und UI-Häkli. Inspect summiert tatsächlechi Stapel nach Itemklasse mit int64; nur gültigi Inventare zähled. Rest0 und Voll100 bleiben exakt. Beträge sind Mindestbeständ, kei Transferbegrenzer. Schema-Fälder sind additiv; kein alts Save wird umgschriebe.

FPTCPresets::Capture baut e dichte Liste nach aktuellem Frachtwaggonindex, setzt ignorierti Positione explizit und entfernt Objekt-/Partner-GUIDs. Apply verlangt gleiche Anzahl und gültigi eindeutigi Ziel-GUIDs, übernimmt nume Verhaltens-/Zielwerte in en Entwurf und erhaltet Aktivierig, Revision, NeedsReview und Sync vom Ziel. SaveRule validiert nachher normal. Server-SaveTemplate liest nur d tatsächlich gspeichereti Source-Regel bi passender Revision. SavedTemplates isch SaveGame; Liste64/Name60 begrenzt, Name case-insensitiv eindeutig. Metadateiliste und einzelne Vollvorlage über separate rate-limitierte RCOs. Client blockiert Bearbeitig während em Vorlagenabruef und verwirft verspäteti Antworten nach Timeout.

FPTCCargoHooks::Describe liest e am normale Trace registrierti schwachi Wage→Plattformzuordnig; physischi Andockidentität und ControlsCargo müend no passe. Kei native Settingsberechnig, Phase-/Inventarmanipulation oder neuer Factory-Tick-Hook. Wartegründ enthalten native Zyklus/Strom/Standby/Filter/Restplatz sowie bekannte exakti Nachladestockwerte. Vorhandeni Flags chönd Platz/Filter nöd immer unterscheide; Text nennt drum beidi Prüefpunkte.

Detail erhält strukturierte aktive Wartegründ und die erscht blockierti Partner-Waggonposition. UI lokalisiert die Date selber. Catalog scannt Inventare nur für d aagfordereti40er-Siite und liefert mittlere Füllständ/Status; Default5s, Detail1s. Letzti Freigabursach pro Zug isch temporär (Bedingige/Timeout/manuell/Paar/Notfall/nativ/ungültig), kei neue Savehistorie. Bestehendi eigentliche Freigababläuf bliebed erhalten.

---

# Historische Dokumentation bis r28

# Aktuelli Ergänzig r28 — Prozentziel und Lebensduur vo de Transferbereitschaft

`PTC::Matches` und de echte `CountRemaining` verwenden pro Full-Bedingig s gspeicherete MinimumFillPercent. Bereich 1–99 vergleicht de gültige ungerundete Füllwert mit Prozent/100; 100 prüeft strikt Cargo.Full. Leer und Ignorieren bliebed unverändert. SaveRule weist Werte usserhalb 1–100 ab. D UI verwendet dieselbi Matches-Funktion fürs Häkli und behält de Entwurf bis zum Speichere. D Paarabfahrt nutzt CountRemaining für beidi Halt, drum au ihri unabhängige Prozentziele.

`TransferCycles` ergänzt de bestehende Start-Scope: nur en nachgwiesene Wechsel nach Loading/WaitingForTransfer erstellt en Cycle mit de exakte Start-Proof. `CarryTransfer` stellt zerscht alte temporäri Werte wieder her, prüeft Autorität/Besuch/Phase/Strom/Inventar/Filter neu und hält canLoad/total/full für genau die laufendi Ladig. Gleicher Bestand und glichi Objekt-/Besuchsidentität sind nötig; verschwundene Eignig sperrt d Korrektur. Es setzt weder Itemmänge, Phase, Busy, pendingTransfer noch mIsFullLoad. De Start-only-Timerbypass wird nöd länger gha.

Native Settings-/Statusprüefige innerhalb vom Update-Context gsehnd restaurierti Flags und werded danach neu beurteilt. Completion, Freigab, Cancel, Undock und Unregister räumed uf. Native sichtbar veränderti Flagwerte bliebed bim Restore erhalten. De aktuelle Transfer gilt vor sim Abschluss nöd als fehlgschlagene Fortschritt.

De rein beobachtende TransferInventory-Hook misst Gesamtbeständ vor/nach genau eim native Originalufruef. Er greift nöd uf PTC-Maps/Sessione zue. Es git kei neue Factory_Tick-Hook. Übertragig im Modell bewiist kei native Ausfüehrig. All älteri Scope-Ende-Aussage drunder beschriibed de damalige Stand; r28 verlängert die drei Bereitschaftsflags nume für de positiv nachgwiesene laufende Nachladig.

---

# Historische Dokumentation bis r27

# Aktuelli Ergänzig r27 — exakti Nachladebereitschaft für belegti Stapel

`InspectTopUp` liest sortereini Feststoffinventare mit nur gültige, belegte, zustandslose Stapel. Es summiert tatsächliche Itemzahl und Restkapazität mit int64, begrenzt d int32-API-Mänge und weist überfüllti/unlesbari Slots ab. Slotgrössi wird nume mit em gültige vorhandene Item abgfragt. Es nutzt de native Quellfilterselector und zählt nume passende zustandslose Quellstapel. `HasEnoughSpaceForStack` prüeft separat d tatsächlechi Stapelbarkeit vom ganze Rest.

`BatchReady` verwendet für dä bekannte Fall d exakti Restmängeschwelle statt mCanDoTotalTransfer. Unbekannti Fäll falle uf de bisherige native Wert zrugg. AnyAmount und PlatformFull bliebed separat. Entlade bleibt r26.

`ApplyTopUp` darf während em autorisierte serverseitige Update in Phase 1/6/7 canLoad/total temporär korrigiere, wenn Quellbestand, Filter, Zielkapazität und Batchregel das bewiese. D bisherige Power-/Standby-/Pending-/Timer-/Abbruchguards gälted. Es git kei direkte Add/Remove/TransferInventory-Aufrüef, kei Unlock, kei Änderung vo mIsFullLoad oder Busy. D native Animation/Transfercode wird nöd ersetzt.

`FUpdateContext` stellt zerscht s innere Startgate, denn d äussere Bereitschaftskorrektur wieder her. Native Settings- und Statushooks rechne uf wiederhergstellte Werte und prüefed danach neu. Completion und Scope-Ende gsehnd native Werte. D aktive Update-Funktion wird wiiter genau einisch ufg'ruefe.

`LastTopUp` merkt de Startbestand nume nach eme beobachtete Wechsel vo Wartephase nach Loading/WaitingForTransfer/Complete. Gleichi Wage-/Station-/Inventar-/Itemreferenz, Slotzahl, Itemzahl, Restmengi und Session-Startziit sperred e wiiteri Runde ohni Fortschritt. D Plattform-Zuelieferig wird nöd als Fortschritt akzeptiert. `CargoVisitStarted` liest d bestehendi physischi Session-Startziit; e neue Besuch hebt d alte Sperri uf. Referenze sind schwach, ungültigi Keys werded bereinigt; Unregister leert de Zustand. Kei neue SaveGame-Fälder; Neustart erlaubt e neue Probe.

Diagnose ergänzt Known/Missing/Available/Fits/Stalled sowie e Startzeile. fullCorrected isch nüm Teil vom Dedup-Schlüssel, damit s temporäre Hin-/Herstelle im Idle nöd sekündlichs Logspam erzeugt. Die ältere Dokumentation drunder beschreibt nur de jeweilige frühere Stand; d bisherigi Aussage «kei positive readiness correction» gilt sit r27 für de exakt bewiesene Fall nüm.

Kei Behauptig über d unbekannt intern FactoryGame-Berechnig. Native Ausfüehrig, Hook-Linkage und tatsächliche Itemtransfer sind nöd lokal testet.

---

# Historische Dokumentation bis r26

# Aktuelli Ergänzig r26 — Entladebeginn und Restplatz

`EPTCUnloadBatch { AnyAmount, FirstThenRemaining }` und `FPTCRule.UnloadBatch` (SaveGame) ergänzed de vorhandene LoadBatch separat. Standard isch FirstThenRemaining. SaveRule validiert beidi Enum-Bereich; d Partnerverknüpfig kopiert kei Lade-/Entlade-Iistellige. D bestehende Detail-/Save-RPCs tragged d komplette USTRUCT.

`FPTCDockSession.UnloadedWagons` und `FPTCSavedWait.UnloadedWagons` merke pro Wagon-GUID de erste Entladebeginn. BeginPlay, Docked und PreSaveGame kopiered d Liste wie bim Ladefortschritt. CargoUnloadBatch/CargoUnloadStarted verwended dieselbe Autoritäts-, aktuelle physischi Station-, Session-, Regel- und Abbruchprüefig wie CargoLoadBatch/CargoLoadStarted. Frischi Besüech bechömed leeri Liste. Native Unloading/Loading bestimmed ihri Richtig explizit; gemeinsame Transfer-/Complete-/Idle-Phase verwended de Plattformmodus.

`BatchReady` deckt beidi Richtige ab: nach em erste Entladezyklus mues d native UpdateUnloadSettings-Berechnig mCanDoTotalTransfer bestätige. `ApplyStartGate` sperrt nur START/WaitForTransferCondition, nimmt temporär mCanUnloadAny und TotalTransfer zrugg und überstüürt de native Timer-Bypass. De Scope merkt sich d Richtig und stellt nur s tatsächlich überschriibene Load-/Unload-Flag wieder her. En eigene UpdateUnloadSettings-Hook wendet s Gate au nach native Wiederberechnige aa. Idle-Rearm prüeft dieselbi Schwelle, bevor bestehendi Timer glöscht werded. Aktivi Transfer-/Animations-/Abschlussphase bliebed unverändert.

DE/EN-Slate: separate ENTLADEBEGINN/START UNLOADING-Karte im vorhandene Scrollbereich. Batch-Diagnose isch jetzt richtungsabhängig; Hold-Log zeigt zusätzlich unloadBatch/unloadedWagons. Gespeichereti Fortschritt-Rekonstruktion und C++-Logik sind mit Ersatz-APIs testet; native Serialisierig/RPC und UI-Rendering sind nöd usgführt.

De neue r25-Spielbeleg zeigt, dass d vorherigi Voll-Cache-Korrektur d Ladeablehnig bi 98.9/99.0 % nöd löst. Kei Erfolg für die Korrektur us Modelltests ableite. r26 ergänzt d Entladesteuerig; de Ladefehler bleibt offe. Die ältere Dokumentation drunder beschreibt de damalige Stand.

---

# Aktuelli Ergänzig r25 — exakti Voll-Prüefig vor em Nachlade

`APTCSubsystem::Inspect` isch jetzt öffentlich als gemeinsame rein lesendi C++-Hilfsfunktion für Menü, Abfahrt und Cargo. D vorhandeni Slot-/Item-/Kapazitätsprüefig wird unverändert wiederverwendet; kei zweiti Näherigsformel.

`ApplyFreightFull` prüeft während em aktuelle Update-Context en verwaltete Ladehalt i Phase 1, 6 oder 7. Strom, Standby, Pending-Transfer, Visibility-Timer und Session-/Plattformabbruch gälted wie bisher. Nur wenn native mIsFreightFull=1 und d gültigi exakti Beobachtig Full=false isch, wird dä Cachewert temporär uf false korrigiert. Ungültigi Inventare und nativ not-full bliebed unverändert. UpdateLoadSettings berechnet selber canLoad/total; PTC fabriziert kei positive Bereitschaft.

En zusätzliche Before/After-Scope uf EvaluateFreightInventoryStatus stellt vor de native Berechnig de ursprüngliche Cache her und prüeft danach d exakti Voll-Bedingig. Expliziti Refresh-Pfäd und de bestehendi LoadSettings-Hook verwended die gliichi Korrektur. FUpdateContext trennt d Wiederherstellig vom Cargo-Startgate und vom Full-Cache, damit e Kapazitätsprüefig de korrigierte Input gseht. Vor native Completion-Regle und am äussere Scope-Ende wird de Full-Cache wiederhergstellt. Inventory-Typ Cast<AFGFreightWagon> und vorhandens GetFreightInventory; kei private Inventarzuweisig.

Diagnose: ptcCargoValid, ptcFreightFull, ptcFill, fullCorrected. Native freightFull wird nach de Wiederherstellig protokolliert. D Restmängeschwelle, Voll-Plattform-Modus, gespeicherete erste Ladig, Abfahrtsregle und Partnerkopplige us r24 bliebed erhalten.

FactoryGame(10).log bestätigt r24: erschte Ladehalt native full=1 uf vier Plattforme, PTC remaining=1, Timeout nach 300 s. Bild grafik(4).png zeigt alli Ladebedingige Voll und Waggon 02 bi 98 %. Entladebild grafik(6)/(7) zeigt Waggon 03 bi 44 %; native Leerstatus und canUnload im Log erkläred e separate Wartebedingig. De genaue Grund, wieso FactoryGame voll anders bewertet, isch ohni native Implementierig nöd bewiise.

---

# PTC r24 — aktuelli Ergänzig

Die folgende Punkte ergänzed/ersetzed d historischi Cargo-Beschriibig wiiter unde.

- `FPTCRule.LoadBatch`: SaveGame-Enum AnyAmount=0, FirstThenRemaining=1 (Standard), PlatformFull=2. Server validiert de Enum vor em Speichere; d vorhandene Detail-/Save-RPCs überträged s ganze Rule-Struct. Partnerkopplige kopiered nume Synchronisierigseinstellige.
- `FPTCDockSession.LoadedWagons` enthält persistierti Waggon-IDs vom aktuelle physische Halt. Beobachteti Loading-/Transfer-/Complete-/Idle-Phase i Laderichtig markiered e bereits aagfangeni Ladig. `FPTCSavedWait.LoadedWagons` wird in PreSaveGame gschribe und bi Docked/BeginPlay wiederhergstellt. Neui Sessions ohni gespeicherete Wartezuestand started leer.
- De Standard verwendet bis zum erste beobachtete Ladebeginn de bisherige Teiltransfer-Start. Danach verlangt er de frisch nativ berechneti `mCanDoTotalTransfer`; laut SDK bedeutet das Wage ganz fülle oder ganz leere. Ladefilter und tatsächlechi Kapazität bliebed native Verantwortung.
- PlatformFull liest über GetInventory/GetSizeLinear/GetStackFromIndex/GetSlotSizeForItem. Nur gültigi belegti Stapel werde uf Kapazität abgfragt; fehlendi/leeri/ungültigi Slots blockiered. Die Prüefig isch pro Plattform und betrifft nur s Lade.
- `RearmIdle` prüeft zusätzlich d Mängeregel vor em Timerersatz. `ApplyStartGate` gilt nur während em aktive Update in Phase 1/6. Wenn d Mängeregel blockiert, setzt de Scope `mCanLoadAny`, `mCanDoTotalTransfer` und de Teiltransfer-Bypass temporär uf false. Die native Wert werde vor de nächste native Berechnig und am Scope-Ende wiederhergstellt. Native Bereitschaft wird nie uf wahr erfunde. En neue Hook nach `UpdateLoadSettings` verhindert, dass e erneuti native Berechnig innerhalb vom Update d Startbedingig umgaht. Completion-/Animationsphase, Entlade und fremdi/freigähni Sessions erhalted kei Mängesperri.
- r23-Busy-Fix, Power/Pending-/Sichtbarkeitstimer-Prüefige, native Filter, 1-Hz-Idle-Prüefig und physischi Session-Berechtigung bliebed erhalte. Freigabtiming und Paarlogik sind unabhängig vo de Ladestartregle.
- UI: zusätzliche scrollbar Karte LADEBEGINN / START LOADING mit drei direkte Uswahle und DE/EN-Erklärig. Kei neue Menüebeni und kei Netzwerk-Objektzeiger.
- `batchMode` protokolliert de effektive Modus (0 au vor em erste Ladebeginn), `batchBlocked` s Warte uf gnueg Ware. Native `totalPossible` wird nach em Wiederherstelle protokolliert.

FactoryGame(9).log belegt r23 und zwölf Idle-Wiederstarts über vier Plattforme. Kei exakti Itemmänge/Animationsbeweis. r24 wird mit API-Modelltest prüeft; native Implementierig, UHT und Engine fehled hie.

---

# Historischi Dokumentation bis r23

## Korrektur für de bestätigte Nachlade-Blocker us FactoryGame(8).log

r22 lauft. Nach em manuelle Abbruch und ere neue Runde dockt «Lagerzug 2» am 05.10.2026 um **19:21:51 Schweizer Ziit** frisch a. D vier Plattforme gönd vo WaitingToStart nach Loading. Um **19:22:20** folgt WaitingForTransfer mit `pendingTransfer=1`, denn Complete und IdleWaitForTime. De native Frachtstatus wechslet vo leer uf nüm leer. Kurz druf isch `relevant=1`, `canLoad=1`, `freightFull=0`, Strom vorhanden, kei usstehende Transfer, aber **busy=1 au im Idle-Zuestand**. Bis zum erneute Abbruch um **19:24:24** wird kei `Cargo retry armed` protokolliert.

Damit isch en konkrete r22-Codefehler bestätigt: `RearmIdle` bricht pauschal bi `IsLoadUnloading()` ab. Dä Wert isch im beobachtete Idle-Zuestand aber wiiter wahr. D Wiederaufnahme chunnt drum gar nie bis zur Bereitschaftsprüefig. **r23 entfernt die falschi Busy-Sperri im exakte Idle-Zuestand.** Strom, Standby, Abbruch, native Filter/Kapazität, volle/leeri Waggons, usstehendi Übertragig und Container-Sichtbarkeitstimer bliebed Schutzbedingige. S native Busy-Flag wird nöd zruggsetzt. Aktivi Loading/Unloading/WaitingForTransfer-Phase bliebed vom Wiederstart usgschlosse.

De Log zeichnet kei sichtbari Animation und kei Itemmengi uf. Er zeigt de erste Transferablauf und de wechselnde Leerstatus, aber kei zweite Ladezyklus. De User het Ladegrüüsch ohni sichtbari Animation beobachtet; ob r23 d Animation korrekt wieder startet, muess im Spiel prüeft werde.

# Ergänzig r23

Basis: FactoryGame(7).log, r22 tatsächlich glade. Vier Plattforme im wiederhergstellte Halt: status/from=6, canLoad=0, relevant=1, empty=1, busy=1, power=1, pendingTransfer=0; kei protokollierte Übergäng. De Log bewiist kei Ursache für canLoad=0.

r23 prüeft über vorhandeni SDK-Methoden EvaluateFreightInventoryStatus und UpdateLoadSettings/UpdateUnloadSettings d Bereitschaft direkt nach EvaluateRuleSet in Phase 1/6. Pro native Update nur einisch; rekursivi Regleprüefig löst kei wiiteri Bereitschaftsprüefig us. Abbruch/Phasenwechsel nach Callbacks wird respektiert. Kei direkti Änderung vo Inventar, canLoad/canUnload, Busy-Flag oder Phase-6-Timer. Exakti Phase plus Power/Standby/Pending-/Visibility-Guards statt IsLoadUnloading als pauschale Sperri für d neue Warteprüefig. FactoryGame(8).log bestätigt busy=1 im Idle nach em erste Ladezyklus. r23 entfernt drum zusätzlich d IsLoadUnloading-Sperri in RearmIdle und vertraut uf de exakte Idle-Zuestand plus Pending-/Visibility-Timer-Schutz. Busy selber bleibt unverändert. Diagnose: readinessRefresh und 10-s-Heartbeat während native Updates.

Prüefbar mit `bash verify.sh --self-test` und `python3 tests/workflow_test.py`. Negative Kontrolle: r23-Cargo-Fixture gegen r22 muss am fehlende Cache-Refresh scheitere. Fixture-Native isch es Modell; SDK exportiert kei native Implementierig. Native Funktion, Transfer, Animation, Save/Load, Flüssigkeite und Multiplayer/DS bliebed Ingame-Gates.

Build: `bash build-install.sh` sichert modlokali Win64-Buildreste und s alte Windows-ZIP, baut neu, prüeft Descriptor + PE-Win64-DLL + r23-Code-Marker und installiert mit Backup/Rollback. `verify.sh --build-all` prüeft s erzeugte ZIP ebenfalls, ohni Installation.

---

Historische Dokumentation vo de vorherige Revision:

# PTC r22 — Entscheid vor de Implementierig

## Prüefti Basis
SDK-Export `PFT-SDK-Context-EChVepAh`, SML.uplugin 3.12.0. De Export stammt vom 19.09.2026. De installierte SDK/Compiler vom Benutzer het Vorrang. r13 isch nume Referenz, kei Basis für d neue Laufzittlogik. D Engine und s Spiel sind i dere Arbeitsumgebig nöd verfügbar.

## Verantwortig
AModSubsystem mit SpawnOnServer, IFGSaveInterface und SaveGame-Daten. Kei UI uf em Server. Es registrierts UFGRemoteCallObject pro PlayerController nimmt validierti Requests aa und liefert gezielti Snapshots. Spieler im gemeinsame Save dörfed Regle bearbeite; Revisionen verhindere stills Überschriibe vo parallele Änderige. S UI gilt nie als Autorität für Inventar, Zugzustand oder Freigab.

## Identität
Persistierti GUIDs für PTC-Züg, Stopps und Waggons, verknüpft mit SaveGame-Objektreferenze. Name sind nur Anzeige. Waggons werde über de native TTrainIterator mit Orientierig erfasst, Regle hanged am Waggonobjekt. Neue Waggons sind ignoriert. Entfernti relevante Waggons mache d Regel prüefpflichtig. E eindeutige Bahnhof cha im Fahrplan verschobe werde; bi mehfach gliche Bahnhöf und native Fahrplan-Mutation wird nöd grate: betroffeni Regle werde deaktiviert. En neu erstellte Train cha nume mit eindeutige Waggon-Anker wiedererkannt werde; bi Merge/Split wird kei unsicheri Migration über Name gmacht.

## Docking
After-Hook uf AFGTrain::GetDockingRuleSetForCurrentStop ergänzt nume e Kopie vo de aktive Docking-Regle. Vanilla-Fahrplan und Itemfilter bliebed erhalte. Aktivi PTC-Regle verlanged FullyLoadUnload UND e sehr langi temporäri Warteziit, damit d Plattformsequenz am Halt bliibt. De PTC-Timeout wird vo PTC kontrolliert, nöd dur die langi native Warteziit. OnDocked bindet d Session a de tatsächliche Bahnhof. En 0.5-s-Timer prüeft nume aktivi Sessions. Freigab bi erfüllte Bedingige, Timeout, manueller Freigab oder ungültig wordener Regel über AFGTrain::CancelDockingSequence; die API wartet laut Header uf laufendi Ladeanimatione. Session-Ziit wird mitgspeicheret. Kei Physics-, Movement- oder Factory-Tick-Manipulation. Laufzittverhalte und Wechselwirkige sind no unbestätigt. Vor em Deinstalliere aktive Halt freigäh, damit kei temporäri native Wartebedingig im Save zruggblibt.

## Inventar
GetFreightInventory, GetStackFromIndex und GetSlotSizeForItem sind d Basis. Voll heisst Kapazität vo allne nutzbare Slots erreicht. Teilstacks sind nöd voll. Flüssigkeit isch i däm SDK als ganzzahligi Inventareinheit gspeicheret; PTC vergleicht die exakt. D Prozentanzeige isch de mittleri Belegigsgrad vo de Slots, kei erfundeni m³-Mengi.

## Menü
Eigeti dunkli Slate-Oberflächi innerhalb vo UFGInteractWidget; über de bestätigte Game-UI-Stack öffne/schliesse. Bewegung, Blick, Gameplay, Build-Gun und Ausrüstigsverwaltig über d vorgsehne Flags sperre. Kei Ignore-Counter pro Frame, kei Pawn DisableInput. ESC über OnEscapePressed/PreviewKeyDown. PreviewKeyDown konsumiert nur ESC, damit Textfälder bedienbar bliebed. Ein Menü pro Spieler. Client-RPC wird nach em Chat-Schliesse verzögert uf em nächste Tick verarbeitet.

## UI-Konzept
Anthrazit, orange Akzänt, helli Schrift, gedämpfti Statusfarbe. Zentrierts Fenster bi rund 72% vo de Viewportbreiti, maximal 1720 logische Pixel; chliini Displays werdet breiter nutzt. Drei Spalte: Züg, Fahrplan, Waggonregle. Listen scrollbar, Suchfeld, Auto-Filter, Namenssortierig. Entwurf wird bi Live-Updates nöd überschriebe; Speichere wartet uf Serverbestätigung. Automatisch DE/EN über d aktuelle Spielkultur.

## Verifikation
Pure C++-Regeltests, Skript- und Paketprüefige laufe hie. UnrealHeaderTool, FactoryEditor Linux Development, FactoryGameSteam Win64 Shipping/Cook und Multiplayer/DS laufe im lokale Projekt. `verify.sh --build-all` startet echte Buildprozäss und übernimmt ihre Exitcodes. Es fehlends Build gilt nöd als Erfolg. Alpakit-Aufruf stammt us em bereitgstellte Log vom 04.10.2026, 18:05:27 UTC.

## Inventar-Crashfix ab r16

Leeri Slots lösend kei `GetSlotSizeForItem`-Aufruf us. De Getter wird nur für belegti Slots mit gültiger Itemklasse und `&Stack.Item` benutzt. Bi ungültigem Leseergebnis, negativer Anzahl oder fehlender Kapazität isch d Waggon-Beobachtig ungültig. Leeri Slots, au mit Filter oder unbekannter Sperri, werded konservativ als nöd voll behandelt.

## Docking-Lebenszyklus ab r17

`StartDocking` liefert de physischi Bahnhof und d Lok. Vor em native Aufruf merkt sich PTC d passendi Stopp-ID; im After-Teil wird s native Resultat protokolliert. De Regel-Getter ändert nur d usgähni Regelkopie, erzeugt aber kei Session. `OnDocked` bindet d Session an de echte Bahnhof und startet de Timer. De After-Teil vo `StartDocking` darf d Bestätigung wiederhole, aber de Timer nöd zruggsetze.

`UpdateSessions` verwendet `mDockedAtStation` und d gspeichereti Stopp-ID. De aktuelle Fahrplanindex isch kei Abbruchbedingig meh. En Stationswechsel bindet neu, ohni de fremdi Dock abzbreche. Timeout, erfüllti Bedingige, manuell Freigab oder tatsächlech deaktivierti/entfernti Regle chönd de eigene Halt freigäh. E native Abbruchafrag wird respektiert.

## Teilladige ab r18

De lange UND-Timer verhindert d Abfahrt, aber cha au de native Ladestart blockiere: `FullyLoadUnload` wartet uf gnueg Ware/freie Kapazität für e Totalübertragig. r18 belässt d Regel und setzt s im SDK dokumentierte `mIgnoreTotalTransferRequirement` nach de native `EvaluateRuleSet`-Uuswärtig. De Hook isch uf en aktive `UpdateDockingSequence`-Aufruf begrenzt; en Scope stellt de native Wert am Schluss wieder her. Vor ere wiederholte Uuswärtig wird zerscht de letzte native Wert wiederhergstellt, damit PTC sin eigene Schalter nöd als native Vorgab übernimmt.

`ControlsCargo` prüeft bestätigti Session, echte Station, Stop-ID, Regle, Serverautorität und native Abbruchstatus ohni e neui Session z erstelle. Zusätzlich prüeft de Cargo-Adapter d temporäri PTC-Regel und de Abbruchstatus vo de Plattform. Kei Änderung vo `mCanLoadAny`, `mCanUnloadAny`, `mCanDoTotalTransfer`, Inventar, Itemfilter oder Ladezustand. Kei direkti Transfer-/Animationsufrüef. Friend-Zuegriff via AccessTransformers; virtuelle Update-Methode mit `SUBSCRIBE_UOBJECT_METHOD`, private nödvirtuelli Evaluationsmethode mit `SUBSCRIBE_METHOD`.

S Benutzerlog vo r17 bestätigt de Halt, aber enthält kei Plattformstatus. De Schluss uf d Startbarriere isch e headergstützti Diagnose; de tatsächlechi Ladestart und wiederholti Teiltransfers sind für r18 no im Spiel z prüefe.

## Phasenbegrenzig ab r19

De Start-Bypass gilt nur bi `ETPDS_WaitingToStart` oder `ETPDS_WaitForTransferCondition`. Bi Loading, Unloading, WaitingForTransfer, Complete, IdleWaitForTime und None wird de native Wert nöd verändert. Das trennt d Erlaubnis für e Teilladig vo de Abschlussprüefig. D r18-Laufzit het 2 → 4 → 5 → 7 zeigt, danach trotz relevantem Material kei zweite Ladig. D neui Begrenzig isch in alle Phase isoliert prüeft; de native Wiederholigsablauf isch no im Spiel z bestätige.

## Abbruch-Lebenszyklus ab r20

E Session speicheret `NativeCancelSeenClear`. Isch s native Abbruch-Flag bim Start bereits wahr, wird dä Wert als Baseline behandelt. En späteres false schaltet d Flanke-Erkennig frei; s nöchste true cha d Session freigäh. Die Flanke isch nume en Fallback. Tatsächlechi Abbruchufrüef an `AFGTrain` oder `AFGBuildableRailroadStation` werded vor em Originalufruef erfasst, markiered d Session sofort als Releasing und lönd s Original unverändert laufe. De Kontext vo `StartDocking` merkt sich au früehi Abbruchufrüef vor de Session-Bestätigung. D bestehendi Speicherlogik erhält laufendi Freigabe über `SavedWaits.Releasing`.

D Cargo-Berechtigung verwendet dieselbi Session-Baseline. En gsetzts Abbruch-Flag vo de einzelne Cargo-Plattform wird wiiter respektiert und jetzt au protokolliert. Das r19-Log belegt s früehe Abschalte dur de Poller, aber nöd de Ursprung vom native Flag. r20 löscht kei native Abbruchzuständ.

## Gegesitigi Abfahrt ab r21

`FPTCRule` ergänzt `SyncEnabled`, `SyncTrainId`, `SyncStopId` und `SyncTimeoutSeconds` als SaveGame-Fälder. SchemaVersion wird uf 2 gsetzt; fehlendi Fälder us alte Saves bliebed ungekoppelt. D IDs verwiised uf bestehendi persistierti Train-/Stop-Records. Kei Rohzeiger chömed über de Picker-RPC.

`SaveRule` validiert die eigene und d erwarteti Partnerrevision, d aktivi Partnerregel, verschiedeni Züg/Statione und allfälligi bestehendi Kopplige. Erst danach löst er e alti Gegenverknüpfig und schreibt s neue Paar in einere Serveraktion. Beidi Revisione werded erhöht. Beim Trenne bleibt d restlichi Partnerregel unverändert.

`SyncState` prüeft Live-Session, tatsächlechi Station, exakti Stopp-ID, beide Regle, Bestand, Minimum und Abbruchstatus. Es git kei zwüschegspeicherete Bereitschaft. `UpdateSessions` verwendet für verknüpfti Halt die Barriere statt em normale Timeout. Sind beidi bereit, setzt `TrySyncDeparture` **zerscht beidi Sessions uf Releasing**, denn ruft er beidi native CancelDockingSequence-Ufrüef i de gliiche Serverrunde uf. Native Rückrüef chönd Sessions sofort entferne; nach em erste Ufruef werde kei Session-Zeiger meh dereferenziert. Animatione und Signäl bliibed im Spiel kontrolliert.

Notfall 0 wartet unbegrenzt. En explizite Notfall-Timeout isch pro Session elapsed und git nume dä Zug frei. Manuell/native Freigab bleibt individuell. E fehlende/ungültige/nöd gegesitig verknüpfte Partner verhindert die gemeinsame Freigab. E ungültig wordeni eigene Regel behaltet s bisherige native Freigabverhalte. Bereits laufendi Freigabe aus SavedWaits werded neu aagforderet und zähled nie als Partnerbereitschaft.

D Partneruswahl scannt d Züg nume uf RPC-Aafrag, paginiert bis 40 Endpunkt pro Antwort und besitzt en eigene Rate-Limiter. S UI zeigt d neue Einstellige im rechte Scrollbereich. DE/EN gilt au für Status, Suechi, Timer und Konflikt. Es paarwiises Setup gilt für ein Haltpaar; d Rückrichtig wird separat gekoppelt.

## Idle-Wiederaufnahme ab r22

De r21-Laufzitbeleg zeigt, dass d Phasenbegrenzig allei nöd längt: nach ere Teilladig bleibt d Plattform in IdleWaitForTime, obwohl Ladepotenzial besteht. `RearmIdle` lauft vor em Original-Update und nume für verwalteti Cargo-Plattforme. En ephemeri Weak-Map begrenzt d Wiederprüefig uf höchstens 1 Hz und verlangt zuerst 1 s Idle-Beobachtig. D Map wird bi andere Phase/Freigab abgruumt und nöd persistiert.

Nach Strom-/Standby-/Animation-/Transfer-/Sichtbarkeitstimer-Prüefige rüeft de Adapter `EvaluateRuleSet`, `EvaluateFreightInventoryStatus` und richtungsabhängig `UpdateLoadSettings`/`UpdateUnloadSettings` uf. Filter und Live-Kapazität müend en weitere Transfer erlaube; Freigab/Abbruch wird danach nochmals prüeft. De Adapter löscht d alte Idle-/Sequenz-Timer und setzt nume de Bereitschaftsstatus WaitingToStart. De originale Update-Ufruef erfolgt genau einisch und übernimmt d native Sequenz. Kei direkte Inventaränderig, kei NotifyTrainDocked-Wiederholig, kei direkte Blueprint-Animationsufrüef, kei Reset vom PTC-Halt-Timer.

D native Sequenz-/Animationsimplementierig fehlt im SDK-Export. De gschützte Wiedereinstieg isch darum e Testkorrektur mit explizitem Ingame-Gate; isolierti Tests bestätiged kei native Timer-/Animationswirkung.
