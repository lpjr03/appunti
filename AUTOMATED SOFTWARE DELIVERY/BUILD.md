## Linguaggi compilati

Questi richiedono l'esecuzione di almeno un programma per produrre uno o più file che possano essere eseguiti dall'utente.

In C e C++, le fasi sono le seguenti:
- **preprocessing**: da codice sorgente otteniamo altro codice sorgente;
- **compilazione:** da codice sorgente otteniamo dell'Assembly;
- **assemblaggio:** da Assembly a codice binario (questi ultimi 2 sono step immediatamente successivi, quasi uniti tra loro);
- **linking:** il compilatore prende tutti i file compilati e li unisce tutti insieme

Il tutto è generalmente eseguito da un solo programma (es. **gcc**).

Java è un linguaggio *ibrido*: c'è una compilazione in bytecode, e poi interpretato dalla JVM in linguaggio macchina.

## Build 

Compilare però non è sufficiente, perché i programmi possono richiedere:
- **esecuzione preliminari di altri programmi**;
- **download di dipendenze**;
- configurazione specifica per la macchina;
- **controlli di qualità**
Questo è riassumibile come **processo di build** che produce eseguibili o libreria.


***IL NOSTRO OBIETTIVO E' AUTOMATIZZARE QUANTO PIU' POSSIBILE QUESTO, GRAZIE A SPECIFICI TOOL, per evitare che tale processo si allunghi troppo se fatto manualmente (per esempio dimenticando 1 solo di questi steps). CIO' VALE ANCHE QUINDI PER I LINGUAGGI INTERPRETATI.***

I file usati per il processo di build:
- **devono essere indipendenti dall'ambiente di sviluppo;
- **devono essere inclusi nei repository dei VCS**.

## Make

E' un tool di build system usato per C e C++ di solito, **ma è generico**.
Funziona così: prende in input un file **Makefile** e lo usa per eseguire i comandi in esso specificati.
Il Makefile specifica determinati **target (di solito un nome di file da creare, tranne per "clean" qui sotto), e per ciascuno di essi, dei prerequisiti e una serie di azioni (comandi) da eseguire**.

Esempio di un Makefile:
``` makefile
CC = gcc
WINCC = i686-w64-mingw32-gcc
CFLAGS = -Wall -g

clean:
rm main.o main.exe

main.o: main.c
${CC} ${CFLAGS} -o main.o main.c

main.exe: main.c
${WINCC} ${CFLAGS} -o main.exe main.c

all: clean main.o main.exe
```
- **sopra troviamo delle costanti che vengono inserite nei comandi**;
- **"clean", "main.o" e "main.exe"** sono i ***TARGET***, e affianco a questi troviamo i prerequisiti (es. uno o più file necessari nella working directory per quel target, per clean no). Se cambia un prerequisito, devi *ricompilare il target* se questo è un file.
- **i comandi si trovano SOTTO i target.**

- *Per eseguire l'intero processo di build basta usare il comando* $make$ nella cartella che contiene il Makefile.
- Il comando $make\space clean$ elimina il file eseguibile e tutti i file oggetto nella cartella.

Guarda qui questo esempio di come vengono usate bene costanti "multiple":
```makefile
objects = main.o kbd.o command.o display.o \
          insert.o search.o files.o utils.o

edit : $(objects)
        cc -o edit $(objects)
main.o : main.c defs.h
        cc -c main.c
kbd.o : kbd.c defs.h command.h
        cc -c kbd.c
command.o : command.c defs.h command.h
        cc -c command.c
display.o : display.c defs.h buffer.h
        cc -c display.c
insert.o : insert.c defs.h buffer.h
        cc -c insert.c
search.o : search.c defs.h buffer.h
        cc -c search.c
files.o : files.c defs.h buffer.h command.h
        cc -c files.c
utils.o : utils.c defs.h
        cc -c utils.c
clean :
        rm edit $(objects)
```


## Build in Java

Abbiamo 3 tool disponibili (ordinati cronologicamente rispetto alla data di uscita):
- **ANT**
- **MAVEN**
- **GRADLE**

## Ant

Usa la stessa filosofia di Make, definendo il processo di build con un file chiamato **build.xml**
Ecco un esempio:

```XML
<project name="Hello" default="compile">
<target name="clean" description="remove intermediate files">
<delete dir="classes"/>
</target>
<target name="compile" description="compile the Java source code to class files">
<mkdir dir="classes"/>
<javac srcdir="." destdir="classes"/>
</target>
<target name="jar" depends="compile" description="create a Jar file for the application">
<jar destfile="hello.jar"> //nome del jar finale
<fileset dir="classes" includes="**/*.class"/> //genera il jar a partire dalla cartella "classes" e ricorsivamente scegliendo tutti i file .class
<manifest> <attribute name="Main-Class" value="HelloProgram"/> </manifest> //Main-Class sarà la classe eseguibile dal Jar
</jar>
</target>
</project>
```

Abbiamo anche qui dei **target**, e in ciascuno di essi abbiamo dei tag XML che possono essere dei veri e propri **comandi**, come "delete" di "dir="classes"", che difatti elimina la cartella "classes" dal target "clean", o come javac ecc... 

