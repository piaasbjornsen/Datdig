markdown


# 1 Introduskjon
## 1.1 Strukturert datamaskin organsisasjon

Det er en stor forskjell mellom hva som er beleilig for mennesker, og hva som er beleielig for maskiner. 
### 1.1.1 Språk, nivå og virituelle maskiner

Vi har to metoder for å fikse problemet nevt over. Begge måtene innebærer å designe et nytt sett med instruksjoner som er mer beleilig for mennesker, enn å bruke de innebygde maskin-funksjonene. 
Funksjonene satt sammen danner et språk vi kaller for **L1**. De innebygde maskin-funksjonene lager et språk vi kaller **L0**.
> **Translation**
> Den første metoden kaldt *translation* er å bytte ut alle instruksjonene i L1 med tilsvarende operasjoner i L0. Maskinen utfører da operasjoner bestående av bare L0 språket. 

> **Interpretation**
> Den andre metoden er å skrive et program i L0 som tar program skrevet i L1 som input data, for så å undersøke hver operasjon og finne ekvivalenten i L0. 

Disse to metodene er svært like. I begge metodene tar maskinen instruksjoner i L1 og utfører den ekvivalente sekvensen i L0. 
Forskjellen er at i *translation* er hele L1 programmet oversatt til L0, så kastes L1 programmet, og det nye L0 programmet lastest opp til maskinens minne og utføres. 
Under utførelsen er det det ny genererte L0 programmet som kjører og kontrollerer maskinen. 
I *interpretation* er hver operasjon undersøkt og dekodet, for så å bli utført med en gang. Det er ikke generert et oversatt program.
Her er tolken i kontroll over maskinen, og for den er L1 bare data. 

I stedet for å tenkte på *translation* og *interpretation* er det ofte lettere å tenke at det finnes en hypotetisk *virituel maskin* som bruker maskin-språket L1. 
La oss kalle denne maskinen for M1. Hvis det finnes en slik maskin hadde det ikke vært noe behov for å ha et L0 språk, eller en maskin som utffører program i L0. Man kunne enkelt å greit bare skrevet program i L1 og ha en maskin som utfører dem direkte.

---------S.3---------------Levels----

På en måte kan en maskin med *n* nivåer sees på en *n* virituelle maskiner, med hvert sitt språk. 

Bare språk skrevet i L0 kan bli dirkete utført av elektriske kretser. 

![A multilevel machine](../../../../../var/folders/xg/9qgl3jxn7tsc9hnr64c8msn40000gn/T/TemporaryItems/NSIRD_screencaptureui_RHTx41/Screenshot 2021-11-21 at 21.00.54.png)

### 1.1.2 Moderne multilevel maskiner

De fleste moderne maskiner består av to eller flere nivåer. Det finnes maskiner med opp til 6 leveler.
Det finnes også et level under level 0 (maskinvare) finnes, og kalles **device level**.
![A six level computer](../../../../../var/folders/xg/9qgl3jxn7tsc9hnr64c8msn40000gn/T/TemporaryItems/NSIRD_screencaptureui_PefgFn/Screenshot 2021-11-21 at 21.06.50.png)

Det laveste nivået vi ser på er **digital logic level**, og det interessante her er **gates**. 
Hver gate har en eller flere digitale inputs (signaler som representerer 0 og 1) og beregner en output en enklere funkssjon av disse inputene, som AND eller OR. 
Et lite antall av gates kan kombineres og danne et 1-bit minne, som kan holde en 0 eller en 1. 
1-bit minner kan kombineres og danne registre. Hvert **register** jan holde binære tall, opp til et visst makimum. 

Det neste nivået er *microarchitecture*. På dette nivået kan vi ha samlinger av registre som former et lokalt minne og en krets kalt **ALU** (arithmetic logic unit), som kan utføre enkle aritmetriske operasjoner. 

## 1.5 Metric units 
I denne boken brukes det metriske enheter.
I tillegg menes ikke kile som *10<sup>3</sup> = 1000*, men som ***2<sup>10</sup> = 1024***

