Appunti sul quaderno!!!
# Graph Statistics
## Connettività
- La connettività di un grafo misura la resilienza della sua struttura.
- Strettamente correlata alla teoria dei problemi di flusso di una rete.
> Rappresenta il numero minimo di elementi (nodi o archi) che se rimossi, disconnettono il grafo.
![[Pasted image 20250304121812.png|250]]

## Eccentricità 
L'eccentricità di un nodo in un grafo connesso è la distanza massima tra un nodo $v$ e qualunque altro nodo $u$ del grafo. In altre parole, la lunghezza del più lungo shortest path di un nodo.
#### Raggio di un grafo 
La minima eccentricità tra tutti i nodi.
#### Diametro di un grafo
La massima eccentricità tra tutti i nodi.

![[Pasted image 20250304122448.png|250]]
- Ecc(1) = 3
- Ecc(2) = 2
- Ecc(3) = 3
- Ecc(4) = 2
- Ecc(5) = 2
- Ecc(6) = 2
- Ecc(7) = 3 
- Raggio = min(Ecc(V)) = 2
- Diametro = max(Ecc(V)) = 3
## Conduttanza
Questa misura è utile per valutare la qualità di una partizione del grafo: una minore conduttanza indica cluster che può essere facilmente diviso in parti indipendenti. Al contrario, un'alta conduttanza indica cluster ben connesso e difficile da separare.

> Data una partizione di un grafo in 2 set disgiunti (G1 e G2), la conduttanza è la somma degli archi che vanno da G1 a G2 diviso il minimo tra gli archi in G1 e G2.

$$
CONDUTTANZA: cut(G1, G2)/min(vol(G1), vol(G2))
$$
in cui 
- vol(Gi) è la somma degli archi interni di Gi e gli archi che escono. (Nell'esempio prendendo Gi come {John, Ted}, vol(Gi) = 4)
- cut(Gi, Gj) è la somma degli archi che hanno direzione Gi -> Gj.

Esempio:
![[Pasted image 20250304123609.png]]
G1 = (John, Ted) 
G2 = (Ron, Lisa)
Conduttanza = 2/3

---
# Graph Structure
## Cliques (o sotto-grafo completo)
Subset di nodi in un grafo indiretto, in cui ciascun nodo è connesso con gli altri.
### K-Core (algoritmo)
Si tratta di un algoritmo che identifica il massimo sotto-grafo di un grafo in cui tutti i nodi hanno almeno degree = k.
Il massimo sotto-grafo è chiamato k-core.
L'algoritmo rimuove iterativamente nodi con degree minore di k e i loro archi incidenti, fino a quando non rimangono solo i nodi con degree >= k.

```
Given k:
Repeat:
	for each node n:
		if degree(n) < n:
			: delete n
until all nodes have degree >= k
```
### Diametro Medio L
La lunghezza media degli shortest paths tra qualsiasi coppia di nodi.
Misura quanto distanti i nodi sono in media.

### Clustering Coefficient C
Il clustering coefficient equivale alla densità del sotto-grafo considerando solo i vicini del nodo $n$ (escludendo $n$) . 
Il clustering coefficient di un nodo misura quanto sono vicini i neighbors all'essere una clique (complete graph). Possiamo dire inoltre, che il clustering coefficient misura quanto è probabile che due vicini di un nodo dato siano connessi tra loro. 

Grafo diretto:
$Cn = edgesneighbors(n) / degree(n)*(degree(n)-1)$
Grafo indiretto:
$Cn = 2 * edgesneighbors(n) / degree(n)*(degree(n)-1)$

dove:
- $edgesneighbors(n)$: indica il numero di archi tra i vicini di $n$

### Wiener Index
La Wiener Index di un grafo è una misura della complessità topologica del grafo.
Rappresenta la somma di tutti gli shortest path di un grafo.

---
# Misure di Centralità
Intuizione di centralità: rappresenta l'importanza di un nodo sulla base del suo ruolo nel mantenere la connettività del grafo.

### Degree Centrality
Numero di vicini che ha un nodo $n$.

### Closeness Centrality
Reciproco della totale distanza tra un nodo $n$ e tutti gli altri nodi. Rappresenta quanto è un nodo è vicino a tutti gli altri nodi.

### Betweenness Centrality
Rapporto tra il numero di shortest paths che passano per un dato nodo $n$ e il numero totale di shortest paths del grafo. Rappresenta quanto un nodo è fondamentale per i paths del grafo.

---
# Community Detection
> **Community**: porzione di grafo con alta connettività interna.

## Girvan-Newman Algoritmo
Questo algoritmo ha lo scopo di identificare e analizzare la struttura delle comunità presenti in un grafo. 
L'algoritmo si basa sull'eliminazione iterativa di edges che hanno il più alto numero di shortest paths, o anche con maggiore valore di Betweenness Centrality. 
Rimuovendo questi archi, la rete si scompone in piccoli parti chiamate **comunità**.
Passi dell'algoritmo:
- Calcolare la betweenness degli archi.
- Eliminare gli archi con betweenness più alta.
- I componenti connessi della rete sono comunità.
![[Pasted image 20250305143750.png]]
![[Pasted image 20250305143813.png|330]]


> [!NOTE] Non-overlapping vs. overlapping communities
> ![[Pasted image 20250305144909.png]]


## Graph Partitioning
> **Graph Cut**: numero di archi che vanno da G1 a G2 (visto nella formula della conduttanza).

Se vogliamo dividere il grafo in 2 parti, vogliamo minimizzare il numero di archi da rimuovere e ottenere le due parti "densamente connesse".
Vogliamo quindi minimizzare: ![[Pasted image 20250305144633.png]]

![[Pasted image 20250305144746.png]]

**In-Degree Prestige**: numero di archi entranti nel nodo $i$.
**Influence Domain**: numero di nodi che possono raggiungere il nodo $i$.
## Proximity Prestige (grafi diretti)
> Considerare l'importanza di un nodo in base al numero di archi entranti (in-degree).

La Proximity Prestige è una misura di centralità che valuta la popolarità del nodo e la misura di quanto velocemente può essere raggiunto.

Un nodo con alta Proximity Prestige è raggiungibile da molti altri nodi con poche connessioni intermedie.
![[Pasted image 20250305145439.png]]
dove:
- |$Ii$| è il numero di nodi che raggiungo il nodo $i$ con un percorso diretto.
- $(n-1)$ numero degli altri nodi nel grafo (escluso $i$).
- $d(i,j)$ lunghezza dello shortest path diretto da $j$ a $i$.
![[Pasted image 20250305145714.png]]
PP(1) = (9/9) / (1+1+1+2+2+2+2+3+4)/9 = 0.5
PP(8) = (2/9) / (1+2)/2 = 0.148

## Misura di Impatto: H-Index
> Considera l'importanza di un nodo in base alla produttività e all'impatto.

L'H-Index di un nodo si basa sul numero di connessioni in ingresso (in-degree) e sulle centralità dei nodi che lo citano. Non basta avere tanti archi entranti, bisogna essere collegati a nodi che a loro volta hanno un alto in-degree.

Un nodo con alto H-Index è raggiunto da molti nodi influenti.