## Alcune definizioni sui robot

- Un robot è un *manipolatore multifunzionale e riprogrammabile* progettato per spostare materiali, parti o altri dispositivi **grazie all'esecuzione di movimenti variabili programmati per l'esecuzione di certi compiti**.

Questi compiti devono essere svolti con *accuratezza, velocità* e devono essere *ripetitivi*: inoltre, sono eseguiti o in **AMBIENTI STRUTTURATI (industrie)** o in **AMBIENTI NON STRUTTURATI (autonomi)**.

I *primi* sono ambienti:
1) **strutturati sui bisogni del robot**
2) **procedure BEN DEFINITE e ripetitive, con posizioni predefinite degli oggetti da manipolare**;
3) **PRESENZA UMANA ben delimitata**.
   
I *secondi*, invece, sono ambienti:
1) **con condivisione dello spazio di lavoro tra uomo e robot**
2) **maggiori capacità percettive**;
3) **comportamento reattivo**.


- Un robot **autonomo** è una macchina capace di accettare ed eseguire ***autonomamente*** comandi in ambienti non completamente strutturati senza l'intervento dell'uomo: quindi il robot qui pianifica ed esegue autonomamente le proprie azioni, e lo fa in maniera dinamica. 
- In un robot **non autonomo** esiste la **teleoperazione**, ovvero robot è *comandato passo passo da un operatore posto in una postazione remota* (grazie a strumenti come display e joystick), attraverso un canale di comunicazione.
- Nei robot **semi-autonomi** c'è un controllo condiviso tra utente e robot, con diversi livelli di **SEMI-AUTONOMIA.**


## Sistema di supervisione di un robot

![[Pasted image 20241205114600.png]]

1) **Controllori di basso livello:** *agiscono direttamente sul dispositivo per controllarne la dinamica* (es per controllare la posizione, velocità e coppia di un motore);
2) **Controllori di alto livello:** essi (tra cui *supervisori e pianificatori*) devono *pianificare e supervisionare il comportamento complessivo del robot*.

## Paradigmi per la supervisione di un robot

Ricordiamo che un paradigma è un **insieme di assunzioni tecniche e teoriche risolutive che definisce un approccio ad una certa classe di problemi**: scegliere il paradigma giusto per affrontare un problema rende facile arrivare alla miglior soluzione.

3 **paradigmi principali organizzano le funzioni primitive** del robot (**percezione** o **SENSE**, **pianificazione** o **PLAN**, **attuazione** o **ACT**), ovvero per organizzare il problema della *supervisione o pianificazione dei suoi comportamenti*.
Intanto ecco una panoramica sulle 3 primitive:
![[Pasted image 20241205125015.png]]

- **Paradigma gerarchico (S-P-A)**:
    - **Pianificazione dettagliata a priori basata su una rappresentazione interna dell'ambiente**.
    - *Vantaggi: **predicibilità ed efficienza**.
    - *Svantaggi: **scarsa adattabilità** in tempo reale, **alta complessità computazionale**.
- **Paradigma reattivo (S-A)**:
    - **Basato su reazioni immediate a stimoli esterni, senza modellazione globale dell'ambiente**.
    - *Vantaggi*: **alta adattabilità, bassa complessità computazionale**.
    - *Svantaggi*: **difficoltà a prevedere il comportamento globale e a gestire conflitti tra moduli**.
- **Paradigma ibrido (P-S-A)**:
    - **Combina i vantaggi di gerarchico (pianificazione) e reattivo (adattabilità**).
    - **Utile per compiti complessi in ambienti dinamici**.

## Architetture di supervisione

Strutture che mettono in relazione componenti di base *e definiscono le loro interazioni*.

**1) Architettura gerarchica**:
- Strutturata su *livelli* (strategico, tattico, esecutivo): il primo *genera una strategia in base al compito da eseguire*, il secondo *genera i comandi*, il terzo *riceve i MACRO-COMANDI dal livello tattico e si occupa del controllo in tempo reale degli attuatori.*
- Applicazione tipica: *scenari ben definiti con compiti sequenziali*.

