- Situazioni strategiche nelle quali esiste un ordine preciso con il quale si svolge il gioco.
- I giocatori decidono le loro mosse e sono consapevoli delle mosse precedenti degli avversari.
- I giocatori devono pensare come la loro attuale mossa influenzi le proprie mosse future e quelle degli avversari.
- I giocatori decidono la loro attuale mossa sulle basi di calcoli di conseguenze future.

# Game Tree
Tecnica grafica di visualizzazione e analisi di giochi sequenziali.
I game trees illustrano tutte le possibili azioni che possono essere prese da tutti i giocatori e indica tutti i possibili risultati del gioco.
![[Pasted image 20250303162447.png|300]]
*La rappresentazione è chiamata "extensive form of a game" e mostra giocatori, azioni e payoffs.* 
Ogni **nodo terminale** indica un possibile risultato finale in cui è espresso il valore dei payoff di ciascun giocatore.
> La cosa difficile è come modellare il gioco e come stabilire il payoff per ciascun termine.

**Mossa**: Singola azione presa da un giocatore.
**Strategia**: Costituita da un piano di mosse per un giocatore.


---

**Esercizio 1**
![[Pasted image 20250303163748.png|200]]
Strategia Albus -> Ha solo 3 possibili scelte dal punto 1. Quindi 3 strategie totali.
- {N}
- {E}
- {S}
Strategia Minerva -> Minerva ha 2 possibili scelte nei 3 possibili nodi. Le sue totali strategie sono 8 ed equivalgono alle combinazioni.
- {N.a, E.a, S.a}
- {N.a, E.a, S.b}
- {N.a, E.b, S.a}
- {N.b, E.a, S.a}
- {N.b, E.b, S.a}
- {N.a, E.b, S.b}
- {N.b, E.a, S.b}
- {N.b, E.b, S.b}

**Applicato il rollback**:
Strategia Albus in equilibrio -> N
Strategia Minerva in equilibrio -> {N.b, E.a, S.b}


---

**Esercizio 2**

![[Pasted image 20250303164628.png|250]]
Strategia Albus -> 4 totali combinazioni
- {N, N}
- {N, S}
- {S, N}
- {S, S}
Strategia Minerva -> 6 totali combinazioni
- {N.a, S.a}
- {N.a, S.b}
- {N.a, S.c}
- {N.b, S.a}
- {N.b, S.b}
- {N.b, S.c}


---

**Esercizio 21 Flags**
Il gioco è giocato da 2 partecipanti e ad ogni turno ciascun giocatore toglie da 1 a 3 bandiere dalle 21 totali iniziali.

---

**Esercizio 21 Matchsticks**
Ci sono 21 matchsticks da rimuovere tra 2 giocatori, a turno possono rimuoverli da 1 a 4 matchsticks alla volta. Vince chi toglie l'ultimo matchstick vince.
Possiamo risolverlo con l'albero e utilizzano la Rollback, ma l'albero verrebbe abbastanza grande. Possiamo quindi semplificarlo simulando lo stesso gioco con 6 matchsticks iniziali, il primo che gioca e ne toglie solo 1 lasciando il secondo giocatore con 5 ha vinto.
Capiamo che il primo giocatore deve togliere tanti matchsticks per lasciare all'altro un multiplo di 5, perché la scelta massima dell'altro è 4.
Nel gioco di 21 vince sempre il primo se fa la mossa giusta potendo lasciare l'altro sempre a multipli di 5 fino all'ultimo turno in cui vince.

---

# Backward Induction
Tecnica di analisi a ritroso: dalla soluzione ritorno alla situazione iniziale di partenza per determinare la strategia adeguata per il migliore payoff.
Utilizzo del Game Tree: parto dai payoff e a ritroso scarto le mosse con peggior payoff fino a risalire tutto l'albero e determinare la strategia migliore.

## Rollback Method
- Inizio le analisi dai nodi terminali.
- Utilizzando i payoff, determino le scelte migliori e risalgo i nodi.

Quando tutti i giocatori utilizzano rollback method, questo set di strategie è chiamato **rollback equilibrium** del gioco.
Il risultato del gioco in cui sono state applicate le strategie di rollback equilibrium è definito **rollback equilibrium outcome**.

> E' fondamentale ricordare salendo di livello nell'albero, i giocatori sono razionali e optano per la loro scelta con payoff migliore, i giocatori sono i grado di prevedere cosa gli altri faranno.

**Esercizio Sequenziale con esempio di Rollback Induction**
Emily, Nina e Talia vivono tutti nella stessa strada, e ad ognuna è stato chiesto di contribuire economicamente per la costruzione del giardino. Migliore è il giardino più sono contente e meno spendono più son contente.

Supponiamo:
- Se 2 contribuiscono sarà sufficiente per la costruzione del giardino e sono soddisfatte.
- Se solo 1 contribuisce il giardino non sarà apprezzato. 

Ciascun giocatore ha 4 tipi di scenari:
- Non paga e le altre 2 si. (Payoff migliore = 4)
- Paga e un'altra ha pagato. (Payoff = 3, abbiamo supposto che il giardino sia più importante del fatto di risparmiare)
- Non paga e solo un'altra ha pagato. (Payoff = 2)
- Paga e nessuno delle altre 2 ha pagato. (Payoff peggiore = 1)

Il gioco essendo sequenziale prevede in ordine le scelte di Emily, Nina e Talia.
Schema dal blocco di slide che deve ancora uscire.
Ogni giocatrice sceglie il ramo che la porta al suo payoff migliore in ogni caso in cui si può trovare.
##### Da notare
Nei giochi sequenziali bisogna analizzare anche se l'ordine con cui i partecipanti giocano influisce sul payoff.

Guarda l'Ultimate Game che dovrebbe essere 
