**1) GIS**
GIS è un tool per visualizzare e analizzare dati di **TIPO GEOGRAFICO** per capire relazioni, trend e pattern.
- I **dati geografici sono legati a un sistema di riferimento geografico** (es. coordinate).
![[Pasted image 20241022143428.png]]
GIS **permette l'esplorazione di domande spaziali più ricercate** che, usando le mappe, non potremmo fare

2) **DATI SPAZIALI E DATI ATTRIBUTO**
I primi sono **fatti da posizione su un oggetto spaziale sulla superficie terrestre** (es una foresta), e sono memorizzati usando coordinate geografiche.
I secondi sono **descrizioni d'informazioni su un oggetto spaziale** (es alcuni attributi della foresta), e sono memorizzate in una tabella.

3) **SISTEMA DI RIFERIMENTO GEOGRAFICO DI COORDINATE**
Permette di identificare univocamente qualsiasi posizione sulla Terra specificata.
Un sistema semplice è rappresentato da un piano cartesiano 2D o 3D. 
La Terra non è una sfera, ma più un GEOIDE, essendo una superficie irregolare e complessa: questo perché la sua massa non è uniforme in tutti i punti e la direzione della gravità cambia.
Proprio per questo, abbiamo bisogno di rappresentare la Terra usando un modello regolare: scegliamo l'ellissoide, che è un ovale con un asse maggiore (il più lungo) e uno minore (il più breve).

**DATUM**: è approssimazione da geoide a ellissoide, e si dividono in 2 gruppi:
- datum *globale* : l’ellissoide è orientato verso il centro di gravità WGS84
- datum *locale*: l’ellissoide è tangente alla superficie reale della terra in un punto particolare  che si trova al centro dell’area geografica da rappresentare.


4) **LATITUDINE e LONGITUDINE di un punto** 
La prima è *l'angolo tra l'equatore e la retta che passa attraverso il punto e attraverso il centro della Terra*.
La seconda è *l'angolo a est o ad ovest da un meridiano di riferimento (GREENWICH) a un altro meridiano che passa attraverso quel punto*.
Entrambe sono misurate *in gradi*.
L'ELEVAZIONE è l'*altezza sopra o sotto un punto fissato*.

![[Pasted image 20241022150649.png]]

5) **COME CONVERTIAMO UN ELLISSOIDE A UNA MAPPA PIATTA?**
Facciamo una "proiezione", che ci permette di rappresentare un oggetto sulla terra che ha una "curva" ad una mappa che è piatta con errori minimi.

![[Pasted image 20241022151443.png]]
**PROIEZIONE CONFORMALE:** usata quando bisogna preservare le relazioni angolari, e incorrette nella rappresentazione di aree.
**PROIEZIONE EQUIDISTANTI:** usate quando l'obiettivo è misurare la distanza, con scala della mappa mantenuta costante: la mappa qui rappresenta correttamente le distanze dal centro della proiezione a ogni altro posto nella mappa.
**PROIEZIONI AD AREE UGUALI**: usate quando l'obiettivo è misurare le aree, dove ciascuna ha lo stesso rapporto proporzionale alle aree della Terra che rappresentano.

Le proiezioni sono fatte proiettando su un PIANO (secante o tangente) relativo a un punto,e usando una superficie sviluppabile (cono o cilindro).
**METODI DI PROIEZIONE** (che inglobano le precedenti):
- *NORMALE*: se il piano è tangente al polo, o il cilindro (o cono) ha l'asse parallelo a quello della terra.
- *TRASVERSALE*: se il piano è tangente all'equatore, o il cilindro (o cono) hanno l'asse perpendicolare a quello della terra.
- *OBLIQUO:* se il piano (o cilindro/cono) sono tangenti a ogni punto della superficie della terra.

**PROIEZIONE AZIMUTHAL**
Sono conformali perché mantengono i rapporti angolari, e rappresentano bene le aree vicino i poli.

**PROIEZIONE CILINDRICA**
Sono conformali, ma di 2 tipi:
- *NORMALI*, dove meridiani e paralleli formano angoli che creano griglie rettangolari, con distorsioni vicino i poli.
- *TRASVERSALE*, e formano una griglia curvilinea: solo il meridiano centrale e l'equatore formano un angolo giusto, e più ti allontani dal meridiano centrale e più le distorsioni aumentano.
- *CONICHE*, usa l'aspetto polare ed è fatto universalmente. I meridiani sono linee dritte equispaziate, che convergono oppure no a un certo polo: ogni parallelo attraversa tutti i meridiani agli angoli giusti e il pattern di distorsione è lo stesso lungo ogni parallelo

![[Pasted image 20241022164043.png]]
***6) UTM (Universal Transverse Mercator)***
E' la proiezione conformale più usata: è pseudo-cilindrica, dove il meridiano centrale e i paralleli sono rette.
Altri meridiani sono curve, spaziate regolarmente tra i paralleli; le distorsioni però aumentano spostandosi dal meridiano centrale.
In UTM il mondo è diviso in 60 (numerate da 1 a 60) zone uguali che sono tutte larghe 6 gradi in longitudine e in 20 bande orizzontali di 8 gradi in latitudine (classificate da C a X).
Una singola zona UTM è identificata univocamente dalla coppia (numero, lettera)

![[Pasted image 20241023114509.png]]
OGNI ZONA E' DIVISA IN UNA GRIGLIA REGOLARE 100km x 100 km, etichettate da lettere maiuscole.

Le coordinate di un punto nel sistema UTM sono *Easting (X) e Northing (Y)*.

**EPSG** è un database delle coordinate del sistema di riferimento esistente nel mondo: ogni *EPSG code* contiene l'ellissoide, il meridiano, il sistema di proiezione, identificando ogni zona UTM.


**_PSEUDO-MERCATOR_**

Variazione della proiezione di Mercator utilizzato come standard per le applicazioni web di mapping (es Bing Maps). Nella proiezione cilindrica di Mercatore:

-          I meridiani e i paralleli si intersecano ad angolo retto;
-          Lungo l’equatore le distanze si mantengono proporzionali;
-          La distanza tra paralleli aumenta progressivamente ai poli: è isogona (angoli inalterati) e conforme (preserva le forme)

![[Pasted image 20241206120946.png]]