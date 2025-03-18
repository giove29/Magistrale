Un Graph Database è un motore di data-storage che combina le basic graph structures di nodi e archi, con una tecnologia persistente e un linguaggio trasversale (query) per creare un database ottimizzato per lo storage e il rapido recupero di dati altamente connessi.

Si tratta di un DB:
- meno rigido strutturalmente rispetto ad un DB relazionale.
- senza limiti nel numero di relazioni che un nodo può avere.
- in cui nodi e archi possono avere caratteristiche multiple che li definiscono.

> Problema con DB relazionali: le relazioni tra entità sono rappresentate da foreign keys.

I Graph Databases forniscono strumenti eccellenti per muoversi tra le relazioni dei nostri dati. Rappresentando le connessioni (archi) con importanza come si fa con gli elementi del DB, il Graph DB rappresenta queste associazioni come costrutti del database che possono essere facilmente osservati e manipolati.

**Vantaggi di un Graph DB**:
- Aumenta e migliora la **produttività** degli sviluppatori.
- Rappresentare i dati in un modo più "realistico e familiare" aiuta la **facile comprensione** e adattamento a chi ci lavora o chi deve imparare.

**Possibili svantaggi di un Graph DB**:
- **Sicurezza e privacy**: richiedono una maggiore implementazione di sicurezza e mostrano chiaramente informazioni sensibili.
- **Implicazioni dell'Integrità dei Dati**: semplificando i modi di come informazioni si relazionano ad altre informazioni, una piccola relazione errata può portare a dati totalmente errati.

 ![[Pasted image 20250312150358.png]]
*Solo il relazionale e il graph sono in grado di relazionare entità coi dati.*

### Graph DB vs. Relational DB
Di seguito 3 aree in cui il Graph DB fornisce soluzioni più semplici ed efficienti rispetto al relazionale.

**1. Recursive Queries**: si eseguono molteplici volte in successione richiamando se stesse, fino a quando non si trova un condizione di terminazione o un'uscita.

`WITH RECURSIVE org AS ( SELECT employee_id, manager_employee_id, employee_name, 1 AS level FROM org_chart UNION SELECT e.employee_id, e.manager_employee_id, e.employee_name, m.level + 1 AS level FROM org_chart AS e INNER JOIN org AS m ON e.manager_employee_id = m.employee_id ) SELECT employee_id, manager_employee_id, employee_name FROM org ORDER BY level ASC;`

VS

`g.V(). repeat( 'works_for') ).path().next()`

**2. Different Result Types**: nel caso avessimo bisogno di risultati più completi e con diverse informazioni

**3. Path**: rappresentazioni di percorsi.

> I primi 2 punti sono rappresentabili sia con Relational che con Graph DB, il Graph permette vantaggi computazionali; mentre per il terzo punto, esso è rappresentabile solo attraverso il Graph DB

---

# Tipi di Graph DB
**Property Graph Database**
Contiene dati sotto forma di nodi e archi, e permette di specificare proprietà per entrambi.
![[Pasted image 20250314122502.png]]

**Resource Description Framework (RDF) Graph Database**
Rappresenta i dati come una tripla tupla composta da un soggetto, un predicato e un oggetto.
![[Pasted image 20250314122441.png]]

**Hypergraph Database**
Contiene nodi e hyperarchi (hyperedges); gli hyperarchi connettono qualunque numero di nodi alla volta.
![[Pasted image 20250314123118.png]]

**Spatial Graph Database**
Permette di contenere e interrogare nodi spaziali, come mappe, coordinate GPS. I nodi rappresentano locazioni e gli archi rappresentano le relazioni. Supportano indexing spaziale e interrogazioni spaziali.
![[Pasted image 20250314123137.png]]

**Temporal Graph Database**
Permette di contenere e interrogare dati con una dimensione temporale come per event logs. I nodi rappresentano entità, e gli archi rappresentano relazioni tra queste entità in specifici momenti temporali.
![[Pasted image 20250314123158.png|300]]

**Property-Graph / Triplestore**
Un Graph DB che combina le caratteristiche di entrambi Property Graph e RDF.
![[Pasted image 20250314123223.png|300]]

---
## Strumenti di modellazione
**GQL Standard**: è il linguaggio standard proposto per l'interrogazione di grafi (Aprile 2024).
- Neo4j
- Thinkerpop
- GraphQL
- Cypher (linguaggio che vedremo di più, più standard).
- Gremlin

