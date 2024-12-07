**1) COS'E' GIT**
E' uno dei VCS più usati ora: è **distribuito e conserva le diverse revisioni (delta).**
E':
- di **alto livello** (VCS).
- sia di **basso livello** (**filesystem**).
- scalabile: **gestisce bene dati crescenti aggiornando solo HW, e non anche il SW.**
  
***GITHUB*** è distribuito sì, ma **usato in una maniera centralizzata** perché abbiamo una copia centrale del repository, dove eventualmente condividiamo una commit.



**2) INIZIALIZZAZIONE**
Per usare ad usare git bisogna creare un repository:
![[Pasted image 20241025162746.png]]
Con $init$ creiamo una cartella ".git" all'interno della cartella specificata.
Questo è fatto localmente.
Dentro questa conserviamo tutti i file che GIT usa **internamente per conservare la storia del progetto**.



**3) COM'E' FATTO UN REPOSITORY?**
E' costituito da 2 parti:
- la **cartella ".git"** che contiene tutte le informazioni storiche del repository (nascosta)
- la **working directory**, che contiene i file su cui si lavora attivamente (es. un progetto Java) e che usiamo AL MOMENTO.
Se la cartella "**.git**" è presente, possiamo sempre **ripristinare la working directory**, ma non è vero.
Un repo permette di tracciare file e quindi anche delle cartelle: i primi sono detti $blob$, i secondi $tree$.

**I REPOSITORY GIT SONO LOCALI DI DEFAULT, dove le modifiche vengono per prima memorizzate nel .git.
E' POSSIBILE, POI, SINCRONIZZARE IL REPO LOCALE CON UN REPO REMOTO**.


**4) COMMIT**
Un repo può essere visto come un **grafo di COMMIT**, dove ciascuna contiene una o più patch e diversi metadati.

**5) AGGIUNGERE UN FILE**
Per registrare una modifica a un file, bisogna eseguire due passaggi:
1) aggiungere il file alla **STAGING AREA**
2) eseguire l'operazione di **COMMIT**.


**6) STAGING AREA (SA)**
Permette di avere uno "stato intermedio tra modifica non tracciata e tracciata", consentendo di:
- **rivedere i particolari della revisione** che si vuole effettuare prima di procedere;
- **dividere le modifiche in più commit**, dato che *non siamo forzati ad eseguire un commit unico che contiene tutte le modifiche* apportate alla working directory.

- Per **aggiungere una versione di un file alla SA**, bisogna eseguire il comando: 
![[Pasted image 20241026102625.png]]
- **Se aggiungiamo "--all" andiamo ad aggiungere TUTTE LE MODIFICHE A TUTTI I FILE modificati e TRACCIATI nella STAGING AREA.**
- **Se abbiamo tipo 3 file modificati ma vogliamo aggiungerne solo 2 contemporaneamente, possiamo fare "git add nomefile1 nomefile2"** 




**7) GIT STATUS**
Mentre si lavora su un progetto, *può essere sempre comodo capire quali file sono stati aggiunti alla SA* prima di effettuare il commit grazie al comando:
![[Pasted image 20241026103329.png]]
Questo comando però è utile anche per altro, difatti ci fa capire lo stato di un singolo file:
- **ignorato:** file che non verrà mai tracciato;
- **non tracciato:** file non ignorato esplicitamente ma che non è ancora tracciato in git (nessuna informazione sua nella storia);
- **modificato**: file modificato ma non aggiunto alla SA (che quindi non farà parte del commit)
- **aggiunto**: file modificato e aggiunto alla SA, pronto a essere incluso nella commit.

Con l'operazione di $add$, un file passa da:
- **"ignorato"/"non tracciato" a "aggiunto"**, se facciamo per la prima volta $add$ a quel file
- **"modificato" a "aggiunto"**, se il file è già tracciato da git.

**E PER SCARTARE UNA MODIFICA EFFETTUATA?**
**Ammesso che un file non sia stato incluso in una commit**, possiamo tornare indietro dallo stato del file nella SA:
- ![[Pasted image 20241026111711.png]]
Se il file è "aggiunto" da una $add$ e **vogliamo rimuoverlo dalla SA**.

- ![[Pasted image 20241026111758.png]]
**Se il file è "modificato" e vogliamo ripristinare la sua versione all'ultimo commit.**

