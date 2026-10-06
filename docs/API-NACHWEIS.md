# 1.0.0 — SML-Icon

`UModLoadingLibrary` isch en `UGameInstanceSubsystem` (SML3.12.0). `LoadModIconTexture(const FString&, UTexture2D*)` ladet s gecachte Plugin-Icon us `Resources/Icon128.png`; `UModIconStorage` hält d Textur. UPTCWidget ergänzt e transiente UPROPERTY-Referenz und en FSlateBrush, serverseitig wird nöd glade. D Datei wird über `[StageSettings] +AdditionalNonUSFDirectories=Resources` i `Config/PluginSettings.ini` mitpackt, wie i de offizielle Alpakit-Iconanleitig. D API isch im mitglieferte SDK kontrolliert; kein nativer Build hie.

https://docs.ficsit.app/satisfactory-modding/latest/Development/BeginnersGuide/Adding_Ingame_Mod_Icon.html

---

# r31 Grafik-APIs

Native FSlateRoundedBoxBrush (Radius, Füllfarb, Randfarb/Randbreiti und Bildgrösse), SBorder BorderImage-Attribut und SProgressBar FillColorAndOpacity als FSlateColor. Öffentlechi Epic-API-Referenze: https://dev.epicgames.com/documentation/unreal-engine/API/Runtime/SlateCore/FSlateRoundedBoxBrush und https://dev.epicgames.com/documentation/unreal-engine/API/Runtime/Slate/SProgressBar/FArguments . Kei lokal installierte Engine-Header; echter Build no offe.

---

# r30 — Formatvertrag us em native Compilerlog

Eingefügter Text(2).txt zeigt d echte installierte Signatur in UnrealString.h.inl: FString::Printf erwartet UE::Core::TCheckedFormatString<FmtCharType, Types...>. De zur Laufziit erzeugti const-char16_t*-Vorlage us Tr(...).ToString() passt nöd. r30 verwendet an jeder betroffene Stelle direkte TEXT-Literale; d Sprachwahl passiert erst nach em Formatieren. Keine PrintfImpl-Umschaltig oder Usschalte vo Formatwarnige nötig.

Elf Formatfehler plus en davon abhängige Slate-Text_Lambda-Typfehler. r29-UHT: laut Userlog erfolgreich; r29-FactoryEditor-C++: abbroche; Win64/Cook: nöd erreicht. r30-native Ergebnisse sind no nöd vorhanden.

---

# Historische Dokumentation bis r29

# API-Ergänzig r29

SDK-lokal bestätigt:

- FGRecipeManager.h: öffentlichs statisches AFGRecipeManager::Get(UWorld*) und GetAllItemDescriptors() const liefert Descriptor-Klassen für d suchbari Itemuswahl. Zusätzlich aktuell transportierti und im Entwurf selektierti Items. Lokali Liste, kei Asset-Registry-Scan oder synchrones Asset-Lade pro Poll.
- Resources/FGItemDescriptor.h: statisch GetItemName(TSubclassOf<UFGItemDescriptor>) und GetForm(...). UI-Name in Clientsprach; Amount wird serverseitig uf RF_SOLID beschränkt.
- Bereits verwendeti Inventar-Stack-/Slotmethoden liefern reale NumItems und Descriptoridentität. Neu aggregiert PTC die Werte ohne Inventarschriibzugriff.
- Neue USTRUCTs/UENUMs und RCOs sind modintern, kei erfundeni Game-API. SaveGame-Migration, serialisierti Klassenreferenze, Reliable-RPCs und Slate-Lambdabindige müend im echten Unreal-Build/Spiel bestätigt werde.

SDK-Header sind im Paket nöd mitverteilt. Kein nativer Engine-/FactoryGame-Build hie vorhanden.

---

# Historische Dokumentation bis r28

# API-Ergänzig r28

