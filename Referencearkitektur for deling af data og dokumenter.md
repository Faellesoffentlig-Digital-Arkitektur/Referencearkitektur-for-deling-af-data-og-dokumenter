# Referencearkitektur for deling af data og dokumenter

## Forord

Hverdagen er digital, og data om borgere, virksomheder, myndigheder, ejendomme, steder, køretøjer m.m. vedligeholdes på en lang række områder af den offentlige administration. Der ligger et stort potentiale i at gøre sådanne data tilgængelige for genbrug, så de kan skabe værdi i flere sammenhænge. Deling af data er et fundament for bedre understøttelse af tværgående, offentlige services, og åbner for anvendelse af data i nye og innovative sammenhænge.

Deling af data kan være teknisk kompliceret og i mange tilfælde omkostningstungt. Herudover er deling af data altid underlagt en række lovmæssige og organisatoriske krav, der synligt og til fulde skal opfyldes for at bevare borgeres og virksomheders tillid til datadeling i det offentlige Danmark. Dette øger kompleksiteten i it-løsningerne og er dermed blandt årsagerne til, at potentialet i deling og genbrug af data endnu ikke er indfriet i det omfang, det er muligt.

Denne referencearkitekturs formål er at hjælpe med at indfri dette potentiale. Dette gøres ved at introducere en fælles beskrivelse af de begreber og sammenhænge, der er væsentlige for at forstå og arbejde med design og implementering af løsninger, der involverer deling af data og dokumenter. Dette sker både på det strategiske plan, hvor vision, mål og arkitektoniske principper fastlægges; på det forretnings- mæssige plan, hvor de typiske brugsscenarier beskrives; og på det tekniske plan, hvor en række implementerings- og integrationsmønstre angiver, hvordan man i og mellem applikationer kan dele og forsende data. Endelig peger referencearkitekturen på en række konkrete specifikationer, der anvendes ved deling af data og dokumenter i dag i den offentlige sektor.

Referencearkitekturen er udarbejdet under Den fællesoffentlige digitaliseringsstrategi 2016-2020 og skal som sådan anvendes i alle projekter, der sorterer under digitaliseringsstrategien. Referencearkitekturen er dermed relevant for såvel offentlige myndigheder, deres leverandører samt for virksomheder, der ønsker at gøre brug af offentlige data.

## Resume

Denne referencearkitektur anvender generelt begrebet _videregivelse_ frem for _deling_ af data. _Videregivelse_ fokuserer på den faktiske delingshandling – der, hvor data konkret gives videre. _Deling_ har en bredere betydning, der fx dækker at udstille data for at gøre dem potentielt tilgængelige for genbrug, uanset at dette måske aldrig sker.

Vi introducerer ikke en specifik og isoleret definition af _data_ – vi regner med, at læseren har en god fornemmelse for, hvad data er, og det er i denne sammenhæng tilstrækkeligt. I forhold til dokumenter introducerer vi en modellering, der fremhæver, at et _dokument_ i bund og grund blot er en form for data. Som afledt konsekvens taler vi i denne referencearkitektur ikke om deling af "data og dokumenter", men blot om "data".

Et af hovedformålene med denne referencearkitektur er at vejlede i valget mellem de to grundlæggende forretningsmønstre for videregivelse af data:

