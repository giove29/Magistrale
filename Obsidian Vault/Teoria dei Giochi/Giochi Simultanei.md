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

### Strategia Dominata
Per Strategia Dominata si intende la strategia peggiore (tra tutte le strategie a sua disposizione) che un giocatore può effettuare e che ottiene sempre payoff peggiore, indipendentemente cosa l'altro giocatore scelga.
Definizione: 
Il giocatore $i$ scopre che la strategia $s'_i$ è strettamente dominata dalla strategia $s_i$ se e solo se, per ogni scelta della strategia ottengo un payoff sempre peggiore.
### Strategia Dominante
Per Strategia Dominante si intende una strategia che ottiene payoff maggiore di tutte le altre indipendentemente da cosa fa l'altro giocatore.

> Quando un giocatore utilizza una strategia dominante, tutti gli altri giocatori utilizzeranno una strategia che è dominata.
> Ma chi è dominato è in grado di prevedere che l'avversario utilizza la strategia dominante. Questo permette di calcolare l'Equilibrio di Nash anticipatamente.

Esempio:
![[Pasted image 20250314162901.png]]
Il Congresso ha una strategia dominante: Budget Deficit perché porta migliori risultati della Budget Balance indipendente dalle scelte della Federal Reserve.
La Federal Reserve non ha una strategia dominante, però può capire che il Congresso ne ha una e anticipare la propria scelta.
Nash Equilibrium (2,2)
(3,4) sarebbe un buon punto per i payoff ma instabile perché il congresso avrebbe anche una scelta migliore.