**LIMITI DI ANT** :
- E' necessario avere **tutte le dipendenze localmente**;
- La versione delle dipendenze è **implicita** (nel nome del file contenente la dipendenza);
- **Le dipendenze transitive vanno risolte MANUALMENTE** (se ho una dipendenza installata X che ha come dipendenza a sua volta Y, devo installare manualmente anche Y e così via per Y....)

## Maven

Nasce per **superare proprio le limitazioni di Ant**.
Questo perché Maven permette di:
- **gestire le dipendenze attraverso un repository centralizzato**;
- **rendere il codice modulare (attraverso i moduli Maven)**
- **gestire automaticamente le dipendenze indirette** (ma includere una dipendenza LOCALE (es. un JAR nel tuo pc) è più difficile);
- **usare plugin per qualsiasi scopo (es. tool di analisi statica)**.

Maven può essere usato anche per generare:
- **documentazione**;
- **statistiche (es. test, metriche di qualità e benchmark)**.

***Come si esegue la build?***
Con uno o più file "POM.xml".

Esempio:
```XML
<project xmlns = "http://maven.apache.org/POM/4.0.0" xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation = "http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
<modelVersion>4.0.0</modelVersion>
<groupId>it.unimol</groupId>
<artifactId>myexample</artifactId>
<version>1.0</version>
</project>
```

Qui è stato creato un progetto Maven, dove all'inizio c'è la versione di Maven (la 4 è la più comune), e il nome del progetto Maven, che è composto da:
- $groupId$: **namespace della compagnia (es. it.unimol)**;
- $artifactId$: **nome dell'artefatto (es. nome del programma o della libreria)**;
- $version$: **versione dell'artefatto**;
- $dependencies$: **insieme di packages da cui il progetto dipende**;

Esempio di dipendenza:
```XML
<dependencies>
<dependency>
<groupId>junit</groupId>
<artifactId>junit</artifactId>
<version>3.8.1</version>
</dependency>
</dependencies>
```
Quando si include una dipendenza Y, *tutte le dipendenze di Y (indirette) vengono incluse automaticamente*.

Abbiamo dipendenze:
- **concreta**: si vuole includere ad es. un JAR nel classpath;
- **POM**: es. una semplice lista di dipendenze indirette.

**Scope delle dipendenze:**
- *compile*: richiesta per la compilazione e l'esecuzione di un programma;
- *provided:* dipendenza richiesta durante la compilazione (fornita da un container o qualcos'altro di esterno durante l'esecuzione), ma non a runtime;
- *runtime*: richiesta solo in fase di esecuzione del programma (in Java ciò accade con le API Reflection);
- *test*: richiesta solo in fase di test (non inclusa nel runtime);
- *system*: come $provided$, ma qui ha un path specifico nel sistema;
- *include*: la dipendenza va sostituita con le dipendenze indirette.

## Problema con dipendenze concorrenti

Può capitare che una dipendenza A richiede una dipendenza indiretta X alla versione 1.0, mentre una dipendenza B può richiedere X alla versione 1.2: in questo caso, si dovrebbe specificare quale versione di X si vuole usare **definendo un blocco "dependencyManagement", in cui si specificano le versioni delle dipendenze indirette da usare**, altrimenti verrebbe scelta una versione in maniera non deterministica.

## Build in Maven

A ogni fase possono essere associati *uno o più goal:* i goal sono definiti all'interno di **plugin**, che registrano i propri goal sulle fasi del ciclo di vita.
Ad esempio, il plugin *compiler* (già incluso di default) associa il goal *compile* alla fase *compile*.

## Ciclo di vita di default di Maven

Prevede le seguenti fasi:
- **validate**: valida i sorgenti;
- **compile**: compila il codice sorgente;
- **test-compile**: compila i test;
- **test**: esegue i test (step obbligatorio);
- **package**: crea pacchetti esportabili (es. JAR);
- **install**: installa i pacchetti nel repository Maven locale;
- **deploy**: carica i pacchetti nel repo Maven centrale

``` BASH
mvn clean #Esegue il ciclo di vita "clean"
mvn deploy #Esegue TUTTE le fasi del ciclo di vita di default
mvn install #Esegue le fasi del ciclo di vita di default fino a "install" (inclusa)
mvn clean install #Esegue prima il ciclo di vita "clean" e poi quello di default fino a "install"
```

- **CLEAN è un altro lifecycle, e pulisce tutto ciò fatto dal lifecycle precedente (es. pulisce tutti i file binari creati precedentemente)**.

Il repository centrale più usato è Maven Central (https://mvnrepository.com/), che include sia **dipendenze sia plugin**.

- Per eseguire un goal specifico di un plugin, si usa il comando *mvn {plugin}:{goal}* (es. mvn compiler:compile).


## Gradle 

E' un build tool alternativo a Maven molto usato, di default per le app Android: combina i vantaggi di Maven (dipendenze remote) e Ant (dipendenze locali).