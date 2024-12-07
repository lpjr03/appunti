## Intro

Quando costruiamo un build file, *uno degli obiettivi è controllare anche la qualità del codice*.

Abbiamo quindi 2 tipi di qualità:
- **interna**: percepita dagli sviluppatori. Se questa è bassa, il tasso di evoluzione del software è *basso*;
- **esterna**: percepita dagli utenti finali. Se questa è bassa, il software può non *rispettare i requisiti richiesti*.

Per quella esterna, scrivere i casi di test è **FONDAMENTALE**, e quindi in fase di build dobbiamo far sì che la qualità esterna sia rispettata a pieno (se un test case fallisce nella build, deve INTERROMPERSI).
Per quella interna (ma anche esterna) sono usati *tool di analisi statica*, e son chiamati così perché funzionano senza che il codice analizzato venga "lanciato".

## Criteri di adeguatezza

E' un predicato (vero o falso) dato dalla coppia:
$<p,S>$ dove:
- $p$ è un *programma*;
- $S$ è una *test suite*.

Esistono 2 tipi di adeguatezza:
- **black box**, dove si controlla la copertura di **requisiti e modelli**, e non il codice ("black box" perché non sappiamo l'implementazione), per la stesura dei test cases.
- **white box**, dove al contrario si controlla la copertura del codice.

Di solito si mischiano, non necessariamente una è più importante dell'altra, anche se col black box abbiamo test cases più "significativi" e sono più facili da scrivere.
## Criteri di adeguatezza white-box

Abbiamo:
- **Statement Coverage**: creiamo test case per coprire OGNI RIGA di un metodo.
Es.
```Java
int div(int a, int b){
if(!b)
	Exception
return a/b;
}
SC->div(7,5)=2/3 of the lines covered=67%
```

- **Branch Coverage**: un branch è un RAMO di un CONTROL FLOW GRAPH d'esecuzione di un algoritmo. *Alcuni branch sono irraggiungibili* (es. un ramo false di un if che ha solo istruzioni nel ramo vero dopo).
```Java
  int div(int a, int b){
if(!b)
	Exception
return a/b;
}
BC->1/3 of the branches covered
```
- **Path Coverage**: riguarda *tutti gli interi percorsi da input a output del metodo* (o del programma) stesso: **se abbiamo un ciclo nel codice è IMPOSSIBILE coprire tutte le path d'esecuzione**.
- **Condition Coverage**: ci concentriamo sulle parti delle condizioni degli if, while che stiamo valutando nel codice.

**Un criterio di adeguatezza può essere espresso come: una classe C deve avere almeno il 90% di branch coverage S per ogni classe, per esempio**.
In Maven, c'è un plugin chiamato *JaCoCo* per esprimere criteri di adeguatezza direttamente nei file di build: qui, ad esempio:

```XML
<configuration>
	<rules>
		<rule>
			<element>CLASS</element>
			<limits>
				<limit>
					<counter>BRANCH</counter>
					<value>COVEREDRATIO</value>
					<minimum>0.90</minimum>
				</limit>
			</limits>
				<excludes> <exclude>it.unimol.myprogram.StrangeClassToExclude</exclude>
				</excludes>
</rule>
</rules>
</configuration>
```

Qui con l'apposito tag abbiamo escluso una classe che aveva una soglia bassa (per qualche ragione non possiamo coprire tutti i suoi branch), ma a noi va bene così quindi non la consideriamo.

https://www.baeldung.com/jacoco


## Lint

E' uno dei tool di *analisi statica* più antichi (1978).
Quelli più nuovi sono chiamati *linter*.
Questi **usano regole per fare controlli veloci sul codice, e sono in grado di individuare una serie di errori predeterminati da chi ha sviluppato le regole.**

Esempi di controlli:
- *utilizzo di funzioni/metodi deprecati*
- *break mancante in un branch switch*
- *utilizzo di funzioni pericolose di un linguaggio* (es: eval in PHP)

Esistono *linter che permettono di fare controlli specifici per la sicurezza* (individuazione di **vulnerabilità**). 
Ad esempio, sono in grado di dare warning su:
```C
char buffer[5];
strcpy(buffer, "Hello World");
```
