Ricorda il preambolo sulle metaeuristiche nel quaderno di ricerca simbolica.

## INTRO

Gli algoritmi genetici **simulano il processo di evoluzione naturale, combinando e mutando soluzioni per trovare quella migliore col fine di migliorare la ricerca locale.** Sono largamente usati nei business e nei circoli scientifici, dato che garantiscono tecniche efficienti e efficaci per ottimizzare e per il machine learning. 

## COMPONENTI PRINCIPALI di un GA

- **Codifica** (*gene*, *cromosoma*): rappresentazione delle soluzioni, come stringhe di bit o numeri reali.
- **Inizializzazione:** creazione della popolazione iniziale.
- **Funzione di valutazione:** misura la qualità di ogni soluzione.
- **Selezione:** scelta dei genitori per la riproduzione in base alla loro adattabilità.
- **Operatori genetici:** introduciamo variabilità e combinazione di schemi con *mutazione e crossover (ricombinazione)*.
- **Parametri di impostazione:** per esempio la dimensione di popolazione e il tasso di mutazione, o le politiche di eliminazione e selezione dei parent.

## PROCESSO di un ALGO. GENETICO
``` PSEUDO
{

initialize population; //inizializzazione della  popolazione

evaluate population;   //valutazione della popolazione

while TerminationCriteriaNotSatisfied 
//finché i criteri di terminazione sono soddisfatti
{

select parents for reproduction; //selezione dei genitori, fatta casualmente e con criteri di selezione basati sulla valutazione di cromosomi

perform recombination and mutation; //riproduzione

evaluate population; //valutazione della nuova popolazione

}

}
```

## APPLICAZIONI e BENEFICI

- **Questi algoritmi sono modulari, paralleli e adatti a spazi di ricerca complessi: offrono inoltre una soluzione sempre migliorabile nel tempo.**
- Sono **usabili quando altre soluzioni sono troppo lente**, **o il problema è simile a uno già risolto con un algoritmo genetico**, **o si desidera un approccio esplorativo per avere nuove soluzioni**.