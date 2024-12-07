1) **TIPI DI PROGRAMMI**
- S: se è scritto a seguito di una specifica precisa (es. calcolatrice). E' corretto se *aderisce alla specifica* (sempre verificabile), e col tempo ciò non varia.
- P: se risolve un problema complesso, attraverso un'approssimazione utile nella realtà (es. previsioni meteo o scacchi). E' corretto se quest'ultima *è accettabile*.
- E: se è scritto per automatizzare una certa attività svolta da umani (es. guida autonoma). E' corretto se l'attività che automatizza *è quella che un umano svolgerebbe in un determinato momento*: dev'essere sempre adattato al contesto attuale o diventa obsoleto, aumentando il numero di funzionalità e il tasso di qualità percepita.
- A: unione di P ed E. E' corretto se *supporta realmente l'attività per la quale è stato scritto.* Col tempo la sua correttezza può cambiare: per esempio un programma P videogioco avrà una grafica insufficiente col tempo, o per un programma E che gestisce un registratore di cassa, se non aggiorniamo una valuta appena cambiata nel Paese, è scorretta col tempo.

**2) TIPI DI CAMBIAMENTI SOFTWARE**
- **ADATTIVI:** nuove feature richieste;
- **CORRETTIVI**: bug fixing.
- **PERFETTIVI**: miglioria della qualità interna.

**3) VERSIONI**
Il nostro obiettivo non è mantenere solo l'ultima versione del programma, ma anche le precedenti. 
Formalmente, una versione è l'insieme di codice sorgente e eventuali altri asset in un certo istante, oltre ad essere un *rilascio* del software.

**4) STANDARD DI VERSIONI**
Uno dei sistemi più adottati è il *SemVer*.
La sintassi è ***{major}.{minor}.{patch}***
- *major*: una modifica che ha grande impatto sulle funzionalità.
- *minor*: una modifica con impatto minimo sulle funzionalità.
- *patch*: modifica minore con zero impatto sulle funzionalità.

**5) COME GESTIRE PIU' VERSIONI?**
Il primo approccio potrebbe essere mantenere più copie del software, una per ciascuna versione: ciò però porta a diversi svantaggi.
Intanto, *più major releases possono coesistere*, applicando lo stesso cambiamento a più funzionalità (es. per Android 13 e 14 allo stesso tempo).

**6) COS'E' UNA PATCH?**
E' un insieme di *cambiamenti applicabili a uno o più file*: essa consiste in rimozioni e/o aggiunte di linee di codice.
Essa può essere applicata a una versione del codice per modificarlo: ogni sviluppatore lavora in locale e genera delle patch da inviare al *maintainer*, che le verifica e le usa per aggiornare le versioni coinvolte.

![[Pasted image 20241024102452.png]]
Con:  
	-return false, **intendiamo che abbiamo rimosso questa.**
    +return x!=null, **abbiamo aggiunto questa riga.**


**7) VCS (Version Control System)**
Usare una metodologia basate su versioni (cartelle) e patch può *rendere molto complesso lo sviluppo di un software*; per questo sono nati sistemi per gestire le versioni, i **Version Control System (VCS)** o i **Source Code Management (SCM)**
I primi sono sistemi (software) che supporta gli sviluppatori nello sviluppo collaborativo e nella gestione delle versioni.

**8) REVISIONI**
Una revisione è un cambiamento atomico effettuato da uno sviluppatore al fine di completare uno specifico task: la differenza con la *versione* è che una revisione non corrisponde sempre a un *RILASCIO*.
**Qual è il loro rapporto coi VCS?**
- I VCS tracciano le diverse revisioni del codice sorgente, ovvero i singoli cambiamenti effettuati dagli sviluppatori. 
**COMMIT** è l'operazione di *creazione di una revisione*, ed essa contiene il contenuto cambiato nel codice, un riassunto testuale del cambiamento e altri metadati (data, autore...)

Data una revisione $R_{i}$ e la successiva $R_{i+1}$, un VCS può memorizzare i cambiamenti in 2 modi:
- registrare la patch che ha portato da $R_{i}$ a $R_{i+1}$ (*delta*), la quale richiede *meno spazio ma più tempo per l'accesso a una data revisione*.
- registrare l'intero $R_{i+1}$, ciò richiede più spazio ma permette di accedere al volo a qualsiasi revisione: le patch VANNO RICALCOLATE.


**9) REPOSITORY**
E' un contenitore di revisioni software: generalmente gli sviluppatori lavorano su **WORKING DIRECTORY COPY LOCALI**, e quando una revisione è completa la salvano (tramite **COMMIT**) nel repository.
I VCS tracciano le revisioni e i relativi autori e consentono di condividere un repository centrale: se una revisione introduce un bug, si può tranquillamente tornare a quella precedente e si può *navigare la storia del progetto per capire l'origine di un problema e risolverlo.* 

**10) CONFLITTI NELLO SVILUPPO COLLABORATIVO**
Uno dei dei problemi nello sviluppo collaborativo riguarda la *modifica concorrente* dello stesso file da più utenti.
Ad esempio, A modifica il metodo _toString_ della classe _Test_ mentre B modifica il metodo _test_ della stessa classe.
Per evitare problemi di questo tipo, generalmente si dichiara il lock sui file su cui si lavora, in modo da evitare conflitti.
Questi vanno **risolti manualmente** dagli sviluppatori.

**11) TIPI DI VCS**
- **CENTRALIZZATI:** hanno un'architettura di tipo client-server: il server ha il repository ufficiale, i client (sviluppatori) invece hanno solo delle *working copy*. I commit vanno fatti sul repository centrale.
- **DISTRIBUITI:** hanno un'architettura di tipo peer-to-peer, dove per ogni sviluppatore ha un repository locale, collegato a diversi repository remoti: **il commit va sempre fatto sul repository locale, e poi si procede alla sincronizzazione di quelli remoti.**
Nella prima abbiamo bisogno di Internet.

**12) BRANCH**
I VCS consentono di avere diverse linee di sviluppo (branch) contemporaneamente: questo permette di gestire facilmente le diverse versioni del software.
![[Pasted image 20241024112559.png]]
Per esempio, questi 2 branch sono descritti da un **albero**.
Data la presenza di branch e dato che questi possono riconciliarsi, **se (in gergo) faremo un "merge" per unirli** *la struttura dati ottenuta è un DAG* (grafo diretto aciclico).
![[Pasted image 20241026101027.png]]
R7 qui sarà un DAG, mentre fino al momento prima del merge avevamo un albero composto dai 2 branch.