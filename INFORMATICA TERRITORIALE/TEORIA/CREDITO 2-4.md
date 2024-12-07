Nel modello vettoriale tutti gli elementi territoriali sono rappresentati da primitive geografiche: sono entità quali sono PUNTI, LINEE, AREE, RETI E SUPERFICI.
In un GIS, gli oggetti spaziali (entità) sono rappresentabili come 2 modelli:

1) **DATI VETTORIALI:** sono memorizzati come una serie di coordinate, dove i *punti* sono una coppia $(X,Y)$ e le *linee* collegano più punti.
Le *aree* sono rappresentate da spazi delimitati da linee, le *reti* sono date da linee connesse tra di loro e le *superfici* sono rappresentate da aree che collegano punti e linee 

- *topologia:* relazione geografica tra punti e linee usate per rappresentare un'entità:
- *informazione topologiche:* ci servono per eseguire analisi spaziali e correggere errori di digitalizzazione 

**FORMATI DEI DATI VETTORIALI**

Ci sono svariati formati che si usano per rappresentare questo tipo di dati, ma quelli che usiamo su QGIS per la maggiore sono gli Shapefile, divisi in 3 tipi di file:
- .**shp** la geometria del’elemento stesso.
- .**shx** è l’indice della geometria della feature.
- .**dbf** tabella degli attributi con le caratteristiche.

2) **DATI RASTER**
Nei dati raster utilizziamo delle tassellature, dove **ogni cella o pixel rappresenta un punto** ; un gruppo di celle rappresenta un'**entità**. Di base si usa la codifica 0 o 1, ma può comportare problemi perché non sappiamo se stiamo parlando di linee aree o punti.
La locazione spaziale è definita dal numero di riga e colonna delle celle.

![[Pasted image 20241113121840.png]]
- In alcuni casi lo spazio raster può esser fatto con diversi tipi di tassellazione, come triangoli e esagoni.
- Esistono anche immagini raster derivate da scansione.
- La profondità di un raster indica il numero di bit a disposizione per rappresentare un pixel, quindi 2(profondità) indica il numero di informazioni rappresentabili.

- I formati raster più diffusi sono Esri GRID, GeoTIFF, IMG, JPEG, netCDF.

A volte possono esserci delle aree omogenee in un dataset raster che non si vogliono far vedere (bordi, sfondi, altri dati) che non si considerano utili come valori. Questi dati sono chiamati **NoData values**.

![[Pasted image 20241113122532.png]]

**CONFRONTO TRA DATI VETTORIALI e RASTER**

Uno dei principali vantaggi del tipo vettoriale è la precisione con cui vengono riprodotte le entità. Lo svantaggio principale è che i dati vettoriali hanno scarse prestazioni quando si tratta di una rappresentazione continua del fenomeno (ad esempio, la densità di popolazione). Il formato raster è l'output naturale dei dati satellitari. L'analisi dei dati raster è solitamente rapida e facile da eseguire. Al contrario, la precisione dei dati raster è inferiore a quella dei dati vettoriali perché si basano su celle (regola della presenza/assenza e regola del 50%).


Il **GEOPROCESSING** è la trasformazione ed elaborazione degli elementi geografici come una sovrapposizione topologica, ovvero una sovrapposizione di 2 temi per creare un nuovo strato:

- Esclusione;
- Sottrazione;
- Unione;
- Intersezione;
- Clip;
- Dissolve;
- Buffer

![[Pasted image 20241113123446.png]]