CASO PARTICOLARE:

![[Pasted image 20241026191519.png]]
Cos'è successo qui? 
**Praticamente ho modificato questo file "GIT.md" e GIT fa il confronto tra questo (nella W. DIR.) e quello della precedente versione (in /.git).**
E qui non ho ancora aggiunto "GIT.md" alla SA.









**7) COMMIT**
Una volta che la SA contiene tutte le modifiche di cui si vuole fare $commit$, per confermare il commit in git dobbiamo eseguire:
- ![[Pasted image 20241026111953.png]]
**UN COMMIT DEVE AVERE UN MESSAGGIO: di default viene aperto un editor di testa per consentire di scrivere un messaggio.**
**POSSIAMO EVITARE QUESTO PASSAGGIO CON "-m MESSAGGIO":**
- ![[Pasted image 20241026112131.png]]

**DOPO LA COMMIT del file, LA SA VIENE SVUOTATA da quel file**

*PROCEDIMENTO COMPLETO:*
![[index1@2x.png]]

- **Se vogliamo fare in una SINGOLA COMMIT più modifiche presenti nella STAGING AREA:**
![[Pasted image 20241026195738.png]]



**8) COME DEVE ESSERE UNA COMMIT?**
I commit devono avere modifiche:
- **CIRCOSCRITTE:** per completare un task devono avere il minimo numero di esse.
- **COERENTI:** devono riguardare la stessa micro-operazione.
Inoltre, un commit dev'essere **ben documentato** attraverso il messaggio: più informazioni contiene il messaggio, più facile sarà capire il motivo di una modifica.
Oltre alle modifiche ai file, un commit contiene i seguenti metadati:
- nome, email e data dell'**AUTORE**, ovvero chi ha fatto il cambiamento.
- nome, email e data del **COMMITTER**, ovvero chi ha fatto il commit nel repository (non sempre lui e l'AUTORE corrispondono!).
- **messaggio**, composto da un **riassunto** di **massimo 50 caratteri** e da una **descrizione** approfondita.
- **stringa alfanumerica** di 40 caratteri che lo **identifica** univocamente (abbreviabile anche ai primi 6-7 caratteri). 




**9) RIMOZIONE**
Se voglio smettere di tracciare un file basta eseguire il comando:
![[Pasted image 20241026173104.png]]
**ATTENTO! QUESTA RIMUOVE IL FILE ANCHE DALLA WORKING DIRECTORY, PER EVIRARE CIO' USA "--cached"**

- **Anche l'operazione di rimozione va prima nella SA e poi confermata con commit.**
- **Dopo l'operazione di commit, il file non viene più tracciato: le versioni precedenti però rimangono nella storia.**

- **PER IGNORARE UN FILE o CARTELLE INTERE SUBITO, anche se la cronologia delle sue modifiche rimane (la togli con "rm cached" vista prima), aggiungi il FILE o la CARTELLA ad un nuovo file chiamato ".gitignore"**: questo è composto da righe dove ciascuna rappresenta i file da ignorare (nella working directory) in futuro, quindi GIT non farà generare più avvisi di tracciamento su questi.


**AD ESEMPIO, SE VOGLIO SMETTERE DI TRACCIARE UNA CARTELLA CHIAMATA "ALLEGATI" D'ORA IN POI, cosa faccio?**
![[Pasted image 20241026184819.png]]

ATTENTO! **Nel .gitignore**, se hai una cartella con spazi, puoi scriverla normalmente nel file, mentre nella bash di linux scrivila tra apici ''.
La prima cartella non ha il '/'.


![[Pasted image 20241026184902.png]]
![[Pasted image 20241026184922.png]]

**COSI', GIT IGNORERA' QUALSIASI CAMBIAMENTO FUTURO DELLA CARTELLA "ALLEGATI", e così posso aggiungere o modificare file esistenti senza essere tracciati.**




**10) RINOMINARE UN FILE**
Non esiste un modo per tracciare esplicitamente il fatto che un file è stato rinominato!
Se ho un file $a$ e lo rinomino in $b$:
![[Pasted image 20241026173824.png]]
Git usa delle euristiche per determinare se un file è stato rinominato (es somiglianza testuale maggiore dell'80%).


**11) STORIA**
Git traccia la storia di uno o più file attraverso i commit: **un commit può avere uno o più genitori, ECCETTO IL COMMIT INIZIALE CHE NE HA ZERO.**

