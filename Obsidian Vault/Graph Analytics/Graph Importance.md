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

---

# HITS: Hypertext Induced Topic Search
Si tratta di un algoritmo di analisi dei link come alternativa all'approccio di Page-Rank (contesto: pagine WEB e link).
1. HITS espande la lista di pagine rilevanti.
2. In seguito produce 2 rankings al set di pagine, Autorità e Hub ranking.
	- **Autorità**: una pagina autoritaria è una pagina con molti link entranti.
	- **Hub**: un hub è una pagina con molti link uscenti.

HITS assegna 2 valori a ciascuna pagina:
- **Authority Score**: Misura il valore del contenuto della pagina stessa. Si tratta di pagine che hanno buoni e contenuti autorevoli nelle quali molti pagine si fidano e si collegano.
- **Hub Score**: Misura il valore dei link della pagina ad altre pagine. Si tratta di pagine che servono come organizzatori di informazioni autorevoli per determinati argomenti.

**Rafforzamento reciproco delle relazioni**:
Il core di HITS sta nel rafforzamento reciproco delle relazioni tra Hubs e Autorità:
- Buone autorità sono pagine che sono connesse a molti buoni hub.
- Buoni hub sono pagine che sono connesse a molte buone autorità.

**Procediamo iterativamente**:
- Per prima cosa al tempo $t_0$, assegnamo Authority score e Hub score a tutti i nodi pari a $1/rad(N)$.
- Successivamente, dal tempo $t_0$ a $t_1$, accumuliamo lo score da ciascuna autorità ad ogni hub, e da ciascun hub ad ogni autorità.
Ripetiamo il processo fino a $t_i$, aggiornando i valori ad ogni step.

**Formula con Matrice**:
- $n$ pagine.
- Utilizziamo 2 vettori per rappresentare gli score:
	- Authority Score: $a = (a_1, a_2 ... a_n)$
	- Hub Score: $h = (h_1, h_2 ... h_n)$
- Matrice di adiacenza $A$ (chiamata anche Link matrix del Web)
- **Fino a convergenza**:
	- $h = A * a$
	- $a = A^T * h$

---

# Page Rank
Page Rank è un algoritmo che misura l'importanza dei nodi in un grafo, analizzando la struttura dei link tra di essi. Ha rivoluzionato la ricerca Web perchè in grado di determinare quali pagine hanno maggior valore.

Concetto di base: 
Una pagina è importante se riceve link da altre pagine importanti. Questo crea una definizione ricorsiva nella quale l'importanza di una pagina dipende dall'importanza delle pagine ad essa collegate.
- La pagina $j$ con importanza $r_j$ ha $n$ out-links, ciascuno dei suoi link avrà $r_j/n$ voti (voti provenienti da pagine con molti voti, valgono di più.)
- L'importanza della pagina $j$ si calcola come la somma di tutti i voti ottenuti dai suoi in-links.
![[Pasted image 20250312130932.png|200]]
$Rank(B) = Rank(C)/4 + Rank(E)/3 + Rank(F)/2$

**Formula con Matrice**:
- Matrice stocastica di adiacenza $M$ (le colonne sommano 1).
- Vettore $r$ per rappresentare il rank di ciascuna pagina -> $r = [1/N, 1/N ...]$
- **Fino a convergenza**:
	- $r^1 = M * r^0$
	- Ci si ferma quando $|r^1 - r^0| < e$, ovvero quando tra un'iterazione e l'altra la variazione del vettore è minima.

**Power Iteration**: Il processo di iterare fino ad una convergenza o una variazione tollerabile per il Page Rank, lo definiamo Power Iteration

#### Stationary Distribution
Si tratta del risultato finale ottenuto dalla Power Iteration. Descrive una distribuzione delle probabilità lungo le pagine, iniziando da un nodo random con quale probabilità mi trovo sul nodo $x$?

**Condizioni di Esistenza e Unicità della Stationary Distribution in processi Markov**
- La matrice di transizione è una matrice stocastica: tutte le colonne sommano 1.
- La matrice è irriducibile: il grafo è fortemente connesso (ciascun nodo può essere raggiunto da ogni nodo).
- La matrice è aperiodica: è possibile tornare indietro ad un nodo in un numero fissato di step.

**PROBLEMA!!**
![[Pasted image 20250312133748.png]]
Nel caso di grafi con Dead end e/o Spider trap, non è possibile ottenere una Stationary Distribution!

**SOLUZIONE!!**
Possiamo trasformare la Matrice delle transizioni facendo in modo che, anche in presenza di Dead end o Spider trap, sia sempre possibile raggiungere un qualsiasi nodo da ogni nodo. 
Come fare?
Aggiungiamo un link da ogni pagina che arriva ad ogni pagina e gli assegnamo una piccola probabilità di transizione.
Esattamente come se stessimo introducendo la **Teleport Probability** nel grafo!

---

# Page Rank Personalizzato: Topic Specific Page Rank

> Page Rank misura una generica popolarità di una pagina, non è specifica per una search query o un argomento.

**Obiettivo**: Valutare le pagine Web in base a quanto sono vicini ad un particolare argomento (sport, storia...).
**Idea**: Ora consideriamo il Teleport Probability ad una pagina random non uniformemente.
- Quando un visitatore effettua un Teleport, sceglie da un set di pagine $S$.
- Il set $S$ contiene solo pagine che sono rilevanti per un argomento.
- Per ciascuna Teleport Probability del set $S$, abbiamo un vettore differente $r_S$.
![[Pasted image 20250312141140.png]]