- `FGBuildableTrainPlatformCargo.h`: privats nichtvirtuells `TransferInventory(UFGInventoryComponent*, UFGInventoryComponent*)`; rein beobachtende SUBSCRIBE_METHOD-Scope, genau ein Originalufruef. De vorhandeni Friend-Transformer erlaubt de Zuegriff.
- Öffentlechi virtuelle `CancelDockingSequence()` und `Undock()` erhalted symmetrisch registrierti/entfernti UObject-Hooks zum Bereinige vor em Originalufruef.
- De Header beschreibt `mShouldExecuteLoadOrUnload` als Signal für en späteri Factory-Tick-Übertragig. r28 hookt Factory_Tick nöd und fabriziert kei pending-Flag.
- `FGInventoryComponent::GetNumItems(TSubclassOf<UFGItemDescriptor>)` erlaubt laut Header nullptr für alli Items. Nur Bestanddiagnose im native Transferhook, kei Session-/Map-Zuegriff in dem möglicherweise im Factory-Tick laufende Hook.
- `FPTCWagonRule.MinimumFillPercent` isch es additives SaveGame-int32 mit Default 100. Vorhandeni vollständigi USTRUCT-Save-/Detail-RPCs tragged s Feld; native Serialisierig/Reflection/Netzwerk muess im Spiel verifiziert werde. Slate nutzt de bereits verwendeti SSpinBox mit int32 und Bereich 1–100.

Native Reihenfolge und interne Verwendung vo de Bereitschaftsflags sind ohni Implementierig nöd bewiese. Compiler-/Link-Kompatibilität, Savegame-Migration und tatsächlechs Transferverhalte sind offeni Build-/Spielgates.

---

# Historische Dokumentation bis r27

# Zusätzliche API-Nachwiis r27

Bereits im SDK-Export vorhanden, kei Änderung an Game-Header:

- `FGInventoryComponent.h`: `FInventoryItem::HasState()`, `IsItemAllowed(class,index) const`, `GetRelevantStackIndexes(TArray<TSubclassOf<UFGItemDescriptor>>, stackLimit=-1, sortResult=false)`, `HasEnoughSpaceForStack(const FInventoryStack&) const`. De Header beschreibt die letzti Methode als Inventar-/Stapelplatzprüefig; d Mengenberechnig wird nöd selber als native Implementation verkauft.
- `FGFreightWagon.h`: `GetFreightCargoType()`, Standard/Liquid-Enum und öffentlechs `GetFreightInventory()`.
- `FGBuildableTrainPlatformCargo.h`: mFreightCargoType, mLoadItemFilter, mCanLoadAny, mCanDoTotalTransfer. De bestehendi Friend-Transformer deckt die Member ab. mIsFullLoad bezeichnet en neue Container uf eme leere Wage, nöd d vollständigi Auffüllbarkeit. r27 verändert dä Animationswert nöd.
- `APTCSubsystem::CargoVisitStarted` isch e neui rein lesendi interne PTC-Methode, kei erfundeni Game-API. Sie nutzt d bestehendi bestätigti physischi Session.

Filtersemantik wird em native GetRelevantStackIndexes überlah. D Testdoubles modelliered leere Filter als alle Items und konkrete Filter als Descriptorliste; de exportiert Header enthält kei Implementation, drum isch das Modell kei Nachwiis fürs Spiel. Negative native Inventarantwort blockiert d Korrektur. r27 testet neu explizit native canLoad=false trotz korrigiertem Voll-Cache.

Tatsächliche Compiler-/Link-Kompatibilität mit em installierte SDK und tatsächliche Transferausfüehrig müend im Unreal-/Spieltest bestätigt werde.

---

# Historische Dokumentation bis r26

# API-Ergänzig r26

SDK FGBuildableTrainPlatformCargo.h beschreibt UpdateUnloadSettings als Prüefig, ob Waggoninhalt ins Plattforminventar passt, und mCanDoTotalTransfer als ganze Wage fülle oder ganz leere. r26 nutzt die vorhandene Methode und de vorhandene Friend-Zuegang; zusätzlich SUBSCRIBE_METHOD/UNSUBSCRIBE_METHOD uf UpdateUnloadSettings. De scoped Start-Veto gilt jetzt au für mCanUnloadAny. Kein SDK-Patch und kei direkter Inventartransfer.

