**ARGOMENTI:** *metodi di ricerca **simbolica** e **locale** nell'intelligenza artificiale, con particolare attenzione alla **soluzione di problemi attraverso la ricerca in uno spazio degli stati.** Questo concetto è fondamentale per molte aree dell'IA, specialmente in contesti ristretti, dove il controllo e la ricerca rappresentano elementi chiave.* 

I problemi possono essere modellati come **problemi di ricerca**, definendo uno **spazio degli stati (Strategie di Ricerca)che include tutti gli stati raggiungibili dallo stato iniziale mediante una sequenza di operatori.**

## Lo Spazio degli Stati
Lo **spazio degli stati** si caratterizza per:
- **uno stato iniziale** , non noto a priori, in cui l'agente sa di essere;
- **un insieme di azioni disponibili,** una funzione successore S che prende in input uno stato x e restituisce l'insieme degli stati raggiungibili;
- **un cammino**, sequenza di azioni da uno stato all'altro

## TEST: Raggiungimento del Goal
La verifica del raggiungimento del goal si effettua c**ontrollando se lo stato raggiunto appartiene all'insieme degli stati obiettivo.** Lo stato finale può essere descritto in maniera astratta attraverso proprietà specifiche. 

Gli obiettivi non sono solo limitati al raggiungimento del goal, ma *includono anche il trovare la sequenza di operatori che porta al goal, tutte le soluzioni o una soluzione ottimale.* In quest'ultimo caso, **una soluzione è considerata preferibile se minimizza i costi definiti dalla funzione costo di cammino**, che assegna un costo a ciascuna azione lungo il percorso.

![[Pasted image 20241026105046.png]]

## ESEMPI di OBIETTIVI 

1) Tra gli esempi discussi c'è il problema di un viaggio attraverso diverse città della Romania, in cui l'obiettivo è raggiungere Bucharest partendo da Arad. Ogni stato rappresenta una città e le azioni sono i viaggi tra le città. 
- **STATO INIZIALE:** Arad
- **FUNZIONI SUCCESSORE:** S(x)= Insieme di coppe azione-stato.  S(Arad)={Arad ->Zerind, Zerind, ...}
- **GOAL TEST:**  può essere *esplicito* (x="Bucharest") oppure *implicito* (controllamappa(x))
- **COSTO DELLA STRADA:** la somma delle distanze 
*Una soluzione sarà quindi una sequenza di azioni che portano dallo stato iniziale al goal.*

2) Un altro esempio è l'8-puzzle, dove gli stati rappresentano le configurazioni delle tessere e l'obiettivo è ottenere una configurazione predefinita muovendo la tessera vuota. 
L'assemblaggio con un robot è un ulteriore esempio in cui gli stati indicano le coordinate dei giunti del robot e le parti dell'oggetto da assemblare, mentre le azioni corrispondono ai movimenti dei giunti. 

3) *Il problema dei 3 missionari e 3 cannibali* illustra come evitare stati di fallimento in cui i missionari sono superati dai cannibali su una sponda del fiume. 
- ***Stato***: sequenza ordinata di tre numeri che rappresentano il numero di missionari, cannibali e barche sulla sponda del fiume da cui sono partiti. Lo **stato iniziale** è: (3,3,1).
- **Operatori**: possiamo portare in barca al massimo due persone. Quindi:
	- 1 missionario, 1 cannibale
	- 2 missionari
	- ecc;
- **Stato Finale:** (0,0,0)
- **Costo Cammino:**  numero traversate

4) L'**N-regine**, dove vogliamo disporre N regine sulla scacchiera in modo che non si mangino, e la **criptoaritmetica** sono altri esempi di problemi di IA affrontati tramite ricerca simbolica.

5) Troviamo poi anche il gioco del **Sudoku**, il problema della **Torre di Hanoi.**, il problema del **commesso viaggiatore**, il problema della **scimmia e la banana**, il problema **della capra, del lupo e del cavolo (variante dei cannibali e missionari, dove la barca ha capienza 1)**...

## *Cosa succede però quando consideriamo giochi quali quello degli scacchi o le parole crociate, in cui abbiamo spazi di ricerca molto ampi?*

Alcuni sistemi sono decomposti in **sottoproblemi risolvibili separatamente**, ma non tutti i sistemi sono decomponibili, **si possono avere sottoproblemi interagenti.** 
Altre domande che dovremmo porci  sono: l'interazione con l'utente, l'importanza della conoscenza incompleta e la possibilità di ignorare o annullare dei passi durante il processo di risoluzione (altrimenti il sistema è detto **irrevocabile**). In alcuni problemi, come l'8-puzzle, è possibile annullare i passi, mentre in altri, come negli scacchi, non è possibile. 