# Neo4j
![[Pasted image 20250314125221.png|450]]
### Pattern
- (): nodo non identificato.
- (matrix): nodo identificato dalla variabile *matrix*.
- (:Movie): nodo non identificato con la label *Movie*.
- (matrix:Movie:Action): nodo con labels *Movie* e *Action* identificato dalla variabile *matrix*.
- (matrix:Movie {title:"The Matrix", released: 1997}): nodo con label *Movie*, identificato dalla variabile *matrix* e con proprietà title="The Matrix" e released=1997.
- --\>: arco non identificato.
- -\[role]-\>: arco identificato dalla variabile *ruolo*.
- -\[role:ACTED_IN {roles:\["Neo"]}]-\>: arco identificato con variabile *ruolo*, con label *ACTED_IN* e con proprietà *roles* che contenga la stringa "Neo".
- (a)--> (b)-->(c)<--(d): ricerca di un path specifico.
- (a)-->(b), (b)-->(a) ricerca di nodi che matchano certi path.
### Match
La clausola di Match permette di ottenere dati dal DB.
MATCH(p:Person)-\[:Likes]-\>(f:Person)
![[Pasted image 20250314131015.png]]
![[Pasted image 20250314130952.png]]
### Return
Restituisce il set dei risultati.
MATCH(p:Person)-\[:Likes]-\>(f:Person)
RETURN p.name, f.sex

```
MATCH(n)
RETURN n, "node" + id(n) + " is" +
	CASE  WHEN n.title IS NOT NULL THEN " a Movie"
	      WHEN EXISTS(n.name) THEN " a Person"
	      ELSE " something unknown"
	ENDS AS about
```
### Optional Match
Matcha patterns in contrasto con la struttura del grafo. Se non ci sono match, utilizza *NULLs* come bindings.
MATCH(a:Movie)
OPTIONAL MATCH (a)<\-\[:WROTE]-(x)
RETURN a.title, x.name

### WHERE
Dopo un MATCH, aggiunge condizioni alla richiesta. Può essere semplificato con l'aggiunta di {} nel MATCH.
MATCH(n)
WHERE n.name="Peter" XOR (n.age<30 AND n.name = "Tobias")
RETURN n

Può essere parzialmente riscritto come
MATCH(n {name="Peter" XOR (age<30 AND name = "Tobias")})

### Variable Length Path Patterns
Archi dello stesso tipo possono espresse specificando la lunghezza con lower e upper bounds. 
> Ricorda che ricerca path univoci e non i nodi univocamente!
- (a)-\[:x\*2]-\>(b)  is equal to  (a)-\[:x]-\>()-\[:x]-\>(b)
- (a)-\[\*3..5]-\>(b)
- (a)-\[\*3..]-\>(b)
- (a)-\[\*..5]-\>(b)
- (a)-\[\*]-\>(b)   (pericolo da eseguire perché ricerca qualunque percorso)
- Esempio completo (in questo esempio non è dichiarata la direzione):
	- MATCH(me)-\[:KNOWS\*1..2]-(remote_friend)
	- WHERE me.name = "Felipa" RETURN remote_friend.name


### Path Variables
Assegna path trovati a variabili.
p = ((a)-\[\*3..5]-\>(b))

### Shortest Path
Ricerca dello shortest path tra una coppia di nodi, dove è possibile aggiungere filtri tramite la clausola WHERE.
- shortestPath((x)-\[\*..6]-(y)): funzione di ricerca shortest path in cui è possibile specificare anche upper e lower bounds per la lunghezza del percorso.
MATCH (m {name:"Martina"}), (o {name: "Olivia"}), p = **shortestPath**((m)-\[\*..15]-(o))
WHERE length(p)>p RETURN p

### Aggregation
- **In RETURN clause**:
	- DISTINCT: rimuove duplicati.
	- COLLECT: colleziona tutti i valori in una lista.
	- COUNT
	- SUM
	- AVG
	- MIN
	- MAX
	- ...
	- Esempio:
		MATCH (me:Person {name: "Ann})--\>(friend:Person)--\>(friend_of_friend:Person)
		RETURN me.name, count(DISTINCT friend_of_friend), count(friend_of_friend)
- **In WHIT clause**: Concatena parti di query insieme, facendo il piping dei risultati, permettendo di:
	- Filtrare sugli aggregati.
	- Aggregare aggregati.
	- Limitare ricerche sulla base di proprietà o aggregati.
	- Esempio:
		MATCH(p)-\[:PLAYS]-\>(t) WITH t, AVG(p.age) AS a WHERE a < 25 RETURN t
		MATCH(p) -\[:PLAYS]-\> (t) WITH t, MIN(p.age) AS a RETURN AVG(a)

---
# High Level View of the Graph Space
Il Graph Space possiamo dividerlo in due parti:
1. Graph Database: Tecnologie utilizzate principalmente per la persistenza di grafici online.
2. Graph Compute Engines: Tecnologie utilizzate principalmente per Graph Analytics offline. Simile a data mining e online analytical processing.
## Graph Database Management System
Si tratta di un sistema manageriale online del DB che utilizza metodi CRUD (Create Read Update Delete) per la modellazione di grafi.
Graph DB sono generalmente costruiti per utilizzi con sistema transazionali, sono normalmente ottimizzati per questo scopo.