Die genaue native Kapazitäts-/Filterimplementierig isch nöd im Header enthalten. r26 wartet uf s native Totaltransfer-Signal und fabriziert kei Bereitschaft. De neue r25-Spielbeleg widerleit d Annahm, dass temporär mIsFreightFull=false alleinig d Top-up-Bereitschaft wieder aktiviert; d tatsächlechi Ablehnig bi rund 99 % bleibt unglöst. D Adaptertests prüefed Codepfäd gegen Ersatz-APIs, nöd die ausgeliefereti FactoryGame-Implementierig.

---

# API-Ergänzig r25

Kei neue SDK-Deklaration nötig. Vorhandeni EvaluateFreightInventoryStatus (privat/nödvirtuell) erhält jetzt zusätzlich SUBSCRIBE_METHOD/UNSUBSCRIBE_METHOD; de bestehendi Friend FPTCCargoHooks deckt s ab. mIsFreightFull wird nur im laufende Bereitschafts-Scope korrigiert und wiederhergstellt. AFGFreightWagon::GetFreightInventory plus de unveränderti APTCSubsystem::Inspect liefern d exakti Beobachtig.

SDK-Header beschreibt mIsFreightFull als Vollstatus, aber enthält kei Implementierig für dessen Berechnig. D Abwiichig zum exakte 98-%-Inventar isch dur Log/UI belegt; wie s Spiel intern «voll» bestimmt, wird nöd als bekannte Tatsache behauptet. De Test modelliert, dass native Ladebereitschaft dä Cache abfragt. Native Hook-Ausfüehrig, Kapazitätsberechnig, UHT/Linking und tatsächlechs Nachlade sind hie nöd testet.

---

# Zusätzliche API-Nachwiis r24

Im vorhandene SDK `Source/FactoryGame/Public/Buildables/FGBuildableTrainPlatformCargo.h`:

- Öffentlichs `GetInventory()` liefert d Plattform-Inventarkomponente. PTC nutzt dä Getter, kei private Inventarzuweisig.
- De Header beschreibt `mCanDoTotalTransfer` als Fähigkeit, de ganze Wage z fülle oder z leere. PTC nutzt dä nativ berechnete Wert für d Restmengi statt eigener Item-/Slot-Simulation.
- `UpdateLoadSettings()` isch privat/nödvirtuell; de bestehendi Friend-Transformer erlaubt jetzt zusätzlich en `SUBSCRIBE_METHOD`-Hook mit symmetrischem Unsubscribe. Kei neui SDK-Änderig.
- `mCanLoadAny`, `mCanDoTotalTransfer` und `mIgnoreTotalTransferRequirement` sind vorhandeni Bitfelder. r24 cha sie ausschliesslich im Start-Scope restriktiv sperre und stellt sie wieder her; keine positive erfundeni Bereitschaft.

`FGInventoryComponent.h` liefert GetSizeLinear, GetStackFromIndex und GetSlotSizeForItem(index, itemClass, &stack.Item). Leeri/ungültigi Items werde vor em Kapazitätsufruef abgwise.

D Headerdokumentation isch de Nachwiis für d Semantik, nöd en native Ausfüehrigstest. Insbesondere d FactoryGame-Implementierig vo de Mänge-/Filterberechnig und d Animatione sind im Export nöd enthalten. Native UHT/Slate/Hook-Linkage sind im lokale Projekt z prüefe. Additivi SaveGame-Fälder und Detail-/Save-RPCs sind quellseitig ergänzt; native Persistenz/Netzwerk bleibt es Spieltest-Gate.

---

# Historische API-Nachwiis bis r23

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

# Prüefti Schnittstelle

Autorität: `PFT-SDK-Context-EChVepAh.tar.gz`, enthält SML 3.12.0. Die Pfad sind relativ zum Projekt. D Original-Header werded nöd im Testpaket wiiterverteilt.

