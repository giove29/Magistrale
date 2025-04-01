La produzione di soluzioni ML è un processo complesso che richiede numerose e difficili scelte, più della semplice scelta dell'algoritmo adeguato.
Progetti ML includono numerosi tasks relazionati a:
- Selezionare le sorgenti dati.
- Collezionare i dati.
- Comprendere i dati.
- Pulire e trasformare i dati.
- Processare i dati per creare ML models.
- Valutare i risultati.
- Distribuire.
Dopo lo sviluppo è necessario monitorare l'applicazione.
## CRISP-DM
Uno dei più comuni processi utilizzati per progetti data mining è il Cross-Industry Standard Process for Data Mining.
Può essere inoltre applicato a progetti generici di machine learning.
Caratteristiche chiave del CRISP-DM:
- Non è proprietario.
- E' neutrale e adattivo a qualunque applicativo, azienda e strumento.
- Permette di vedere esplicitamente il processo di data analytics sia da un punto di vista dell'applicazione, sia da un punto di vista tecnico.
![[Pasted image 20250328123314.png]]
![[Pasted image 20250328123336.png]]

---
# Le sfide del ML
### The source of truth
I dati di training rappresentano la sorgente della verità dalla quale qualunque informazione e predizione può essere estratta. Gestire la fase di training richiede molto sforzo.
E' stato stimato che i data scientist spendono fino all'80% del loro tempo nella preparazione dei dati.
- **Insufficiente quantità di dati**: ML richiede molti dati di training per fare in modo che funzioni correttamente. Anche per semplici casi applicativi sono necessari molti dati, per problemi complessi (es. deep learning) o per algoritmi non lineari sono richiesti milioni di esempi.
- **Scarsa qualità dei dati**: La scarsa qualità dei data set influenza negativamente i risultati del processo ML perché è difficile per gli algoritmi scartare gli errori. Le sorgenti data contengono sempre errori e rumore:
	- dati mancanti.
	- informazioni errate.
	- dati inappropriati.
	- dati non conformi al caso applicativo.
	- dati duplicati.
- **Dati non-rappresentativi**: Se i dati di training sono troppo numerosi o specifici solo per subset di casistiche, il learner potrebbe generare bias e non sarà in grado di generalizzare su tutti i possibili casi.
- **Caratteristiche irrilevanti**: Utilizzare più feature di quelle effettivamente utili, porta il learner a definire una mappatura più dettagliata aumentando il rischio che il modello overfit i dati. Feature selection e feature extraction rappresentano due importanti task.
### Problemi
I problemi associati alla qualità degli esempi di training determinano il set di requisiti e limiti del data management per l'infrastruttura del progetto ML.
Managing big data -> Collezionare data da multipli sorgenti e merging in una sorgente unificata genererà un enorme dataset. Aumentando la qualità dei dati, aumenterà la qualità del processo di apprendimento.
- Designing uno schema flessibile: Lo schema dovrebbe evolvere facilmente con il progetto. Provare a creare uno schema di modello che fornisce la capacità di merging multipli schemi eterogenei in un'unica ed omogenea struttura di dati che soddisfa i requisiti informativi e di navigazione.
- Sviluppare pattern di accesso efficienti: Rapide letture dei dati migliora le performance, in termini di processing time, del processo di training. 
### Performance 
Le performance sono un argomento complesso in machine learning perché sono associate a diversi fattori:
- **Precisione Predittiva**: può essere valutata utilizzando diverse misurazioni. 
	- RSME: misura la standard deviation degli errori fatti dal sistema nelle sue predizioni. Osserva le differenze tra il valore stimato e il valore conosciuto fra tutti gli esempi di un test dataset.
- **Training Performance**: tempo richiesto per la computazione del modello.
	- La quantità di dati e il tipo di algoritmo determinano il tempo di processing e di storage per la computazione del Prediction Model.
	- Questo problema di performance incide sugli algoritmi che producono un modello attraverso una fase di training, diversamente da Online Learning Approach che impara incrementalmente da piccoli set di dati.
- **Prediction Performance**: il tempo di risposta richiesto per fornire le predizioni.
	- L'output del progetto ML può essere un one-time static report per aiutare una scelta manageriale di un'azienda, o può rappresentare un servizio di raccomandazione online.
	- In base alla casistica in cui ci troviamo, il tempo di Prediction è richiesto più o meno rapido.
	- Nel caso di decision making non è fondamentale che il risultato sia real-time.
	- Nel caso di un recommendation system invece la velocità della risposta è fondamentale perché ne influenza User Experience e l'efficacia della prediction.


> [!NOTE] Benefici dell'uso di Grafi
> I fattori precedentemente descritti possono essere tradotti in requisiti per i progetti di ML. In questo contesto i grafi possono fornire meccanismi di storage adeguati per la ricerca e la modellazione di dati, riducendo il tempo di accesso di lettura ai dati, e offrire tecniche algoritmiche per migliorare la precisione delle predizioni.

### Storage del Modello
Il modello risultante dalla fase di training verrà utilizzato per effettuare predictions.
Questo modello richiede tempo per la computazione e necessità di essere salvato in un livello persistente per evitare ulteriori computazioni ad ogni restart del sistema.
- Item-to-item similarities: per engine di raccomandazioni utilizzando l'approccio "nearest-neighbor".
	- Esempio 100 items: sono richieste 100x100 entries da salvare. Ottimizzando -> 10x10.