### *Sistemi di produzione MONOTONI* E NON-MONOTONI
I sistemi di produzione monotoni **non richiedono il backtracking** poiché l'applicazione di una regola non invalida le altre regole applicabili nel momento della selezione della regola stessa.
*E' possibile trasformare un sistema di produzione non-monotono in uno monotono.* (**FORMULAZIONE DI GREEN, FORMULAZIONE DI KOWALSKI**)

### *Problema A STATI SINGOLI*
Si tratta di problemi in cui lo ***stato è sempre accessibile*** e ***l'agente sa esattamente cosa produce ciascuna delle sue azioni e può ricavarsi in quale stato sarà dopo una qualunque sequenza di azioni**

### *Problema A STATI MULTIPLI*
Problemi in cui, al contrario dei primi, ****lo stato non è completamente accessibile e  l'agente deve ragionare su quali possibili stati potrebbe raggiungere. L'EFFETTO DELLE AZIONI PUO' ESSERE SCONOSCIUTO O IMPREVISTO.*** 

### RICERCA DI SOLUZIONI (*come generare sequenze di azioni* ): RICERCA ed ESECUZIONE

Dinanzi a tali scenari, la scelta migliore è quella di *mantenere ed estendere un insieme di sequenze e soluzioni PARZIALI* . 
Un agente così può decidere sul da farsi esaminando prima le sequenze possibili di azioni che conducono a stati con esisto SCONOSCIUTO, scegliendo poi quella migliore -> **PROCESSO DI RICERCA** (scegliamo ad ogni passo quale stato estendere), che possiamo vedere anche come **la costruzione di un albero di ricerca i cui nodi sono STATI  e i rami sono OPERATORI** . Tale albero rappresenta quindi *l'espansione degli stati a partire da quello iniziale, le foglie saranno quelli invece ancora da espandere*.

Una volta trovata la soluzione, le azioni dovranno essere realizzare: **FASE DI ESECUZIONE**

=> ***ALBERI DI RICERCA***
![[Pasted image 20241026120227.png]]
**STRUTTURA DATI:** ogni nodo possederà 
- *lo stato (nello SPAZIO DEGLI STATI) a cui corrisponde; 
- *il nodo genitore* 
- *l'operatore usato per ottenere tale nodo*
- *la sua profondità*
- *il costo del cammino dallo stato iniziale al nodo stesso*

![[Pasted image 20241026120541.png]]

***IL COSTO TOTALE DELLA RICERCA DARA' UGUALE AL COSTO DEL CAMMINO  SOMMATO AL COSTO DI RICERCA(tempo impiegato alla ricerca di una soluzione)***

### *LE STRATEGIE DI RICERCA*: INFORMATE (euristiche) E NON INFORMATE (blind)
![[Pasted image 20241026124753.png]]![[Pasted image 20241026125015.png]]
***I problemi che i sistemi basati sulla conoscenza devono risolvere sono NON DETERMINISTICI. In un certo istante più azioni possono essere svolte, ovvero più operatori possono essere applicati***.

**STRATEGIA:** informazione sulla conoscenza che sarà applicata potendo avere molteplici. 
*Con essa scegliamo quale stato espandere nell'albero di ricerca.*
Potremmo, in particolare:
- *Non usare alcuna conoscenza sul dominio: **Strategie NON INFORMATE (BLIND)** e procedere a fare una ricerca esaustiva* (il che ovviamente è impraticabile in certi contesti). 
  !!!Vengono sfruttate la ricerca *breadth-first e depth-first*, che espandono rispettivamente *i nodi a profondità minore o maggiore*. 

## RICERCA IN AMPIEZZA

- NELLA BFS **la PROFONDITÀ del nodo da cui si parte è uguale a 0; la profondità di un qualunque altro nodo è la profondità  del genitore più 1.*: essa ESPANDE sempre i nodi  MENO PROFONDI dell'albero. •All’ultimo livello sottraiamo 1 perché il goal non viene ulteriormente espanso.

- Questo valore coincide anche con la complessità spaziale (numero di nodi che manteniamo contemporaneamente in memoria). In particolare, con profondità 10 e fattore di ramificazione 10 dovremmo espandere 1010 nodi,  (tempo 128 giorni e 1 terabyte di memoria immaginando che un nodo richieda 100 byte di memoria e vengano espansi 1000 nodi al secondo): quindi il problema della memoria sembra essere il più grave.

