### Concetti Generali di Pianificazione

La **pianificazione** consiste nel trovare una sequenza di azioni che permetta a un agente di raggiungere uno stato finale o obiettivo partendo da uno stato iniziale.
Viene fornito:

1. Un **insieme di descrizioni degli operatori** (azioni primitive possibili),
2. Una descrizione dello **stato iniziale**,
3. Una descrizione dello **stato obiettivo** (o predicato).

L'obiettivo è calcolare un **piano**: **una sequenza di azioni che, eseguite dallo stato iniziale, portano al raggiungimento dello stato obiettivo.**

### Differenza tra Pianificazione e Risoluzione di Problemi

La pianificazione è generalmente più potente della risoluzione di problemi poiché:

- **Utilizza rappresentazioni più ricche**, ad esempio scomponendo stati, obiettivi e azioni in insiemi di frasi logiche.
- **Esplora lo spazio dei piani piuttosto che lo spazio degli stati**, permettendo di pianificare sub-obiettivi indipendentemente per ridurre la complessità.

### Assunzioni Tipiche nella Pianificazione

1. **Tempo atomico**: ogni azione è indivisibile.
2. **Azioni deterministiche**: ogni azione ha un effetto certo.
3. **Agente unico**: solo l'agente causa i cambiamenti.
4. **Onniscienza dell'agente**: l'agente conosce completamente lo stato del mondo.
5. **Assunzione del mondo chiuso**: ogni fatto vero è specificato nella descrizione dello stato; ciò che non è specificato è falso.

### Esempio: Il Mondo dei Blocchi

Il "mondo dei blocchi" è un **ambiente di micro-mondo usato per simulazioni di pianificazione**:

- Ci sono blocchi che possono essere posizionati su altri blocchi o sul tavolo.
- Un robot può afferrare un solo blocco alla volta.

Stati come "ontable(A)" e "clear(B)" descrivono la posizione e lo stato di ogni blocco.

### Algoritmi di Pianificazione

- **GPS (General Problem Solver)**: uno dei primi pianificatori che utilizzava l'analisi dei mezzi e fini per ridurre la differenza tra lo stato attuale e l'obiettivo.
- **Calcolo delle Situazioni**: rappresenta il problema di pianificazione con la logica del primo ordine e usa teoremi per dedurre una sequenza di azioni che portano allo stato desiderato.
- **STRIPS (Stanford Research Institute Problem Solver)**: utilizza rappresentazioni compatte di stati e obiettivi. Ogni **azione** (operatore) ha:
	1) una descrizione
	2) ***precondizioni***: un insieme di assegnamenti di valori a variabili che devono essere vere per l'avverarsi dell'azione.
	3) **effetti**: un insieme di assegnamenti risultanti a quelle variabili che cambiano come risultato dell'azione.  
	STRIPS mantiene uno stack di obiettivi, risolvendo uno alla volta fino a raggiungere lo stato desiderato.

### Componenti degli Operatori/azioni

Un operatore di azione contiene:

1. **Descrizione dell'azione**: cosa fa l'azione.
2. **Precondizioni**: condizioni che devono essere vere prima dell'applicazione dell'azione.
3. **Effetti**: cambiamenti nello stato causati dall'azione.

Esempio per l'azione "Go(there)":

- **Precondizioni**: $at(here)\space \wedge \space Path(here,there)$
- **Effetti**: $At(there)\space \wedge \neg At(here)$

### Esempio di Algoritmi di Manipolazione dello Stack in STRIPS

**STRIPS utilizza uno stack per gestire gli obiettivi, risolvendo sub-obiettivi con regole specifiche**:

1. Ogni obiettivo **non soddisfatto** *viene messo in cima allo stack*.
2. Se un *obiettivo è composto da più sub-obiettivi*, **questi vengono messi in cima in ordine**.
3. **Si risolvono le precondizioni per le azioni, aggiungendo e rimuovendo effetti nello stato corrente per avvicinarsi all'obiettivo finale**.

### ESEMPIO di STRIPS PLANNING
![[Pasted image 20241112213504.png]]
![[Pasted image 20241112213517.png]]

### Limitazioni di STRIPS e Conclusioni

Nell'anomalia di Sussman, il sistema STRIPS trova difficoltà a pianificare correttamente senza generare passaggi inefficaci o ridondanti. 
**STRIPS ha limitazioni, in particolare nel gestire obiettivi che si annullano a vicenda, e può generare piani inefficienti. 
In alcuni casi complessi, non riesce a differire la soluzione di un obiettivo abbastanza a lungo da evitare conflitti.**
