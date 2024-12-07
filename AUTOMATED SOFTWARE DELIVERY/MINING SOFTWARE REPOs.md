### **Come capiamo quali cambiamenti (commit) introducono bug?**

Ci sono 3 tipi di commit:
- *bug-inducing commits*;
- *bug-fixing commits*;
- *nessuna dei 2*.

Sapendo di avere a nostra disposizione:
- *Bug reports* presenti in un bug tracker;
- *commit* registrati in un VCS.

Potremmo:
- *collegare i commit di fix ai bug report (LINKING)*
- si cercano i *commit che hanno corretto il bug*
## Fase di linking

A ogni coppia $(bug\space report, commit)$ si assegna un punteggio:
- **sintattico (syn)**: $0\leq syn\leq2$
- **semantico (sem)**: $0\leq sem\leq 4$

Ogni bug nel bug tracker è identificato dalla coppia $(bug \space id, commit \space id)$, ad esempio Il messaggio *"fixed bug 1234" del commit a3243* indica che **quel commit corregge il bug 1234 presente nel BT**.

Si assegna un punto di confidenza *sintattica* per 2 criteri: 
- se uno dei numeri del fixing commit è un *ID VALIDO NEL BT*;
- se il messaggio ha una *PAROLA CHIAVE RILEVANTE* (es. "bug") o non contiene altre parole (solo il numero del bug stesso).

Poi si assegna un punto di confidenza *semantica*, ovvero si **attribuisce una probabilità maggiore che un commit risolva un bug report**, per ciascuno di questi criteri: 
- lo stato del bug in questione è *passato almeno una volta nello stato FIXED*;
- la descrizione del bug report è contenuta nel *messaggio del fixing commit*;
- l'autore del fixing commit è registrato come *assegnatario del bug report*;
- uno o più *dei file modificati sono allegati al bug report*

Vengono poi mantenute le coppie $(bug \space report, fixi ng \space commit)$ tali per cui $sem>1\space OR \space  (sem=1\space AND \space syn>0)$

## Fase di fixing

Dato un fixing commit:
- si estraggono le *linee rimosse* in questa revisione;
- per ogni linea rimossa *si cerca il commit in cui questa è stata aggiunta*;
- *si escludono come commit sospette tutte quelle avvenute dopo che il bug report collegato dalla fixing commit è stato pubblicato*. 

Otteniamo quindi una tripla $(b,f,i)$, dove:
- $b$ è il bug report;
- $f$ è il fixing commit legato a $b$;
- $i$ è un cambiamento che ha corretto $b$;

## Probabilità di bug e fix di un commit

Per un repository, queste sono le probabilità per un commit che:
- $P(bug)= \frac{\#bug}{\#commit}$ 
- $P(fix)= \frac{\#fix}{\#commit}$  

## Mining di repository git

Ricordiamo che per estrarre informazioni da un repo abbiamo si può usare il comando:
- ***git log***
che permette di *esportare la storia dei cambiamenti del repo a partire da HEAD e tornando indietro*.

- ***git log --branches*** stampa i commit effettuati su tutti i branch.

**!!ATTENZIONE!!**, devi partire sempre dal commit da cui si vuol tornare indietro, quindi prima potresti dover fare:
- ***git checkout "nome_branch"***.

Il comando ***git log*** permette di stampare il log in diversi formati, ad esempio:
- ***oneline***, formato breve;
- ***fuller***, riporta tutto;
- ***format***, con esso decidiamo un formato, ad es: ***--pretty=format:"%H,%an"*** per commit e autore separati da virgola)
-  ***--patch***, permette di stampare, dopo le informazioni di ogni commit, la revisione.

## Mining di GitHub

GitHub fornisce delle ***API REST*** che consentono di acquisire informazioni sui vari repository: queste richiedono un ***API KEY*** per funzionare e forniscono un numero limitato di chiamate, attivate da terminale con le funzionalità CRUD.
Trovi alcuni esempi di uso in questa chat: https://chatgpt.com/share/673f6aae-d6dc-800b-9318-32127e89674f e la documentazione di GitHub qui: https://docs.github.com/en/free-pro-team@latest/rest
Sono molto **comode per acquisire informazioni semplici** (es. informazioni generali su una repo) **ma non per analisi complesse**.

**GitHub Archive** è un servizio che memorizza tutte le commit di tutte le repo nel mondo, ora per ora, salvandoli su file JSON.

## PushEvent

Per tracciare i commit fatti su un repo, bisogna analizzare i *PushEvent* (**eventi di push**).
I JSON possono aver subito cambiamenti di formato nel tempo.

Esempio di una push event della repo "rspt-theme" creata il 1 gennaio 2015.
``` JSON
{
"type": "PushEvent",
"actor": { "login": "rspt" },
"repo": { "name": "rspt/rspt-theme" },
"payload": {
"size": 1,
"ref": "refs/heads/master",
"commits": [
{
"sha": "6b089eb4a43f728f0a594388092f480f2ecacfcd",
"author": { "name": "rspt" },
"message": "Fix main header height on mobile"
}
]
},
"created_at": "2015-01-01T15:00:01Z"
}
```
