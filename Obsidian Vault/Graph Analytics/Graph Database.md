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

#### Neo4j
![[Pasted image 20250314125221.png|450]]
