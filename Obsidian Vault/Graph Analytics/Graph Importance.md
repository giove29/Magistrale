# Basic Concepts:
- Random Walk
- Transition Probability
- Teleport
- Markov Model
- Algebraic Representaion

# Applications:
- Co-Citation
- HITS
- Page Rank
- Personalized Page Rank

---

# Random Walk
Attraversamento del grafo selezionando vicini a random. E' possibile visitare alcuni nodi/archi molteplici volte. Teniamo conto della frequenza con la quale abbiamo attraversato ciascun nodo.
- Prendi un nodo.
- Seleziona un vicino a random, e fai uno **step**.
- Continua a fare steps fin quando non sei "stanco".
- Prendere nota del nodo in cui siamo finiti e di quanto frequentemente abbiamo visitato ciascun nodo.

# Transition Probability
Si tratta della probabilità, dato un nodo $i$, con la quale attraversando l'arco $j$ arriviamo al nodo vicino $j$.
- Nel caso in cui tutti gli archi sono trattati in maniera equivalente: la probabilità dipende dal numero di archi uscenti dal nodo, e gli archi di un nodo hanno probabilità uniformi.
- Nel caso invece di archi pesati: non abbiamo probabilità uniformi tra gli archi.

> Ricordando che la somma delle probabilità degli archi di un nodo deve essere = 1.

# Transition Probability in a Path
Dato un nodo, ipotizzando di effettuare una sere di K passi random, qual è la probabilità di trovarsi in uno specifico nodo del grafo?
![[Pasted image 20250305152044.png]]
> Calcoliamo le probabilità

# Teleport Probability in a Random Walk