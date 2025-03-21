### Obiettivi
- Definire gli obiettivi di progetto e la terminologia.
- Costruire un *modello dati concettuale* per le entità e le loro relazioni.
- Traslare un modello dati concettuale in un *graph data model*.
## Data Modeling
Si tratta del processo di translation dalle entità e relazione del mondo reale, nelle equivalenti rappresentazioni software.

Steps:
1. **Comprendere il problema**: specificare i termini comuni e i patterns di accesso principali.
	- *A cosa servirà il grafo/applicativo?*
	- *Quali sono i building blocks fondamentali della nostra applicazione?*
	- *Come le persone utilizzeranno il sistema?*
2. **Creare un modello concettuale**: disegnare un diagramma che fornisce un'immagine ad alto livello del dominio del problema.
	- Identificare e raggruppare le entità.
	- Identificare le relazioni tra le entità.
	![[Pasted image 20250321123608.png|300]]
3. **Creare un modello dati logico**: definire i nodi e gli archi, e le loro proprietà.
	- **Schemaless**: i Graph DB non hanno schemi predefiniti che indicano come i nodi e le relazioni devono essere definiti.
	- 3.1: Tradurre le entità in nodi.
	- 3.2: Tradurre le relazioni in edges, definendo labels coincise e corrette (occhio alle direzioni).
		- **Edge Uniqueness**: descrive il numero di volte in cui un nodo si può relazionare (\[0:n]) con un altro nodo tramite edges con la stessa label (un attore può aver recitato due ruoli distinti in un film). Definire in modo errato singola unicità o multipla unicità può causare problemi di performance e di informazioni.
	- 3.3: Trovare e assegnare le proprietà ad archi e nodi.
		- In base allo scopo e alle funzionalità del grafo/applicativo andremo a definire e assegnare le proprietà adeguate agli archi e ai nodi (es: se il sistema deve identificare la rete di amicizie, potrebbe essere utile specificare i nomi dei nodi e non le età).
	- 3.4: Check your model. Best Practice:
		- *Nodi e archi è possibile leggerli come una frase? Deve essere così!*
		- *Non devo avere labels diverse di nodi o archi con le stesse proprietà.*
		- *Ad un'analisi più attenta, il modello deve avere senso.*
4. **Testare il modello**: verificare che il modello sviluppato soddisfi i requisiti stabili dal problema.

**Physical Data Model**: modello dati logico che richiede uno schema e quindi una traduzione rigida in base al tipo di DB scelto.