| Zweck | Vorhandeni Datei | Gnutzti API |
|---|---|---|
| Chat | Mods/SML/Source/SML/Public/Command/ChatCommandInstance.h | CommandName, Aliases, bOnlyUsableByPlayer, ExecuteCommand_Implementation |
| Spieler | Mods/SML/Source/SML/Public/Command/CommandSender.h | IsPlayerSender, GetPlayer |
| RCO | Source/FactoryGame/Public/FGRemoteCallObject.h | GetOwnerPlayerController, Netzwerkfunktione über Outer |
| Registrierig | Mods/SML/Source/SML/Public/Module/GameInstanceModule.h | RemoteCallObjects |
| Registrierig | Mods/SML/Source/SML/Public/Module/GameWorldModule.h | mChatCommands, ModSubsystems |
| Server | Mods/SML/Source/SML/Public/Subsystem/ModSubsystem.h | SpawnOnServer |
| Server | Mods/SML/Source/SML/Public/Subsystem/SubsystemActorManager.h | GetSubsystemActor |
| UI | Source/FactoryGame/Public/UI/FGInteractWidget.h | Input-Sperrflags, SetInputMode, OnEscapePressed |
| UI | Source/FactoryGame/Public/UI/FGGameUI.h | GetInteractWidgetOfClass, PopWidget, RemoveInteractWidget |
| UI | Source/FactoryGame/Public/FGHUD.h | OpenInteractUI |
| Zug | Source/FactoryGame/Public/FGRailroadSubsystem.h | GetAllTrains, TTrainIterator |
| Zug | Source/FactoryGame/Public/FGTrain.h | GetTimeTable, IsSelfDrivingEnabled, IsDocked, OnDocked, OnDockingComplete, GetDockingRuleSetForCurrentStop, CancelDockingSequence |
| Fahrplan | Source/FactoryGame/Public/FGRailroadTimeTable.h | GetStops, GetCurrentStop, SetStops, AddStop, RemoveStop; FTimeTableStop het kei GUID |
| Bahnhof | Source/FactoryGame/Public/FGTrainStationIdentifier.h | GetStationName, GetStation (serverseitig) |
| Waggon | Source/FactoryGame/Public/FGFreightWagon.h | GetFreightInventory, GetFreightCargoType |
| Inventar | Source/FactoryGame/Public/FGInventoryComponent.h | GetStackFromIndex (Rückgab prüeft), GetSizeLinear, GetSlotSizeForItem (nur mit gültigem belegtem Item) |
| Persistenz | Source/FactoryGame/Public/FGSaveInterface.h | ShouldSave, NeedTransform, GatherDependencies, PreSaveGame |
| Hooks | Mods/SML/Source/SML/Public/Patching/NativeHookManager.h | SUBSCRIBE_METHOD_AFTER, UNSUBSCRIBE_METHOD |

Zusätzlich gläse: FGBuildableRailroadStation.h, FGBuildableTrainPlatform.h, FGBuildableTrainPlatformCargo.h. D private Plattform-State-Machine wird nöd überschriebe. D offizielle SML-Hook-Dokumentation bestätigt d Const-/After-Hook-Signature und d Usschluss-Regel im Editor: https://docs.ficsit.app/satisfactory-modding/latest/Development/Cpp/hooking.html .

**Das isch en Header-/Quellcode-Nachwiis, kei Compilerbestätigung.** D eigentliche FactoryGame-Implementierige, Game-UI-Blueprints und Unreal-Engine-Header ligged hie nöd vor. Besonders d temporäri Docking-Wartebedingig und s native Menü-Push/Pop bruuched de Build plus Laufzittest.

## r17 — zusätzlich verwendeti SDK-Deklaratione

- `FGBuildableRailroadStation.h`: `bool StartDocking(AFGLocomotive*, float)` und `GetDockedTrainRuleSet()`; de Hook ruft s Original genau einisch uf.
- `FGTrain.h`: öffentlichs `mDockedAtStation` unter `public: //@todo-trains private`, plus `IsDockingCancelRequested()`.
- `NativeHookManager.h`: de Before-Scope cha explizit ufg'ruefe werde und liefert bi bool-Funktione s Resultat zrugg.

## r18 — native Teilladig-Schalter

