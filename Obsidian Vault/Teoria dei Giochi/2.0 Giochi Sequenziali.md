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
- Nei giochi sequenziali bisogna analizzare anche se l'ordine con cui i partecipanti giocano influisce sul payoff.
- Nei giochi sequenziali è importante analizzare anche gli effetti in seguito all'aggiunta di più giocatori e/o più regole al gioco (gioco dei leoni).
	- In alcuni giochi, aggiungere un giocatore possiamo ottenere un nuovo equilibrio totalmente diverso nel gioco.

Guarda l'Ultimate Game!

## Nim Theory
Considerando il gioco già visto:
- ci sono 10 bastoncini.
- ciascun giocatore può rimuovere da 1 a 3 bastoncini.
- chi rimuove l'ultimo vince.
Definiamo n stati in base a quanti bastoncini rimangono.
States: 0, 1, 2, 3, ... n.
Definiamo inoltre:
- Winning States: il giocatore che si trova in questi stati vince se gioca razionalmente.
	- 1
	- 2
	- 3
- Loosing States: il giocatore che si trova in questi stati perde se l'avversario gioca razionalmente.
	- 0
	- 4
> Per vincere devo portare il mio avversario in un stato perdente.
> ![[Pasted image 20250310173747.png]]

**Divisibility Game**
In ogni stato $k$, il giocatore è in grado di rimuove un numero $x$ di bastoncini tale per cui $x<k$ e $x$ si divisore di $k$. (Nello stato 8 posso rimuovere 1,2,4 bastoncini; nello stato 7 posso rimuovere solo 1).
Perde chi arriva ad un bastoncini rimasto perché non può rimuoverlo.
> In questo gioco il pattern è:
> - Stati perdenti: dispari.
> - Stati vincenti: pari.

### Nim Game
Ci sono $n$ heap contenenti $x_i$ bastoncini. Ogni turno un giocatore può rimuovere quanti bastoncini vuole da un sono heap.
\[$x_1$, $x_2$, $x_3$\] -> \[10, 12, 5]
Loosing state -> \[0, 0, 0]
**nim sum** = $x_1$ xor $x_2$ xor $x_3$ 
*(ricorda che lo xor da risultato 1 se i due valori sono diversi, 0 se sono uguali; può essere concatenato perché associativa)*

> La Nim Theory ci dice che gli stati con **nim sum** = 0 sono stati perdenti, mentre tutti gli altri sono vincenti.

Nel caso di \[10, 12, 5]
![[Pasted image 20250310175444.png]]
Il giocatore che si trova nello stato attuale deve fare in modo che la **nim sum** sia = 0.
- Per capire da quale heap rimuovere i bastoncini: devo guardare quale heap contiene un "1" nelle colonna corrispondente all' "1" più significativo (più a sx) nella nim sum.
	- Nel nostro caso: la terza colonna ha un "1" in corrispondenza del primo heap.
- Per capire quanto rimuovere dall'heap individuato: devo arrivare al numero ottenuto facendo lo xor tra heap e nim sum.
	- Nel nostro caso: 10 xor 3 = 9. Quindi tolgo un bastoncino dal primo heap per lasciarne 9.
![[Pasted image 20250310175859.png|100]]

---
## Grundy Numbers
Possiamo utilizzare la Nim Theory in questo gioco, applicando una trasformazione e interpretazione degli stati per avere dei numeri per ciascun heap.
E' possibile associare a ciascuno stato un valore che indica se lo stato è vincitore o perdente (solitamente se stato = 0 -> stato perdente).
Utilizziamo il "mex", ovvero a partire dallo stato 0 calcolo il valore degli altri stato applicando la funzione "mex". Associo allo stato il valore minimo (>0) che non è compreso negli stati in cui posso muovermi.
- Esempio: se sono su uno stato in cui posso muovermi su "1" e "0", il valore del mex=2.
- Se posso muovermi su "1", allora il mex=0.

Utilizzeremo la nim sum nel caso in cui ci sono più sub-games, per comprendere se lo stato collettivo è vincente, e come muoversi razionalmente verso la "vittoria" (esercizio in cui ci sono 3 quadrati in cui è possibile muoversi, ciascuno dei quali può avere lo stesso significato degli heap in cui è possibile capire in quale heap muoversi).

> Per capire ancora meglio il Grundy e il mex guarda le slide "Gioco di Grundy", capire però il valore di (4) = 0