- **PUNTATORE HEAD:** per convenzione punta sempre all'ultimo commit della working directory.
Esempio:
![[Pasted image 20241029152449.png]]
C3 è HEAD.

- **LA COMMIT DEL MERGE DI 2 BRANCH HA 2 PADRI (VEDRAI DOPO)**, e solo per loro succede in GIT.

- Ovviamente **non sempre HEAD punta all'ultima commit**, **possiamo andare indietro** e **avanti** nel branch.

- Se **HEAD punta al nome di un branch, allora punterà automaticamente all'ultima commit di quel branch**.



**12) BRANCH**

Un **branch** in GIT è una LINEA DI SVILUPPO.
Il nome del branch **è il puntatore all'ultima commit di quel branch**.

**13) TORNARE INDIETRO**
Abbiamo 2 opzioni:
- **REVERT:** registra un nuovo commit che ripristina lo stato del repo ad un commit passato (fa l'esatto opposto di ciò che ha fatto l'ultima commit).
  Opera esclusivamente su un singolo commit!
- **RESET:** sposta HEAD ad un commit passato, ignorando i commit in mezzo a quello precedente e il nuovo. 

**Se voglio tornare a 2 commit precedenti eliminando quelle successive, con RESET vado direttamente a 2 commit prima, mentre se usassi REVERT dovrei fare il revert di ogni commit in mezzo (quindi delle singole 2).!!!!**

- **IN UNA COMMIT DI UN MERGE, spostare HEAD è diverso perché bisogna specificare in quale branch spostarsi.**

- QUANDO SPOSTIAMO HEAD INDIETRO nel branch, non possiamo creare una commit! 

- **SOLO SE SIAMO NELL'ULTIMA COMMIT DEL BRANCH, POSSIAMO CREARE UN ALTRA COMMIT: ALTRIMENTI, SE CI SIAMO SPOSTATI INDIETRO L'UNICA COSA CHE POSSIAMO FARE E' RIPRISITINARE LO STATO OPPURE CREARE UN NUOVO BRANCH A PARTIRE DA LI'**.

- SIA CON REVERT CHE RESET, le commit che noi virtualmente "annulliamo" non sono mai eliminate a basso livello, anche se sono inaccessibili da GIT.
  L'unico modo è salvare precedentemente l'hash del commit e accedervi dopo REVERT o RESET. **QUESTA OPERAZIONE POSSIAMO FARLO PER QUALUNQUE COMMIT, genericamente, con questo comando:**
![[Pasted image 20241030123413.png]]
	**(spostiamo HEAD su questo commit)**




**14) COME CREARE UN BRANCH e CAMBIARE BRANCH**
Può essere comodo biforcare la storia e crearne 2 versioni mentre si lavora **per evitare che le modifiche fatte impattino sulla storia "ufficiale" del progetto finché non sono abbastanza stabili (testate)**.
Per creare una biforcazione:
![[Pasted image 20241030122657.png]]

Guarda qui:
![[Pasted image 20241030122729.png]]
Abbiamo 2 branch, master e x: ciascuno punta all'ultima commit di ciascuna.

- **Se siamo su master e vogliamo spostarci su x**: 
![[Pasted image 20241030122854.png]]
Con questo comando GIT **AGGIORNA TUTTI I FILE DELLA WORK. DIRECTORY in modo che siano allineati con l'ultimo commit del branch.**
Quindi **HEAD punta a quel nome del branch (e quindi ci spostiamo sulla sua ultima commit)**.

![[Pasted image 20241030132005.png]]



**15) UNIRE BRANCH**
Se non si fa nulla, le storie relative ai 2 branch procederanno parallele per sempre.
Se serve, possiamo "mergiarli" attraverso il comando merge, da eseguire mentre si è sul branch in cui si vogliono avere i risultati.
![[Pasted image 20241030131538.png]]

- 
![[Pasted image 20241030131531.png]]


- Se faccio il merge tra 2 branch nei quali si è lavorato su **FILE DIVERSI, il merge va a buon fine.**
- Se invece io e un altra persona lavoriamo su branch diversi ma modifichiamo **STESSI FILE, c'è un conflitto**. Dovremmo noi arbitrariamente scegliere, in accordo coi colleghi, cosa fare.

