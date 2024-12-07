### Team di sviluppo

Esso può avere 2 ruoli chiave:
- **SVILUPPATORE:** *semplicemente scrive codice*.
- **MAINTAINER**: oltre a scrivere codice, ha il compito di gestire le versioni e, quindi, *accettare o rifiutare le richieste di cambiamento fatte dagli sviluppatori*. Chiunque sia un maintainer (può esisterne anche più di uno) **può avere l'accesso esclusivo ad alcuni branch**. Loro possono direttamente scrivere sui repository.

### Segnalazione di problemi

Gli **ISSUE TRACKER** permettono di *segnalare problemi (aprendo dei "ticket") e tenere traccia delle segnalazioni*: alcuni issue tracker sono Jira, Bugzilla, Trac. 
- **GitHub** ne fornisce uno tra questi.
Un issue tracker è usato, generalmente, **sia dagli utenti che dagli sviluppatori.**
Ma quali sono i problemi più comuni:
- **richiesta di funzionalità**;
- **bug**.

**Ma come funziona un issue tracker?**
- Esso conserva diverse informazioni riguardanti lo *stato* della segnalazione (SEGNALATO, ASSEGNATO, RISOLTO), la *versione* del software di riferimento, l'*assegnatario* ecc...

Com'è fatta una segnalazione?
- **riassunto**, "di cosa si tratta?";
- **procedura**, "cosa fare per riprodurre il problema";
- **risultato atteso**, "cosa ci aspetta che il software faccia?";
- **risultato reale**, "cosa succede in realtà?";

Esempio di issue: https://bugs.kde.org/show_bug.cgi?id=424649


**Revisioni del codice (peer review)**: consistono nel *sottoporre all'attenzione di altri sviluppatori una serie di cambiamenti, i quali ricevono feedback* da altri sviluppatori e:
- *mantenere alta la qualità* del codice.
- *trasferire conoscenza* tra sviluppatori.
- *assicurare il rispetto delle linee guida* del progetto.
Questo processo è facilitato da tool come **Gerrit**.

## Piattaforme di sviluppo condiviso

Esistono per esempio GitHub e GitLab, che forniscono i tool elencati precedentemente, di **issue tracking e code review**, oltre a ospitare **repository centralizzati**.

## Pull/Merge Requests

Una pull request in GitHub (chiamata *merge request* in GitLab) è un tool di code review che, di fatto, **permette a sviluppatori di richiedere dei cambiamenti su BRANCH protetti al/ai MAINTAINER di un repository remoto**.
- Una pull/merge request ha uno specifico branch di *riferimento*, e la richiesta può riguardare diversi commit. 
- A seguito di *commenti*, è possibili aggiungere altri commit al branch di riferimento, che vengono poi inclusi nella richiesta.

**UNA PULL/MERGE REQUEST ALLA FINE PUO' ESSERE ACCETTATA (merged) o RIFIUTATA (closed) dal/dai maintainer.**

Esempio di pull request: https://github.com/Anuken/Mindustry/pull/1022
## Come si fa una pull request?

Nello sviluppo open source, si potrebbe voler fare cambiamenti a un dato progetto: **all'inizio però non si hanno I PERMESSI PER CREARE BRANCH DIRETTAMENTE NEL REPOSITORY DEL PROGETTO.**

Per inviare una pull request:
- effettuare una **fork** del repository (ovvero un *clone remoto duplicato che diventa un nostro nuovo repository, a differenza del git clone classico*)
- si lavora nella fork;
- si crea la **pull request** nel repository ufficiale

## Conflitti

Nella storia di un repository, si ha un conflitto se e solo se:
- esistono 2 branch $a$ e $b$, che condividono la storia fino al commit $c_{s}$
- esistono 2 commit successivi a $c_{s}$, una per il branch $a$ che è $c_{s+1}^{a}$ e uno per il branch $b$ che $c_{s+1}^{b}$
- si prova a fare il merge di $b$ su $a$ o viceversa.

Git è in grado di usare strategie per *risolvere automaticamente i conflitti legati alla storia del repository e creare un commit di merge valido*. In questi casi, al commit saranno associate due revisioni non vuote (a differenza del caso in cui non ci sono conflitti, in cui una delle due revisioni sarà vuota).

Git prova a risolvere automaticamente i conflitti anche nel caso in cui più persone modificano lo stesso file. 
Esistono, però, **casi in cui è richiesto l'intervento manuale dello sviluppatore.**

Un conflitto non può essere risolto automaticamente se **git trova due modifiche diverse alla stessa riga:**

```RUBY
def a
+ return 0
end
```

```RUBY
def a
+ return 1
end
```

**CONFLITTI IRRISOLVIBILI**

Abbiamo 3 strategie:
- **mantenere la versione LOCALE, scartando la modifica fatta al file dal branch remoto**.
- **mantenere la versione REMOTA, scartando la modifica al file fatta sul branch locale**.
- **risoluzione manuale:** lo sviluppatore decide quali modifiche prendere dal branch locale e quali da quello remoto (quasi sempre la strategia più adeguata). 
