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
Durante un random walk, modelliamo la probabilità di interrompere il walk con un parametro α.
Teleport Probability -> la probabilità di interrompere il random walk e "saltare" in un altro nodo a random.
> Transition probability + Teleport probability = 1

*Data una Teleport probability: 0.1*
La somma delle probabilità degli archi non è 1.0 perché bisogna sommare anche la Teleport.
![[Pasted image 20250308104458.png]]


> [!NOTE] Random Surfer
> La random walk può essere utilizzata per rappresentare la navigazione di un utente sul Web.
> Il Random Surfer inizia la navigazione da una pagina e segue link a random, dopo un certo numero di step decide di iniziare a navigare da un'altra pagina a random, effettuando quindi una *Teleport*.

# Markov Model
- Ciascun nodo è nodo di partenza con equa probabilità.
- Ciascun nodo è connesso con i suoi vicini.
- Settiamo una Teleport probability per terminare in un qualunque dei nodi.
- Gli archi hanno Transition probability uniforme.
- Sommiamo la Transition probability di ciascun nodo la Teleport probability.

**Grafo di partenza**:
![[Pasted image 20250308124410.png]]
**Markov Model** (teleport = 0.1):
![[Pasted image 20250308124452.png]]
Descrizione dell'immagine a partire da sinistra:
- Ciascun nodo preso come nodo di partenza a random ha probabilità 0.25.
- Ciascun arco uscente ha ***Transition probability =  (1-Teleport probability)/n. edges***.
- La probabilità di capitare da un arco di un nodo iniziale ad un nodo finale è calcolato con il prodotto ***0.25 x Transition probability***
- La probabilità di terminare su un nodo (nodi chiari) è la somma delle probabilità di capitare su un nodo dato un certo arco(punto precedente) + la Teleport probability/4 (probabilità di capitare su uno dei 4 nodi possibili con teleport).

Iterando il Markov Model n volte troveremo una distribuzione stazionaria delle probabilità.
![[Pasted image 20250308125624.png]]
## Adjency Matrix / Transition Probability Matrix
> Si tratta del metodo computazionale per calcolare il Markov Model.

![[Pasted image 20250308130326.png]]
Data la matrice di adiacenza di un grafo, se normalizzata per le righe otteniamo la matrice delle Transition probability (ovvero fare in modo che le somme dei valori di ciascuna riga sia = 1).
![[Pasted image 20250308130704.png]]
La trasposta della matrice delle Transition probability moltiplicata con il vettore delle probabilità iniziali di ciascun nodo, restituisce il vettore contenente le probabilità di terminare su un nodo.

**Aggiungendo la Teleport transition**:
![[Pasted image 20250308131224.png]]
Tenendo conto anche della Teleport la formula cambia come vista sopra.
Da tenere a mente: durante le iterazioni, il vettore *V0* nella seconda parte della formula *α x V0* rimane sempre quello.
Nelle **iterazioni** del Markov Model il vettore calcolato al passo successivo viene inserito nella formula e moltiplicato con la matrice trasposta, seguendo la formula:
![[Pasted image 20250308131640.png|500]]

---
# Co-Citation and Bibliographic
Una rete Citation è un grafo diretto che rappresenta pubblicazioni scientifiche come nodi, in un cui un arco che va da $A$ a $B$ rappresenta che il nodo $A$ contiene una reference (citazione) del nodo $B$.
> Quando un articolo cita un altro articolo, viene stabilita una connessione tra le due entità.

![[Pasted image 20250308132316.png|450]]

Se articoli $i$ e $j$ sono entrambi citati da $k$, allora possono essere tra di loro correlati in un certo senso. -> Più articoli citano $i$ e $j$, più è forte la loro relazione.
### Co-Citation Matrix
![[Pasted image 20250308133113.png]]
- $L$ rappresenta esattamente la matrice di adiacenza del grafo.
- $L^T$ rappresenta la trasposta.
- $C$ rappresenta la matrice di Co-citazione.
- $Cii$ rappresenta il numero di articoli che citano l'articolo $i$ (in-degree).
- $Cij$ rappresenta il numero di articoli che citano sia l'articolo $i$ che l'articolo $j$.
	- Esempio: $Cab$ = 2 -> indica che ci sono 2 articoli che citano sia $a$ che $b$ {$d$, $e$}.
### Bibliographic Matrix
La matrice Bibliografica opera secondo principi simili a quelli della Co-citazioni.
> Se gli articoli $i$ e $j$ citano entrambi l'articolo $k$, potrebbero essere correlati.

![[Pasted image 20250308135801.png]]
- $L$ rappresenta esattamente la matrice di adiacenza del grafo.
- $L^T$ rappresenta la trasposta.
- $B$ rappresenta la matrice Bibliografica.
- $Bii$ rappresenta il numero di citazioni del nodo $i$ (out-degree).
- $Bij$ rappresenta il numero di articoli che sono citano da entrambi $i$ e $j$.
	- Esempio: $Bde$ = 2 -> indica che ci sono due articoli che sono citati sia da $d$ che da $e$ {$a$, $b$}.
# HITS: Hypertext Induced Topic Search
Si tratta di un algoritmo di analisi dei link come alternativa all'approccio di Page-Rank (contesto: pagine WEB e link).

HITS assegna 2 valori a ciascuna pagina:
- Authority Score: Misura il valore del contenuto della pagina stessa.
- Hub Score: misura il valore dei link della pagina ad altre pagine.

Rafforzamento reciproco delle relazioni:
Il core di HITS sta nel rafforzamento reciproco delle relazioni tra Hubs e Autorità:
- Buone autorità sono pagine che sono connesse a molti buoni hub.
- Buoni hub sono pagine che sono connesse a molte buone autorità.



