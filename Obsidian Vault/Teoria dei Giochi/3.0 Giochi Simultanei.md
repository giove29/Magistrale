Si tratta di giochi do le mosse di ciascun giocatore avviene in maniera simultanea, senza che nessuno sia a conoscenza della mossa dell'altro. Presentano quindi informazioni imperfetta.
Nei giochi simultanei, ciascun giocatore ha esattamente una sola opportunità per fare la sua mossa.
Le strategie possono essere probabilistiche.
**Strategie pure**: strategie non probabilistiche.
**Strategie mixed**: strategie probabilistiche.

### Nash Equilibrium
Si tratta di una lista di strategie per ciascun giocatore, tale per cui nessuno dei due può ottenere un migliore payoff cambiando la propria strategia, mentre l'altro la mantiene.
> Nash non assicura il payoff assoluto migliore per entrambi perché i due giocatori sono indipendenti e razionali.

**Metodo veloce** per trovarlo ad occhio: la cella ($x$, $y$)con Nash Equilibrium è quella che ha $x$ > di tutti gli elementi della colonna, e $y$ > di tutti gli elementi della riga.

![[Pasted image 20250314152806.png]]
In questo caso nessuno cambierebbe la scelta (caso con Nash Equilibrium):
- Row mantiene Low perché se Column mantiene la sua strategia su Middle, ha già il suo massimo payoff.
- Column mantiene Middle perché se Row mantiene la sua strategia su Low, ha già il suo massimo payoff.
![[Pasted image 20250314153046.png]]
In questo caso non si ha equilibro perché se Column mantiene Left, allora Row sceglie Bottom per un migliore payoff.

## Interpretazione dell'equilibrio di Nash
#### 1. Dare suggerimenti
Essendo l'equilibrio di Nash il miglior consiglio, se tutti i giocatori seguono la strategia data dall'equilibrio avrebbero il miglior compromesso.
#### 2. Fare previsioni
L'equilibrio di Nash, essendo un punto stabile in cui i giocatori otterrebbero i migliori risultati, sarà il punto in cui cadranno le scelte dei giocatori. 
Nash è quindi utilizzato per predire cosa succederà. 
## Inefficienza di Equilibrio
![[Pasted image 20250317171400.png]]
> L'equilibrio di Nash è C, C.

In questo caso l'equilibrio non è la scelta migliore in assoluto per entrambi i giocatori.
Utilizzando la funzione di Welfare (somma payoffs)
- W(C, C) = -10
- W(S, S) = -2
**Price of Anarchy**: è il rapporto massimo tra i valori di equilibrio e il valore della soluzione ottimale.
- W(C, C)/W(S, S) = 5 -> misura l'inefficienza dell'equilibrio.

---
### Strategia Dominata
Per Strategia Dominata si intende la strategia peggiore (tra tutte le strategie a sua disposizione) che un giocatore può effettuare e che ottiene sempre payoff peggiore, indipendentemente cosa l'altro giocatore scelga.
Definizione: 
Il giocatore $i$ scopre che la strategia $s'_i$ è strettamente dominata dalla strategia $s_i$ se e solo se, per ogni scelta della strategia ottengo un payoff sempre peggiore.

**Strategia debolmente dominata**: si tratta di una strategia peggiore o uguale alle altre.
### Strategia Dominante
Per Strategia Dominante si intende una strategia che ottiene payoff maggiore di tutte le altre indipendentemente da cosa fa l'altro giocatore.

**Strategia debolmente dominante**: si tratta di una strategia che non è mai peggiore alle altre, o migliore o uguale.

> Quando un giocatore utilizza una strategia dominante, tutti gli altri giocatori utilizzeranno una strategia che è dominata.
> Ma chi è dominato è in grado di prevedere che l'avversario utilizza la strategia dominante. Questo permette di calcolare l'Equilibrio di Nash anticipatamente.

Esempio:
![[Pasted image 20250314162901.png]]
Il Congresso ha una strategia dominante: Budget Deficit perché porta migliori risultati della Budget Balance indipendente dalle scelte della Federal Reserve.
La Federal Reserve non ha una strategia dominante, però può capire che il Congresso ne ha una e anticipare la propria scelta.
Nash Equilibrium (2,2)
(3,4) sarebbe un buon punto per i payoff ma instabile perché il congresso avrebbe anche una scelta migliore.

---
## Eliminazione di Strategie Dominate
Si tratta di un algoritmo per ottenere in maniera semplice l'equilibrio di Nash.
**NON** funziona con le strategie debolmente dominate!!!!

Dato un gioco *G* con un set di strategie *S*:
- Trova una strategia dominata *s*.
- Rimuovere la strategia *s* dal set *S*. 
- Ripetere fin quando non ci sono più strategie dominate.
> Se l'algoritmo termina con un solo risultato, allora il gioco è "dominance solvable", e le ultime strategie rimaste costituiscono l'equilibrio di Nash.

Ad ogni passo un giocatore elimina la propria strategia peggiore (o di più se presenti). Nel passo successivo l'avversario sapendo che strategia l'altro ha tolto sceglie anche lui la sua strategia peggiore, "diminuendo" ulteriormente il gioco.
![[Pasted image 20250317172339.png|300]]
![[Pasted image 20250317172414.png|300]]
![[Pasted image 20250317172510.png|300]]
![[Pasted image 20250317172536.png|300]]
**Low, Middle** equivale al punto di Equilibrio del gioco.

---
## P-Beauty e Nash Equilibrium
Simile a quello di scegliere un numero e chi va più vicino alla metà della media vince.
L'equilibrio si ottiene con valore di 0, perché tutti i giocatori "vincono". Nessun giocatore avrebbe vantaggio a cambiare numero != 0.