- `Buildables/FGBuildableTrainPlatformCargo.h`: `UpdateDockingSequence()` virtuell, `EvaluateRuleSet()` privat/nödvirtuell; `mIgnoreTotalTransferRequirement` umgaht laut Header s Warte uf e Totalübertragig bim Ladestart.
- `Buildables/FGBuildableTrainPlatform.h`: `mStationDockingMaster`, `GetDockingStatus()` und `IsDockingCancelled()`; Station und Status werded nume gläse.
- `NativeHookManager.h`: `SUBSCRIBE_UOBJECT_METHOD`, `SUBSCRIBE_METHOD`, passendi Unsubscribe-Makros. De Scope ruft s Original einisch uf.
- Offizielli Access-Transformer-Dokumentation: https://docs.ficsit.app/satisfactory-modding/latest/Development/ModLoader/AccessTransformers.html . `Config/AccessTransformers.ini` enthält en `Friend` für `FPTCCargoHooks`; de Timestamp wird bim Installiere erneueret, wil UHT druf reagiert. Kei manuelle Game-Headeränderig.

D C++-Fixture kompiliert au de Zuegriff uf privat/protected Member über e simulierti Friend-Deklaration. Sie ersetzt kei UHT-Prüefig oder ABI-/Link-Prüefig mit em tatsächliche SDK.

## r19 — Phase und Diagnose

`ETrainPlatformDockingStatus` im bereits verwendete `FGBuildableTrainPlatform.h` definiert None=0, WaitingToStart=1, Loading=2, Unloading=3, WaitingForTransfer=4, Complete=5, WaitForTransferCondition=6, IdleWaitForTime=7. De Adapter aktiviert de Teilladig-Schalter ausschliesslich i Phase 1 und 6. `mIsFreightFull` und `mIsFreightEmpty` us em Cargo-Header werded nur für Diagnose gläse. Kei zusätzliche Game-API und kei neue Friend-Deklaration.

## r20 — Abbruchereignis

- `FGTrain.h`: öffentlichs nödvirtuells `CancelDockingSequence()` und `IsDockingCancelRequested()`.
- `FGBuildableRailroadStation.h`: öffentlichs virtuelles `CancelDockingSequence()`; `SUBSCRIBE_UOBJECT_METHOD` erfasst die native Implementierig.
- `FGBuildableTrainPlatform.h`: öffentlechs `IsDockingCancelled()` für Bahnhof und Cargo-Plattform. Native Abbruchflags werded ausschliesslich gläse.
- Beidi neue Hooks rüefed de native Scope genau einisch uf; kei Override oder Cancel vom Hook.

## r21 — Züg synchronisiere

Kei neui native Zug-/Cargo-API und kei neue AccessTransformer. Paarlogik nutzt die bereits belegte Train-/Station-/Inventar-Getter und CancelDockingSequence. Neue interne Fälder sind UPROPERTY(SaveGame); Partnerkatalog und Revisionsprüefig sind gezielti RCO-RPCs. D UI ergänzt SComboButton mit paginiertem Suechmenü; Engine-Slate-Header/UHT sind hie nöd vorhanden, drum bleibt de lokale Unreal-Build verbindlich.

## r22 — Beleg für d Idle-Wiederaufnahme

Im bereitgstellte SDK enthält `FGBuildableTrainPlatformCargo.h` d private native Methode EvaluateRuleSet, EvaluateFreightInventoryStatus, UpdateLoadSettings, UpdateUnloadSettings und IsLoadUnloadBlockedByNoneFilter. IsLoadUnloading/GetIsInLoadMode sind öffentlechi Getter. mShouldExecuteLoadOrUnload schützt en no usstehende Transfer; mSwapCargoVisibilityTimerHandle schützt de sichtbare Containerwechsel. `FGBuildableFactory.h` liefert HasPower/IsProductionPaused. `FGBuildableTrainPlatform.h` definiert IdleWaitForTime, WaitingToStart, mPlatformDockingStatus und d Idle-/Sequenz-Timer als gschützti Fälder. De bereits vorhandene Friend uf de Cargo-Klasse deckt die Zuegriff ab; kei SDK-Headeränderig.

Native Implementatione sind nöd im Export. Vor em Original-Update wird nur de Start-Prüefstatus wiederhergstellt. TimerManager und NativeHookManager API-Nutzig mues im echte Unreal-Build bestätigt werde. Kei Beleg behauptet, dass e echte zweite Animation scho testet isch.
