Un **modello digitale di elevazione** è la rappresentazione della distribuzione delle quote di un territorio, o di un'altra superficie, in formato digitale. 
Il modello digitale di elevazione viene in genere prodotto in formato raster associando a ciascun **pixel** **l'attributo relativo alla quota assoluta**.

I DEM possono essere impiegati in un GIS per produrre nuovi dati, con particolare riguardo alle indagini per la mitigazione dei rischi naturali.

### **Elementi fondamentali dei dati raster**

- **Celle di griglia (pixel):** Rappresentano le unità base.
- **Risoluzione:** Definisce la dimensione delle celle.
- **Sistema di coordinate, coordinate di origine ed estensione:** Determinano la georeferenziazione.
- **Dimensioni:** Numero di righe e colonne.

### **Tipologie di analisi raster**

1. **Generazione di superfici:**
    
    - **Hillshade:** *Simula l'illuminazione di una superficie utilizzando la posizione ipotetica del sole, determinando i valori di illuminazione per ogni cella in un raster*.
      Per impostazione predefinita, *ombra e luce sono in tonalità di grigio associate a numeri interi da 0 a 255* (da nero a bianco).
        - *Parametri chiave*: **azimut** (*direzione angolare del sole*, predefinito a 315°) e **altitudine** (*angolo della sorgente luminosa sopra l'orizzonte*, predefinito a 45°).
        - Formula di calcolo basata su **funzioni trigonometriche con conversione degli angoli in radianti** per determinare **ANGOLO e DIREZIONE di illuminazione**.

Nei GIS la superficie terrestre è *descritta dall'equazione* $z=f(x,y)$, ovvero l'elevazione è legata tramite una funzione al variare della coppia $(x,y)$.
La *pendenza* risulta essere veramente importante in termini di irraggiamento solare di una zona, *in quanto l’energia solare che incide su quest’ultima dipende dalla sua inclinazione*.
Questa viene quindi calcolata come rapporto tra la **differenza di quota (rise) tra la cella immediatamente vicina e quella corrente e la distanza (run) tra i centri delle due celle.**
La pendenza può essere espressa in gradi o in percentuale.
      ![[Pasted image 20241206123035.png]]
    - **Aspect:** Determina l'orientamento di una pendenza.

Dal punto di vista matematico la funzione $z=f(x,y)$, utilizzata per
modellare la superficie del terreno, è una funzione delle due
variabili x e y, le quali rappresentano anche le direzioni dei due
assi coordinati del sistema di riferimento geografico (o
cartografico). 
Ciò comporta che la pendenza possa assumere valori diversi a seconda della direzione considerata.