Nelle architetture gerarchiche la **percezione** si usa per mantenere la corrispondenza (*modello interno del mondo*, *modello esterno*), dove il primo contiene **l'informazione sensoriale percepita, una rappresentazione dell'ambiente dove il robot opera e altre informazioni necessarie per eseguire il compito**: la rappresentazione del mondo **cambia ogni volta che il robot percepisce l'ambiente, e il PIANO DELLE AZIONI E' STABILITO SULLA BASE DI TALE RAPPRESENTAZIONE**.

Esempio per il task "prendi la bottiglia dal frigo":

```C
#Livello strategico: 
-vai in cucina
-vai davanti al frigorifero
-apri al frigorifero
-prendi la bottiglia…
#Livello tattico:
 Vai in cucina: 
-muovi_base(X1,Y1); 
-muovi_base(X2,Y2)…
 Apri il frigorifero: 
-muovi_braccio(P1), 
-Apri_Mano()….
#Livello esecutivo:
 Muovi_base(X1,Y1); 
muovi_base(X2,Y2); 
muovi_braccio(P1)…
```

*Svantaggi*:
- **Alta complessità computazionale** dovuta principalmente alla modellazione dellambiente e al ragionamento
- **Poca adattabilità alle modifiche in tempo reale dell‟ambiente** o bassa reattività
- **Basso parallelismo**

**2) Architettura reattiva**:
    - Basata su *comportamenti modulari INDIPENDENTI TRA LORO * (es. evitare ostacoli), **dove ciascuno ha una specifica competenza assegnata e determina un certo comportamento**. 
      Il robot interagisce solo con sensori e attuatori: la conoscenza del mondo *non è né modellizzata né memorizzata nel robot* (quindi **non esisterà un planning delle azioni del robot**), ma è **estratta in tempo reale dal mondo stesso attraverso i sensori**.
    - **Vantaggi e Svantaggi:** tra i vantaggi c'è un **alta adattabilità alle modifiche dell'ambiente**, a **differenza di prima**, poi **abbiamo una bassa complessità di ogni livello e basso costo computazionale complessivo** e possiamo avere **parallelismo nel controllo**. 
      Tra gli svantaggi, invece, c'è **difficoltà nel prevedere a priori il comportamento globale del robot**, specialmente aumentando i comportamenti del robot, e quindi con una conseguente difficoltà nella **risoluzione di conflitti nella concorrenza tra moduli**.

Un esempio è l'architettura *subsumption*, nel quale i **comportamenti sono organizzati in una architettura a
strati ed hanno priorità diversa a seconda del loro livello**: di conseguenza gli input ai moduli possono essere soppressi e output inibiti dagli output di altri moduli (meccanismo tramite il quale *strati superiori assumono il controllo degli stati inferiori*).

**3) Architetture ibride**:

In queste i robot sono dotati di capacità di eseguire compiti semplici in maniera efficiente, ma *non garantisce l'esecuzione di task più complessi, che includono modellizzazione dell'ambiente e comportamenti più complessi*. 

- Includono pianificatori strategici e moduli reattivi.
- Bilanciano efficienza di esecuzione e capacità di risposta rapida.

Tipicamente una architettura ibrida comprende un modulo
*pianificatore strategico* e un modulo *pianificatore tattico* per la gestione dei comportamenti di un robot.
- Il pianificatore strategico pianifica a lungo termine le azioni del robot, individuando la sequenza di sotto-obiettivi da realizzare per raggiungere il goal e passando i risultati per l'esecuzione al pianificatore tattico. 
- Il pianificatore tattico inizializza e monitora i comportamenti prendendosi cura degli aspetti temporali per la loro coordinazione.


**4) Architetture distribuite**:
    - **Sistemi robotici multipli di complessità inferiore, che collaborano per eseguire un compito**.
    - L'**intelligenza è distribuita tra i vari sistemi, ognuno dei quali è autonomo**.