![Måleenheter](../../../../../var/folders/xg/9qgl3jxn7tsc9hnr64c8msn40000gn/T/TemporaryItems/NSIRD_screencaptureui_kHUFPq/Screenshot 2021-11-22 at 00.04.14.png)

# Computer systems organization
En digital datamaskin består av et sammenkoblet system av 
* prosessorer
* minne
* input/output enheter. 

Dette kapitlet er en introduksjon til disse tre komponentene. 
## 2.1 Prosessorer 
**CPU (Centra Processing Unit** 
CUP er "hjernen" av en maskin. Dens funksjonalitet er å utføre program som er lagret i hovedminne, ved å hente ut deres intruskjoner, undersøke dem, og så utføre dem, en etter en . 

**CPU i en BUS**
![CPU BUS](../../../../../var/folders/xg/9qgl3jxn7tsc9hnr64c8msn40000gn/T/TemporaryItems/NSIRD_screencaptureui_fXHSbx/Screenshot 2021-11-22 at 00.15.18.png)
Komponentene er koblet av en *bus*, som er en samling av parallelle ledninger som sender adresser, data og kontroll signal. Busser kan være ekerne fra en CPU, og koble den til minne og I/O enhetene, men kan også inni CPU'en. 
CPU'en er satt sammen av flere distinkte deler. 
Kontroller enhetene er ansvarlige for å hente instrukser fra hovedminne og avgjøre deres type.Den aritmetiske logiske enheten utfører operasjoner som addisjon og Boolean AND, som trengs for å utføre instruksjonene. 
CPU'en inneholder også et lite, høy-hastighet minne som brukes til å lagre midlertidige resultater og en viss kontroll informasjon. Dette minne er laget av registre, som hver har en spesiell funksjon og størrelse. Vanligvis har alle registrene samme størrelse. Hvert register kan holde ett nummer, opp til et visst maksimum som er bestemt av registerets størrelse. Regristere kan leses og skrives raskt fordi de er interne i CPU'en. 
Det viktigste registre er PC, programmtelleren (Program Counter), som viser til den neste instruksjonen som skal hentes og utføres. 
Et annet viktig register er IP, intruksjonsregister (Intruction Register), som holder instruksjonene som blir utført.

### 2.1.1 CPU organisasjon
Den interne organisasjonen av en del av en typisk **von Neumann CPU** er vist på bildet under. Denne delen er kalt **data path** og består av registre (typisk 1 til 32), **ALU (Arithmetic Logic Unit)** og flere andre busser som kobler sammen bitene.
Registrene mater inn til to ALU input registre mens ALU utfører noen utregninger. Data path'en er veldig viktig i alle maskiner. 

![von Neumann CPU](../../../../../var/folders/xg/9qgl3jxn7tsc9hnr64c8msn40000gn/T/TemporaryItems/NSIRD_screencaptureui_fR1pH9/Screenshot 2021-11-22 at 00.30.27.png)

ALU'en i seg selv utfører addisjon, subtraksjon og andre enkle operasjoner på dens input, og dermed gir ut et resultat i output registre. 
Senere kan registre bli strkevet (dvs. lagret) i et minne, hvis det ønsket. 

De fleste instuksjoner kan bli delt inn i én av to kategorier: registre-minne eller registre. 
Register-minner instuksjoner lar minne ord bli hentet inn til registre, der de kan blu brukt som ALU-inputs. 
Andre register.minne instruksjoner lar registre bli lagret tilbake i minnet. 
Den andre typen av instuksjoner er registre-register. En typisk registre-register instuksjon henter to operatorer fra registre, tar dem med til ALU inpute registre, utfører noen operasjoner på dem, og lagrer resultatet i et av registrenen. 
Prosessen av å kjøre to operasjoner gjennom ALU og lagre resultatet kalles **data path cycle** og er hjertet av de fleste CPU'er. 

### 2.2.2 Instukdjons utførelse 
> En CPU utfører hver instuksjon i en serie av små steg. 
> 1. Hente den neste instuksen fra minnet og inn til registret.
> 2. Endre programtelleren (PC) til å peke på den følgende instruksjonen
> 3. Avgjøre typen til instuksjonen som akkurat er hentet
> 4. Hvis instuksjonen bruker et ord i minnet, avgjøre hvor det er.
> 5. Hente ordet, om det trengs, inn till CPU registre
> 6. Utføre instuksjonen
> 7. Gå tilbake til punkt 1 og begynne å utføre den neste instuksjonen.


Denne rekken av steg er ofte kalt **fetch-decode-execute** syklus. 

### 2.1.3 RISC vs. CISC
RISC (Reduced Instuction Set Computer) hadde typsik rundt 50 operasjoner den kunne utføre.
CISC (Complex Instruction Set Computer) 

### 2.1.4 Design prinsipper for moderne datamaskiner
> RISC design prinspper
> 
>Alle instuksjoner er direkte utført av Hardware
>* Alle vanlige instruksjoner er direkte utført av hardware. De er ikke tolket av microinstrictions. Ved å eliminere et nivå av tolkning oppnår man høy-hastighet for de fleste instuksjoner. For maskiner som implementerer CISC instuksjons set, må mer komplekse instuskjoner brytes ned til seperate deler, som så kan li utført som en rekke mikroinstuksjoner. Dette ekstra steget gjør maskinen tregere, men for mindre hyppige instruksjoner kan det være akseptabelt.
> 
> Maksimere hastigheten for utstedelse av instuksjoner
>* Moderne maskiner prøver å maksimere hvor mange instuksjoner som kan startes per sekund. Selvom instuksjoner alltid møtes i programmets rekkefølge, er de ikke alltid utstedet i programmets rekkefølge. 
> 
> Intruksjoner burde være lette å dekode 
>* En kritisk grense for raten til utstedelse av instuksjoner er dekodingen av individuelle instuksjoner for å avgjøre hvilke resurser som kreves. Alt som kan hjelpe denne prosessen er nyttig. Det innebærer å lage instuksjoner vanlig, med en gitt lengde og en lite antall felter. Jo mindre formatet for instuksjonene er, desto bedre. 
> 
> Ha mange registre
> * Man må passe på å ha nok registre. Å gå tom for registre, så man må sende et ord tilbake til minnet etter å hentet det ut, for å så hente det ut igjen når man har et ledig register er ikke ønskelig, og burde ungåes. Det letteste er da å ha nok registre (minst 32).
> 

### 2.1.5 Instuction-level parallelism 
De fleste datamaskin arkitekter ser til parallellisme (å gjøre to eller flere ting samtidig) som en måte for å bedre opptreden for en gitt klokkehastighet. 
Parallelisme opptrer på to generelle former, instruksjons-nivå og prosessor nivå. 

*Instuksjons nivå* blir brukt innen individuelle instuksjoner for å få flere instuskjoner per sekund ut av maskinen. 
*Prosses nivå* blir brukt jobber flere CPU'er sammen om det samme problemet. 

**Pipelining** 
Å hente ut instuksjoner fra minne er en stor flaskehal for hastigheten. For å fikse dette problemet har man lenge brukt en metode for å hente ut instuksjoner fra minnet på forhånd, så de er der når de trengs. Disse intsuksjonene blir lagret i noe kalt **prefetch buffer**. På denne måten deles instuksjonsutførelse inn i to deler, henting og faktisk utførelse. Konseptet av **pipeline** bruker denne strategien videre. I stedet for å dele instruksjonsutførelse inn i to deler, deles det inn i mange flere deler (ofte et dusin eller flere). Hver del er dedikert til hver sin del av hardware, som kan kjøres parallelt. 
Bilde under viser en fem-dels pipeline, hver del kalles ofte **stage**.

![Five part pipeline](../../../../../var/folders/xg/9qgl3jxn7tsc9hnr64c8msn40000gn/T/TemporaryItems/NSIRD_screencaptureui_FZzzCg/Screenshot 2021-11-22 at 14.25.55.png)

**Stage 1:** Hener instuskjoner fra minnet og legger de i en buffer del til den trengs.

**Stage 2:** Dekoder instuksjoner, bestemmer hvilke type operander som trengs.

**Stage 3:** Lokaliserer og henter operasjonene, enten fra register eller minnet.

**Stage 4:** Utfører instuksjonene, typsik ved å kjøre operandene gjennom en data path.

**Stage 5:** Skriver resultatet tilbake til det riktige registret.

Pipelinging tillater en trade-off mellom ventetiden (hvor lang tid det tar å utføre en instuksjon) og hvor mange MIPS CPU'en har. 
Med en sykel-tid T nsec, og n stages i pipelinen, er ventetiden n*T nsec fordi hver instruksjon går gjennom n steg, som hver tar T nsec.

Fordi én instuksjon gjøres per klokkesykel og det er 10<sup>9</sup>/T klokkesykler per sekund, antall instuskjoner utført per sekund er 10<sup>9</sup>/T. 
F.eks. hvis T = 2 nsec, 500 millioner instukser blir utført hvert sekund. For å få antall MIPS, må vi dele instuksjonsraten på 1 million (10<sup>9</sup>/T)/10<sup>6</sup> = 1000/T MIPS. 

**Superskaler arkitekturer**
### 2.1.6 Prosessor nivå parallelisme 

Den eneste måten å gjøre datamaskiner raskere med en factor av 50, 100 eller mer, er å designe maskiner med flere CPU'er. Nå skal vi se litt på hvordan disse er organisert. 

**Array datamaskiner**
En array prosessor består av mange like prosessorer som utfører de samme rekkene med intruksjoner på forkjellige sett med data. 
En vektor prosessor ser veldig lik ut som en arrat prosessor. I likhet med en arrat prosessor, utfører den rekker av operasjoner på par av dataelementer raskt. Men ulikt en array prosessor, blir alle addisjons operasjonene utført på én tungt pipelinet prosessor. 

Bårde array og vektor prosessorer funker på arrays av data. Bege utfører én instruksjon. Men der en array prosessor gjør det ved å ha like mange adderere som elementer i vektoren, har vektor prosessoren en konsept om **vektor registre**, som består av et set registre som kan lades fea minnet i én instruksjon, som laster dem fra minnet i serie. Så utfører en vektor addisjon intruks parvis addisjon av elementene av to slike vektorer ved å mate dem til en pipelined adderer fra de to vektor reistrene. 

**Multiprocessors**

**Multicomputers**

### 2.2.1 Bits
* BCD (Binary Coded Decimal)

### 2.2.2 Minne adresser
## 2.3 Sekundær minne
### 2.3.1 Minne hierarki 
### 2.3.2
## 2.4 INPUT/OUTPUT
### 2.4.1 Busser


# 3 Digitalt logisk nivå (Digital logic level)
I dette kapitler blir det gått gjennom aspektre ved digital logikk, som en byggesten for de neste kapitlene. 
## 3.1 Gates og boolean algebra 
En digital krets er en hvor bare to logiske verdier finnes. Typisk er det et signal mellom 0 og 1 volt som representerer én verdi (f.eks. binær 0) og et signal mellom 2 og 5 velt som representerer den andre verdien (f.eks. binær 1). Volt utenfor disse to verdiene er ikke lovlige. 
Små elektroniske enheter, **gates**, kan utføre forskjellige funksjoner på disse to signalverdiene. Disse komponentene danner basisen for hardware som alle maskiner er bygget på. 

> De tre enkleste gates 
> ***NOT***
* Blir ofte kaldt inverterere
* 
> ***NAND***
> ***NOR***
> 
### 3.1.1 Gates
### 3.1.2 Boolsk algebra 
* Switching algebra 

### 3.2.4 Klokker
I mange kretser er rekkefølgen tinge skjer på kritisk. Noen ganger må en hendelse komme før en anne, noen ganger må to hendelser skje samtidig. For å få til dette bruker mange kretser klokker. 
En **klokke** i denne konteksten er en krets som sender ut en pulsserie med presis bredde og pulser. 
Tidsintervallet mellom to tilsvarende kanter av to påfølgende pulser kalles **klokkesykel tiden** (clock cycle time). 

I en datamaskin kan mange ting skje på en klokkesykel. Hvis disse må skje i en spesiell rekkefølge, må klokkesyklen deles inne i subsykler. En måte å gjøre dette på der å tappe inn på hovedsyklen og sette inn en krets med en gitt og kjent forsinkelse. Dette lager en sekundær klokkesykel som er faseskiftet fra hovedsyklen. 
![Delayd clock cycle](../Bilder/Delayd clock cycle.png)

I noen kretser er man mer interesert i tidsintervaller enn diskre øyeblikk av tiden. 
F.eks. kan noen hendelser skje så lenge C1 er høy, heller enn akkurat på en stigende flanke. En annen hendelse kan skje når C2 er høy. 

Det er verdt å merke seg at klokker er symetriske. Dvs. tiden den er høy er lik tiden den er lav. For å generere en asymetrisk puls kan kolkken skiftes ved å bruke en delay  og en AND med den originale klokken (Fig. 3-21 (c)).

## 3.3 Minne

En essensiell komponent av alle datamaskiner er minnet. 

> **Bruk:**
> * Lagre intruksjoner
> * Lagre data

### 3.3.1 Vipper (Latches)
For å lage et 1-bit minne, trenger vi en krets som "husker" tidligere input verdier. En slik krets kan lages av to NOR gates (Fig. 3-22 (a)).

![img_2.png](../Bilder/Vippe.png)

Figur (a) er kaldt en SR vippe. Den er to inputs, S (for å sette vippen) og R (for å resette). Den har også to outputs, Q og komplementet av Q. 
For R = S = 0 har vippen to stabile tilstander, 0 eller 1, avhengid av Q. 
Setter vi S = 1, vil vippen få tilstanden Q = 1.
Setter vi R = 1, vil vippen få tilstanden Q = 0. 
Kretsen "husker" om S eller R var den siste til å være 1. 

**Clocked SR latched**
Hvis man bare ønsker at vippen skal være aktiv på visse tidspunkter kan man koble den til en klokke som vist under. Nå har kretsen tre inputs, S, R og klokken.
![img_2.png](../Bilder/ClockedLatch.png)

Klokken er vanligvis 0, og da vil AND gatene gjøre S og R er ubetydelig (og uansett gi ut 0). 
Når klokken er 1, vil S og R gatene være avgjørende. Vippen blir altså sensitiv til S og R inputsene. 
Man burkes ofte **enable** eller **strobe** for å vise til klokke-inputen (altså om vippen er sensitiv til S og R, eller ikke).

**Clocked D latches**
Denne vippen har bare én input, D. Fordi begge AND gatene bruker D som input (D og komplementet til D) vil de to AND gatene aldri begge være 1. 
Når klokken er 1 og D = 1, vil vippen få tilstand Q = 1. 
Når klokken er 1 og D = 0, vil vippen få tilstand Q = 0. 
Med andre ord. Når klokken er 1, vil den nåværende verdien til D bli lagret i vippen. 
For å laste den nåværende verdien av D til minnet, må klokkepulsen være 1. 

![img_2.png](../Bilder/DLatch.png)

### 3.3.2 Flip-Flops
I mange kretser er det nødvendig å sample verdien på en spesiell linje til en spesiel tid og lagre den. 
I denne varianten er ikke verdien lagret når klokken er 1, men når flanken er stigende eller synkende. Dermed er lengden på pulsen uviktig, så lenge overgangen er rask. 

### 3.3.3 Registre
### 3.3.4 Minne organisering
![img_2.png](../Bilder/Minne.png)
![img_2.png](../Bilder/MinneForklart.jpg)

> **Signalene**
> * CS (Chip Select):
>  * Forteller minnet hvilken chip vi ønsker å bruke
> * WE (Write Enable)
>  * Indikerer at data skal bli skrevet
> * RD (Read)
>  * Indikerer at data skal leses
> * OE (Output Enable)
>  * Signaliserer at outputs skal sendes


### 3.3.5 Minne chips
Det som er fint med minnet avbildet over, er at det er lett å lage større minner. 
I bildet er det et 4x3 minne (fire ord på 3 bits). For å utvide til et 4x8 minne (fire ord på 8 bits), må vi bare legge til 5 kolonner til (med 4 flip-flops hver), fem flere I<sub>i</sub> inputs, og en adresse linje A<sub>3</sub> til. 

### 3.3.6 RAMs og ROMs
***RAM***
Så langt har vi sett på minner som kan skrives og leses til, dette er RAM (Random Access Memory). 
RAM kommer i to typer; Statiske og dynamiske.

>**Statisk RAM**
>* Er kontruert ved å bruke krretser lignende D flip-flops. 
>* Verdiene er beholdt så lenge strømmen er på 
>* Raske; Typsik access tid er et par nsek. 
>* Vanlige som level 2 cache minne 

>**Dynamisk RAM**
>* Bruker ikke flip-flops
>* Array av celler 
>  * Som hver inneholder én transistor og én kondensator per bit (vs 6 transistorer i statisk)
>  * Kondensatoren kan bli ladd eller uladd (0 og 1)
>* Hver bit må bli refreshed (reloaded) for å motvirke at data lekker
>  * Ekstern logikk må refreshe, dermed krever dynamisk mer kompleks interfacing enn statisk
>* Stor kapasitanse 
>* Høy tetthet av bits per chip
>* Tregere

***ROM***
Minner som bare kan lese. Brukes gjerne i leker, biler osv (ting hvor den interne dataen aldri trengs å forandres). 
Når det er instalert, trengr vi aldri å endre program eller data. 
ROM står for Read Only Memory. Den eneste måten å endre program i en ROM på, er å bytte ut hele chipen. 
ROM er mye billige enn RAM. 

### 3.4.1 CPU chips
Alle moderen CPUer er inkapslet i en eneste chip. Hver CPU har et set av pins, hvor all kommunikasjon med det eksterne må gjennom. Noen gir ut informasjon, noen tar inn. Ved å forstå funksjonene til alle pinsene, kan vi lære hvordan CPUen interagerer med minnet og I/O enhetene via en samling av parallelle koblinger (en buss). 

For å hente instruksjoner, legger CPUen minneadressen til intruksjonene på adresse pinnene. Deretter forteller den til en eller flere av kontrolllinjene at minne vil lese. Minne responderer ved å legge det ønskede ordet på CPUens datapins og fortelle at det er gjort. Når CPU'en ser dette signalet, aksepterer den ordet og utfører instuksjonen. 
For nå er det viktige å vite at CPUen kommuniserer med minnet og I/O enheten ved å gi signaler til pinsene og akseptere singaler på pinsene. Ingen annen kommunikasjon er mulig 

To av de viktigste variablene som bestemmer CPUens prestasjon er hvor mange adresse- og datapins den har. En chip med *m* adressepins kan adressere opp til 2<sup>*m*</sup> minne lokasjoner. Lignende kan en chip med *n* datapins lese og skrive et n-bit ord i én operasjon. 
Altså en CPU med 8 datapins bruker 4 operasjoner på å lese et 32-bit ord, hvor en med 32 datapins kan gjøre det samme i én operasjon. 

I tillegg til dette har CPUer også kontrollpins. Disse regulerer flyten og timingen til data fra og til CPUen. Kontrollpinsene kan grupperes inn i 6 hovedkategorier.

>***Kontrollpins***
>1. Buss kontroller
>   * Hovedsakelig outputs fra CPUen til bussen (dermed inputs til minnet og I/O chips) som forteller om CPU vil lese eller skrive til minnet, eller gjøre noe annet.
>2. Interrupts
>   * Inputs fra I/O enheten til CPUen som forteller CPUen at den er ferdig å gjøre sin operasjon.
>3. Buss arbitration
>   * Regulerer trafikk på bussen, for å forhindre at to enheter prøver å bruke den samtidig.
>4. Coprocessor signaling
>5. Status
>6. Miscellaneous


### 3.4.2 Databuss
En buss er en vanlig elektronisk pathway mellom flere enheter. De kan kategoriseres etter deres funksjon. De kan brukes internt i en CPU for å flytte data til og fra ALU'en, eller eksternt fra CPUen, for å forbinde minne til I/O enhetene.
![img_2.png](../Bilder/Bus.png)











# Se på 
* Egenskaper vedd RISC-prosessor
* Egenskaper ved CISC-prosessor 
* 