![[Pasted image 20250328131152.png|100]]
- Item-cluster mapping: esprime come gli elementi sono raggruppati in clusters.
	- Esempio 100 items: richieste 100 entries.
![[Pasted image 20250328131208.png|150]]
**Model Storage Management**: rappresenta una sfida significante in ML.

### Real Time
ML è sempre più utilizzato nella delivery di servizi in real-time.
Esempio: recommendation systems che reagiscono ai click degli utenti in real time.
Obiettivi:
- **Learn fast**: il learner deve aggiornarsi il prima possibile appena i dati sono disponibili. Più il modello è allineato con gli ultimi eventi, più il modello è in grado di incontrare i bisogni dell'utente in quel momento.
- **Predict fast**: quando il modello si è aggiornato, le prediction devono essere veloci per non perdere l'interesse dell'utente.
---
# Il ruolo dei Grafi in ML
**PRO** dei Grafi:
- Esplorare più dati.
- Accessi rapidi.
- Pulire e arricchire i dati facilmente.

**Graph-Powered Machine Learning Platform**:
- I Grafi sono utilizzati per caratterizzare le interazioni tra oggetti di interesse, per modellare in generale problemi real-world (semplici o complessi).
- ML basati sui Grafi stanno diventando sempre più comuni.
- Costruire un Graph-Powered Machine Learning Platform ha numerosi benefici perché i grafi possono fornire features più avanzate che sono impossibili da implementare senza grafo.

Le **Graph Features** sono raggruppate in 3 aree principali:
- **Data Management**: fornisce feature che aiutano a trattare con i dati.
- **Data Analysis**: features e algoritmi utili per l'apprendimento e il predicting.
- **Data Visualization**: sottolinea l'utilità dei grafi nella rappresentazione visiva che aiuta l'uomo a comunicare, interagire coi dati e scoprire insights.
#### Data Management
- **Connected Sources of Truth**: i grafi permettono di fondere diversi data source in uno unico, semplificando il data management.
- **Knowledge Graphs**: forniscono strutture dati omogenee per il combinamento di data sources, prediction models, dati manuali, e sorgenti dati esterne.
- **Fast Data Access**: i grafi hanno multipli punti di accesso per lo stesso set di dati, aumentando così le performance diminuendo la quantità di dati che devono essere acceduti per una richiesta particolare.
- **Data Enrichment**: è semplice estendere i dati esistenti con sorgenti esterne.
- **Feature Selection**: identificare le caratteristiche rilevanti di un dataset è fondamentale permettendo accessi, identificazione e estrazione rapidi.

#### Data Analysis
I Grafi possono essere utilizzati per modellare e analizzare le relazioni e le proprietà tra le entità.
La flessibilità dello schema permette di avere diversi modelli che coesistono nello stesso dataset.
Le Graph-powered data analysis feature includono:
 - **Graph Algorithms**: numerosi algoritmi di grafi, come clustering, page rank, che sono utili per identificare approfondimenti nei dati.
 - **Graph-Accelerated Machine Learning**: il graph-powered feature extraction è un esempio di come i grafi possono accelerare e migliorare la qualità del sistema di apprendimento.
 - **Network Dynamics**: la consapevolezza dei contesti di contorno e delle forze che agiscono sulla rete non serve solo per una conoscenza delle dinamiche della rete, ma possono essere usate per migliorare la qualità della predictions.
 - **Mixing Models**: svariati modelli possono coesistere nello stesso grafo, favorendo la flessibilità e la velocità di accesso, fornendo fasi di prediction mescolate.
 - **Fast Model Access**: i grafi forniscono i pattern giusti per scopi real-time.

#### Data Visualization
I Grafi hanno un grande potere comunicativo, sono in grado di visualizzare molteplici tipi di informazioni allo stesso momento, in un modo che il cervello è in grado di comprendere facilmente.
Le Graph-powered data visualization features includono:
- **Data Navigation**: i grafi mettono in risalto le relazioni tra gli elementi di una rete, favorendo la navigazione nei dati e l'analisi attraverso strumenti.
- **Human-Brain Analysis**: la visualizzazione di dati tramite grafo combina il potere del ML con il potere del cervello umano, abilitando efficienza, avanguardia e pattern recognition.
- **Improved Communication**: i grafi, in particolar modo i property graph, sono "whiteboard friendly", che significa che il modo in cui sono salvati nel DB può essere rappresentato su una lavagna. Questa caratteristica riduce il gap tra le tecnicità di un modello complesso e come viene descritto e comunicato agli stakeholders.

## Grafi in 4 Fasi
>Il ruolo dei grafi dipende da ciascun specifico caso. Non in tutti i progetti ML i grafi sono utilizzati in tutti Data Management, Data Analysis e Data Visualization.

Possiamo utilizzare grafi in modalità diverse per ciascuna delle 4 fasi del Machine Learning Workflow:
1. Managing the data sources.
2. Learning.
3. Storing and Accessing the model.
4. Visualizing.
![[Pasted image 20250328143007.png]]