- Nel caso peggiore, se abbiamo profondità $d$ e fattore di ramificazione $b$ il numero massimo di nodi espansi nel caso peggiore sarà $bd$. (complessità temporale).

  ![[Pasted image 20241026125051.png]]

- **STRATEGIA A COSTO UNIFORME:** se nella BFS espandiamo SEMPRE il nodo a costo minimo. Questa è completa e, a differenza della ricerca in ampiezza, ottimale anche quando gli operatori non hanno costi uniformi (complessità temporale e spaziale uguale a quella in ampiezza).


## RICERCA IN PROFONDITA'

Esplora prima il livello più profondo disponibile. 

 La strategia ***depth-first*** può essere *efficiente dal punto di vista della memoria* ma rischia di essere ***incompleta*** (non porta alla soluzione) se ci sono loop o ***RAMI INFINITI***. 
  ![[Pasted image 20241026125138.png]]
La DFS ESPANDE per primi nodi PIÙ PROFONDI e i nodi di UGUALE PROFONDITÀ vengono selezionati ARBITRARIAMENTE (quelli più a sinistra).
Per uno spazio degli stati con fattore di ramificazione $b$ e profondità massima $d$ la ricerca richiede la memorizzazione di $bd$ nodi.
La complessità temporale è invece analoga a quella in ampiezza.
Nel caso peggiore, se abbiamo profondità $d$ e fattore di ramificazione b il numero massimo di nodi espansi nel caso peggiore sarà $bd$. (complessità temporale).


  - ***La ricerca a PROFONDITA' LIMITATA*** introduce un *limite massimo di profondità* per evitare di esplorare inutilmente rami infiniti, oltre il quale l'algoritmo passa ad analizzare il successivo ramo o cammino.
  
 -  **L'algoritmo di approfondimento iterativo** combina i vantaggi della breadth-first e della depth-first, *espandendo i nodi con profondità crescente.* ***Questa strategia è completa e sviluppa un solo ramo alla volta, risultando particolarmente utile in spazi di ricerca ampi.*** In altri termini, inizialmente l'algoritmo effettua le operazioni di ricerca nei nodi poco profondi, quelli vicini al nodo radice, aumentando progressivamente la profondità di scansione nei cicli di ricerca successivi. Nel momento in cui l'algoritmo trova una soluzione interrompe il ciclo di ricerca senza dover scandagliare ulteriormente l'albero logico alla ricerca di altre soluzioni.

  ![[Pasted image 20241026125231.png]]![[Pasted image 20241026125254.png]]
  
  
- Le ***strategie INFORMATE*** si basano sull'uso di **conoscenza euristica** per selezionare gli stati da espandere. In particolare, l*a funzione di valutazione stima il costo per raggiungere il goal e viene utilizzata per scegliere il nodo più promettente da espandere.* 

Un esempio è l'algoritmo **GREEDY BEST FIRST**, che cerca di muoversi verso il massimo (minimo) di una funzione che “stima” il costo per raggiungere il goal. L'algoritmo A*, invece, combina il costo effettivo per raggiungere un nodo con una stima euristica del costo per raggiungere il goal, cercando di trovare il percorso più efficiente. A* garantisce di trovare una soluzione ottima se la funzione euristica è ammissibile, ossia se non sovrastima mai il costo per raggiungere il goal (Russell & Norvig, 2009).

Le strategie si valutano su quattro criteri: **Completezza, complessità temporale, complessità spaziale e ottimalità**.

## **RICERCA NON INFORMATA**
Viene definita "non informata" poiché *non utilizza alcun tipo di conoscenza del problema al di là della definizione del problema stesso*. La ricerca non informata è un metodo di ricerca (spesso) non efficiente poiché, non utilizzando alcuna  Informazione ulteriore sul problema da risolvere, implica l'esplosione
combinatoria di tutti gli stati possibili. 


**PERCHE' PREFERIRE LA RICERCA INFORMATA?**
I principali vantaggi sono i seguenti:
- **Evitare l'esplosione combinatoria**: L'algoritmo di ricerca informata non necessita l'espansione completa di tutti i nodi dell'albero di ricerca.
- Decidere quale nodo espandere: Nel processo di ricerca l'algoritmo decide quale nodo espandere tra quelli possibili in un medesimo livello senza doverli espandere tutti.
- Riconoscere i cammini promettenti. Sulla base della funzione di conoscenza l'algoritmo stima la probabilità di successo dei vari nodi/cammini prima di espanderli nel processo di ricerca.