ESISTE UN **MERGE TOOL** che fa vedere, solo in caso di conflitti, i file responsabili del problema, sia della versione del mio branch che di quello del collega, e poi vediamo quello ufficiale, e possiamo scegliere quali modifiche MANUALMENTE AGGIUNGERE.

**Come detto, merge crea un commit con 2 padri (gli ultimi commit dei 2 branch coinvolti)**; questo commit ha:
- una revisione **vuota** (rispetto al branch di origine);
- una contenente una **fusione di tutte** le revisioni dei branch.


**16) DIFFERENZA**
Per visualizzare una revisione relativa a un commit abbiamo il comando:
![[Pasted image 20241030132445.png]]
Così, funziona:
- **sia prima di mettere un file nella SA**
- **sia per confrontare diversi commit**.

PERO', **possiamo specificare un commit-hash per vedere la differenza rispetto a uno specifico commit o file**:
![[Pasted image 20241030132701.png]]

**17) TRACCIARE STORIA DEL REPO**
Un comando che abbiamo visto è :
- **git log**.
Questo sarebbe il risultato:
![[Pasted image 20241111143515.png]]
Abbiamo il puntatore HEAD che punta all'ultima commit su master qui, che corrisponde quindi al commit stesso.
Per ogni commit abbiamo l' hash, autore, data e ora e messaggio di riepilogo.

**18) GIT CLONE**
![[Pasted image 20241111144604.png]]
Permette di creare una copia (o clone) di **un repository già esistente in remoto** nella cartella corrente, **senza poter collaborare alla modifica del repo remoto clonato**.

L'URL possiamo indicarlo in diversi modi, in base al protocollo offerto dal server che ospita il repository remoto:
![[Pasted image 20241111144747.png]]
Se cloniamo un repository su GITHUB, è possibile:
![[Pasted image 20241111144849.png]]
Una volta completato, il comando **git clone** avrà creato nella directory corrente **una directory che ospita il clone del repository remoto e avrà creato una connessione chiamata origin che punta al repository remoto originale**. Tale connessione verrà usata da altri comandi per inviare e ricevere nuove modifiche dal repository remoto.

**19) COME CREO UN REPOSITORY REMOTO?**
- Crea prima una repo locale da bash.
- Crea su GitHub.com con la UI il repository remoto.
- Aggiungi il repository remoto al repo locale.

![[Pasted image 20241111150147.png]]
ORIGIN è il nome del repo remoto (sarebbe main o master, ma con questa procedura è chiamato così per convenzione).

**20) SINCRONIZZAZIONE**
Per sincronizzare il repo locale e quello remoto si possono eseguire diverse operazioni:
- **push: per caricare i cambiamenti locali in remoto, se ci sono conflitti fallisce.**
- **fetch: per scaricare i cambiamenti remoti in locale.**

1) Il comando **git push in Git** serve a fare l’upload delle modifiche locali su un repository remoto. In questo modo, i commit locali sono resi disponibili agli altri collaboratori del progetto, che potranno recuperarli tramite un fetch e incorporarli nei rispettivi repository locali.

COMANDO git push:
- ![[Pasted image 20241112094317.png]]
- ![[Pasted image 20241112094325.png]]

Nella modalità standard, **git push** invia solo le nuove modifiche, poiché Git sa quali commit sono già presenti nel repository remoto.
![[Pasted image 20241111152644.png]]
**Eseguendo git push senza indicare argomenti, verranno inviate al repository remoto collegato al branch attualmente in uso nella propria working copy locale solo i nuovi commit.**
Con l’argomento **–all** invece viene fatto l’upload di tutti i branch presenti nel repository locale verso il repository remoto.

ATTENZIONE!
![[Pasted image 20241111152903.png]]

2) Il comando **fetch** fa SOLO **il download dei branch remoti in locale**, senza fare il merge.
Difatti poi, di solito, si esegue il merge dopo fetch.
**IN ALTERNATIVA:**
![[Pasted image 20241112094938.png]]


https://aulab.it/guide-avanzate/3/guida-git-in-italiano/?_gl=1*cbzrvn*_up*MQ..*_ga*ODk3MDM5MTA1LjE3MzEzMzI5OTg.*_ga_CLQWCBG221*MTczMTQwMjA4My4yLjEuMTczMTQwMjM1MC4wLjAuMTQyOTUzMjY3MA..