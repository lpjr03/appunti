## Intro

E' un algoritmo fondamentale per i giochi da tavolo computerizzati, e delle sue ottimizzazioni.
E' usato in giochi dove i giocatori prendono turni e hanno "informazione perfetta" (scacchi, dama, tattiche), ma potrebbe funzionare in giochi senza questa peculiarità (come il Poker o Monopoly), i quali sono giochi con casualità.

## Funzionamento

Si basa su un albero decisionale, dove:

- **I nodi rappresentano stati del gioco.**
- **I rami sono le mosse possibili.**
- **I livelli sono chiamati "plies", con alternanza tra i giocatori (_Min_ e _Max_) in base ai turni.**
- è un albero **n-ario**, perché il numero di figli di un nodo dipende dalla situazione di gioco.

![[Pasted image 20241205173245.png]]

Immaginiamo un gioco come il **tris (tic-tac-toe)**. Supponiamo che tu sia il giocatore **Max** (vuoi massimizzare il punteggio) e il tuo avversario sia **Min** (vuole minimizzare il tuo punteggio). Ogni mossa porta a una situazione di gioco diversa, e dobbiamo scegliere la migliore mossa per **Max**, assumendo che **Min** giochi sempre al meglio.

## **MinMax e Scacchi**

- **Sfida**: L'albero decisionale degli scacchi cresce **esponenzialmente**, rendendo impossibile esplorare tutte le possibilità.
- **Soluzione**: Usare una funzione di valutazione (_Evaluate()_) per stimare il valore di una posizione senza raggiungere la fine del gioco.

La forza dell'algoritmo sta quindi nel quanto in profondità esso possa cercare, e quanto bene possa "valutare" una posizione nella scacchiera a priori (come gli umani in un certo senso, un grand master può valutare la scacchiera meglio e può prevedere mosse ben prima).

- **Limiti del MinMax**:
    - *Complessità per giochi con molte possibilità*.
    - *Richiede una funzione di valutazione efficace*.
## AlphaBeta Pruning

Qui MinMax esplora tutto l'albero, anche quando alcune sezioni sono irrilevanti.
In generale, ci si ferma (nel valutare una mossa) quando se ne trova una peggiore di quella precedente, cioè se quella mossa non beneficia il giocatore allora non verrà proprio esplorata.

Esempio:


![[Pasted image 20241205185719.png]]



2 punteggi vengono passati durante la ricerca:
    - **Alpha**: Il miglior punteggio che Max può garantire. Tutti i valori inferiori possono essere ignorati.
    - **Beta**: Il peggior punteggio che Min può garantire. Tutti i valori superiori sono ignorabili.
    - Si smette di esplorare quando **Beta < Alpha**.
- **Esempio**: Se un ramo offre un valore chiaramente inferiore a uno già trovato, non si esplorano ulteriori rami di quel sottogruppo.
- **Benefici**: Riduce drasticamente il numero di nodi da valutare, *raddoppiando la profondità esplorabile nei giochi complessi* come gli scacchi