La ricerca informata non elimina il processo di ricerca ma ne riduce fortemente i tempi di esecuzione. Pur non essendo una ricerca completa, la ricerca informata consente di raggiungere comunque soluzioni accettabili con maggiore efficienza rispetto a una ricerca non informata.






## **RICERCA BIDIREZIONALE**
A partire da due nodi, un nodo iniziale e un nodo finale (nodo obiettivo), l'algoritmo effettua due ricerca parallele. 
1) La prima ricerca scandaglia i cammini a partire dal nodo iniziale sui nodi successori. 
2) La seconda ricerca scandaglia a ritroso i cammini a partire dal nodo finale sui nodi predecessori. 
3) L'algoritmo di ricerca bidirezionale, infine, verifica l'esistenza di punti di contatto a metà strada tra le due ricerche.



## RICERCA LOCALE

Oltre agli algoritmi di RICERCA COSTRUTTIVA (quelli visti finora, **che generano una soluzione ex-novo aggiungendo ad una situazione di partenza (vuota o iniziale) delle componenti in un particolare ordine, o percorso, fino a “costruire” la soluzione completa**), esistono anche algoritmi di RICERCA LOCALE, che partono da una soluzione iniziale e cercano di migliorarla iterativamente esplorando soluzioni vicine. 


 Un esempio è l'**algoritmo Hill Climbing**, che si muove verso il massimo locale, ma può bloccarsi in massimi locali di bassa qualità, pianori o crinali. 
 - Il nome indica la capacità dell'algoritmo di *"scalare" i nodi verso quelli con valori maggiori*
 - Lo spazio di ricerca dell'algoritmo è limitato ai soli nodi vicini a quello corrente: quando un nodo vicino è migliore del nodo di riferimento ( nodo corrente ), quest'ultimo viene sostituito con il nuovo nodo.
 - Il ciclo di elaborazione dell'algoritmo  termina quando viene raggiunto il nodo con valore più alto ( "picco" ) ossia quando nessun nodo vicino ha valore superiore a quello di riferimento.

Per evitare tali problemi, si può utilizzare l'algoritmo di **Simulated Annealing**, che permette di fare occasionalmente mosse in discesa per uscire da massimi locali.
- La ricerca locale inizia da un nodo corrente iniziale e la scelta del nodo successore è generata casualmente ( esplorazione randomizzata ). 
- A differenza dell'algoritmo hill climbing stocastico, nell'algoritmo simulated annealing la probabilità di conferma delle "mosse peggiorative" ( mosse verso il basso ) è ponderata allo scarto del peggioramento e al tempo ( temperatura ) di esecuzione dell'algoritmo. 
- L'algoritmo non esclude a priori l'analisi delle mosse peggiorative ma le ammette con una probabilità decrescente nel corso del tempo.
- Evita il problema del massimo locale: Invece che ricominciare casualmente accetta dei valori inferiori della sua soluzione per poi cercare di arrivare ad una soluzione migliore

## METAEURISTICA

Metodo euristico per la soluzione di una classe molto ampia di problemi computazionali combinando diverse procedure a loro volta euristiche, con l'obiettivo di ottenere una procedura più robusta ed efficiente: troviamo, per esempio, gli algoritmi GENETICI (*evolutivi*) e la TABU SEARCH: questi *MIRANO A MIGLIORARE LA RICERCA LOCALE.* 

La **Tabu Search**, in breve, utilizza una memoria per evitare di ripetere stati già esplorati, mentre l'ottimizzazione basata sulle formiche imita il comportamento delle colonie di insetti nella ricerca del cammino più breve (Dorigo et al., 1996).
Il principio base è quello di impiegare una ricerca locale tradizionale e qualora si giunga in corrispondenza di ottimi locali, **essere disposti ad accettare delle mosse precedenti non-miglioratrici, ritornando indietro ad esaminare le soluzioni già esplorate (già registrate in un vettore)**.
## MIN MAX
Il file termina con un approfondimento sull'algoritmo MinMax, comunemente utilizzato nei giochi come scacchi e dama, in cui i giocatori alternano le loro mosse cercando di massimizzare il proprio punteggio e minimizzare quello dell'avversario. 
E' un algoritmo *ricorsivo* (computazionalmente costoso), che funziona calcolando tutte le possibili mosse di entrambi i giocatori e scegliendo la mossa con il punteggio maggiore per “MAX” e minore per “MIN”.
L'algoritmo crea un albero decisionale in cui ogni livello rappresenta le mosse di un giocatore, con il giocatore Max che cerca di massimizzare i punti e il giocatore Min che cerca di minimizzarli: *può funzionare per i giochi senza informazioni o possibilità perfette*.