* [_Videregivelse på forespørgsel_ – typisk via et API i system til system-integrationer](#351-videregivelse-på-forespørgsel)
* [_Videregivelse ved meddelelse_ indeholdende data (herunder dokumenter)](#352-videregivelse-ved-meddelelse) – typisk brugt ved beskeder til borgere/virksomheder, der skal have retsvirkning, men også et klassisk mønster brugt i system til system-integrationer.

Den fundamentale forskel på disse to scenarier er, om det er den aktør, der _videregiver_ data eller den aktør, der _modtager_ data, der er ansvarlig for den konkrete sagsgang eller det konkrete procesforløb, som videregivelsen af data indgår i.

Ved videregivelse på forespørgsel er den dataansvarlige som udgangspunkt ikke bekendt med modtage- rens anvendelse men er naturligvis forpligtet til at håndhæve relevant hjemmel. Et eksempel på dette er en myndigheds forespørgsel på personoplysninger i CPR-registeret.

Ved videregivelse ved meddelelse er det afsenderen, der i en given kontekst afsender en meddelelse med et givent formål – typisk som led i afviklingen af en arbejdsgang, der enten kan være manuel eller automatiseret. Et eksempel på dette er politiets fremsendelse af en fartbøde til en borger.

Figur 1 opsummerer denne referencearkitekturs væsentligste elementer. [Afsnit 3 Forretningsarkitektur](#3-forretningsarkitektur) beskriver de to forretningsmønstre i yderligere detaljer. For hvert forretningsmønster er der tre mulige implementeringsmønstre. Disse foldes ud i [afsnit 4 Teknisk arkitektur](#4-teknisk-arkitektur), der også udpeger de gennemgående integrationssnitflader, der er kandidater til standardisering.

![Figur1](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur1.jpg)

Figur 1 : Oversigt over de væsentligste mønstre i referencearkitektur for deling af data og dokumenter – to generiske forretningsprocesmønstre med hver tre forskellige tekniske implementeringsmønstre.

## Executive summary

This reference architecture revolves around describing _disclosure of data by transmission_ (Danish: videregivelse af data). _Disclosure by transmission_ focuses on the actual action of passing on data whereas _sharing_ (Danish: deling) of data has a broader interpretation that includes making data available for potential reuse, even if the data may never be accessed.

We do not introduce a specific, isolated definition of _data._ We assume that the reader already has an intuitive notion of what data is which is sufficient in this context. Regarding documents, a modelling is introduced to point out how a _document_ is, basically, just data. Consequently, we will not speak of sharing “data and documents” but only speak of “data”.

A main purpose of this reference architecture is to guide and assist in the choice between two funda- mental business patterns for disclosure of data by transmission:

* [_Transmission on request_](#351-videregivelse-på-forespørgsel) – typically, system-to-system integrations using an API
* [_Transmission by message_](#352-videregivelse-ved-meddelelse) – typically used in legally binding communication of data (possibly in the form of documents) from public authorities to citizens and businesses, but also a classical pattern used in system to system integrations.

The fundamental difference between these two scenarios is whether it is the actor _transmitting_ data or the actor _receiving_ data who is responsible for the concrete process flow or the management of the concrete case in context of which data is transmitted.

For transmission on request, the data controller does not necessarily know the specific purpose for which the requesting party plans to use the data. The data controller must, however, enforce access to data by requesting that the requester has a proper legal basis that justifies the transmission of data. One example of this is when a public authority seeks information on a citizen in the CPR register.

When transmitting data by a message it is the sender who transmits data for a well-known and specific purpose, typically as part of a manual or automated workflow. An example of this pattern would be the police sending a speeding ticket to a citizen.

Figure 2 shows the central elements of this reference architecture. [Section 3 Forretningsarkitektur](#3-forretningsarkitektur) describes the two business patterns in further detail. Each business pattern may be implemented using one of three implementation patterns. These patterns are described in [Section 4 Teknisk arkitektur](#4-teknisk-arkitektur) which also points to the recurring integration interfaces that are candidates for standardization work.





![Figur2](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur2.jpg)

Figure 2 : Overview of the patterns described in this reference architecture – two generic business patterns, each with three distinct technical implementation patterns. 

## 1 Introduktion

### 1.1 Formål, anvendelse og målgruppe

Det overordnede formål med denne referencearkitektur er at understøtte offentlig digitalisering i regi af Den fællesoffentlige digitaliseringsstrategi 2016-2020. Derudover kan referencearkitekturen anvendes generelt i projekter i både offentlige og private digitaliseringsinitiativer.

Specifikt i sammenhæng med udmøntningen af den aktuelle strategi skal referencearkitekturen anvendes:

* som vejledning og reference i udarbejdelse af løsningsdesign, der involverer deling af data, særligt med henblik på valg af implementeringsmønstre, ud fra et ’følg eller forklar’-princip

* ved review af løsningsbeskrivelse

* som udgangspunkt for udarbejdelse af domænespecifikke referencearkitekturer for deling af data og dokumenter

* til at danne et fælles sprog til at formulere en fælles handlingsplan blandt digitaliserings-strategiens parter

Værdien på overordnet plan af denne referencearkitektur er, at den bidrager til at skabe sammenhængende, sikre og effektive digitale services for borgere og virksomheder ved at skabe rammer for større genbrug af data, hvilket bl.a. vil understøtte øget automatisering.

Dokumentet er primært målrettet it-arkitekter tilknyttet offentlige digitaliseringsprojekter, fx enterprisearkitekter, forretningsarkitekter og løsningsarkitekter, der har til opgave at kravspecificere og designe løsninger.

De første dele af dokumentet (Strategi og Forretningsmæssig arkitektur) henvender sig endvidere til projektledere og beslutningstagere, herunder forretningsansvarlige, digitaliseringschefer, it-chefer, afdelings- og kontorchefer og andre med rollen som systemejer.

Dokumentet i sin helhed er også relevant for nuværende og potentielle leverandører af offentlige it- løsninger.

### 1.2 Scope

Referencearkitektur for deling af data og dokumenter understøtter design, udvikling/indkøb og anvendelse af offentlige it-systemer, der videregiver eller modtager registrerede oplysninger i elektronisk form til/fra andre myndigheder, virksomheder og borgere.

Referencearkitekturen skrives på baggrund af Den fællesoffentlige digitaliseringsstrategi 2016-2020 under initiativ 8.1 med tilslutning fra FM, UFM, EVM, SIM, JM, EFKM, MBUL, SÆM, SKM, MFVM, BM, KL og Danske Regioner. Heri beskrives referencearkitekturen således:

For at operationalisere, hvilke krav hvidbogen konkret stiller til initiativer og systemer udarbejdes en referencearkitektur for deling af data og dokumenter, der blandt andet beskriver fælles behovsmønstre og mønstre for teknisk understøttelse, herunder de forskellige roller, der skal afklares i initiativerne. Referencearkitekturen udpeger også eventuelle områder for eksisterende og nye fælles standarder og infrastruktur, som skal lette initiativernes implementering. Referencearkitekturen bliver således en generel ramme og støtte for alle initiativernes egen specifikke arkitektur.

I et juridisk perspektiv er dette område reguleret af en lang række forordninger og love. Afsnit 2.5 opridser de relevante love og forordninger, der sætter de juridiske rammer for deling af data og dokumenter.

Scope for denne referencearkitektur er, som navnet angiver, selve delingen/videregivelsen af data (herunder persondata og evt. i form af dokumenter). Vi søger ikke at definere den bredere _anvendelse_ af data, herunder hvordan data registreres, eller hvordan den aktør (fx en myndighed), der afsender eller modtager data, benytter disse data i en konkret arbejdsgang. Processerne for registrering af data samt afsendelse og modtagelse af en meddelelse er dog summarisk beskrevet for at introducere begreber, der er relevante for at kunne tale om selve delingen/videregivelsen af data.

Specifikt er det uden for scope af denne referencearkitektur at definere:

* Anvendelse af data, herunder:
  * Registrering og intern anvendelse af data hos den dataansvarlige myndighed
  * Konteksten for en aktørs behov for at forespørge på data, videregive data via en meddelelse eller modtage data via en meddelelse
  * Sletning og arkivering af data styret af den dataansvarlige myndighed
* Streaming af data (videodata, IoT-data m.m.)
* Partsrepræsentation, hvor én aktør efter samtykke agerer på vegne af en anden
* Grænseoverskridende (cross-border) videregivelse af data

I forhold til streaming af data bemærker vi, at streaming løseligt kan beskrives som en seriel række af processen videregivelse på forespørgsel, som vi beskriver senere i dette dokument. Eventuelle, yderligere aspekter ved streaming, der kan være relevante at belyse i en referencearkitektur, er ikke inkluderet i denne referencearkitekturs nuværende version.

Partsrepræsentation er en generel problemstilling, der ikke er isoleret til deling af data og dokumenter. Problemstillingen vil derfor bliver behandlet andetsteds, fx i forbindelse med en revision af den fælles- offentlige referencearkitektur for brugerstyring.

I forhold til grænseoverskridende videregivelse af data er mandatet for denne referencearkitektur be- grænset til bestemte initiativer forankret hos de myndigheder, der er del af Den fællesoffentlige digitali- seringsstrategi 2016 - 2020. Mandatet rækker dermed ikke ud over landets grænser.

### 1.3 Centrale begreber

Vi vil i denne referencearkitektur ikke give en komplet udredning af forskelle og ligheder mellem begreberne _data_, _oplysning_ og _information_ , der bruges meget forskelligt på tværs af faggrupper og praksisser i den offentlige sektor. I stedet vil vi fokusere på en mere pragmatisk og lokal definition og holde os til data som generelt begreb.



![Figur3](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur3.jpg)

Figur 3 : Figuren beskriver, hvordan data opbevares i datasamlinger og videregives i form af meddelelser, samt at dokumenter er en særlig form for data. Denne referencearkitektur beskæftiger sig generelt med data som en samlende betegnelse for både data og dokumenter.

Figur 3 viser de centrale begreber i denne referencearkitektur, hvor data ikke overraskende ligger i midten. I afsnit 3 Forretningsarkitektur foldes begrebsmodelleringen yderligere ud, både i en diskussion af data og dokumenter samt i en overordnet model af forretningsobjekter og begreber, der er nødvendige for at beskrive videregivelse af data.

### 1.4 Tilblivelse og governance

Første udgave er udarbejdet i Kontor for Data og Arkitektur, Digitaliseringsstyrelsen med konsulentbistand fra Omnium Improvement.

I udarbejdelsen har en arbejdsgruppe af offentlige arkitekter bidraget gennem en række af workshops. I gruppen har deltaget repræsentanter fra følgende organisationer: Kommunernes Landsforening, Danske Regioner, Styrelsen for Dataforsyning og Effektivisering, Sundhedsdatastyrelsen, Styrelsen for Arbejdsmarked og Rekruttering, Miljø- og Fødevareministeriet, Styrelsen for It og Læring, Arbejdsmarkedets Tillægspension (ATP), SKAT, Erhvervsstyrelsen og Digitaliseringsstyrelsen.

Første udgave af referencearkitekturen godkendtes i version 1.0 i Styregruppe for Data og Arkitektur under Digitaliseringsstrategien i maj 2018. Styregruppen er herefter ejer af dokumentet, med Kontor for Data og Arkitektur som ansvarlig for vedligehold af referencearkitekturen frem til 2020 som en del af den Fællesoffentlige, Digitale Arkitektur.

### 1.5 Anvendt metode, notation og signaturforklaring

Metodemæssigt er referencearkitekturen udarbejdet inden for rammerne af Den fællesoffentlige digitale arkitektur og følger så vidt muligt den fælles skabelon for referencearkitekturer som udarbejdet i Sekre- tariatet for Styregruppen for Data og Arkitektur under digitaliseringsstrategien. Metoderammen bygger blandt andet på erfaringer fra OIO referencearkitektur, og indarbejder også elementer fra European Interoperability Reference Architecture (EIRA), The Open Group Architecture Framework (TOGAF), ArchiMate m.m.

I forhold til ejerskab af de elementer, der indgår i dokumentets figurer og definitioner, markerer:

* **Fed tekst (i rød)** : At et element eller en relation ejes og defineres i denne referencearkitekturs begrebsmodel
* Almindelig tekst (i blå): At et element eller en relation er kendt, men ejes og defineres et andet, nærmere angivet sted, fx i andre referencearkitektur eller i lovgivning.
* _Kursiv:_ At et element eller en relation er identificeret, men ikke nærmere defineret i denne referencearkitektur.

I dokumentets tekst markerer:

* Sans serif _:_ At et ord har en særlig betydning i denne referencearkitektur – jf. de tre markeringer af ejerskab ovenfor
* _Kursiv_ anvendes for betegnelser, der er hentet fra ArchiMate-begrebsapparatet.

Prefixet 'data-' kan være udeladt på begreber og elementer i tekst og figurer fx af formaterings- eller læsbarhedshensyn uden, at der ligger en indholdsmæssig skelnen bag (fx dataanvender/anvender, datasam- ling/samling o.a.)

I elementerne i dokumentets figurer angiver (med mindre anden betydning er angivet i figurteksten):

* Runde hjørner: et Procestrin ( _Business Functions_ )
* Skarpe hjørner: en Applikationsservice ( _Application Services_ )
* Pil med stiplet linje (fra Applikationsservice mod Procestrin): at en Applikationsservice helt eller delvist realiserer et Procestrin ( Realization Relation )
* "Slikkepind": en Snitflade ( _Application Interface_ )

### 1.6 Relation til rammearkitektur og andre referencearkitekturer

Denne grundlæggende referencearkitektur er del af rammearkitekturen i den samlede, fællesoffentlige digitale arkitektur (FDA). FDA-rammearkitekturen udfoldes i en række referencearkitekturer, som hver dækker et emnefelt og gensidigt supplerer hinanden. For en introduktion til og overblik over den sam- lede rammearkitektur samt relateret information henvises til arkitektur.digst.dk/rammearkitektur.

Denne referencearkitektur relaterer sig til en række andre referencearkitekturer, både eksisterende og planlagte. Specifikt gør referencearkitektur for deling af data og dokumenter brug af:

* Fællesoffentlig referencearkitektur for brugerstyring (del af FDA-rammearkitektur, version 1.0)

Den skal kunne anvendes af:

* Fællesoffentlig referencearkitektur for selvbetjening (del af FDA-rammearkitektur, godkendt i version 1.0 i regi af Initiativ 1.2 af Den fællesoffentlige digitaliseringsstrategi 2016-2020)
* Fællesoffentlig referencearkitektur for overblik over egne sager og ydelser (del af FDA-rammearkitektur, primo 2018 under udarbejdelse i regi af Initiativ 1.3 af Den fællesoffentlige digitaliserings- strategi 2016-2020)

... og indgår i kontekst sammen med:

* Referencearkitektur for sags- og dokumentområdet (OIO, 2008)
* Referencearkitektur for deling af dokumenter og billeder (National sundheds-it, 2012)
* Referencearkitektur for informationssikkerhed (National sundheds-it, 2013)
* Indberetning til registre på sundhedsområdet (under godkendelse pr. november 2017)

### 1.7 Læsevejledning

Dette dokument følger generelt skabelonen for referencearkitekturer under FDA-rammearkitekturen i Den fællesoffentlige digitaliseringsstrategi 2016-2020. Dokumentets afsnit 1 udgør en generel introduktion til referencearkitekturens formål, scope, de centrale begreber omkring deling af data og dokumenter, og beskriver konteksten for dokumentets anvendelse og tilblivelse.

[Afsnit 2 Strategi](#2-strategi) beskriver på det strategiske plan hvilke temaer, principper, love m.m., der sætter rammer og retning for denne referencearkitektur. Afsnittet beskriver visionen for deling af data og dokumenter og afdækker den værdi, som brug af referencearkitekturen forventes at skabe.

I [afsnit 3 Forretningsarkitektur](#3-forretningsarkitektur) beskrives forretningen i form af de grundlæggende use cases, roller og ansvar omkring videre- givelse af data. Begrebsmodellen, der fanger de termer, der introduceres i denne referencearkitektur, præsenteres også her.

[Afsnit 4 Teknisk arkitektur](#4-teknisk-arkitektur) beskriver den tekniske arkitektur i form af en række implementeringsmønstre for, hvordan deling af data kan implementeres. Ud fra mønstrene identificeres en række gennemgående integrationssnitflader, der leder op til en analyse af, hvor der er behov for standardisering.

Det er tilstræbt at bygge dokumentet op omkring enkle og relativt stramt definerede termer, der beskriver de centrale begreber omkring videregivelse af data og de mulige forretnings- og implementeringsmønstre. Definitionerne introduceres løbende gennem dokumentet og er endvidere opsamlet i [Bilag B: Ord- og begrebsliste](#62-bilag-b-ord--og-begrebsliste).

Videregivelse af data er en grundlæggende kapabilitet og kan dermed relateres til en lang række af konkrete anvendelser, teknologier og arkitekturstile. I dette dokument søger vi at holde beskrivelserne til den generiske begrebs- og funktionsmæssige kerne omkring videregivelse af data. Hvor det er relevant, indeholder dokumentet dog en række kortfattede ”kroge” for at fange relationer og referencer, der går ud over kernebeskrivelserne, uden dog at søge at give udtømmende detaljer eller definitioner.

## 2 Strategi

Dette afsnit introducerer visionen for deling af data og dokumenter med baggrund i identificerede temaer, principper, arkitekturregler og den forventede værdiskabelse.

### 2.1 Temaer

Referencearkitekturen udmønter og understøtter beslutninger i Den fællesoffentlige digitaliseringsstra- tegi 2016-2020. Strategien har tre, overordnede målsætninger:

* Det digitale skal være let, hurtigt og sikre god kvalitet
* Offentlig digitalisering skal give gode vilkår for vækst
* Tryghed og tillid skal i centrum

De tre målsætninger er understøttet af en række, specifikke initiativer, hvoraf _Initiativ 8.1: Gode data og effektiv datadeling_ er det konkrete ophæng for denne referencearkitektur.

Ved at kigge på tværs af initiativerne samt inddrage trends fra den digitale udvikling i samfundet i øvrigt kan man opridse en række forretningsmæssige og teknologiske temaer, der er relevante i forhold til at sætte retningen for den ønskelige arkitektur for datadeling:

* **Sammenhængende offentlige services** er et meget tydeligt, gennemgående tema. Den offentlige forvaltning ønsker at tilbyde borgere og virksomheder services, der ikke er tæt knyttet til enkelte myndigheder, men opleves som sammenhængende for dem, der anvender servicen. Mest tydeligt er det udtrykt i European Interoperability Frameworks koncept om integrated service delivery
* **Offentlige data skal deles og genbruges:** En øget deling af data giver mulighed for nye generationer af digitale løsninger, som i højere grad kan trække de nødvendige data automatisk. Det sparer tid for borgere og virksomheder, når de slipper for unødige indberetninger. Og det kan lette de administrative processer og sagsbehandling, når manuelle arbejdsgange og i nogle tilfælde afgørelser kan automatiseres.
* **Grænseoverskridende services:** I takt med, at de enkelte nationer udvider deres ambitioner for offentlig, digital service til borgere og virksomheder, stiger også behovet for at koordinere arkitektur og it-løsninger på tværs af landegrænser for dels at understøtte services, der i deres natur krydser grænser (fx arbejde eller ejerskab af fast ejendom i et andet land), men også for at standardisere og dermed undgå opbygning af nationale "siloer". EU er en aktiv spiller i at drive denne standardisering gennem initiativer som ISA^2 (EIF/EIRA m.m.), CEF Digital (eDelivery m.m.) samt forordninger som GDPR, eIDAS m.fl.
* **Øget skalerbarhed:** Der har de sidste 5-10 år været fokus på at få løsninger til at skalere forudsigeligt til web scale, ved hjælpe af teknologier som clustering og cloud. Der har medført et voldsomt løft af de ressourcer, der globalt set er blevet brugt på large-scale implementeringer. Nu er området så modent, at teknologierne også er tilgængelige for projekter på national skala og endda i enkeltprojekter.
* **Microservices:** En måde at håndtere den stigende kompleksitet i forvaltningen af it-landskaber er en udbredt strategi om at levere it-løsninger i mindre enheder, der kan idriftsættes og afvikles uafhængigt og/eller parallelt. Microservices er en sådan strategi.
* **Dataaktualitet:** Med henblik på automatisering og sammenhængende services er der fokus på at have kortest mulig tid mellem registrering og anvendelse af data. En ambitiøst mål er at digitale selvbetjening kan gennemføres i inden for 5-10 minutter, selvom de involverer ændringer i grundlæggende oplysninger hos flere myndigheder.
* **Suverænitet og beskyttelse mod cyberangreb** er et tema, som har været på dagsordenen længe, men har med regeringens cybersecurity-strategi fået en vægt og et fokus, der ikke er set tidligere. Tendensen udgør et større, strategisk skifte, som mindsker noget af den tillid, som tidligere har været vist store it-leverandører, og peger i retning af hjemtagning af centrale/kritiske/vitale funktioner som fx fysiske netværksforbindelser.
* **Øget opmærksomhed om behandling af personlige oplysninger:** Den europæiske forordning om beskyttelse af personoplysninger (GPDR) og tilhørende dansk implementering udvider den dataansvarliges risiko i forhold til tidligere. Det har ført til et fornyet fokus på overblik over behandling af persondata og tilsynet hermed.

Mange af disse temaer kan genfindes i en række aktuelle offentlige og politiske strategiarbejder, herunder sammenhængsreformen, den nationale cybersikkerhedsstrategi, kommunernes digitaliseringsstrategi "Lokal og Digital", Strategi for digital Sundhed 2018 - 2020 samt det europæiske rammeværk for inter- operabilitet (New European Interoperability Framework for European Public Services).

### 2.2 Strategiske principper

De strategiske principper, der ligger til grund for denne referencearkitektur, udspænder sig i et spændingsfelt. På den ene side åbner visionen om det datadrevne samfund, hvor data ses som et råstof for samfundsudviklingen, for en lang række muligheder og ønsker. På den anden side er deling og data også underlagt begrænsninger og indskrænkninger i lovgivning. Dette afsnit opridser de væsentligste principper i dette spændingsfelt.

På mulighedssiden er det en fundamental målsætning, at:

"_Det_ _digitale skal være let, hurtigt og sikre god kvalitet_" (kilde: Digitaliseringsstrategien)

Mere generisk kan man, med inspiration fra the European Interoperability Framework (EIF), fremhæve fire overordnede principper:

* **Interoperabilitet** princip om sammenhængende services og smidige brugerrejser på tværs af myndighedsskel
* **Once-only** princip om, at borger og virksomhed kun skal afgive den samme information til det offentlige én gang.
* **Gennemsigtighed** princip om, at borgere skal sikres indsigt i, hvilke personoplysninger der behandles af offentlige myndigheder og med hvilke formål.
* **Genbrug** princip om genbrug af it med henblik på lavere omkostninger

På begrænsningssiden er der også en række principper, der skal tages i agt. Nedenstående principper er hentet fra EUs databeskyttelsesforordning (GDPR) og er i vores sammenhæng dækkende uden behov for yderligere definition:

* **Lovlighed, rimelighed og gennemsigtighed**
* **Formålsbegrænsning** (undtaget er arkiver, forskning og statistiske formål)
* **Data-minimering**
* **Rigtighed** (urigtige data skal straks slettes eller berigtiges)
* **Opbevaringsbegrænsning** (data må ikke opbevares "for evigt")
* **Integritet** og **fortrolighed**
* **Ansvarlighed** (man skal kunne påvise, at ovenstående overholdes)

### 2.3 Vision

Visionen i denne referencearkitektur er at stræbe efter en situation, hvor:

Data er en fælles, værdifuld og velbeskyttet ressource, som er nem at dele og bruge, men svær at misbruge.

**Fælles** betyder, at data i videst muligt omfang (og ud fra _once only_ - princippet) betragtes som et fælles gode på tværs af myndigheder ud fra en betragtning om, at data, der registreres ét sted til ét formål, kan have stor værdi for andre myndigheder og virksomheder, der udbyder private tjenester.

**Værdifuld** betyder, at data, der er registeret i det offentlige, betragtes som et økonomisk og kvalitetsmæssigt aktiv på lige fod med kontantbeholdninger og fysiske ejendom.

**Velbeskyttet** betyder, at der er taget tilstrækkelige og effektive sikkerhedsmæssige tiltag til at beskytte borgere og virksomheders data og dermed deres tillid til, at opbevaring, anvendelse og videregivelse sker under gennemskuelige og retmæssige forhold.

**Nem at dele** betyder, at udgifterne ved at anvende data i en ny sammenhæng ikke alene løftes af den dataansvarlige myndighed, samt at der er tydelig vejledning i udarbejdelse af nødvendige aftaler.

**Nem at bruge** betyder, at der er fastlagte processer, _best practices_ og generiske infrastrukturelementer, der kan genbruges.

**Svær at misbruge** betyder, at enkeltpersoner, organisationer og fremmede magter, der måtte have til hensigt at bruge data uretmæssigt, begrænses mest muligt gennem en indsats, der står i forhold til truslerne og de mulige konsekvenser af misbrug.

Denne vision kræver, at en række forretningsevner i det offentlige forstærkes væsentligt, herunder:

* **Koordination af lovgivning** - handler om at der er enighed om centrale definitioner på tværs af flere ressortområder. Samt, at der er adgang til effektiv vejledning ved tvivl.
* **Aftaleindgåelse** kan tage lang tid og kræver meget arbejde. Bør kunne ske ved brug af generelle og eksisterende aftaler, så der ikke startes forfra, hver gang nye videregivelser skal etableres.
* **Identifikation og dokumentation af data** - sker allerede i ISO 27000-sammenhæng for den interne brug, men også behov for at dække, at data udstilles til andre.
* **Genbrug af løsninger** - sikrer, at vi kan lave hyppige udvidelser både af funktionalitet og anvendelsesområde.

### 2.4 Værdiskabelse

Værdien ved at følge denne referencearkitektur kan deles op i den direkte og indirekte værdiskabelse. Den direkte værdiskabelse opnås ved, at referencearkitekturen:

* Muliggør effektiv systemudvikling relateret til videregivelse af data, da den indskrænker udfaldsrummet for løsninger samt opsamler best practice
* Skaber juridisk værdi gennem designmæssig indlejring af compliance-understøttelse for GDPR, eIDAS m.m.

Med effektiv systemudvikling og compliance på plads er vejen banet for, at data i langt højere grad kan deles ensartet, effektivt og sikkert. Dette åbner for en lang række fordele, der kan betragtes som indirekte værdiskabelse fra referencearkitekturen, i form af:

* Enklere og mere effektive digitale services for borgere og virksomheder
* Simplere arbejdsgange og øget potentiale for automatisering hos organisationer (myndigheder og virksomheder)
* Borgere oplever hurtigere arbejdsgange med færre fejl, når genindtastning af data undgås
* Højere kvalitet i organisationers data og dermed også i de informationer og den viden, der kan udledes af data gennem analyser
* Vækst i samfundet gennem nye typer af services baseret på eksisterende data
* Øget transparens og bevarelse af tillid til registre

### 2.5 Juridiske rammer

De mest relevante love og forordninger (med særligt fokus på videregivelse af persondata) er:

* **EU-databeskyttelsesforordningen (GDPR)**  
  beskriver pligter og rettigheder ved behandling af persondata. I sammenhæng med denne referencearkitektur er GDPR central, da en stor del af de data, der er registreret af offentlige myndigheder, er personhenførbare. Da persondata er en af de datatyper, der er strengest reguleret (sammenlignet med fx virksomhedsdata, geodata, registrering af objekter m.m.), har vi valgt at genbruge mange termer og begreber fra GDPR i denne referencearkitektur. Herudover er en række aspekter, der dækkes af GDPR, relevante - fx definitionen af gyldige grunde til videregivelse af persondata, den nødvendige hjemmel i form af borgerens (den registreredes) samtykke, m.v.
* **Persondataloven**  
  beskriver pligter og rettigheder ved behandling af persondata. Relevansen for denne referencearkitektur er i høj grad den samme som for GDPR. Det bemærkes, at Persondataloven forventes helt eller delvist erstattet af en kommende Databeskyttelseslov, der på tidspunktet for dette dokuments udarbejdelse behandles i folketinget, og som sammen med GDPR fremover vil definere den registreredes rettigheder.

Med hensyn til digitalisering generelt er følgende love særligt relevante:

* **EU-forordningen eIDAS** (electronic IDentification, Authentication and trust Services) definerer registrerede tillidstjenester. Forordningen specificerer bl.a., at elektroniske transaktioner, der opfylder kravene i eIDAS, altid har samme juridiske gyldighed som klassiske, papirbårne transaktioner. Forordningen fjerner dermed en klassisk barriere for digitalisering. I forhold til denne referencearkitektur bemærker vi, at eIDAS har et udpræget grænseoverskridende ( cross border ) fokus. Det grænseoverskridende aspekt af videregivelse af data behandles ikke i dette dokument.
* **Lov om Digital Post fra offentlige afsendere** gør det obligatorisk for virksomheder og borgere at modtage digitale meddelelser fra offentlige afsendere. Digital Post er således en central kanal, når myndigheder ønsker at dele data og dokumenter med borgere og virksomheder gennem meddelelser.

Derudover er der en række mere specifikke love, der sætter rammer for videregivelse af data i den of- fentlige forvaltning, fx inden for særlige sektorer eller domæner. Listen nedenfor inkluderer de væsent- ligste, men er ikke udtømmende.

* **Sundhedsloven** regulerer hvem der har ansvar for behandling, forebyggelse og sundhedsfremme i det danske sundhedsvæsen. Sundhedsdata om borgere udgør en særlig følsom kategori af data, og Sundhedsloven regulerer derfor i detaljer, hvordan og til hvilke formål data kan behandles. Hvem, der har adgang til data, og hvordan adgang kan begrænses (herunder 'negativt samtykke’, der i nogen grad svarer til GDPR-begrebet 'begrænsning af behandling'), er reguleret i detajler. Derudover beskrives også ’indhentning af oplysninger’, som adskiller sig væsentligt fra den videregivelse, der beskrives i dette dokument. Endelig begrænser Sundhedsloven også den registreredes ret til indsigt i oplysninger, der er registreret i forbindelse med behandling.
* **Serviceloven** udstikker rammerne for rådgivning og støtte for at forebygge sociale problemer samt for at tilbyde ydelser til borgere med nedsat fysisk eller psykisk funktionsevne eller særlige sociale problemer. Loven danner baggrund for sagsbehandlingsforløb, der typisk kan involvere en række forskellige myndigheder. Dermed er loven et godt eksempel på, hvordan der juridisk kan gives hjemmel til deling/videregivelse af data i en række, konkrete scenarier.
* **Forvaltningsloven** indeholder regler om borgernes retsstilling over for den offentlige forvaltning. I forbindelse med sagsbehandling i offentlige forvaltninger regulerer loven bl.a. aktindsigt fx i begrundelse for afgørelser. I forhold til denne referencearkitektur spiller Forvaltningsloven bl.a. ind i diskussionen om forholdet mellem data og dokumenter.
* **Arkivloven** sikrer bevaringsværdige data. Ved design af løsninger, der indebærer etablering af nye datasamlinger eller ændringer til eksisterende, skal myndigheder tage højde for, at bevaringsværdige data skal kunne eksporteres til offentligt arkiv.
* **Lov om krav til sikkerhed for net og informationssystemer inden for sundhedssektoren** (i skrivende stund under behandling) skal implementere dele af EU’s NIS-direktiv (direktiv 2016/1148/EU af 6. juli 2016). Lovforslaget har til formål at sikre et højt sikkerhedsniveau inden for sundhedssektoren for så vidt muligt at undgå hændelser, der forstyrrer behandling, pleje og patientsikkerhed, og forventes at få stor betydning for videregivelse af data på sundhedsområdet.

I den konkrete situation, hvor videregivelse af data med henblik på genbrug af data overvejes, kan der være yderligere juridiske rammer, der vil påvirke løsningsarkitekturen. Dette må analyseres og afsøges i det enkelte tilfælde.

### 2.6 Sikkerhed

Sikkerheden ved videregivelse af data beror altid på forholdet mellem en konkret risikovurdering og de tiltag, der gøres for at imødegå de identificerede risici. I denne referencearkitektur er det forsøgt at be- skrive sikkerhedsovervejelser i forbindelse med de relevante arkitekturelementer, fremfor at samle dem i et særskilt afsnit. Dette ud fra en betragtning om, at sikkerhed ikke er et særskilt emne, men bør være gennemgående for alle betragtninger i emnet videregivelse af data.

Mere generelt kan informationssikkerhed betragtes som evnen til at kontrollere fortrolighed, integritet og tilgængelighed af de behandlede data. For videregivelse af data betyder dette mere specifikt at den dataansvarlige skal sikre sig at:

* Tilliden til identifikationen af modtageren af data er passende i forhold til den følsomhedsklassifikation, data har (fortrolighed)
* Protokoller til overførsel af data sikrer, at disse ikke kan læses eller ændres af uvedkommende (fortrolighed, integritet)
* Data opbevares og udstilles på en måde, så de ikke slettes eller gøres utilgængelige ved uheld eller direkte misbrug (tilgængelighed)

I øvrigt er de generelle forhold ved informationssikkerhed, der er beskrevet i blandt andet referencear- kitektur for brugerstyring samt vejledning om informationssikkerhed, også gældende for området vide- regivelse af data.

Endelig kan der omkring videregivelse af konkrete typer data gælde mere specifik lovgivning, der regu- lerer niveauet af sikkerhed og tekniske tiltag for at opnå denne. Det er altid den dataansvarliges ansvar at sikre sig, at den specifikke lovgivning overholdes.

### 2.7 Fællesoffentlige arkitekturprincipper og -regler

Den Fællesoffentlige Digitale Arkitektur (FDA) udpeger en række principper til rammesætning og styring af den offentlige digitalisering. Under hvert princip angiver FDA fra 1 til 5 konkrete arkitekturregler. Oversigten nedenfor gengiver FDA's arkitekturprincipper (kilde: [https://arkitektur.digst.dk/](https://arkitektur.digst.dk/)).

1. Styring, Arkitektur styres på rette niveau efter fælles rammer
2. Strategi, Arkitektur fremmer sammenhæng, innovation og effektivitet
3. Jura, Arkitektur og regulering understøtter hinanden
4. Sikkerhed, Sikkerhed, privatliv og tillid sikres
5. Opgaver, Processer optimeres på tværs
6. Information, **Gode data deles og genbruges**
7. Applikation, It-løsninger samarbejder effektivt
8. Infrastruktur, Data og services leveres driftssikkert

I denne referencearkitektur er fokus at understøtte arkitekturprincip 6 om, at _Gode data deles og genbruges_ og i særlig grad den underliggende regel: _6.1 Del og genbrug data_. Referencearkitekturen for deling af data og dokumenter tilbyder to måder, hvorpå data kan videregives til genbrug, og seks forskellige, tekniske implementeringsmønstre, som videregivelse/deling af data kan realiseres gennem.

Derudover kan en række af de øvrige arkitekturregler udfoldes og konkretiseres i forhold til denne referencearkitektur:

* **AR 1.2 Optimer arkitektur efter projektets og de fælles mål**.
  * Som eksempel på et arkitekturmæssigt dilemma i forhold til at indfri det fælles mål om at dele data kan nævnes den udgift, der er forbundet med at holde systemer kørende for at udstille data. Udgiften falder typisk til den dataansvarlige, der ikke har en isoleret gevinst ud af, at data genbruges. Det bør i designet af it-systemer fremadrettet overvejes, om man kan designe mønstre, styringsstrukturer og aftaler, der afløfter byrden ved videregivelse af data fra den dataansvarlige for at understøtte genanvendelse.
* **AR2.2 Anvend åbne og internationale standarder.**
  * Beskrevne applikationsservices bør kunne genfindes i eksisterende standarder.
* **AR2.5 Stil data og løsninger til rådighed for private.**
  * Ensartede forretningsprocesser, implementeringsmønstre og tekniske specifikationer vil understøtte sammenstilling af data og tværgående brug blandt myndigheder og virksomheder.
* **AR3.1 Tag højde for juridiske bindinger i forhold til deling og genbrug af data og it-systemer.**
  * Modeller funderes (med eksplicitte referencer) i relevant lovgivning nationalt og internationalt.
  * Dataudveksling mellem organisationer skal understøtte behovene omkring journalisering, forvaltningsret, tvistafgørelse, indsigter m.m., der er funderet i den klassiske "dokument-tankegang"
* **AR4.1 Opfyld krav til informationssikkerhed og privatlivsbeskyttelse.**
  * Understøtte borgeres og virksomheders indsigt i opbevaring og anvendelse af personoplysninger.
  * Beskrivelse af data, adgang til data og anvendelse af data sker under klar governance og håndhæves ud fra tydelig hjemmel.
  * Peger mod at begrænse eksistens og anvendelse af kopiregistre.
* **AR4.2 Anvend fælles arkitektur for informationssikkerhed.**
  * Ansvar for begrænsning af adgang ligger hos dataansvarlig.
  * Vedligehold af fuldmagter og samtykker sker løst koblet fra deres anvendelse til adgangskontrol.
* **AR5.1 Optimér tværgående processer efter fælles mål.**
  * Data beskrives, fordeles, forbedres og beskyttes i fællesskab
* **AR6.2 Anvende fælles regler for dokumentation af data.**
  * Anvend fælles referenceinformationsmodel, grund- og referencedata
* **AR 7. 1 Design og udstil snitflader efter fælles integrationsmønstre og tekniske standarder.**
  * Anvend et eller flere af de tekniske implementeringsmønstre i denne referencearkitektur ved deling af data og dokumenter.
  * Overvej genbrug af tekniske standarder og specifikationer nævnt i denne referencearkitektur.
* **AR 8. 1 Levér data og services i henhold til aftalte servicemål.**
  * Ved tilslutning til dataservices aftales servicemål og mål for datakvalitet

## 3 Forretningsarkitektur

Dette afsnit beskriver på forretningsniveau de centrale forretningsfunktioner, der er dækket i denne referencearkitektur, i form af use cases og tværgående processer. De medvirkende aktører og deres roller beskrives. Sluttelig gives en oversigt over forretningsobjekter omkring deling af data og dokumenter.

### 3.1 Forretningsmæssig kontekst for videregivelse af data

Emnet for denne referencearkitektur er "deling af data og dokumenter". Det er ikke urimeligt at sige, at denne funktion er så generisk, at den indgår i snart sagt alle processer, der går ud over den enkelte myndighed, hvad enten det er i forbindelse med sagsbehandling, selvbetjening eller noget tredje. Over- ordnet set finder referencearkitekturen dermed anvendelse i løsningen af alle offentlige opgaver.

Som beskrevet i afsnit 1 har vi præciseret scope for dette dokument til at dreje sig om selve _videregivelsen_ af data - og ikke de mulige _anvendelser_ , der muliggøres gennem videregivelsen. Vi gør dette ud fra en betragtning om, at typen af denne referencearkitektur er en grundlæggende referencearkitektur. Når det er sagt, er det alligevel meningsfuldt kort at overveje de typiske anvendelser for derigennem at forstå konteksten for videregivelse af data bedre.



![Figur4](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur4.jpg)

Figur 4 : Anvendelse af data falder i to kategorier: Behandling af data i forbindelse med sagsbehandling, der typisk udgør den primære årsag til registrering af persondata, og anden, sekundær behandling. Sags- behandling skal her forstås bredt og inkluderer fx patientforløb i sundhedssektoren. Den særlige marke- ring af offentlig selvbetjening indikerer, at dette emne er specifikt håndteret inden for Den fællesoffentlige digitaliseringsstrategi 2016-2020 i og med, at det har sin egen referencearkitektur for selvbetjeningsløs- ninger, der indgår i den fællesoffentlige rammearkitektur.

Figuren ovenfor illustrerer, at anvendelsen af delte data kan deles ind i to kategorier: Den primære an- vendelse, som består af behandling af data i forbindelse med en sagsgang, som oftest vil være det formål, data er indsamlet til. Primære anvendelser er typisk knyttet til sagsbehandling, borgerens/virksomhedens selvbetjening eller til forskellige, private tjenester, der gør brug af delte data.

Herudover findes der sekundære anvendelser, som indbefatter brug af data til styringsformål, økonomi- opfølgning og økonomisk afregning, statistik, forskningsformål og meget mere.

Som eksempler på anvendelser, der vil have gavn af effektiv datadeling, kan nævnes nedenstående sæt af generiske procesmønstre:

* Myndigheders sagsbehandling (forstået i bred forstand, inkluderer fx patientforløb i sundhedssektoren)
* Selvbetjening, vendt mod borgere og virksomheder
* Indsigt i oplysninger og deres anvendelse
* Brug af Digital Post (herunder påmindelser)
* Brug af abonnementsfunktionalitet (herunder tilmelding)
* Medbringelse af et dokument til en anden, offentlig/privat serviceudbyder, der ikke har adgang til registre - herunder bekræftelse af dokumentets ægthed og validering af dets indhold
* Tværgående analyse, tilsyn og kontrol

### 3.2 Om data og dokumenter

Figur 5 viser de centrale begreber i denne referencearkitektur, hvor data ikke overraskende ligger i mid- ten. Vi vil ikke introducere en specifik og isoleret definition af data - vi regner med, at læseren har en god fornemmelse for, hvad data er, og det er i denne sammenhæng tilstrækkeligt.



![Figur5](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur5.jpg)

Figur 5 : Begrebet data er noget, der enten har form af et dokument (og evt. kan opbevares i et reposi- tory), eller har form af en registrering, der indgår i et register. Begrebsmæssigt indgår data i samlinger og kan - evt. i form af et dokument - videregives i en meddelelse.

Vi vil i stedet tale om data ud fra de relationer, der er afbildet i figuren. Har man fx mange, ens struktu- rerede data samlet samme sted, indgår data i en samling. En datasamling vil typisk have en standardiseret måde, hvorpå man kan hente data på forespørgsel.

Data kan også indgå i en meddelelse i forbindelse med, at de videregives fra en afsender til en modtager. En meddelelse og et dokument kan være både struktureret og ustruktureret.

Data har to specialiseringer. Den første er en registrering, der betegner, at en myndighed har registreret oplysninger på standardiseret og struktureret vis, typisk ud fra specifik, lovmæssig hjemmel. Registreringerne udgør tilsammen et register, der dermed er en specialiseret datasamling. Registeret understøtter opslag af data i form af den oprindelige registrering, fx i kontekst af myndigheders sagsbehandling eller for at understøtte selvbetjeningsprocesser. Registeret kan også understøtte mere finkornede opslag. Et eksempel på dette kunne være en anvendelsesorienteret dataservice, der baserer sig på finkornede opslag i flere registre for at kombinere udvalgte data til brug i en given, specifik sammenhæng.

Den anden specialisering af data er i form af et dokument. Med denne modellering viser vi, at et dokument i bund og grund blot består af data. Dokumenter behøver således ikke at være ustrukturerede, men kan have indlejret fuldt strukturerede data. Som afledt konsekvens vælger vi som generelt princip i denne referencearkitektur ikke tale om deling af "data og dokumenter", men i stedet indskrænke til at tale om "data".

Med det sagt, er der alligevel nogle kvaliteter ved et dokument, der skal fremhæves. For det første er et dokument typisk karakteriseret ved, at det er optimeret mod at være tilgængeligt for menneskeøjne, da det binder data i en grafisk, læsbar opsætning (i tilgift til, at mange dokumenttyper også tilbyder indlejring af data i fuldt struktureret, maskinlæsbar form). For det andet har et dokument nogle iboende egenskaber, der er hensigtsmæssige i forvaltningsmæssige sammenhænge: Et dokument kan samle en række data, der i praksis håndteres som en samlet enhed, eller som er nødvendige på et givet tidspunkt i et sagsbehandlingsforløb, for eksempel som beslutningsgrundlag eller ved videregivelse af data fra én myndighed til en anden. Et dokument kan være tidsstemplet og signeret, og er dermed et klart grundlag for aktindsigt, retslige afgørelser og i det hele taget den historiske dokumentation af en sagsgang. Til sammenligning vil det ofte være vanskeligere at afgøre, nøjagtigt hvordan en specifik registrering så ud i et register på et givet tidspunkt. Dette vil typisk kræve, at registeret på forespørgselstidspunktet teknisk gendanner, hvordan registreringen så ud på det givne tidspunkt - hvorimod de historiske data, hvis de var gemt i dokument- form, ville være direkte tilgængelige.

Endelig findes der også en specialisering af datasamling for dokumenter, nemlig en dokumentsamling eller et repository, som er det fysiske sted, hvor dokumenter lagres efter oprettelse, og hvorfra de hentes ved efterfølgende anvendelse. Vi anvender den engelske term repository med reference til Referencearkitektur for deling af dokumenter og billeder, 2012, hvor dokumentbegrebet foldes yderligere ud for sundhedsområdet.

Endvidere vil vi undlade at bruge ordet metadata. Ordet anvendes historisk set meget forskelligt, typisk med en betydning der er tæt knyttet til en konkret anvendelsessituation. Fra denne referencearkitekturs synspunkt er metadata imidlertid blot en særlig form af data.

To virkelige eksempler kan gøre begreberne omkring data mere konkrete:

* **CPR-registeret**: data om borgere indgår i den datasamling, der kaldes CPR-registeret og i praksis benævnes netop som et register. Data om en enkelt borger udgør én specifik registrering i CPR-registeret, der kan hentes via en standardiseret forespørgsel.
* **Røntgenbilleder**: data relateret til et røntgenbillede består dels af billeddata, dels af yderligere informationer som fx tidsstempel, patient-ID, datakilde m.m. I praksis håndteres data for et røntgenbillede i et samlet, standardiseret objekt, som vi kan referere til som et dokument. Røntgenbilleder er gemt i flere repositories decentralt i røntgensystemer hos de enkelte regioner/hospitaler.

### 3.3 Forretningsfunktionen videregivelse

Den centrale delte use case i denne referencearkitektur er:

**Videregivelse** - forretningsfunktion hvorved data overføres ud af organisation

samt yderligere to use cases, der ikke er beskrevet uddybende i denne referencearkitektur; registrering samt sletning og arkivering. En særlig variant af videregivelse omhandler den registreredes ret til indsigt i behandling af persondata. Den betragtes her som et særtilfælde af videregivelse og vil i praksis realiseres som en digital selvbetjening og følge retningslinjer beskrevet i den fælles offentlige referencearkitektur for selvbetjening.



![Figur6](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur6.jpg)

Figur 6 : Den delte use case videregivelse , de relaterede use cases registrering og sletning og arkivering samt de funktioner, der er knyttet til de involverede roller, modelleret med relevante juridiske roller og forret- ningsmæssige funktioner.

### 3.4 Forretningsroller og aktører

I denne referencearkitektur defineres en forretningsrolle:

**Dataanvender** - en fysisk eller juridisk person, en offentlig myndighed, en institution eller et andet organ, der med specifik hjemmel behandler data fra en datasamling til eget formål.

Rollen skal ikke forveksles med GDPR-rollen databehandler, der betegner en fysisk eller juridisk person, en offentlig myndighed, en institution eller et andet organ, der behandler personoplysninger på den dataansvarliges vegne

Derudover indgår nedenstående roller, som er defineret i Databeskyttelsesforordningen:

Den registrerede - den person (datasubjekt), som oplysningerne vedrører (rolle fra GDPR)

Dataansvarlig - en fysisk eller juridisk person, en offentlig myndighed, en institution eller et andet organ, der alene eller sammen med andre afgør, til hvilke formål og med hvilke hjælpemidler der må foretages behandling af personoplysninger (rolle fra GDPR)

Endelig berøres en rolle, som i øvrigt ikke er beskrevet i detaljer i denne referencearkitektur:

Registrator - rolle som bringer oplysninger på digital form

Det skal bemærkes, at begrebet registrator ikke har en udbredt anvendelse og ikke kan genfindes i lovgivning. Begrebet er alene medtaget for at beskrive videregivelse i en bredere kontekst af en datasamlings livscyklus.

Ovenstående tager udgangspunkt i, at det er persondata, der behandles. Der findes imidlertid mange typer af data, der ikke er personhenførbare. I et sådant tilfælde falder den registrerede væk fra ovenstående billede, sammen med de GDPR-relaterede handlinger ret, begræns anvendelse og få indsigt.

Aktørerne ved deling af data og dokumenter er:

* **Offentlige myndigheder** (herunder virksomheder, der handler på vegne af offentlige myndigheder). Kan typisk være dataansvarlig eller dataanvender, men også ofte agere som registrator.
* **Borgere**, oftest i rollen som den registrerede, men også som registrator.
* **Virksomheder** som dataanvendere, særligt i forbindelse med private tjenester, der anvender oplysninger registreret i offentligt regi i forbindelse med at levere ydelser til den registrerede, men også, når anvendelsen er for virksomhedens egen skyld. Og som databehandlere, når de leverer løsninger og services til offentlige myndigheder.

### 3.5 Tværgående processer

I ovenstående diagram over centrale use cases er videregivelse den væsentligste, da den rummer selve delingen af data. Dykker man ned i den, findes den i to grundvarianter, hhv. videregivelse på forespørgsel og videregivelse ved meddelelse. Figuren nedenfor beskriver disse to varianter på procesform og knytter dem tillige sammen med en kort beskrivelse af processen registrering af data.



![Figur7](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur7.jpg)

Figur 7: Overblik over de centrale processer for videregivelse af data og deres aktiviteter fordelt på roller

Nedenfor er de to grundvarianter for videregivelse af data, videregivelse på forespørgsel og videregivelse ved meddelelse, beskrevet i detaljer. Registrering af data er ligeledes beskrevet, dog mere summarisk, da den i kontekst af denne referencearkitektur kun er med af referencehensyn.

#### 3.5.1 Videregivelse på forespørgsel

Denne proces dækker, at en dataanvender - typisk en myndighed, men kan også være en virksomhed - søger adgang til data, der på forhånd er til stede og kan gøres tilgængelige af en dataansvarlig.

**Videregivelse på forespørgsel** - integrationsmønster hvor data videregives af dataansvarlig på forespørgsel på anvenders initiativ.

De indgående procestrin er:

* **Behov opstår**  
  Processen starter hos dataanvender, der identificerer et behov for at indhente data. Dette behov opstår typisk i kontekst af andre processer, som vi ikke specificerer nærmere her, men som indbefatter sagsbehandling, selvbetjeningsløsninger, analyser og meget mere.
* **Forespørg om data**  
  Dataanvender sender en forespørgsel på data, der beskriver, hvilke data der ønskes. Ved adgang til andet end åbne data skal den nødvendige hjemmel foreligge, fx fremgå af forespørgslen, så dataan- svarlig kan håndhæve den nødvendige adgangskontrol. Forespørgslen kan i praksis ske ved anven- delse af flere meddelelser, eksempelvis ved kriteriebaseret søgning forud for, at data hentes, eller ved at starte med en forespørgsel til et indeks, der udpeger relevante dataservices, hvorfra data kan hentes.
* **Vurder adgang**  
  Dataansvarlig myndighed vurderer i dette trin forespørgslen med henblik på at håndhæve adgangs- kontrol. Kun, hvis den foreliggende hjemmel giver lovmæssig adgang til de forespurgte data, kan dataansvarlig fortsætte til videregivelsen. Hjemlen kan være eksplicit angivet eller ligge implicit i bru- gerstyringen. Hjemlen kan enten give generel adgang til en given datasamling eller til specifikke data i samlingen, hvorfor der i mange situationer vil være behov for at se på hjemlen og de efterspurgte data i sammenhæng for at håndhæve adgangskontrollen. Et særligt aspekt i at vurdere adgang er håndhævelsen af 'negativt samtykke', hvor adgang til bestemte data er fjernet, fx fordi datas korrekt- hed er bragt i tvivl og skal undersøges. Dette procestrin kan i øvrigt benyttes af dataansvarlig til at håndhæve adgangskontrol også på andre planer som håndhævelse af en Service Level Agreement, beskyttelse mod misbrug, mistænkelig adfærd m.m. Det bemærkes endvidere, at dataansvarlig kan have overladt distributionsopgave og de praktiske opgaver for håndhævelse af adgangskontrollen til en datadistributør, hvilket i øvrigt ikke ændrer ved beskrivelsen af dette trin.
* **Videregiv data**  
  Dataansvarlig håndterer forespørgslen ved at slå data op i datasamlingen, evt. ved at sammenstille data fra flere datasamlinger, og sender et svar tilbage til anvender. Delingen af data bliver logget af dataansvarlig, indbefattende hvilke data, der blev delt; til hvilken anvender; og med hvilken hjemmel. Det bemærkes, at dataansvarlig ikke nødvendigvis er klar over, hvilket databehov forespørgslen har tjent til at tilfredsstille - så længe, adgangen er legitim og foretaget på baggrund af gyldig hjemmel, har dataansvarlig ikke behov for at kende til dataanvenders brug af data i den konkrete forespørgsel.
* **Modtag svar**  
  Dataanvender modtager svaret, der indeholder det efterspurgte data, fra dataansvarlig.
* **Transformer data**  
  Efter modtagelsen kan der være brug for at transformere de modtagne data til en model tilpasset modtagerens processer og systemer. Transformeringen kan handle alene om tekniske formater og navngivning af felter, involvere oversættelse mellem forskellige referencedata som fx klassifikationer og endda oversættelser mellem forskellige identiteter af parter og aktører. Den Dataansvarlige leverer ikke denne mapning, men bidrager til den ved at gøre egne modeller og referencedata tilgængelige for anvenderen.

I forhold til trinnet ’vurder adgang’ bemærkes det, at hjemlen for en specifik forespørgsel fx fra én myndighed til en anden kan være givet i love, forordninger, bekendtgørelser m.v. Det kan i sådanne tilfælde være muligt at ”indbygge” hjemlen i integrationsdesignet, således at den anvendende myndighed generelt gives adgang til data uden behov for at dokumentere hjemlen _run-time_. Dette fritager imidlertid ikke dataansvarlig fra at sikre sig, at hjemlen til enhver tid vedbliver at være gyldig. En måde at sikre sig dette på er ved at abonnere på ændringer i de relevante retskilder og på baggrund af sådanne ændringer eventuelt opdatere sin adgangspolitik og integrationsdesign. Når man skal vurdere processen videregivelse på forespørgsel, er følgende kvaliteter og kriterier de mest væsentlige at forholde sig til:

* **Identifikation**: Det skal være muligt for både dataansvarlig og dataanvender at identificere hinanden entydigt og sikkert.
* **Adgangskontrol**: Der skal være en effektiv adgangskontrol, der opfylder kravet til at kunne dokumentere en tydelig og nødvendig hjemmel
* **Søgning**: Dataansvarlig bør tilbyde en søgefunktionalitet, der tillader dataanvender at fremsøge data effektivt, særligt hvor der samtidigt kan søges i ensartede datasamlinger hos flere dataansvarlige.
* **Sammenstilling**: Dataansvarlig kan, hvor det måtte være hensigtsmæssigt ift. specifikke behov, vælge at sammenstille data fra flere datasamlinger og udstille en service, der tilbyder de sammenstil- lede data. Sammenstilling af data forudsætter, at dataanvender har gyldig hjemmel til alle data, der indgår i sammenstillingen.
* **Indsigt**: Processen skal understøtte effektiv indsigt i anvendelse, hvilket bl.a. kræver logning af konkrete videregivelser af data
* **Opbevaring**: Dataanvender bør benytte den autoritative datasamling direkte hvis muligt. Herved undgås, at der opbygges 'skyggekopier' af datasamlinger, der introducerer kompleksitet i forbindelse med synkronisering, aktualitetsudfordringer m.m.

#### 3.5.2 Videregivelse ved meddelelse

Denne proces dækker, at en afsender - typisk en myndighed eller en virksomhed - har behov for at sende  
data (evt. i form af et dokument) til en modtager.

**Videregivelse ved meddelelse** - integrationsmønster hvor data videregives ved meddelelse af dataansvarlig på dennes initiativ

Generelt betragtet dækker videregivelse ved meddelelse både menneske til menneske-kommunikation (kommunikation til borgere/virksomheder, kommunikation mellem sagsbehandlere som led i en sagsgang m.v.), system til system-kommunikation (hvor meddelelse-mønsteret benyttes som ren teknisk integration), samt varianter, hvor enten afsendelsen eller modtagelsen af meddelelsen er automatiseret.

Til forskel fra videregivelse på forespørgsel starter denne proces hos afsenderen (der tillige kan være dataansvarlig). Afsender har udvalgt og pakketeret data i en meddelelse (evt. helt eller delvist i form af et dokument), adresserer meddelelsen (fx ved brug af et kontaktregister) og sender den herefter til modtager.

**Afsender** - person eller organisation der sender en elektronisk meddelelse

**Modtager** - person eller organisation der modtager en elektronisk meddelelse

Modtager kan være alle typer af aktører; for myndigheder og virksomheder bemærkes, at det i forbindelse med modtagelsen kan være relevant at fordele/route meddelelsen internt ud fra dens adresseringsoplysninger. I sammenligning med videregivelse på forespørgsel er det nu afsender, der som den part, der deler data, 'ejer' den fulde forretningskontekst - hvor den dataansvarlige ovenfor ikke var bekendt med formålet med at dele data.

Det skal bemærkes, at en særlig form for videregivelse ved meddelelse medfører fuld overdragelse af dataansvaret. Dette er fx tilfældet, når en registrator (afsender) har opsamlet nye data og ønsker at registrere dem i et register (modtager). Dette aspekt er dog ikke udfoldet yderligere i denne referencearkitektur, som fokuserer på afsenders behov for at dele data ud fra et genbrugsperspektiv – ikke fra et overdragelsesperspektiv.

De trin, der indgår i processen for videregivelse ved meddelelse, er:

* **behov opstår**  
  Processen starter hos afsender, der - typisk i kontekst af en anden, overliggende proces - har behov for at dele data ved at sende en meddelelse til en modtager.  
   
* **Dan indhold af meddelelse**  
  Første trin er, at afsender danner indholdet af meddelelsen. Indholdet kan være data under kontrol af afsender selv, men kan også indhentes fra andre via processen videregivelse på forespørgsel (der der- med bliver en underproces til videregivelse ved meddelelse, der i sig selv typisk også er en underproces).  
   
* **Adressér meddelelse**  
  Dette trin giver mulighed for at angive en slutmodtager for meddelelsen, der kan være mere specifik end blot modtager. Som eksempel kan modtager i nogle tilfælde være en organisation, og der kan være behov for at specificere en bestemt ansat som modtager En del af dette procestrin kan være at søge oplysninger i et kontaktregister for entydigt at identificere modtager, undersøge modtagers evne til at håndtere forskellige meddelelsesformater, identificere modtagers præference mht. sprog m.m.  
   
* **Afsend meddelelse**  
  Afsendelse af meddelelsen sker i dette trin. Afsender er ansvarlig for at logge hvilke data, der er sendt, til hvem, de er sendt, og med hvilket formål/hjemmel. Implicit i trinet ligger, at videregivelsen af data er lovmedholdelig, hvilket er ensbetydende med at sige, at modtager har et legitimt formål med at modtage data. Ansvaret for dette påhviler afsender.  
   
* **Modtag meddelelse**  
  Meddelelsen ankommer hos modtager. Der kan afsendes kvittering for modtagelse, hvorved afsender er garanteret, at meddelelsen er nået frem. (Det kan i nogle tilfælde være fordelagtigt at sende endnu en kvittering, der bekræfter, at meddelelsen også kunne parses og indholdet kan accepteres. Dette betragtes i denne sammenhæng som en del af fejlhåndteringen omkring integrationer i tværgående processer og er ikke beskrevet yderligere i denne referencearkitektur.)  
   
* **Fordel meddelelse**  
  Modtager har mulighed for at benytte oplysningerne i meddelelsen til at fordele meddelelsen internt. Meddelelsen kan være et svar på en tidligere fremsendt forespørgsel. Er dette tilfældet, har modtager behov for at sammenknytte meddelelsen med den kontekst, fra hvilken den oprindelige forespørgsel blev sendt.  
   
* **Transformer data**  
  Efter modtagelsen vil der typisk være brug for at transformere de modtagne meddelelser og data til en model tilpasset modtagerens processer og systemer. Transformeringen kan handle alene om tekniske formater og navngivning af felter, involver oversættelse mellem forskellige referencedata som fx klassifikationer og endda oversættelser mellem forskellige identiteter af parter og aktører. Den Dataansvarlige leverer ikke den oversættelse, men bidrager til den ved at gøre egne modeller og referencedata tilgængelige for anvenderen.

Når man skal vurdere processen videregivelse ved meddelelse, er følgende kvaliteter og kriterier de mest væsentlige at forholde sig til:

* **Identifikation**: Der bør være fuld sikkerhed for identifikation af afsender og modtager, understøt- tet gennem brugerstyring, kontaktregister eller lignende.
* **Integritet**: Indholdet i en meddelelse skal være beskyttet mod ændringer foretaget, mens meddelel- sen er på vej fra afsender til modtager.
* **Leverancesikkerhed**: Der skal være en tydeligt specificeret leverancesikkerhed, særligt relevant i situationer, hvor meddelelser skal kunne afleveres uafviseligt fx i forbindelse med retslig forkyn- delse.
* **Sporbarhed**: Der skal være et klart revisionsspor i logs for meddelelsers vej gennem systemet, bl.a. for at understøtte klarhed over, hvornår meddelelser er overført og ansvaret for eventuel videre behandling dermed overgået til modtager. Evt. kan loggen understøtte en 'track and trace'-funkti- onalitet.
* **Automatisering**: Meddelelser bør være velstrukturerede og understøtte automatisering på modta- gers side, fx ved at gøre data til fordeling/håndtering af meddelelser tilgængelig i en meddelelses- header.

#### 3.5.3 Registrering af data

Denne proces dækker de overordnede trin i at registrere data. Procestrinene er ikke foldet så meget ud som for de øvrige use cases, da registrering af data ikke falder i scope for denne referencearkitektur. Dog er en kort beskrivelse medtaget for reference på grund af den tætte sammenhæng mellem registrering og udstilling af data. Procestrinene er:

* **Registrer data**  
  En registrator er i besiddelse af data, der skal registreres hos en dataansvarlig. I denne sammenhæng skelnes ikke mellem, om registreringen angår ny data eller ajourføring i form af ændringer til data (i sidstnævnte tilfælde kan det være den registrerede, der agerer som registrator.)  
   
* **Modtag data**  
  Den dataansvarlige myndighed modtager data fra registratoren. I denne forbindelse skelnes ikke mellem, om data modtages automatisk eller manuelt. I begge tilfælde er den dataansvarlige ansvarlig for at håndhæve adgangspolitik og herunder sikre, at registratoren har gyldig hjemmel til at fremsende registreringen.  
   
* **Valider data**  
  Den dataansvarlige myndighed validerer de modtagne data. Den dataansvarlige kan have varierende krav til datas kvalitet og komplethed, afhængig af formålet med datasamlingen. Fejlscenarier, hvor data ikke kan valideres, dækkes ikke af denne referencearkitektur.  
   
* **Udstil data**  
  Når data er korrekt registreret, skal de udstilles (under antagelse af, at den pågældende datasamling er udstillet). Her kan der være forskel på, om data gøres tilgængelige øjeblikkeligt eller først på et senere tidspunkt (fx ved registrering af fremtidigt skift af adresse). Begge muligheder kan være relevante, og vil i mange tilfælde afhænge af dataanvenderens typiske behov. Udstillede data skal i øvrigt være forberedt til transformation og sammenstilling med andre data. Dette gøres ved at udstille anvendte datamodeller og referencedata for anvendere.

Når man skal vurdere processen registrering af data, er følgende kvaliteter og kriterier de mest væsentlige at forholde sig til:

* **Identifikation**: Sikker identifikation af registrator (så dataansvarlig kan håndhæve adgangskontrol) og dataansvarlig (så registrator kan have tillid til, at de potentiel følsomme data ender hos rette mod- tager).
* **Sikkerhed**: Tillid til, at data når ukompromitteret frem, herunder tjek af registreringens integritet, mulighed for kryptering af følsomme data, transaktionssikkerhed m.m.
* **Kontekst**: I hvilken kontekst er data skabt/opsamlet - hvor og af hvem?
* **Kvalitet**: Hvilke krav er der til datas komplethed, hvordan valideres i forhold til datatyper, og er registreringens granularitet passende?
* **Øvrig anvendelse**: Baseret på datas følsomhed, fortrolighedsniveau m.m. kan der være mulighe- der for anvendelse af data ud over den primære anvendelse. Er data lagret og udstillet på den mest hensigtsmæssige måde, der ikke begrænser genbrug unødigt? Er den datasamling, hvori registreringen indgår, velbeskrevet i et katalog?

#### 3.5.4 Hybrid-varianter

I dette dokument betragter vi de ovenstående to processer for videregivelse af data hhv. på forespørgsel og ved meddelelse som de atomare grundelementer, der er nødvendige for at kunne beskrive og tale om videregivelse af data. Det er dog værd at bemærke, at der i praksis kan skabes 'hybrid-varianter' af de to processer, der kan være velegnede i særlige situationer. Som eksempler kan nævnes:

* **Forespørgsel via meddelelse:** Processen videregivelse på forespørgsel kan i simpel form imple- menteres gennem to anvendelser af processen videregivelse ved meddelelse, i det den første medde- lelse udgør forespørgslen og den anden meddelelse udgør svaret. Dette procesmønster kan være re- levant for ad hoc-forespørgsler, der ikke er fuldt it-understøttede, eller i scenarier, hvor processen med at forberede svaret er tidskrævende, og det derfor er hensigtsmæssigt at lave en fuld, asynkron afkobling af forespørgslen og svaret. Procestrinet fordel meddelelse bliver i denne sammenhæng en opgave om at sammenkæde svaret med den oprindelige, tilhørende forespørgsel.  
   
* **Videregivelse via link til data:** Denne proces er en variant af videregivelse ved meddelelse, hvor der imidlertid ikke sendes data direkte i meddelelsen, men i stedet et link til, hvor data kan hentes. Linket kan enten være til en særligt forberede 'pakke' af data, fx i form af et dokument, eller til specifikke data, der er relevante for modtageren i den givne sammenhæng. Modtageren vil herefter kunne hente data gennem processen videregivelse på forespørgsel. Dette procesmønster kan fx være relevant, hvis man ønsker et ekstra lag af sikkerhed ved at undgå, at data kopieres fra datasamlingen til en meddelelse, hvilket giver en ekstra, sikkerhedsmæssig angrebsvektor (jf. GDPR-princippet privacy by design ).

### 3.6 Forretningsobjekter og begreber

Når processerne omkring videregivelse af data skal implementeres, er der en række begreber, det er væsentligt at holde styr på gennem god modellering. De fleste af begreberne er defineret, hvor de an- vendes første gang i denne referencearkitektur. Dette afsnit nævner eksplicit en række elementer, der beskriver data, der enten overføres eller opbevares i forbindelse med processer (forretningsobjekter).



![Figur8](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur8.jpg)

Figur 8 : Model med centrale begreber omkring videregivelse af data

Denne referencearkitektur definerer en række forretningsobjekter, uden at gøre dem til genstand for en decideret datamodellering. Specifikationen af nogle af disse vil følge af de standarder, tekniske specifi- kationer og anvendelsesprofiler, der vælges i den konkrete implementering. Andre vil kunne modelleres inden for et enkelt domæne. Og endelig vil nogle kunne modelleres i et fællesoffentligt domæne. Beslutninger herom overlades til en yderlig konkretisering af visionen for den fællesoffentlige digitale infrastruktur.

**Datasamling** - en samling af oplysninger bestående af enkelte dele der forvaltes under et.

Beskrivelsen af en datasamling bør understøtte design af løsninger og integrationer, offentlighedens ind- sigt i data hos myndigheder samt den registreredes indsigt i formålet med registreringen. I regi af Digita- liseringsstrategien arbejdes der medio 2018 på en datamodel for beskrivelser af datasamlinger.

**Log** - datasamling der beskriver de faktiske, historiske behandlinger af data i en given datasamling, herunder med hvilken hjemmel, behandlingen er sket

De enkelte log-linjer bør indeholde oplysninger nok til at understøtte den registreredes ret til indsigt i videregivelse af persondata. I regi af Digitaliseringsstrategien arbejdes der medio 2018 på en datamodel for log-linjer.

**Meddelelse** - formel besked der sendes elektronisk med veldefineret sikkerhed, tillid, integritet og leverance-sikkerhed

Meddelelser bør som minimum have en struktureret indhold, der gør det muligt automatisk at distribuere den enkelte meddelelse.

**Påmindelse** - en besked der får modtager til at tænke på en vigtig begivenhed

**Adresse** - angivelse af hvor en person eller organisation ønsker at modtage bestemte typer af meddelelser

**Forespørgsel** - meddelelse der sendes til en dataservice med forventning om svar indeholdende specifikke data

**Svar** - meddelelse dannet af dataservice som besvarer en forespørgsel

**Dataabonnement** - specifikation der anvendes til at filtrere hvilke beskeder om ændringer til en datasamling der ønskes

Diagrammet rummer en række øvrige elementer, der knytter sig til og grænser op til de ovenfor beskrevne. Dels en række begreber taget fra Databeskyttelsesforordningen, dels en række begreber beskrevet i Referencearkitektur for brugerstyring (begge markeret med blå skrift).

Endelig er der i arbejdet med denne referencearkitektur blevet identificeret en række yderligere begreber, der kan gøres til genstand for begrebsmodellering: begrebs- og datamodel, registeroplysning, dokument, registreringsbegivenhed, forretningshændelse/begivenhed, klassifikation, fuldmagt og generelle samtykker.

## 4 Teknisk arkitektur

Dette afsnit beskriver, hvordan de forretningsmæssige processer, begreber og objekter beskrevet i det forrige afsnit kan udmønte sig i konkrete applikationsservices. Dette leder samtidigt til et overblik over de områder, hvor der er behov for standardisering. Vi supplerer dette overblik med en oversigt over eksisterende standarder og specifikationer, der allerede er i anvendelse i den offentlige sektor.

I næste afsnit beskrives først det minimale sæt af _nødvendige_ applikationsservices, der kan bruges til at realisere de tværgående processer, der er beskrevet tidligere. For hver af de to processer for videregivelse af data beskrives først et basalt implementeringsmønster, og herefter yderligere to, mere avancerede mønstre. De avancerede mønstre kræver ekstra roller og applikationsservices, som vil blive introduceret løbende.

Implementeringsmønstrene, der beskrives i denne referencearkitektur, er:

| Forretningsmønster              | Implementeringsmønster                                                                                                                                                                                                                           | Beskrivelse                                                                                                    |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------- |
| Videregivelse på forespørgsel   | Direkte adgang                                                                                                                                                                                                                                   | Data videregives ved, at en dataanvender forespørger direkte mod den dataansvarliges system                    |
| Datadistributør                 | Den dataansvarlige har overdraget videregivelsen af data til en distributør, der servicerer forespørgsler fra dataanvendere                                                                                                                      |                                                                                                                |
| Fælles service- og dataplatform | Data opbevares og videregives på forespørgsel fra en fællesoffentlig, distribueret platform                                                                                                                                                      |                                                                                                                |
| Videregivelse ved meddelelse    | Direkte forsendelse                                                                                                                                                                                                                              | Data videregives i en meddelelse fra afsender til modtager via en sikker, direkte, punkt til punkt-forbindelse |
| Fælles system                   | Meddelelsen med data holdes i dette mønster af et fælles system, der tilbyder postkasser til afsender og modtager (fx Digital Post)                                                                                                              |                                                                                                                |
| Servicefællesskab               | En række forsendelsesservices, der er koblet sammen i et servicefællesskab (udbudt i et økosystem af serviceudbydere), og som tilbyder udveksling af meddelelser indeholdende data. Hver serviceudbyder kan betjene et antal afsendere/modtagere |                                                                                                                |

Ud over den tekniske beskrivelse angives der for hvert mønster en kort forretningsmæssig diskussion af fordele og ulemper. I en konkret anvendelsessituation kan denne diskussion benyttes som vejledende input i forhold til valg af implementeringsmønster.

### 4.1 Nødvendige applikationsservices

Applikationsservicen datasamling samt tilhørende log og brugerstyring udgør de nødvendige applikations- services for at implementere processen videregivelse på forespørgsel i en simpel form. Derudover er appli- kationsservicen selvbetjening inkluderet som en praktisk nødvendighed for at kunne tilbyde den registre- rede effektiv indsigt i anvendelsen af data om vedkommende. For at implementere en simpel form for videregivelse ved meddelelse er også applikationsservicen forsendelse (samt tilhørende log og brugerstyring hos afsender og modtager) nødvendig.

Derudover kan der indgå andre, understøttende services i en given løsning til videregivelse af data, der kan være fordelagtige at implementere for at øge tilgængelighed, performance, brugervenlighed m.m.



![Figur9](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur9.jpg)

Figur 9 : Oversigt over de fem nødvendige applikationsservices til understøttelse af videregivelse af data, både på forespørgsel og ved meddelelse.

De indgående applikationsservices kan på kort form defineres som:

**Dataservice** - applikationsservice der videregiver oplysninger fra datasamling på forespørgsel under håndhævelse af nødvendig adgangskontrol

**Forsendelse(sservice)** - applikationsservice, der gør det muligt at sende og modtage meddelelser samt dokumenterer behandlingen af disse, herunder leverer bevis for afsendelse og modtagelse af dataene, og som beskytter dem mod tab, tyveri, beskadigelse og uautoriseret ændring

**Logning** - applikationsservice, der konsoliderer og formidler data om ændringer, videregivelse og anvendelser af data fra en given datasamling

Brugerstyring - forretningsfunktion indeholdende nødvendige applikationsservices til administration og anvendelse af identiteter og rettigheder (jf. Referencearkitektur for brugerstyring, 2017)**.**

Selvbetjening - applikationsservice, der implementer en sammenhængende række af aktiviteter

Som nævnt i afsnit 1.2 er partsrepræsentation ikke i scope for denne referencearkitektur, og det vil derfor ikke blive foldet yderligere ud. Vi bemærker dog, at emnet er relevant i flere af de ovenstående applika- tionsservices omkring håndhævelse af adgangskontrol, logning af anvendelse, adgang og design af selv- betjeningsløsninger m.m.

#### 4.1.1 Ønskelige egenskaber ved videregivelse (både ved meddelelse og på forespørgsel)

Dette afsnit sætter flere ord på de kvaliteter, der grundlæggende knytter sig til videregivelse af data. De forskellige kvaliteter er her stillet op i sammenhæng med den relevante applikationsservice.

**Datasamling:** En datasamling er et helt centralt begreb i denne referencearkitektur og blev introduceret allerede i afsnit 1.3. Når datasamlingen udgøres af dokumenter, kaldes den et repository. Udgøres den af registreringer, kaldes den et register.

Datasamlinger er kendetegnet ved følgende, ønskede egenskaber:

* **Identificeret og dokumenteret:**  
  Datasamlingen bør registreres som et Information Asset (jf. ISO 27000). Registreringen dækker formålet med indsamlingen, og kategorier af personoplysninger m.m.  
   
* ' **Forvaltningsegnede** ':  
  Data i samlinger bør indeholde oplysninger om den kontekst, de er registreret i, så anvender kan vurdere tilliden til dem. Samlinger kan have temporale og bi-temporale egenskaber. Dette handler blandt andet om at holde styr på datas gyldighedsperiode og registreringstidspunkt for fx at kunne understøtte dobbelt historik (overblik både over, hvad der var korrekt på en given dato, og hvad registeret på et givent tidspunkt betragtede som korrekt på samme tidspunkt).  
   
* **Beskyttet:**  
  Samlinger skal have deres deres data beskyttet på basis af adgangspolitik bestemt af den dataansvarlige. Adgangskontrol er en funktion af identitet og attributter, herunder rettigheder og roller. I praksis er der behov for et trade-off mellem et adgangspolitik-design, der udspringer af den enkelte datasamling, og et design, der i stedet tager udgangspunkt i dataanvenders fx ved at anvende eksisterende trusted attributes fra andre samlinger hvis muligt. Anvenderperspektivet er relevant eksempelvis, hvor flere datasamlinger skal integreres i samme, tværgående proces. Referencearkitektur for Brugerstyring under Den fællesoffentlige digitaliseringsstrategi 2016-2020 har bl.a. til formål at lægge fælles rammer for adgangspolitik, der understøtter fællesoffentlig interoperabilitet.  
   
* **Robust og kontrolleret:**  
  En god datasamling kan (som applikationsservice betragtet) sikre sig mod overforbrug. Rimelig brug er beskrevet i aftaler, der kan være generelle eller bilaterale i forhold til en bestemt anvender. Ud over en passende håndhævning af den juridisk bestemte brug skal en datasamling også på det tekniske niveau kunne sikre robusthed imod perioder med høj belastning samt deciderede forsøg på blokeringer af tekniske services.

**Forsendelse:** Skal generelt kunne distribuere en meddelelse fra en afsender til en modtager. I praksis kan behovet være at understøtte menneske til menneske-kommunikation, system til system-kommunikation, eller varianter, hvor enten afsendelsen eller modtagelsen af meddelelsen er automatiseret. Kaldes også en _Messaging Service_ i den europæiske interoperabilitetsreferencearkitektur EIRA, samt en _elektronisk leverings- tjeneste_ i eIDAS.

Gode egenskaber omkring forsendelse inkluderer:

* **Identifikation af afsender og modtager:** Entydig identifikation ved brug af elektronisk signatur eller id.
* **Integritet:** Understøttelse af, at meddelelsen som udgangspunkt leveres i sin oprindelige form uden at være blevet ændret in-flight - sekundært, at ændringer har fuld sporbarhed.
* **Sporbarhed:** Tidspunkter for afsendelse og modtagelse samt relevante, øvrige punkter/handlinger i distributionskæden logges. Tidsstempler i distributionskæden er kvalificerede (jf. eIDAS).
* **Kvalificeret tillidstjenesteudbyder:** Der bruges kvalificerede (godkendte og underlagt tilsyn) tjenester for elektronisk signering, elektronisk segl, leverance m.m. hvor muligt og relevant (jf. eIDAS)
* **Aftaler:** Når der designes forsendelsesmønstre, er det vigtigt at forholde sig til behovet for en aftale , der regulerer den samlede forsendelse og dermed videregivelsen af data. Det kunne fx være en aftale om modtagers pligt til at tømme sin postkasse. Lov om Digital Post er et konkret eksempel på et juridisk instrument, der forpligter modtager til at åbne sin post i og med, at en meddelelse her er uafviselig og kan have retsvirkning. Aftaler kan være bi- eller multilaterale.

**Log:** Applikationsservicen log (i EIRA-termer: _Logging Service_ ) har følgende gode egenskaber:

* **Understøttelse af ret til indsigt:** En log skal i denne sammenhæng kunne understøtte den forretningsmæssige indsigt i data og deres faktiske anvendelse. Herunder, hvor data (registreringer eller dokumenter) stammer fra samt konkrete videregivelser og deres hjemmel. Understøttelsen er ekstra stærk, hvis en log er opbygget brugercentrisk og designet til at være umiddelbar forståelig
* **Integritet:** At den ikke kan ændres/forfalskes. Dette gør fx loggen anvendelig som juridisk bevis for, at en meddelelse er overført og at modtageren dermed har overtaget et eventuelt ansvar for videre behandling.
* En log kan indeholde personhenførbare data og andre **følsomme oplysninger** og skal derfor være behørigt beskyttet.

**Brugerstyring:** Generelt er brugerstyring som forretningsfunktion beskrevet i Referencearkitektur for Brugerstyring, og gode egenskaber ved brugerstyring vil derfor ikke blive beskrevet nærmere her. I kontekst af deling af data og dokumenter er brugerstyring central for at kunne identificere afsender/dataansvarlig samt modtager/dataanvender entydigt. Derudover er det i forbindelse med den registreredes indsigt i anvendelse af data om sig selv interessant at overveje identitetsstyringen på tværs af de logs, der rummer information om anvendelsen af data fra forskellige samlinger. Et brugercentrisk design har som forud- sætning, at brugerens identitet kan anvendes på tværs af logs og kræver dermed, hvis de enkelte logs opererer med servicespecifikke id'er, at identiteter kan henføres til fysiske personer.

**Selvbetjening** : En forudsætning for sammenhænge og effektiv betjening af borger og virksomheder – også i forbindelse med videregivelse af data – er brugervendte selvbetjeningsløsninger. Disse er genstand for en selvstændig fællesoffentlig referencearkitektur, men er medtaget her for at understøtte den regi- streredes ret til indsigt i behandling af persondata. Selvbetjening er også en forudsætning for at kunne afgive og administrere samtykker effektivt og sammenhængende – hvilket i øvrigt er uden for scope af denne referencearkitektur.

### 4.2 Implementering af videregivelse på forespørgsel

Når en dataanvender (virksomhed eller myndighed) har brug for adgang til data hos en dataansvarlig myn- dighed, kan det ske via ét af nedenstående tre implementeringsmønstre.

#### 4.2.1 Direkte adgang

Hvis målet for en anvender er at benytte data fra en specifik datasamling hos en bestemt dataansvarlig myndighed, som måske i forvejen har gjort data tilgængelige via en simpel dataservice med tilhørende log, og som har et ønske om selv at forestå videregivelsen af data, kan mønsteret direkte adgang være relevant.



![Figur10](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur10.jpg)

Figur 10: Implementeringsmønster for direkte adgang til en datasamling

I dette mønster, som er simpelt og måske det mest klassiske, er det dataansvarlig, der selv udstiller sin datasamling (gennem en simpel dataservice, der for overblikkets skyld er udeladt på Figur 10 ) for at tilbyde en anvender at få adgang til data via en service-orienteret snitflade. Dataansvarlig er også ansvarlig for at betjene den registreredes forespørgsler om indsigt i den dataansvarliges og alle dataanvenderes brug af personlige data ved at registrere anvendelse af data i en log. (Hvordan, log-informationerne gøres tilgængelige for den registrerede er ikke defineret nærmere her – se diskussion af portal-komponenten i afsnit 4.2.2.)

Fordelen ved dette mønster er først og fremmest, at det er simpelt. Fra dataansvarligs synspunkt tilbyder mønsteret endvidere en meget tæt kontrol med adgang til data, hvilket måske kan være ønskværdigt.

Udfordringerne ved mønsteret er bl.a., at dataansvarlig kommer til at bære hele udgiften ved at stille data bredt til rådighed. Dette er specielt relevant, hvis det ikke er den dataansvarliges primære kompetence at vedligeholde og drifte en applikationsplatform. Endvidere kræver genbrug af data, at dataansvarlig indgår bilaterale aftaler med nye anvendere, hvilket giver ekstra arbejde til dataansvarlig uden nødvendigvis at medføre en gevinst. Fra anvenders perspektiv er det en ulempe, at anvender selv skal håndtere en eventuel, nødvendig transformation af data, samt at sammenstilling med data fra andre datasamlinger påhviler anvender. Fra den registreredes perspektiv er det en konsekvens af dette mønster, at det er vanskeligt at få et samlet overblik over anvendelse af egne data på tværs af datasamlinger.

Næste mønster adresserer en række af udfordringerne ved direkte adgang.

#### 4.2.2 Datadistributør

Hvis man ønsker en situation, hvor anvender kan hente data fra en dedikeret datadistributør, der afløfter en væsentlig del af byrden ved videregivelse af data fra den dataansvarlige myndighed, og hvor man har mulighed for at designe anvendelsesorienterede dataservices, der evt. kombinerer data fra flere datasamlinger i et format, der er tilpasset anvenders behov, er mønsteret datadistributør relevant at overveje.



![Figur11](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur11.jpg)

Figur 11: Implementeringsmønster, der introducerer en datadistributør

I dette mønster er dataansvarlig fortsat ansvarlig for at tilbyde en service til registrering af data. Udstillin- gen af data overfor anvendere varetages derimod af en datadistributør (evt. flere). Dette giver datadistribu- tøren mulighed for at fokusere netop på distributionen, dvs. at gøre data bredt tilgængelige for dataan- vendere – dog naturligvis under håndhævelse af adgangskrav specificeret af dataansvarlig. I databeskyttelsesforordningstermer er datadistributøren dermed en databehandler.

En typisk fordel ved dette er, at det giver mulighed for at designe en dataservice målrettet anvenders behov hvilket evt. kan betyde, at dataservicen aggregerer data på tværs af flere datasamlinger. Sker dette, er datadistributør naturligvis ansvarlig for, at adgangskrav fra alle de indgående datasamlinger/dataansvarlige håndhæves for den aggregerede service.

Når nye data registreres, har den dataansvarlige ansvar for at opdatere kopien af datasamlingen hos datadistributøren. Afhængigt af anvenders behov for aktualitet kan det ske i forbindelse med registreringen (hændelsesbaseret, fx i en EDA-arkitektur) eller på fastlagte tidspunkter (batchbaseret). For batch-mønsteret skal det overvejes, om der foretages en fuld kopi af den autoritative datasamling i forbindelse med opdatering, eller om det kun er ændringer siden seneste opdatering, der sendes (delta-kopi).

I det tilfælde, hvor ensartede datasamlinger ligger hos flere, separate dataansvarlige - eksempelvis sundhedsdata opbevaret i forskellige regioner - er det fordelagtigt fra anvenders perspektiv at anvende et indeks for at sikre effektive opslag. Dataansvarlig opdaterer dette indeks, når en registrator opdaterer datasamlingen.

Logningsmæssigt er den enkelte distributørs opgave at logge dataanvenders forespørgsler på data. For at sikre den registreredes mulighed for at få indsigt i anvendelsen ved henvendelse til den dataansvarlige, må distributøren også sørge for overføre loggen til den dataansvarlige med henblik på konsolidering, så den dataansvarlige kan opfylde den registreredes ret til indsigt. Hvis dataansvarlig kun benytter sig af én datadistributør, kan ansvaret for at opfylde den registreredes krav om indsigt dog være aftalemæssigt uddelegeret fra dataansvarlig til datadistributør.

Portal-komponenten er kun overordnet introduceret og behandlet i denne referencearkitektur. Grundlæggende er det et interface mellem den registrerede og loggen, der har til formål at gøre anvendelsesinformationerne i loggen tilgængelig for den registrerede. Portalen er i dette afsnit vist som en selvstændig komponent under den dataansvarliges kontrol. Hvis den dataansvarlige kun benytter sig af én datadistributør, er det – ligesom med loggen – muligt for den dataansvarlige at uddelegere ansvaret for portalen til datadistributøren, hvorved portal-komponenten ville rykke ind i datadistributør-kassen.

Her introduceres:

**Distributør** - forretningsrolle der som databehandler giver anvendere adgang til data på vegne af den dataansvarlige

For en dataansvarlig med få, men hyppigt anvendte datasamlinger vil det være en forholdsmæssig stor opgave at vedligeholde en dataservice. Der kan dermed være betydelige fordele ved at løfte opgaven via en distributør.

**Distributionskopi** - forretningsobjekt som er en kopi af en datasamling, der opbevares hos databehandler med henblik på distribution efter instruks fra dataansvarlig

**Indeks** - applikationsservice som er en datasamling, der indeholder oplysninger om, hvilke datasamlinger der indeholder oplysninger om personer, virksomheder og andre forvaltningsobjekter.

Et indeks kan gå på tværs af flere datasamlinger, der kan have forskellige dataansvarlige. Ligeledes har indekset (som er en datasamling) i sig selv en dataansvarlig, der ikke behøver at være sammenfaldende med den/de aktører, der er dataansvarlige for de underliggende datasamlinger.

**Portal** - applikationsservice og selvbetjeningsløsning, der lader den registrerede have indsigt i dataanvendelse m.m.

Fordelen ved dette mønster er først og fremmest, at det introducerer en dedikeret infrastrukturkompo- nent for videregivelse på forespørgsel i form af en datadistributør, der har mulighed for at specialisere sig fuldt og helt i distributionsopgaven. Hvis flere dataansvarlige vælger samme distributør, deles mange af omkostningerne. Fra den dataansvarliges perspektiv gælder det endvidere, at en del af aftaleindgåelsen kan afløftes til datadistributør, der i højere grad vil have mulighed for at anvende standardkontrakter.

De væsentligste udfordringer i dette mønster udspringer af, at man nu har skabt en kopi af en datasamling, der skal vedligeholdes. Derudover bliver det en vanskeligere at konsolidere en anvendelseslog, når data ligger fordelt på mere end én platform. Fra den dataansvarliges synspunkt medfører datadistributør-mønsteret endvidere, at der introduceres et behov for styring/tilsyn med distributøren.

En specifik udfordring i forbindelse med dette mønster er, at det er muligt at lægge dette mønster ’i forlængelse af sig selv’, hvorved man kan skabe en ny distributionskopi på basis af en eksisterende distri- butionskopi. Selv om det i særlige tilfælde kan være rimelige eller nødvendige grunde til at benytte et sådant mønster, kan det generelt ikke anbefales. Kopier af kopier introducerer ekstra kompleksitet i opdateringer med mulige konsekvenser for datas aktualitet. Derudover bliver det markant vanskeligere for dataansvarlig at håndhæve sit dataansvar, fx i forbindelse med ’retten til at blive glemt’, hvor GDPR foreskriver, at dataansvarlig generelt set er ansvarlig for at kunne slette data på den registreredes anmodning. Ligeledes bliver det vanskeligere for den dataansvarlige at understøtte den registreredes ret til indsigt i anvendelse af data om ham/hende selv – hvilket i sidste ende kræver, at enhver n’te-ordens distributionskopi skal implementere en fuld anvendelseslog, der skal kunne konsolideres bagud mod dataansvarlig, og hvor ethvert ekstra lag af distributionskopier dermed introducerer yderligere kompleksitet, mulighed for forsinkelser m.m. i forhold til, at dataansvarlig kan konsolidere anvendelse af data om den registrerede. Bl.a. af disse årsager må ’kopi af kopi’-mønsteret kun anvendes efter nærmere aftale mellem datadistribu- tør og dataansvarlig.

Det næste mønster søger at adressere nogle af de udfordringer, der ligger i at arbejde på en kopi af en datasamling.

#### 4.2.3 Fælles service- og dataplatform

Hvis man ønsker at benytte en dedikeret infrastrukturkomponent til distribution af data, men uden at man ønsker at indføre en distributionskopi med den kompleksitet, det medfører – og hvis man har mulighed for at lade dataansvarlig og dataanvender operere på samme platform, således at de respektive datasamlinger ligger fysisk samlet, men logisk adskilt, kan mønsteret Fælles service- og dataplatform være interessant.



![Figur12](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur12.jpg)

Figur 12: Implementeringsmønster for fælles service- og dataplatform

Figuren viser, hvordan deling i dette mønster er håndteret af en fælles dataplatform. Platformen er distri- bueret og er i stand til at replikere data på tværs af dataansvarlige og dataanvendere. Dvs., at data, der registreres via en dataansvarlig myndighed, gøres tilgængelige for andre, dataanvendende myndigheder via platformen.

Da dataplatformen kan rumme data fra mange forskellige dataansvarlige, muliggøres effektiv sammenstil- ling af data hos dataanvenderen, der kan kombinere data fra egne samlinger med data fra andre samlinger. i en anvendelsesorienteret dataservice. Data kan her forstås både som simple opslag i egne eller andres datasamlinger, og som sammenstillinger, hvor data fra flere samlinger kombineres for at servicere dataan- venders applikationer.

Platformen er ansvarlig for (på vegne af dataansvarlig) at håndhæve adgangskontrol, herunder at sikre, at anvendelsesapplikationer har den nødvendige lovhjemmel til at tilgå en given, distribueret samling. Even- tuelle services hos dataanvender, der gør brug af data, er ansvarlige for at logge deres brug. Platformen konsoliderer brugs-loggen og gør det muligt for den registrerede at få overblik over brug af personlige data.

Portalen er her vist som en del af dataplatformen. Der er for så vidt intet i vejen for at lægge portalen uden for platformen og basere den på læs-interfacet til loggen. Denne variant åbner mulighed for, at portalen kan konsolidere anvendelse af data på tværs af flere platforme. Dette kunne være interessant ud fra et borger-orienteret UX-perspektiv, hvor anvendelsen af data måske kunne præsenteres i kontekst af det selvbetjeningsforløb eller den sagsgang, der ledte til den specifikke videregivelse af data. Sådanne, mere vidtgående aspekter af portalen er dog ikke foldet yderligere ud i denne referencearkitektur. Det væsent- ligste er, at den registrerede gennem portalen får et interface til at få indsigt i anvendelse af personhenfør- bare data.

Her introduceres:

**Platformsudbyder** - forretningsrolle der forvalter en fælles platform på vegne af flere aktører.

Fordelen ved dette mønster er den umiddelbare og standardiserede tilgængelighed til data, som en data- platform kan levere. Derudover er det en fordel fra den registreredes synspunkt, at platformen konsoli- derer loggen, så indsigten i anvendelse af data om en selv centraliseres.

Ulempen ved mønsteret er, at kompleksitet og governance (herunder audit) omkring den enkelte data- samling øges, da den pludselig gøres tilgængelig meget tæt på andre dataansvarliges datasamlinger. Derud- over stilles der større krav til dataanvenders modenhed ift. den tekniske adgang til data (da dataanvenders applikationer i praksis vil skulle afvikles på den fælles service- og dataplatform).

### 4.3 Implementering af videregivelse ved meddelelse

Når en myndighed vil initiere en specifik og målrettet videregivelse - dvs. sende data (herunder doku- menter) til en anden myndighed, virksomhed eller borger - kan det ske via ét af de tre nedenstående mønstre.

#### 4.3.1 Direkte forsendelse

Hvis målet er at kunne sende meddelelser fra en afsender til få, kendte modtagere, hvor man har mulighed for forud at opsætte en sikker og krypteret punkt til punkt-forbindelse fra afsender til modtager, og hvor der ikke er forventning om den store, dynamiske ændring af modtager-kredsen, kan implementerings- mønsteret direkte forsendelse være relevant. Dette mønster tilbyder den enkleste måde at videregive data via en meddelelse på.



![Figur13](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur13.jpg)

Figur 13: Implementeringsmønster for direkte forsendelse

Figuren viser de to procestrin ’afsend meddelelse’ og ’modtag meddelelse’ hos hhv. afsender og modtager. Begge trin må understøttes af en lokal forsendelse-service, der kan tale direkte med modpartens, så der skal på forhånd være enighed mellem de to parter om, hvordan distributionen realiseres. Procestrinet ’adresser meddelelse’ er ikke medtaget, da der ikke er nogen fælles understøttelse af dette. Det påhviler dermed parterne selv at sikre modpartens identitet, hvilket typisk vil kræve en bilateral aftale.

Et eksempel på dette mønster er den type myndighed til myndighed-kommunikation, der kommunikerer meddelelser fra afsender til modtager gennem brug af sikker e-mail. Her er det nødvendigt, at begge parter på forhånd opsætter sikkerhed i form af nødvendige certifikater m.m. for at kunne håndhæve kryptering, identitetskontrol m.m.

Fordelen ved dette mønster er, at det er simpelt og i høj grad har mulighed for at benytte sig af stan- dardteknologi (fx sikker e-mail eller sikker FTP). Det vil typisk være baseret på bilaterale aftaler, der kan rumme høj grad af fleksibilitet i forhold til særlige krav hos afsender eller modtager (SLA-krav, særlige formater, afleveringsmønstre, fejlretningsprocesser osv.)

Udfordringerne ved dette mønster inkluderer, at implementeringen – både hvad angår den tekniske integration og dataformater – risikerer at blive skræddersyet til den specifikke løsning, hvilket typisk vil være en forhindring for at kunne genbruge data i andre sammenhænge. Derudover er der ingen fælles sikring af identiteter på afsender/modtager, og i det hele taget ingen fast platform at læne sig op ad hvad angår leverancesikkerhed, standarder for funktionalitet, der kan muliggøre automatisk routing hos modtagende virksomhed/myndighed i det tilfælde, hvor meddelelsen ikke har én specifik modtager, m.m. Setup’et med bilaterale aftaler om punkt til punkt-forbindelser mellem afsender og modtager skalerer heller ikke godt, hvis der pludselig bliver flere aftagere af den givne type data.

Næste mønster adresserer en række af udfordringerne ved Direkte forsendelse.

#### 4.3.2 Fælles system

Hvis man som afsender har en bred og/eller varierende modtager-kreds på de meddelelser, der skal afsen- des – hvis man fx skal designe standardkommunikation fra myndighed til borgere – og hvis man i øvrigt ikke kan stille særlige krav til en forsendelsesservice, der på modtagers side kan håndtere modtagelse af meddelelser, kan det være en fordel at anvende en infrastrukturkomponent i form af et fælles system. Dette mønster tilbyder, at man kan genbruge en eksisterende infrastrukturløsning, der afkobler afsender og modtager på det tekniske og i nogen grad også på det aftalemæssige plan, og som giver mulighed for at benytte nye applikationsservices som fx notifikation og adresse.



![Figur14](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur14.jpg)

Figur 14: Implementeringsmønster for fælles system

Ved brug af Fælles system-mønsteret til forsendelse af en meddelelse benytter afsender og modtager en fælles forsendelsesservice til at sende meddelelsen, modtage den og eventuelt også læse den. I den analoge verden svarer dette mønster til, at afsender og modtager benytter et fælles postbokskontor. Digitalt er dette mønster fx implementeret af Digital Post, hvor såvel myndigheder, virksomheder og borgere kan placere meddelelser, der efterfølgende kan hentes af modtager. Også messaging-funktionaliteten i mange af de sociale medieplatforme (fx Facebook) falder i denne kategori.

Til forskel fra direkte forsendelse-mønsteret ovenfor er fælles system-mønsteret mere sikkert og robust, da der tilbydes opslag/verifikation mod en identitets-baseret adresseservice for at bekræfte afsenders/modta- gers adresse. Desuden kan infrastrukturen tilbyde, at meddelelsen opbevares, indtil modtager aktivt læser den.

Forsendelsesservicen har endvidere mulighed for at trække på en notifikation, der kan tilbyde en indholds- reduceret påmindelse til modtager om den nye meddelelse.

Et Fælles system-mønster kan fungere på mange niveauer, herunder nationalt (fx Digital Post); inden for et specifikt domæne, fx på sundhedsområdet; eller rent bilateralt, hvor to organisationer enes om dette mønster og vælger en passende meddelelsesplatform.

I dette mønster introduceres:

**Adresse (til forsendelse)** - applikationsservice som er en specialiseret datasamling (fx et kontaktregister), der indeholder oplysninger til brug ved adressering af meddelelser

**Notifikation** - applikationsrolle der udsender påmindelser.

Selv om dette mønster har mange fordele – hovedsageligt, at det benytter sig af en forsendelses-infra- struktur og en adresse-komponent, der kvalificerer afsender og modtager – er det ikke uden udfordringer. Når man kigger ud over den enkelte afsenders og modtagers behov i forbindelse med at forsende en enkelt meddelelse og kigger på platformen som helhed, opstår der paradoksalt nok en risiko, hvis platformen vinder popularitet og bliver benyttet af mange myndigheder, virksomheder og borgere. En ”stor” løsning får en vis dominans, der kan føre til, at den i praksis bliver en silo – måske én blandt flere. Hvis platformene ikke er designet til at være interoperable, har konkurrencen dårlige vilkår, og der er risiko for at ende i en _vendor lock-in_ - situation.

Det næste mønster sigter mod at adressere nogle af de infrastruktur-relaterede udfordringer i Fælles system.

#### 4.3.3 Servicefællesskab

Hvis man som afsender/modtager ønsker at etablere videregivelse af data ved meddelelse, og fra starten ønsker at vælge en infrastruktur, der er designet til at være fleksibel, interoperabel og skalerbar, kan det være en fordel at følge mønsteret Servicefællesskab.



![Figur15](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur15.jpg)

Figur 15: Implementeringsmønster for servicefællesskab.

I dette mønster deltager både afsender og modtager i et meddelelses-fællesskab ved at vælge hver sin ser- viceudbyder (eng. _service provider_ ) til forsendelse. Alle service providers indgår på forhånd i en infrastruktur i form af et aftalemæssigt og teknisk servicefællesskab, der bl.a. garanterer fuld interoperabilitet i distributi- onen. Mønsteret er bl.a. kendt i kontekst af den europæiske eDelivery-standard som en _four corner model_.

En fælles adresseservice udgør en central komponent i mønsteret, der gør det muligt for alle parter at slå den relevante adresseringsinformation op. En afsender kan via adresseservicen se/verificere mulige mod- tagere, samt evt. afgøre hvilken konkrete meddelelsesformater/kanaler, modtager kan håndtere. Forsen- delsesservicen, der på infrastruktursiden håndterer distribution af meddelelsen, kan benytte adresseservicen til at finde modtagers konkrete serviceudbyder og bliver dermed i stand til at levere meddelelsen.

Mønsteret vil typisk være symmetrisk, således at en afsender også kan indgå som modtager og vice versa. Mønsteret kan i øvrigt enten være generisk eller specifikt for et domæne, der fx kan stille ekstra krav til meddelelsens format. For eksempel benytter NemHandel sig af PEPPOLs eDelivery-netværk for at kunne udveksle elektroniske fakturaer, kreditnotaer m.m. med internationale modtagere.

Fordelene ved servicefællesskab-mønsteret er, at det er en robust og fleksibel måde at levere asynkrone meddelelser på, og at det skalerer godt, da det løbende kan udvides med nye serviceudbydere. Derudover stilles der umiddelbart ingen krav til formatet af integrationen mellem en serviceudbyder og en afsen- der/modtager – hvilket åbner for, at forskellige serviceudbydere kan tilbyde løsninger skræddersyet til for- skellige behov, hvor nogle modtagere fx vil have et ønske om fuld automatisering, mens andre vil have et ønske om et manuelt betjent interface.

Der er også udfordringer ved servicefællesskab-mønsteret. Der stilles fx store krav til servicefællesskabets centrale adresseservice, hvilket kan medføre en kompliceret governance. Man er ligeledes afhængig af, at der er en kritisk masse af brugere tilstede (og dermed tilgængelige) på platformen. Man skal også være opmærksom på, at det generiske og robuste design, der typisk vil være i et servicefællesskab, måske ikke altid vil være det rigtige valg, fx hvis man i en bestemt anvendelsessituation har helt særlige krav til performance.

Samtidig er det for eDelivery-standarden en specifik udfordring, at etableringen primo 2018 fortsat er i sin indledende fase, og at der dermed endnu ikke findes bredt anvendte standardteknologier, der dækker mønsteret.

**Serviceudbyder** - forretningsrolle der stiller der stiller applikationsservices til rådighed

**Servicefællesskab** - forretningsrolle der regulerer services udbudt af en række serviceudbydere

### 4.4 Understøttende applikationsservices

I de ovenstående mønstre er der introduceret en række yderligere services, der bidrager med forskellige, ønskelige egenskaber ved implementeringsmønstrene (dataservices, distributionskopi, dataindeks, og notifi- kationsservice). Fælles for disse er, at de oftest anvendes run-time i videregivelsen af data. Derudover vil en række services, der ikke er medtaget i ovenstående mønstre, også kunne understøtte etablering og vedligeholdelse af integrationer (referencedata, modelkatalog og datakatalog).



![Figur16](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur16.jpg)

Figur 16: Det minimale sæt af applikationsservices, der er nødvendige for at kunne videregive data, samt øvrige, understøttende applikationsservices, der kan være fordelagtige at implementere i en given løsning

Figur 16 giver en samlet oversigt over de applikationsservices, der skal overvejes i forbindelse med videregivelse af data, fordelt på de nødvendige hhv. understøttende applikationsservices. For hver applikationsservice er den generiske snitflade angivet. Da applikationsservices typisk indgår i flere implementeringsmønstre, er det hensigtsmæssigt at kigge på standardisering af operationerne i snitfladerne. Derved opnås en afkobling, der giver større fleksibilitet i forhold til senere redesign af en given løsning, specifikt i forhold til, at et skift til et andet implementeringsmønster vil blive lettere, hvis snitfladen kan opretholdes.

Udover de services der er beskrevet i kontekst af de enkelte mønstre, kan videregivelse af data med fordel understøttes af en række andre applikationsservices.

**Referencedata** - datasamling der anvendes til at organisere eller kategorisere andre data, eller til at relatere udvekslede data med interne data.

Anvendelse af forudspecificerede udfaldsrum for de enkelte felter i udvekslede meddelelser bidrager til at sikre den semantiske interoperabilitet gennem en fælles entydig forståelse af koder, begreber og lig- nende. De indgår typisk ikke direkte ved udveksling af beskeder, men kan anvendes i forskellige former for valideringer. Også i forbindelse registrering er referencedata og deres mapninger til interne data re- levante. Referencedata kan videregives som alle andre datasæt.

**Datakatalog** - datasamling der beskriver datasamlinger og deres anvendelser af referencedata og datamodeller.

Organisationer bliver i stigende grad afkrævet overblik over deres opbevaring af data gennem forskellige former for regulering. Når data skal registreres, vedligeholdes og anvendes effektivt kræver det indsigt i andre organisationers data. Datakatalog er datasamlinger der understøtter dette overblik.

**Modelkatalog** - applikationsservice der udstiller datamodeller og referencedata der anvendes i datasæt og i meddelelse.

Udvekslede data skal struktureres, og et modelkatalog kan udstille de anvendte datamodeller og deres anvendelse af referencedata. Datamodeller bør overholde fælles modelleringsregler for at sikre den ind- holdsmæssige kompatibilitet og dermed muligheden for sammenstilling af data og automatisk transfor- mation.

Hjemmel - applikationsservice der understøtter håndhævelse af, at videregivelse af data sker ud fra korrekt hjemmel, samt den registreredes indsigt i anvendelse af persondata.

Data må alene videregives på baggrund af gyldig hjemmel. Videregivelse skal logges med henvisning til aktuel hjemmel, således at den registrerede efterfølgende kan få indsigt i, hvorfor data om vedkommende er blevet videregivet (med hvilken hjemmel og til hvilken anvendelse).

Denne applikationsservice håndterer endvidere samtykker og fuldmagter, der i mange tilfælde kan udgøre den nødvendige hjemmel til videregivelse. Den nærmere modellering og håndtering af samtykker og fuldmagter sker i spændingsfeltet mellem brugerstyring og videregivelse af data og er ikke uddybet i denne referencearkitektur.

### 4.5 Områder for standardisering

Et af referencearkitekturens formål er at udpege områder, hvor standardisering i form af fælles anven- delsesprofiler vil være særligt værdifuld. Både for videregivelse på forespørgsel og videregivelse ved meddelelse er der — set fra ‘forretningens’ synspunkt — en række snitflader, der går igen. Standardisering af disse vil tillade anvender at anvende samme snitflader uanset hvilket implementeringsmønster, der realiseres.

I udarbejdelsen af referencearkitekturen er der foretaget en delvis afdækning af de standarder, anvendelsesprofiler m.m., der pr. 2017 anvendes i den offentlige sektor. Lister over disse standarder er medtaget for at beskrive og belyse de enkelte integrationstyper og kan benyttes til inspiration. De nævnte standar- der skal dermed ikke ses som en hverken udtømmende eller autoritativ liste. For en nærmere beskrivelse af begreberne omkring standardisering, se Bilag E: Om specifikationer, standarder og profiler.

#### 4.5.1 Tekniske specifikationer

I forbindelse med udarbejdelsen af referencearkitekturen har arbejdsgruppen identificeret en række relevante, tekniske specifikationer, der som nævnt indledningsvist ikke skal ses som en autoritativ liste i forhold til fremtidige anvendelser, men blot er inkluderet til inspiration og til at belyse området.

##### Adgang til dataservices

Særligt adgangen til dataservices, herunder til den særlige dataservice, der indeholder log, er værdifuld at standardisere. En Dataanvender forholder sig typisk til data fra mange forskellige kilder, og det vil være omkostningsfyldt at skulle anvende mange forskelligartede tekniske specifikationer.

* [**IHE XDS**](https://wiki.ihe.net/index.php/Cross-Enterprise_Document_Sharing) er en sundhedsspecifik profilering af ebXML Messaging Service Specifications med anvendelse af HL7 CDA som dokumentmodel. IHE XDS er identificeret til anvendelse i offentlige udbud af EU. Specifikationer er profileret til dansk brug af Sundhedsdatastyrelsen og er i anvendelse i 2018.
* [**OGC Webservice Standards**](http://www.opengeospatial.org/standards/common) er en geodataspecifik profilering af ebXML. INSPIRE direktivet EU 2010/1089 forpligter medlemslandene til at udstille geodata i en fælles datamodel. Styrelsen for dataforsyning og effektivisering implementerer specifikationerne for danske data.
* [**DK-REST**](/node/1094#bilag-1---dokumentation-for-rest-webservices) er en profilering af en række webstandarder, herunder W3C’s HTTP-specifikation og JSON (ECMA-404). Profilen udarbejdes af Digitaliseringsstyrelsen og afprøves i foråret 2018 i et eller flere projekter under Digitaliseringsstrategien.
* [**HL7 FHIR**](https://www.hl7.org/fhir/) er en international, sundhedsspecifik profilering af en række webstandarder, herunderW3C’s HTTP-specifikation.
* [**Linked Data Platform 1.0**](http://www.w3.org/TR/ldp/) er en samling af W3C-specifikationer relateret til anvendelse af Resource Description Framework (RDF) over HTTP. De fællesoffentlige regler for begrebs- og datamodellering indeholder en profilering af bl.a. RDF.
* [**OIO IDWS**](https://digitaliser.dk/resource/3457606) er en samling af profiler af SOAP og WS-Trust specifikationerne og er udviklet i fællesoffentligt regi.

##### Log over videregivelse

Ved videregivelse af persondata er dataansvarlig forpligtiget til at logge dette. Med henblik på muligheden for at lade den registreredes ret til indsigt implementere som en selvbetjeningsløsning er det nødvendigt at specificere indholdet af loggen.

* [**Vejledning om logning**](https://digst.dk/styring/standardkontrakter/klausuler-til-informationssikkerhed/logning/) er en specifikation af minimumsindhold i logning ved videregivelse af persondata udformet af Digitaliseringsstyrelsen i forbindelse med DK-REST.
* [**IHE ATNA**](https://wiki.ihe.net/index.php/Audit_Trail_and_Node_Authentication) er en sundhedsspecifik teknisk specifikation af snitflader til og indhold af logning.

##### Indeks over dokumenter

Ved registrering af dokumenter i indeks er det nødvendigt at have en fælles specifikation for data om dokumenter.

* [**IHE XDS Metadata**](https://wiki.ihe.net/index.php/Cross-Enterprise_Document_Sharing) er en sundhedsspecifik profilering af ebXML Registry Information Model. Sundhedsdatastyrelsen har yderligere profileret denne til dansk brug.

##### Meddelelse om ændring i datasamling

Hvis en dataservice tilbyder en dataabonnementsservice:

* [**IHE D-SUB**](https://wiki.ihe.net/index.php/Document_Metadata_Subscription) er en international sundhedsspecifik profil af OASIS Web Services Notification.
* **OIO hændelsesbesked** er en teknisk specifikation af meddelelser om ændringer i datasamlinger. Specifikationen er profileret af både KOMBIT og Styrelsen for dataforsyning og effektivisering.

##### Beskrivelse af datasamling

Datasamlinger kan beskrives i kataloger og oplysninger om samlinger og deres indhold kan udveksles ved brug af tekniske specifikationer.

* **ADMS** er en anvendelsesprofil af DCAT til brug for beskrivelse af blandt andet datasæt. Digitaliseringsstyrelsen har udarbejdet en DCAT profil til anvendelse i Datavejviser. ADMS anvendes tillige i EU, se [https://joinup.ec.europa.eu](https://joinup.ec.europa.eu).
* **XMI** er en XML-profil til beskrivelse af modeller. De fællesoffentlige regler for begrebs- og datamodellering indeholder en profilering til brug ved udveksling af modeller.

##### Distribution af meddelelser

Ved distribution af meddelelser er det nødvendigt at specificere, hvordan de nødvendige egenskaber opfyldes ved brug af tekniske specifikationer.

* **AS4** er en profilering af ebMS til anvendelse ved elektronisk forsendelse af meddelelser. Profilen er udviklet af PEPPOL og vedligeholdes i dag af OASIS.

##### Meddelelsesheader

Ved distribution af meddelelser anvendes ofte et standardiseret minimumsindhold eller ’elektronisk ku- vert.’

* **SBDH** er en teknisk specifikation af indholdet en meddelelsesheader. Den er profileret til anvendelse i dansk e-handel af Digitaliseringsstyrelsen. Specifikationen forventes erstattet af en kommende fælles specifikation mellem OASIS og UN/CEFACT.
* **Digital Post Meddelelsesmodel** er en begrebsmodel til anvendelse i næste generation Digital Post, der pr. 2018 er under anskaffelse af Digitaliseringsstyrelsen.

##### Adresser

Ved anvendelse af flere forsendelsesservices er det ønskeligt at have en standard for at finde hvilke serviceudbydere, der kan modtage hvilke typer meddelelser på vegne af en modtager.

* **Service Metadata Publisher** (SMP) er en teknisk specifikation udgivet af OASIS og anvendes til udstilling af oplysninger om modtagers services og deres ønskede anvendelser (Metadata Management Services i EIRA). SMP er identificeret til anvendelse i offentlige udbud i EU. Specifikationen er profileret i eDelivery og anvende blandt andet af PEPPOL.
* **BDX Location** er en teknisk specifikation udgivet af OASIS og beskriver i EIRA Service Discovery Services, der anvendes til at lokalisere Metadata Management Services (SMP’er). BDX Location er identificeret til anvendelse i offentlige udbud i EU. Specifikationen er profileret i eDelivery og anvendes blandt andet af PEPPOL.
* **CorePartyID** er den tekniske specifikation for angivelse af identifikation af modtager ved hjælp af en URI og er profileret af PEPPOL til anvendelse ved forsendelse af elektroniske fakturaer i EU.

Digitaliseringsstyrelsen har i efteråret 2017 gennemført en dokumentation af den danske offentlige sek- tors datainfrastruktur, hvor flere datadistributørers løsninger beskrives.

Digitaliseringsstyrelsen har i 2017 gennemført en foranalyse om eDelivery-anvendelse i Danmark. Med udgangspunkt i foranalysen er det besluttet at igangsætte analysefasen af et eDelivery-implementerings- projekt. Analysefasen gennemføres i 2018 med fokus på strategiske gevinster samt fastlæggelse af tekni- ske, organisatoriske og økonomiske rammer for en efterfølgende implementering og udrulning.

#### 4.5.2 Øvrige standarder

##### Organisatoriske standarder og aftaler

Standardisering af Deling af data og dokumenter på det organisatoriske plan indbefatter bl.a. nedenstå- ende elementer. Der har dog i udarbejdelsen af denne referencearkitektur ikke været muligt at gå i detaljer med hverken afdækning eller specifikation af disse elementer.

* **Aftale** om systemtilslutning samt databehandleraftaler
* **Samtykke** til videregivelse af personoplysninger
* Specifikation af **dataleverance**

##### Semantiske standarder og begrebsmodeller

Standardisering på det semantiske niveau er nødvendig for at sikre, at systemer kan ’tale sammen’. Her er det særligt vigtigt at fremhæve forskellige aspekter af informationssikkerhed som emner, der er vær- difulde at adressere i et standardiseringsarbejde:

* **Metadata** for opslag/søgning/anvendelse samt kontekst
* **Hjemmel** (samtykke, lov)
* **Kontekst** (klassifikation af anvendelse)
* **Klassifikation** af følsomhed

## 5 Perspektivering

I dette afsnit fremhæves en række punkter, hvor arbejdet i denne referencearkitektur peger frem mod yderligere initiativer, eller hvor indholdet i referencearkitekturen (fx set i kontekst af teknologitrends) giver interessante fremtidsperspektiver.

### Anvendelse og genbrug af data i tværgående processer

Dette dokument centrerer sig om at beskrive begreber og mønstre for den konkrete videregivelse af data. Imidlertid vil genbrug af data typisk understøtte et konkret anvendelsesscenarie og dermed finde sted i kontekst af en proces, der kan gå på tværs af myndigheder, virksomheder og borgere. En sådan proces vil, specielt hvis den afvikles over tid, have sine egne udfordringer i forhold til indhentning, sammenstilling og opbevaring af de data, der genbruges fra eksisterende datasamlinger. Disse udfordringer inkluderer:

* Klassifikation af samt konteksten for processen skal beskrives (er det en sag? et selvbe- tjeningsforløb? en udbetaling af en ydelse?)
* Der er behov for principper omkring sikring af dataaktualitet (hvordan og hvornår tjek- kes, om data indhentet tidligere i et procesforløb fortsat er aktuelle?)
* I hvilke situationer overdrages dataansvaret i forbindelse med en konkret videregivelse af data?
* Der er behov for et designmønster til at sikre, at en svar-meddelelse i en dobbelt-anven- delse af mønsteret Videregivelse via meddelelse til at implementere et asynkront request/re- sponse-mønster kan finde tilbage til den konkrete procesinstans, der afsendte forespørg- sel-meddelelsen
* Der er behov for at forholde sig til, hvor og hvordan de data, der er blevet indhentet af en specifik procesinstans, opbevares undervejs (ift. sikkerhed, fortrolighed m.m.)
* Der er behov for at afklare, hvordan personhenførbare data, der er omfattet af GDPR’s ret til at blive glemt, og som er indhentet af en proces og dermed har et midlertidigt ”liv” i en specifik procesinstans, skal håndteres, hvis den registrerede gør brug af retten til at blive glemt.

### Log

Denne referencearkitektur har benyttet komponenten log i betydningen en persondataanvendelseslog. Formålet med og brugen af en log-komponent er klart beskrevet, hvorimod den indholdsmæssige modellering af selve indholdet i loggen er forbigået. Det vil være hensigtsmæssigt at adressere en fælles modellering af en persondataanvendelsesloginddatering i det videre arbejde omkring standardisering af begreber relateret til videregivelse af data.

### Samtykker

I denne referencearkitektur har vi talt om den registrerede, afsender og modtager som roller, der indtages af en ’direkte’ aktør, fx den virksomhed eller den borger, der er part i en given sags- eller procesforløb. Imidlertid kan en anden aktør i praksis agere på vegne af den underliggende aktør (partsrepræsentation), hvis sidstnævnte har givet behørigt samtykke. Det kan fx være en advokat, der opererer på vegne af en klientvirksomhed, eller en borger, der har fuldmagt/samtykke fra et familiemedlem til at agere på vegne af vedkommende. Samtykker udfolder sig som begreb hovedsageligt inden for brugerstyringsområdet. En yderligere udfoldning af samtykke-begrebet i FDA-sammenhæng, herunder en afklaring af særlige aspekter, der indvirker på videregivelse af data, ville være værdifuld set fra denne referencearkitekturs synspunkt.

### Standardisering

Afsnit 4.5 har peget på en række områder, hvor standardisering vil være fordelagtig for at forløse denne referencearkitekturs overordnede mål om at gøre det enklere at dele og genbruge data. I det videre arbejde med at skabe gode rammer for deling af data og dokumenter blandt offentlige myndigheder, virksomheder og borgere i Danmark vil være formålstjenligt at definere initiativer, der kan adressere de standardiseringsbehov, der er identificeret her, gennem yderligere analyse og anbefalinger.

### Blockchain

Blockchain er en ny teknologi, der på tidspunktet for dette dokuments udarbejdelse har givet anledning til en trend. Blockchain er baseret på et fuldt distribueret og modifikationssikret datasæt og kendes særligt fra kryptovalutaer (med Bitcoin som den mest kendte). Samtidigt foregår der en afsøgning af blockchain-teknologiens muligheder generelt. I sammenhæng med denne referencearkitektur bemærker vi, at blockchain kan være en måde at implementere integritetssikret anvendelseslog på. Blockchain kan også udgøre en dataplatform som beskrevet i afsnit 4.2.3. Dog vil det medføre, at ikke blot den fysiske platform, men også forretningsrollen ’platformsansvarlig’ bliver distribueret, hvilket vil have konsekvenser fx i forhold til håndhævelse af adgangskontrol, der skal afsøges yderligere.

### Øvrige anvendelser af data

Afsnit 3.1 beskriver en række (gen)-anvendelser af data, der rækker ud over digital selvbetjening i offentlige sammenhænge. Der er behov for at understøtte disse anvendelser også, evt. ved at introducere yderligere forretnings- og implementeringsmønstre.

## 6 Bilag

### 6.1 Bilag A: Tjekliste for anvendelse af referencearkitekturen

Denne tjekliste kan anvendes af projekter, der designer, bestiller eller udvikler løsninger til deling af data. Tjeklisten trækker mange af de væsentligste punkter fra denne referencearkitektur frem og er desuden skrevet med projektarbejde for øje, i det den fremhæver mange af de nødvendige afklaringer, der skal foretages i projektsammenhæng.

Punkterne i tjeklisten følger opdelingen i _interoperability levels_ fra European Interoperability Framework (EIF). EIF benytter fire niveauer for interoperabilitet: Legal (L), Organisational (O), Semantic (S) og Technical (T). Nummereringen nedenfor afspejler, hvilket interoperabilitetsniveau det enkelte punkt er relevant for.

Tjeklisten anvendes desuden som en del af det arkitekturmæssige review af projektet.

| Nr. | Arkitekturegenskaber                                                                                                                                                                                                                                                                                                                   | Reference til afsnit i referencearkitekturen                              | Reference til hvidbog                                                                                                                          |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| L1  | Har projektet identificeret, hvilke data der udveksles mellem aktører, samt om data er klassificeret i forhold til persondatalov og GDPR?                                                                                                                                                                                              | 3.6 Forretningsobjekter og begreber                                       | 3: Arkitektur og regulering understøtter hinanden<br><br>4: Sikkerhed, privatliv og tillid sikres<br><br>6: Gode data deles og genbruges       |
| L2  | Har projektet identificeret, om det data, der adresseres, er beskrevet i offentlige kataloger i form af datasamlinger og datamodeller?                                                                                                                                                                                                 | 3.6 Forretningsobjekter og begreber                                       | 6: Gode data deles og genbruges                                                                                                                |
| L3  | Er det undersøgt, med hvilken hjemmel i GDPR eventuelle persondata tænkes videregivet, samt om denne hjemmel er yderligere beskrevet i dansk lovgivning?                                                                                                                                                                               | 2.5 Juridiske rammer                                                      | 3: Arkitektur og regulering understøtter hinanden<br><br>4: Sikkerhed, privatliv og tillid sikres                                              |
| L4  | Har projektet afklaret, hvilke aftaler mellem dataansvarlig, dataanvender og eventuelle databehandlere som er nødvendige (databehandleraftale, Service Level Agreement, håndhævelse af adgangskontrol m.m.)?                                                                                                                           | 3.4 Forretningsroller og aktører  <br>4.1 Nødvendige applikationsservices | 1: Arkitektur styres på rette niveau efter fælles rammer<br><br>3: Arkitektur og regulering understøtter hinanden                              |
| L5  | Har projektet afklaret, hvem der har ansvaret for "den registreredes" ret til indsigt i opbevaring og videregivelse af persondata, samt igennem hvilken brugerflade/proces, dette sker?<br><br>Er der forskel på, hvem der er responsible (dataansvarlig) og accountable (måske en datadistributør)?                                   | 3.3 Forretningsroller og aktører                                          | 3: Arkitektur og regulering understøtter hinanden<br><br>5: Processer optimeres på tværs                                                       |
| O1  | Er det klarlagt, hvilken/hvilke forretningsprocesser, den specifikke videregivelse af data indgår i?<br><br>Og om data videregives på forespørgsel eller ved meddelelse?                                                                                                                                                               | 1.5 Tværgående processer                                                  | 5: Processer optimeres på tværs<br><br>6: Gode data deles og genbruges                                                                         |
| O2  | Er udvekslede meddelelser, der videregiver data, egnet til at indgå i offentlig forvaltning?<br><br>Kan de knyttes til sager, journalplaner og parter?<br><br>Er meddelelsen forberedt på arkivering?<br><br>Skal meddelelsen konsolideres i et dokument egnet til visning til borgere?                                                | 3.2 Om data og dokumenter                                                 | 3: Arkitektur og regulering understøtter hinanden<br><br>5: Processer optimeres på tværs                                                       |
| O3  | Er det afklaret, hvordan ændringer til fælles informationsmodeller, referencedata, applikationsprofiler og specifikationer, der påtænkes anvendt i projektet, håndteres?<br><br>Kan projektet blive ramt af ændringer?<br><br>Kan projektet anmode om ændringer?                                                                       | 3.6 Forretningsobjekter og begreber                                       | 1: Arkitektur styres på rette niveau efter fælles rammer                                                                                       |
| O4  | Er den overliggende forretningsproces/anvendelse de- signet til at håndtere fejlscenarier ifm. tjek af hjemmel, fx at en dynamisk angivet hjemmel (angivet i fore- spørgslen) ikke vurderes gyldig af dataansvarlig, eller at negativt samtykke forhindrer videregivelsen?                                                             | 3.5.1 Videregivelse på forespørgsel                                       | 5: Processer optimeres på tværs                                                                                                                |
| O5  | Benyttes den autoritative datasamling direkte?<br><br>Hvis der benyttes en dataservice eller en distributionskopi, er alle evt. begrænsninger ift. datakvalitet, aktualitet m.m. da velbeskrevne fra distributøren?<br><br>Og er der taget stilling til hvor og hvordan log af persondataanvendelse konsolideres?                      | 3.5.1 Videregivelse på forespørgsel                                       | 7: It-løsninger samarbejder effektivt<br><br>8: Data og services leveres driftssikkert                                                         |
| O6  | Er der taget stilling til, hvordan hjemmel skal angives og håndhæves, herunder om det skal ske design-time (hvor forespørgsler fra en given Dataanvender altid accpteres), runtime (hvor hjemmel angives dynamisk) eller reaktivt (hvor evt. misbrug spores gennem loggen)?                                                            | 3.5.1 Videregivelse på forespørgsel                                       | 3: Arkitektur og regulering understøtter hinanden<br><br>4: Sikkerhed, privatliv og tillid sikres<br><br>7: It-løsninger samarbejder effektivt |
| O7  | Har projektet afklaret, hvilken organisation der skal bære omkostningen ved videregivelse af data på forespørgsel - herunder, om det er en dataansvarlig, en distributør eller en platformsansvarlig?                                                                                                                                  | 4.2 Implementering af videregivelse på forespørgsel                       | 1: Arkitektur styres på rette niveau efter fælles rammer                                                                                       |
| O8  | Har projektet klarlagt, om genbrug af data involverer transformation mellem datamodeller?<br><br>\- Hvis ja, er det afklaret, om dette skal ske på Anvenderside eller om det skal ske i en anvendelsesorienteret dataservice?<br><br>Er der afklaring om governance ift. fremtidigt vedligehold af datamodeller/transformation?        | 4.2 Implementering af videregivelse på forespørgsel                       | 6: Gode data deles og genbruges                                                                                                                |
| O9  | Har projektet klarlagt, om en modtager, der er en organisation, har særlige krav/ønsker til at kunne route meddelelsen efter modtagelse?                                                                                                                                                                                               | 3.5.2 Videregivelse ved meddelelse                                        | 5: Processer optimeres på tværs                                                                                                                |
| O10 | Hvis servicefællesskab-mønsteret for meddelelser anvendes, er det da klarlagt, hvilke organisationer der er ansvarlige for service provider agreements?                                                                                                                                                                                | 3.5.2 Videregivelse ved meddelelse                                        | 1: Arkitektur styres på rette niveau efter fælles rammer<br><br>3: Arkitektur og regulering understøtter hinanden                              |
| S1  | Har projektet afklaret, hvor der sker sammenstilling og transformation af data? Om der anvendes fælles referencedata og oversættelser?                                                                                                                                                                                                 | 3.5.1 Videregivelse på forespørgsel                                       | 5: Processer optimeres på tværs  <br>6: Gode data deles og genbruges                                                                           |
| S2  | Har projektet taget stilling til anvendelse af selvbeskrivende data som beskrevet i niveau 3 af de Fællesoffentlige regler for begrebs- og datamodellering? Både ift. genbrug af eksisterende, selvbeskrivende data, samt ift. om data, som projektet selv skal gøre tilgængeligt for andre, skal modelleres som selvbeskrivende data? | 4.1.1 Ønskelige egenskaber ved videregivelse                              | 6: Gode data deles og genbruges                                                                                                                |
| T1  | Har projektet anvendt relation til EIRA og andre internationale modeller med henblik på at identificere standarder og specifikationer som udgangspunkt for anvendelsesprofiler?                                                                                                                                                        | 6.6 Bilag F: Mapning til EIRA                                             | 1: Arkitektur styres på rette niveau efter fælles rammer<br><br>2: Arkitektur fremmer sammenhæng, innovation og effektivitet                   |
| T2  | Har projektet vurderet og prioriteret de forskellige implementeringsmønstre for videregivelse hhv. på forespørgsel eller ved meddelelse?<br><br>Er skalerbarhed overvejet, både på kort sigt og i forhold til langsigtede behov?                                                                                                       | 4.2/4.3 Implementering af videregivelse på forespørgsel/ved meddelelse    | 7: It-løsninger samarbejder effektivt<br><br>8: Data og services leveres driftssikkert                                                         |
| T3  | Er der taget stilling til, om en påtænkt, ny anvendelse har et omfang, der påvirker en eksisterende data- eller forsendelsesservices robusthed (ift. SLA/availability)?                                                                                                                                                                | 4.1.1 Ønskelige egenskaber ved videregivelse                              | 8: Data og services leveres driftssikkert                                                                                                      |
| T4  | Er det afklaret, hvordan den enkelte meddelelses integritet og fortrolighed sikres?                                                                                                                                                                                                                                                    | 4.1.1 Ønskelige egenskaber ved videregivelse                              | 4: Sikkerhed, privatliv og tillid sikres                                                                                                       |
| T5  | Er der taget stilling til, hvordan log/logdata beskyttes? -Både med hensyn til fortrolighed, integritet og tilgængelighed?                                                                                                                                                                                                             | 4.1.1 Ønskelige egenskaber ved videregivelse                              | 4: Sikkerhed, privatliv og tillid sikres                                                                                                       |
| T6  | Har projektet afklaret, hvordan dataanvender skal identificere sig over for data- eller forsendelsesservices og hvilken komponent der håndhæver adgangskontrol?                                                                                                                                                                        | 4.1.1 Ønskelige egenskaber ved videregivelse                              | 4: Sikkerhed, privatliv og tillid sikres                                                                                                       |
| T7  | Indebærer forespørgslen på data en søgning/brug af indeks? Og er det afklaret hvem der har dataansvar herfor?                                                                                                                                                                                                                          | 3.5.1 Videregivelse på forespørgsel                                       | 5: Processer optimeres på tværs                                                                                                                |
| T8  | Har projektet klarlagt evt. eksisterende message-infrastruktur hos hhv. afsender og modtager?                                                                                                                                                                                                                                          | 4.3 Implementering af videregivelse ved meddelelse                        | 5: Processer optimeres på tværs<br><br>7: It-løsninger samarbejder effektivt                                                                   |
| T9  | Har projektet klarlagt, om der findes et adresseregister, der kan genbruges til adressering af meddelelser og påmindelser?                                                                                                                                                                                                             | 3.5.2 Videregivelse ved meddelelse                                        | 5: Processer optimeres på tværs<br><br>7: It-løsninger samarbejder effektivt                                                                   |

### 6.2 Bilag B: Ord- og begrebsliste

Listen på de næste sider definerer og forklarer betydningen af de væsentligste ord og begreber, der indgår i den fællesoffentlige referencearkitektur for deling af data og dokumenter.

#### Begrebsliste: Begrebsmodel

##### Forretningsmetadata:

**Namespace** : data.gov.dk/datasharing

**Prefix** : **Modelnavn** (label): Videregivelse af data

**Modelejer** (publisher): Digitaliseringsstyrelsen

**Versionnummer** (versionInfo): 1. 0

**'Seneste opdateringsdato** (dateModified): 26 - 04 - 2018

**Modelstatus** (modelStatus): development

**Godkendelsesstatus** (approvalStatus) : in review

**Forretningsområde** (theme): 06.38.10 Digital Infrastruktur

**Juridisk** kilde (legalSource): Databeskyttelsesforordningen (GDPR) (EU) 2016/679; Fordning om elektroniske tillidstjenester (eIDAS) (EU) 2014/910

**Kilde** (source): Fællesoffentlig Digital Arkitektur (arkitektur.digst.dk), Archimate 3.0.1 Specification (via opengrup.org)

**Kommentar** (comment): begrebsmodel under udarbejdelse i forbindelse med referencearkitektur for deling af data og dokumenter

#### Begreber

| Foretrukken dansk term                   | Accepteret dansk term                                                         | Frarådet dansk term | Definition                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Eksempel                                                                                                                                                         | Kommentar                                                                                                                                                                                  | Juridisk kilde | Kilde                                                          |
| ---------------------------------------- | ----------------------------------------------------------------------------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------- | -------------------------------------------------------------- |
| _besked_                                 |                                                                               |                     | _Skriftlig eller mundtlig oplysning som sendes eller overbringes til andre_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |                                                                                                                                                                  |                                                                                                                                                                                            |                | [Den Danske Ordbog](https://ordnet.dk/ddo/ordbog?query=besked) |
| data                                     |                                                                               |                     | _Information lagret med henblik på (gen)anvendelse_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                                                                                                  | Tidligere dansk definition: repræsentation af fakta eller idé i enhver en sådan form, at den kan kommunikeres eller omformes ved en eller anden proces \[Bogen om EDB. H.B. Hansen, 1969\] |                | [ISO/IEC 111794:2004](https://www.iso.org/standard/35346.html) |
| dataansvarlig                            | persondataansvarlig                                                           |                     | _en fysisk eller juridisk person, en offentlig myndighed, en institution eller et andet organ, der alene eller sammen med andre afgør, til hvilke formål og med hvilke hjælpemidler der må foretages behandling af personoplysninger_                                                                                                                                                                                                                                                                                                                                                                                                                                              | En privatpraktiserende læge er dataansvarlig for hendes patientjournal                                                                                           |                                                                                                                                                                                            | (EU) 2016/679  |                                                                |
| databehandler                            | persondatabehandler                                                           |                     | _en fysisk eller juridisk person, en offentlig myndighed, en institution eller et andet organ, der behandler personoplysninger på den dataansvarliges vegne_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Driftleverandøren af en database til en offentlig myndighed er databehandler på vegne af denne.                                                                  |                                                                                                                                                                                            | (EU) 2016/679  |                                                                |
| **dataabonnement**                       | abonnement på registreringshændelser; abonnement på ændringer i datasamlinger |                     | abonnement der specificerer hvilke meddelelser - om ændringer til en datasamling - en beskedmodtager ønsker at modtage                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | En kommune kan have et dataabonnement der sender meddelelser ved ændringer i CPR oplysninger for kommunens indbyggere.                                           | Her indskrænket til at omhandle ændringer i datasamlinger i modsætning til abonnement på forretningshændelser                                                                              |                | FDA Referencearkitektur for deling af data og dokumenter       |
| adgangskontrol                           |                                                                               |                     | _forretningsfunktion der afgør hvilke funktioner og data en bruger får adgang til på baggrund af brugerens attributter og tjenestens sikkerhedspolitik_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |                                                                                                                                                                  | ændret process til forretningsfunktion jf archimate.                                                                                                                                       |                | FDA Referencearkitektur for brugerstyring                      |
| adgangspolitik                           |                                                                               |                     | _definition af kriterierne for at få adgang til en applikationsservice._                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | En skoleleder kan have adgang til CPR oplysninger hvis personen er elev, ansat på skolen eller pårørerende til elever.                                           | ændrer it service til applikationsservice jf archimate                                                                                                                                     |                | FDA Referencearkitektur for brugerstyring                      |
| **elektronisk adresse**                  | adresse til modtagelse af elektroniske meddelelser; adresse                   |                     | _dataobjekt der angiver hvor en person eller organisation ønsker at modtage bestemte typer af elektroniske meddelelser_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | e-mail eller EAN/GLN-nummer med tilhørende angivelse af hvilke typer af meddelelser der kan modtages fx fakturaer                                                |                                                                                                                                                                                            |                | FDA Referencearkitektur for deling af data og dokumenter       |
| **afsender af elektroniske meddelelser** |                                                                               |                     | _afsender person eller organisation, der sender en elektronisk meddelelse_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | En kommune, der sender et meddelelse via Digital Post til en borger, er en (offentlig) afsender                                                                  |                                                                                                                                                                                            |                | FDA Referencearkitektur for deling af data og dokumenter       |
| **dataanvender**                         | anvender af data; anvender                                                    |                     | _person eller organisation der behandler data til eget formål_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Danmarks Statistik anvender data om CPR data til udarbejdelse af levealdersstatisk                                                                               |                                                                                                                                                                                            |                | FDA Referencearkitektur for deling af data og dokumenter       |
| behandling af personoplysninger          | persondatabehandling; behandling af persondata; behandling; databehandling    |                     | enhver aktivitet eller række af aktiviteter — med eller uden brug af automatisk behandling — som personoplysninger eller en samling af personoplysninger gøres til genstand for, f.eks:<br><br>*   indsamling<br>    <br>*   registrering<br>    <br>*   organisering<br>    <br>*   systematisering<br>    <br>*   opbevaring<br>    <br>*   tilpasning eller ændring<br>    <br>*   genfinding<br>    <br>*   søgning<br>    <br>*   brug<br>    <br>*   videregivelse ved transmission<br>    <br>*   formidling eller enhver anden form for overladelse<br>    <br>*   sammenstilling eller samkøring<br>    <br>*   begrænsning<br>    <br>*   sletning eller tilintetgørelse |                                                                                                                                                                  |                                                                                                                                                                                            | (EU) 2016/679  |                                                                |
| brugerstyring                            |                                                                               |                     | _håndhævelse af adgangskontrol og administration af brugere og deres rettigheder_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |                                                                                                                                                                  | egen definition                                                                                                                                                                            |                | FDA Referencearkitektur for brugerstyring                      |
| **databehandling**                       |                                                                               |                     | _behandling af persondata eller anden data i en organisation_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | En skole behandler oplysninger om elevers karakter                                                                                                               |                                                                                                                                                                                            |                | FDA Referencearkitektur for deling af data og dokumenter       |
| **datadistributør**                      | datafordeler; distributør                                                     |                     | _databehandler der som databehandler giver anvendere adgang til data på vegne af den dataansvarlige_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Styrelsen for Dataforsyning og Effektivisering distribuerer CPR data på vegne af Indenrigsministeriets CPR kontor                                                |                                                                                                                                                                                            |                | FDA Referencearkitektur for deling af data og dokumenter       |
| **datasamling**                          | datasæt; register; registrant                                                 |                     | en samling af oplysninger bestående af enkelte dele der forvaltes under et                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | CPR registeret, Det Interregionale billedindex (IBI)                                                                                                             | Minder om begrebet ’arkiv’ fra Sag og Dokument, samt om PSI lovens definition af datasamling. Det kan overvejes at anvende PSI definitionen.                                               |                | FDA Referencearkitektur for deling af data og dokumenter       |
| **dataservice**                          |                                                                               |                     | _applikationsservice der videregiver oplysninger fra datasamlinger på forespørgsel under håndhævelse af nødvendig adgangskontrol_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Kommunernes serviceplatform udstiller en person-service til opslag i CPR og skoledistrikter.                                                                     | oftest ved håndhævelse af adgangskontrol, men ikke nødvendigvis                                                                                                                            |                | FDA Referencearkitektur for deling af data og dokumenter       |
| den registrerede                         | datasubjekt                                                                   |                     | _person om hvem oplysninger behandles_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |                                                                                                                                                                  | egen definition                                                                                                                                                                            | (EU) 2016/679  |                                                                |
| **distributionskopi**                    |                                                                               |                     | _kopi af datasamling der opbevares hos databehandler med henblik på distribution efter instruks fra dataansvarlig_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |                                                                                                                                                                  |                                                                                                                                                                                            |                | FDA Referencearkitektur for deling af data og dokumenter       |
| dokument                                 |                                                                               |                     | _afgrænset samling af informationer, i en kendt struktur, gemt på et kendt medie_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Dokumenter i ESDH systemer, patientjournaler, selvbetjeningsløsninger og vedhæftet digitale post meddelelser                                                     |                                                                                                                                                                                            |                | OIO Referencearkitektur for Sag og Dokument                    |
| **forespørgsel**                         |                                                                               |                     | request _meddelelse der sendes til en dataservice med forventning om svar indeholdende specifikke data_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | En link på en hjemmeside er en forespørgsel til en server der svarer med en hjemmeside                                                                           |                                                                                                                                                                                            |                | FDA Referencearkitektur for deling af data og dokumenter       |
| **forsendelsesservice**                  | elektronisk leveringstjeneste                                                 |                     | _applikationsservice, der gør det muligt at sende og modtage meddelelser samt dokumenterer behandlingen af disse, herunder leverer bevis for afsendelse og modtagelse af dataene, og som beskytter dem mod tab, tyveri, beskadigelse og uautoriseret ændring_                                                                                                                                                                                                                                                                                                                                                                                                                      | Bemærk at denne definition ikke kræver at en applikationsservice er registreret, men alene udtaler sig om funktionelle egenskaber.                               | egen definition                                                                                                                                                                            | (EU) 2014/910  |                                                                |
| _fuldmagt_                               |                                                                               |                     | _formel tilladelse til at handle på vedkommendes vegne i nærmere bestemte situationer_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |                                                                                                                                                                  |                                                                                                                                                                                            |                | Den Danske Ordbog                                              |
| hjemmel til behandling af persondata     | hjemmel                                                                       |                     | _forhold der gør behandling af persondata lovlig_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |                                                                                                                                                                  | egen definition.                                                                                                                                                                           | (EU) 2016/679  |                                                                |
| indsigt i behandling af persondata       | persondataindsigt; indsigt                                                    |                     | _den registreredes indsigt i opbevaring, anvendelse, videregivelse og anden behandling af persondata omhandlende sig selv_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |                                                                                                                                                                  | egen definition                                                                                                                                                                            | (EU) 2016/679  |                                                                |
| personoplysninger                        | persondata                                                                    |                     | _enhver form for information om en identificeret eller identificerbar fysisk person (»den registrerede«); ved identificerbar fysisk person forstås en fysisk person, der direkte eller indirekte kan identificeres, navnlig ved en identifikator som f.eks. et navn, et identifikationsnummer, lokaliseringsdata, en onlineidentifikator eller et eller flere elementer, der er særlige for denne fysiske persons fysiske, fysiologiske, genetiske, psykiske, økonomiske, kulturelle eller sociale identitet_                                                                                                                                                                      |                                                                                                                                                                  |                                                                                                                                                                                            | (EU) 2016/679  |                                                                |
| **persondatalog**                        | log over videregivelse af persondata; persondatalog; log                      |                     | _datasamling der beskriver de faktiske, historiske videregivelse af oplysninger i en given datasamling, herunder med hvilken hjemmel, behandlingen er sket_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | MinLog på sundhed.dk dokumenterer hvem der har haft adgang til en persons sundhedsdata                                                                           |                                                                                                                                                                                            |                | FDA Referencearkitektur for deling af data og dokumenter       |
| **meddelelse**                           | elektronisk meddelelse;                                                       |                     | _formel besked der sendes elektronisk med veldefineret sikkerhed, tillid, integritet og leverancesikkerhed_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |                                                                                                                                                                  | En e-mail sendt via sikker e-mail mellem myndigheder betragtes som ulæselig for andre end modtagerens organisation, men den er ikke garanteret at nå frem.                                 |                | FDA Referencearkitektur for deling af data og dokumenter       |
| **modtager af elektroniske meddelelser** |                                                                               |                     | modtager forretningsrolle (person eller organisation), der modtager elektronisk meddelelse                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | En borger kan være modtager af en meddelelse sendt via Digital Post                                                                                              |                                                                                                                                                                                            |                | FDA Referencearkitektur for deling af data og dokumenter       |
| **påmindelse**                           | advis; notifikation                                                           |                     | _en besked der får modtager til at tænke på en vigtig begivenhed_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |                                                                                                                                                                  | Typisk uden behandling eller dokumentation af beskyttelse jf meddelelse.                                                                                                                   |                | FDA Referencearkitektur for deling af data og dokumenter       |
| _registrator_                            |                                                                               |                     | _person eller apparat der registrerer noget_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |                                                                                                                                                                  |                                                                                                                                                                                            |                | Den Danske Ordbog                                              |
| _retskilde_                              |                                                                               |                     | _omstændighed som er med til at fastlægge gældende ret ved løsningen af juridiske problemer_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Persondatalov, Arkivlov                                                                                                                                          | omfatter først og fremmest loven og retspraksis. Her mere specifikt retskilde der beskriver forhold om behandling af ((person)data                                                         |                | Den Danske Ordbog                                              |
| adgangsrettighed                         |                                                                               |                     | _rettighed der tildeles en bruger eller roller, der giver adgang til at udføre funktioner i et it-system._                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |                                                                                                                                                                  | egen definition                                                                                                                                                                            |                | FDA Referencearkitektur for brugerstyring                      |
| samtykke til persondatabehandling        |                                                                               |                     | _klar bekræftelse, der indebærer en frivillig, specifik, informeret og utvetydig viljestilkendegivelse fra den registrerede, hvorved vedkommende accepterer, at personoplysninger om vedkommende behandles_                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |                                                                                                                                                                  |                                                                                                                                                                                            | (EU) 2016/679  |                                                                |
| **svar**                                 | respons                                                                       |                     | _meddelelse dannet af dataservice som besvarer en forespørgsel_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |                                                                                                                                                                  |                                                                                                                                                                                            |                | FDA Referencearkitektur for deling af data og dokumenter       |
| **videregivelse af data**                | deling af data; datadeling                                                    |                     | _forretningsfunktion hvorved data overføres ud af organisation ._                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | sende meddelelse indeholdende sagsoplysninger; Sundhedsdatastyrelsen videregiver medicinoplysninger fra Fælles Medicinkort til SOSU assistenter i Ålborg Kommune |                                                                                                                                                                                            |                | FDA Referencearkitektur for deling af data og dokumenter       |
| **videregivelse på forespørgsel**        |                                                                               |                     | _integrationsmønster hvor data videregives af dataansvarlig på forespørgsel på anvenders initiativ_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |                                                                                                                                                                  |                                                                                                                                                                                            |                | FDA Referencearkitektur for deling af data og dokumenter       |
| **videregivelse ved meddelelse**         |                                                                               |                     | _integrationsmønster hvor data videregives ved meddelelse af dataansvarlig på dennes initiativ_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |                                                                                                                                                                  |                                                                                                                                                                                            |                | FDA Referencearkitektur for deling af data og dokumenter       |

#### Begreber oversat og anvendt fra Archimate©

| Foretrukken dansk term | Accepteret dansk term                       | Frarådet dansk term | Definition                                                                                       | Eksempel                        | Kommentar         | Juridisk Kilde | Kilde                   |
| ---------------------- | ------------------------------------------- | ------------------- | ------------------------------------------------------------------------------------------------ | ------------------------------- | ----------------- | -------------- | ----------------------- |
| dataobjekt             |                                             |                     | data struktureret med henblik på automatisk behandling                                           | e-mail, word-dokument, database | egen oversættelse |                | Archimate specifikation |
| applikationsservice    | it-service; webservice; service             |                     | veldefineret funktionalitet udstillet af applikationskomponent Opslag i CPR, modtagelse af email |                                 | egen oversættelse |                | Archimate specifikation |
| forretningsfunktion    |                                             |                     | gruppering af opgaver i relation til en organisations opbygning                                  |                                 | egen oversættelse |                | Archimate specifikation |
| forretningsobjekt      |                                             |                     | begreb som det anvendes i specifik domæne                                                        |                                 | egen oversættelse |                | Archimate specifikation |
| forretningsrolle       |                                             |                     | samling af funktioner en aktør har ansvar for i en specifik kontekst                             |                                 | egen oversættelse |                | Archimate specifikation |
| intergrationsmønster   | business collaboration; tværgående use case |                     | to eller flere forretningsrollers koordinerede handlinger i en specifik kontekst                 |                                 | egen oversættelse |                | Archimate specifikation |
| implementationsmønster | application collaboration                   |                     | to eller flere applikationskomponenter der samarbejder for at udføre en fælles opgave            |                                 | egen oversættelse |                | Archimate specifikation |

### 6.3 Bilag C: Eksempel: Anvendelse af referencearkitekturen i et projekt

Dette bilag har til formål at give et eksempel på, hvordan man kan anvende Referencearkitektur for deling af data og dokumenter i en konkret (men fiktiv) projektsammenhæng. Eksemplet er opfundet til lejligheden, og det skal understreges, at løsningsskitser og diagrammer i dette afsnit således ikke på nogen måde hævder at repræsentere den virkelige proces.

Eksemplet tager udgangspunkt i brugerrejsen ”jagttegns-aspirant under 18 år ønsker at tilmelde sig jagtprøve”. Projektet har et ønske om at bygge en selvbetjeningsløsning, der understøtter denne brugerrejse, og har indled- ningsvist identificeret og skitseret nogle af de nødvendige procestrin og datatyper, der skal understøtte løsningen (som vist på Figur 17 ).



![Figur17](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur17.jpg)

Figur 17 : Indledende skitse til en løsning, der involverer videregivelse af data. Det (fiktive) eksempel beskriver bru- gerrejsen ”jagttegns-aspirant under 18 år ønsker at tilmelde sig jagtprøve”.

Projektet ønsker nu at anvende Referencearkitektur for deling af data og dokumenter for at kvalificere sit løs- ningsdesign og løfte den indledende, rå skitse til et mere modent arkitekturdesign. I denne sammenhæng vælger projektet at gå frem på følgende måde:

#### Identificer de konkrete procestrin, hvor data videregives

Projektet finder frem til, at der skal videregives:

* Et samtykke i form af en forældreaccept, der indhentes separat og videregives fra borger.dk

* Data om aspiranten (fra CPR-registeret)

* Information om tilgængelige prøvetilbud samt detaljeret information om det enkelte tilbud

* Tilmeldingsblanket (slutresultat fra selvbetjeningsforløbet)

#### Analyser de implementeringsmønstre, der påtænkes anvendt ved den enkelte videregivelse

Projektet kommer frem til følgende valg:

* Samtykker fra forældre etableres som en ny datasamling på borger.dk. Selvbetjeningsforløbet, der afvikles på Miljø- og Fødevareministeriets servere, forespørger på videregivelsen af data via mønsteret **direkte adgang**.

* Data om aspiranten hentes fra Datafordeleren, der distribuerer CPR-registeret (som er en datasamling) på vegne af Indenrigsministeriet ifølge **datadistributør**\-mønsteret.

* Information om tilgængelige kurser og prøvetilbud viser sig at være spredt ud over en række udbydere, der benytter sig af forskellige datadistributører. Heldigvis viser det sig, at en eksisterende løsning hos Undervisningsministeriet, der indekserer prøvetilbud på tværs af kursus- og prøveudbydere, kan udvides med denne type prøver. Projektet vælger derfor implementeringsmønsteret **datadistributør (med brug af indeks).**

* Tilmeldingsblanketten, der er resultatet af brugerens valg af jagtprøve, skal videregives som en meddelelse til den valgte prøveudbyder. Fra prøvetilbud-dataservicen kender vi CVR-nummeret på den valgte prøveudbyder. For at undgå at skulle kommunikere direkte med den valgte udbyders system (som vi ikke kender, og hvor de mulige udbydere i øvrigt kan ændre sig over tid) vælger projektet implementeringsmønsteret **fælles system** og lader Digital Post stå for formidlingen af tilmeldingen (og sørger i den forbindelse for at designe en meddelelse, der i form af et struktureret dokument både kan læses af en menneskelig modtager og afkodes automatisk hos de udbydere, der har systemer, der understøtter dette).

#### Annoter med begreber fra Referencearkitekturen og Fællesoffentlig Digital Arkitektur

For at kunne tale et fælles sprog med de øvrige parter, der skal videregive data til projektet eller modtage data fra projektet, opdaterer projektet den indledende løsningsskitse (se Figur 18 ):

* Selvbetjeningsforløbet annoteres med begreber fra Referencearkitektur for selvbetjening, fx for- beredelse, kerne, afrunding – se blå tekst på Figur 18

* De identificerede videregivelser af data markeres med deres planlagte implementeringsmønster – røde note-bokse på Figur 18

* De øvrige, underliggende komponenter annoteres med de relevante begreber, fx dataservice, da- tasamling, distributionskopi m.m. – se øvrige bokse med rød tekst på Figur 18

#### Løber tjeklisten igennem

Referencearkitektur for deling af data og dokumenter rummer en tjekliste for anvendelse. Tjeklisten kommer rundt om såvel juridiske aspekter ved videregivelse af data (L – legal) , de forretningsmæssige overvejelser, som projektet bør gøre sig (O – organisational) , det semantiske design i form af dokumentation, datamodeller m.v. (S – semantic) samt sluttelig de tekniske overvejelser, der understøtter valg af implementeringsmønstre, guider til valg af standarder m.m. (T – technical).

Ved at anvende Referencearkitektur for deling af data og dokumenter (samt de øvrige værktøjer, der er tilgænge- lige som en del af Fællesoffentlig Digital Arkitektur) har projektet nu fået løftet sit løsningsdesign. De relevante data, der kan genbruges, er blevet identificeret, og der, hvor der skal bygges nye komponenter, sikrer det fælles sprog og begrebsapparat imod misforståelser og imod, at projektet overser væsentlige aspekter i designfasen, hvilket ville kunne føre til forsinkelser eller fordyrelser senere i projektets levetid.



![Figur18](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur18.jpg)

Figur 18 : En mere detaljeret løsningsskitse, der er kvalificeret med begreber og implementeringsmønstre hentet fra Referencearkitektur for deling af data og dokumenter.

### 6.4 Bilag D: Eksempler på løsninger pr. implementeringsmønster

Implementeringsmønstrene i denne referencearkitektur er beskrevet som selvstændige mønstre bygget på det begrebsapparat, vi har valgt at beskrive videregivelse af data ud fra – uden konkrete referencer til faktiske løsnin- ger. Det betyder imidlertid ikke, at der ikke i dag (primo 2018) findes konkrete, produktionssatte løsninger, der i overvejende grad følger de beskrevne mønstre. Nedenfor gives en kort oversigt over faktiske løsninger, der på væsentlige punkter passer ind i de beskrevne mønstre.

| Forretningsmønster              | Implementeringsmønster              | Eksempel på løsning                              |
| ------------------------------- | ----------------------------------- | ------------------------------------------------ |
| Videregivelse på forespørgsel   | Direkte adgang                      | Opslag i CPR-registeret hos Indenrigsministeriet |
| Datadistributør                 | Datafordeleren                      |                                                  |
| Fælles service- og dataplatform | Den Nationale Serviceplatform (NSP) |                                                  |
| Videregivelse ved meddelelse    | Direkte forsendelse                 | Sikker e-mail mellem myndigheder                 |
| Fælles system                   | Digital Post                        |                                                  |
| Servicefællesskab               | NemHandel via PEPPOL                |                                                  |

### 6.5 Bilag E: Om specifikationer, standarder og profiler

I forbindelse med udbud har man behov for at beskrive de krævede egenskaber for løsningen i en ’teknisk specifikation’. Betydningen fremgår af EU's direktiv 2014/24/EU, der regulerer offentlige udbud og definerer ‘tekniske specifikationer’ som: _Specifikation i et dokument, som fastlægger krævede egenskaber ved et produkt eller en tjenesteydelse_. I relation til indkøb af it-løsninger til brug ved deling af data og dokumenter inkluderer dette egenskaber ved udstillede applikationsservices.

Ofte er det muligt at beskrive den tekniske specifikation ved en henvisning til en ’standard’. Direktivet definerer en standard således: _teknisk specifikation, som er vedtaget af et anerkendt standardiseringsorgan \[...\]._ Sådanne standarder kan kategoriseres efter den udgivende organisations udbredelse; global, europæisk eller national (fx ISO, CEN og DS).

Inden for indkøb af it-løsninger har det vist sig, at mange vigtige, tekniske specifikationer har fundet udbredelse uden at være officielt udgivet af en anerkendt standardiseringsorganisation. Derfor indeholder direktivet også begrebet ‘fælles teknisk specifikation’ som henviser til it-specifikationer, der er blevet identificeret som egnet til anvendelse i offentlige indkøb af EU gennem formel behandling i European Multi Stakeholder Platform on ICT Standardisation.

Til en given anvendelse er det ofte hensigtsmæssigt at benytte ‘profiler’. En profil kan fx være en samling af delmængder af forskellige standarder og kan dermed præcisere, hvordan den endelige løsning forventes at gøre brug af de forhåndenværende standarder og tekniske specifikationer. Dette er udtrykt som: ” _\[...\] standards alone often leave too many degrees of freedom for efficient deployment. For that purpose, organisations \[...\] have introduced the concept of Profiles, which can be seen as the cement that holds building blocks together, forming functional modules. Profiles are guidelines for implementation of specific use cases, by selecting relevant standards and defining how they have to be configured._

[https://www.antilope-project.eu/wp-content/uploads/2013/05/D1.1-Refinement\_of\_Antilope\_Use\_Cases\_v1.2.pdf](https://www.antilope-project.eu/wp-content/uploads/2013/05/D1.1-Refinement_of_Antilope_Use_Cases_v1.2.pdf)

I den fællesoffentlige rammearkitektur dækker begrebet ’anvendelsesprofil’ over denne betydning. Referencearkitekturens formål kan dermed også beskrives som, at den skal være det dokument, der udpeger områder, hvor der mangler relevante anvendelsesprofiler.

### 6.6 Bilag F: Mapning til European Interoperability Reference Architecture v2

EU-kommissionen støtter gennem ISA2 - programmet udvikling af digitale løsninger, der sætter offentlige instanser, borgere og virksomheder i Europa i stand til at drage fordel af offentlige services, der er interoperable på tværs af landegrænser, sektorer m.m.

En del af ISA2 - programmet er European Interoperability Reference Architecture (EIRA), der har som mål at facilitere interoperabilitet gennem fælles arkitektur, herunder genbrug af arkitektoniske byggeblokke på tværs af løsninger i de europæiske lande.

EIRA definerer 4 niveauer for interoperabilitet under samlebetegnelsen LOST, der dækker over Legal, Organisational, Semantic og Technical interoperabilitet.

Som en del af udarbejdelsen af rammearkitekturen under Den fællesoffentlige digitaliseringsstrategi har Digitaliseringsstyrelsen afholdt workshops med EIRA-repræsentanter for dels at rette ind mod EIRA-rammeværket, hvor det er relevant, dels at give input til den videre udvikling af EIRA.

Referencearkitektur for deling af data og dokumenter indgår i den fællesoffentlige rammearkitektur. Nedenfor er de fire LOST-views angivet for denne referencearkitektur.



![Figur19](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur19.jpg)

Figur 19 : EIRA Legal View: De væsentligste elementer fra et lovmæssigt perspektiv



![Figur20](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur20.jpg)

Figur 20 : EIRA Organisational View: De væsentligste elementer på det forretningsmæssige/organisatoriske inter- operabilitetsniveau



![Figur21](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur21.jpg)

Figur 21 : EIRA Semantic View: De væsentligste elementer i det semantiske lag af interoperabilitet



![Figur22](https://github.com/Faellesoffentlig-Digital-Arkitektur/Referencearkitektur-for-deling-af-data-og-dokumenter/raw/main/assets/Figur22.jpg)

Figur 22 : EIRA Technical View: De væsentligste elementer til at understøtte deling af data og dokumenter fra det tekniske perspektiv

### 6.7 Bilag G: Oversigt over kilder og baggrundsmateriale

Nedenstående liste viser det baggrundsmateriale, der indgår i udarbejdelsen af denne referencearkitektur.

| Kilde                                                 | Materiale                                                                                                                                                                                                                                                                                                                                                               |
| ----------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Digitaliseringsstyrelsen                              | Vejledning i vurdering af offentlige it-projekters potentielle konsekvenser for privatlivet ; maj 2013. [https://digst.dk/sikkerhed/vejledninger-til-sikkerhedsarbejdet/konsekven...](https://digst.dk/sikkerhed/vejledninger-til-sikkerhedsarbejdet/konsekvensvurdering-for-privatlivet/)                                                                              |
| Digitaliseringsstyrelsen og Center for Cybersikkerhed | Anbefalinger til styrkelse af sikkerheden i statens outsourcede it-drift ; august [https://www.ft.dk/samling/20131/almdel/REU/bilag/353/1394280.pdf](https://www.ft.dk/samling/20131/almdel/REU/bilag/353/1394280.pdf)                                                                                                                                                  |
| EU-Kommissionen                                       | GDPR – EU’s databeskyttelsesforordning (også kendt som Persondataforordningen); maj 2018. [http://eur-lex.europa.eu/legal-content/DA/TXT/PDF/?uri=CELEX:32016R0679&from=DA](http://eur-lex.europa.eu/legal-content/DA/TXT/PDF/?uri=CELEX:32016R0679&from=DA)                                                                                                            |
| EU-Kommissionen                                       | ISA2 - programmet – Interoperability solutions for public administrations, businesses and citizens. 2017. [https://ec.europa.eu/isa2/isa2\_en](https://ec.europa.eu/isa2/isa2_en)                                                                                                                                                                                       |
| EU-Kommissionen                                       | EIF – European Interoperability Framework. [https://ec.europa.eu/isa2/eif\_en](https://ec.europa.eu/isa2/eif_en)                                                                                                                                                                                                                                                        |
| EU-Kommissionen                                       | EIRA – European Interoperability Reference Architecture. V2.0.0, juli 2017. [https://ec.europa.eu/isa2/solutions/eira\_en](https://ec.europa.eu/isa2/solutions/eira_en)                                                                                                                                                                                                 |
| EU-Kommissionen                                       | Europa-Parlamentets og Rådets direktiv (EU) 2016/2102 af 26. oktober 2016 om tilgængeligheden af offentlige organers websteder og mobilapplikationer (EØS-relevant tekst); oktober 2016. [http://eur-lex.europa.eu/legal-content/DA/TXT/?qid=1481622494924&uri=CELEX:32016L2102](http://eur-lex.europa.eu/legal-content/DA/TXT/?qid=1481622494924&uri=CELEX:32016L2102) |
| EU-Kommissionen                                       | EU-wide digital Once-Only Principle for citizens and businesses: Policy options and their impacts; april 2009. [https://op.europa.eu/en/publication-detail/-/publication/4c429e34-e3a6-11e7-9749-01aa75ed71a1](https://op.europa.eu/en/publication-detail/-/publication/4c429e34-e3a6-11e7-9749-01aa75ed71a1)                                                           |
| Regeringen                                            | National strategi for cyber- og informationssikkerhed ; december 2014. [https://digst.dk/strategier/cyber-og-informationssikkerhed/national-strategi-for-cyber-og-informationssikkerhed-2015-2016/](https://digst.dk/strategier/cyber-og-informationssikkerhed/national-strategi-for-cyber-og-informationssikkerhed-2015-2016/)                                         |
| Regeringen                                            | Sammenhængsreformen: Borgeren først - en mere sammenhængende offentlig sektor; april 2017. [https://www.regeringen.dk/media/3260/sammenhaengsreform\_borgeren-foerst-en-mere-sammenhaengende-offentlig-sektor.pdf](https://www.regeringen.dk/media/3260/sammenhaengsreform_borgeren-foerst-en-mere-sammenhaengende-offentlig-sektor.pdf)                                |
| Regeringen, KL og Danske Regioner                     | Et stærkere mere trygt digitalt samfund: Den fællesoffentlige digitaliseringsstrategi 2016 - 2020 ; maj 2016. [https://digst.dk/strategier/digitaliseringsstrategien/](https://digst.dk/strategier/digitaliseringsstrategien/)                                                                                                                                          |
| Regeringen, KL og Danske Regioner                     | Den fællesoffentlige digitale arkitektur , [https://arkitektur.digst.dk/](https://arkitektur.digst.dk/)                                                                                                                                                                                                                                                                 |
| Regeringen, KL og Danske Regioner                     | Den fællesoffentlige rammearkitektur ; [https://arkitektur.digst.dk/rammearkitektur](https://arkitektur.digst.dk/rammearkitektur)                                                                                                                                                                                                                                       |
| Regeringen, KL og Danske Regioner                     | Den digitalt sammenhængende offentlige sektor: Hvidbog om fællesoffentlig digital arkitektur ; juni 2017. [https://arkitektur.digst.dk/node/241](https://arkitektur.digst.dk/node/241)                                                                                                                                                                                  |
| Regeringen, KL og Danske Regioner                     | Referencearkitektur for: Overblik over egne sager, Tværgående processer; Under udarbejdelse. [https://arkitektur.digst.dk/rammearkitektur/referencearkitekturer](https://arkitektur.digst.dk/rammearkitektur/referencearkitekturer)                                                                                                                                     |
| Regeringen, KL og Danske Regioner                     | Referencearkitektur for Selvbetjening ; april 2017. [https://arkitektur.digst.dk/referencearkitektur-selvbetjening](https://arkitektur.digst.dk/referencearkitektur-selvbetjening)                                                                                                                                                                                      |
| Regeringen, KL og Danske Regioner                     | Referencearkitektur for Brugerstyring ; april 2017. [https://arkitektur.digst.dk/rammearkitektur/referencearkitekturer/refere...](https://arkitektur.digst.dk/rammearkitektur/referencearkitekturer/referencearkitektur-brugerstyring)                                                                                                                                  |
| OIO                                                   | Referencearkitektur for sags- og dokumentområdet (ESDH). OIO, 2008. [https://digitaliser.dk/resource/230688](https://digitaliser.dk/resource/230688)                                                                                                                                                                                                                    |
| Sundhedsdatastyrelsen                                 | Referencearkitektur for deling af dokumenter og billeder. National sundheds-it, [https://sundhedsdatastyrelsen.dk/da/rammer-og-retningslinjer/om-referenc...](https://sundhedsdatastyrelsen.dk/da/rammer-og-retningslinjer/om-referencearkitektur-og-standarder)                                                                                                        |
| Sundhedsdatastyrelsen                                 | Referencearkitektur for informationssikkerhed. National sundheds-it, 2013. [https://sundhedsdatastyrelsen.dk/da/rammer-og-retningslinjer/om-referenc...](https://sundhedsdatastyrelsen.dk/da/rammer-og-retningslinjer/om-referencearkitektur-og-standarder)                                                                                                             |
| Sundhedsdatastyrelsen                                 | Strategi for digital sundhed 2018-2022. Sundhedsdatastyrelsen, 2018. [https://sundhedsdatastyrelsen.dk/da/rammer-og-retningslinjer/strategi-fo...](https://sundhedsdatastyrelsen.dk/da/rammer-og-retningslinjer/strategi-for-digital-sundhed)                                                                                                                           |
| Justitsministeriet                                    | Bekendtgørelse om sikkerhedsforanstaltninger til beskyttelse af personoplys- ninger, som behandles for den offentlige forvaltning ; marts 2001. [https://www.retsinformation.dk/Forms/R0710.aspx?id=842](https://www.retsinformation.dk/Forms/R0710.aspx?id=842)                                                                                                        |
| Justitsministeriet                                    | Forvaltningsloven ; april 2014. [https://www.retsinformation.dk/forms/r0710.aspx?id=161411](https://www.retsinformation.dk/forms/r0710.aspx?id=161411)                                                                                                                                                                                                                  |
| Justitsministeriet                                    | Arkivloven ; juni 2016. [https://www.retsinformation.dk/Forms/R0710.aspx?id=183862](https://www.retsinformation.dk/Forms/R0710.aspx?id=183862)                                                                                                                                                                                                                          |
| Regeringen                                            | Lov om behandling af personoplysninger ; maj 2000. [https://www.retsinformation.dk/forms/r0710.aspx?id=828](https://www.retsinformation.dk/forms/r0710.aspx?id=828)                                                                                                                                                                                                     |
| Styrelsen for Arbejdsmarked og Rekruttering           | Bekendtgørelse om obligatorisk digital selvbetjening vedrørende ansøgninger og meddelelser mv. om sociale ydelser mv.; november 2015. [https://www.retsinformation.dk/Forms/R0710.aspx?id=175675](https://www.retsinformation.dk/Forms/R0710.aspx?id=175675)                                                                                                            |
| The Open Group                                        | TOGAF – The Open Group Architecture Framework. [http://www.opengroup.org/subjectareas/enterprise/togaf](http://www.opengroup.org/subjectareas/enterprise/togaf)                                                                                                                                                                                                         |
| The Open Group                                        | ArchiMate V3.0, juni 2016. [https://publications.opengroup.org/archimate-library](https://publications.opengroup.org/archimate-library)                                                                                                                                                                                                                                 |
| W3C                                                   | Linked Data Platform v1.0, inkl. profilering af Resource Description Framework (RDF). [http://www.w3.org/standards/semanticweb/data](http://www.w3.org/standards/semanticweb/data)                                                                                                                                                                                      |


