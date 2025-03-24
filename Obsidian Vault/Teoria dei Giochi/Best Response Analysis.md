Si tratta di un metodo sistematico per l'individuazione dell'equilibrio di Nash.
Idea: Determiniamo la migliore risposta in funzione ad ogni strategia disponibile dell'avversario.
Possiamo definire il concetto di Nash Equilibrium in base alla migliore risposta come segue:
> Un profilo strategico $S* = (s*_i, s*_-i)$ è un equilibrio di Nash se ciascun giocatore sceglie la migliore risposta sapendo la strategia avversaria.

**Esempio**
![[Pasted image 20250321145432.png|350]]
**ROW** (cerchi neri):
- Sceglie Bottom come migliore payoff nel caso COLUMN scelga Left.
- Sceglie Low come migliore payoff nel caso COLUMN scelga Middle.
- Sceglie Low come migliore payoff nel caso COLUMN scelga Right.
**COLUMN** (cerchi azzurri):
- Sceglie Middle come migliore payoff nel caso ROW scelga Top.
- Sceglie Left come migliore payoff nel caso ROW scelga High.
- Sceglie Middle come migliore payoff nel caso ROW scelga Low.
- Sceglie Right come migliore payoff nel caso ROW scelga Bottom.
**Nash Equilibrium**: La cella che ha entrambi i payoff cerchiati rappresenta l'equilibrio di Nash in questa tabella (Low, Middle).

![[Pasted image 20250321145841.png|350]]
E' possibile determinare più equilibri di Nash con il metodo Best Response, come in questo caso in cui ne abbiamo trovati 3.

Nel caso in cui **non** è possibile determinare alcun Nash Equilibrium con la Best Response, il gioco non ha equilibri per strategie pure (non probabilistiche).


> [!NOTE] Ordinal Payoffs 
> L'equilibrio di Nash in strategie pure dipende solo sui payoff "ordinali", non i payoff "reali" (nel senso che conta solo se un payoff è maggiore dell'altro, non importa quanto più grande).
> Nell'immagine sotto non è possibile determinare l'equilibrio se manteniamo come payoff gli effettivi anni di prigione!
> ![[Pasted image 20250321150356.png]]

## Eliminazione Dominated Strategies vs. Best Response
- L'eliminazione iterativa consente di evidenziare il processo decisionale razionale di ciascun giocatore, eliminando ciò che non è razionale da giocare.
- Il metodo delle best response si concentra sui payoff, portando ad essere meno intuitivo o affidabile in situazioni complesse.
- L'eliminazione delle strategie dominate semplifica il problema riducendo lo spazio strategico in caso di situazioni complesse.
- L'equilibrio di Nash non riguarda solo i payoff individuali, ma anche il fatto che ogni giocatore scelga la sua strategia in base a ciò che gli altri giocatori fanno.
- L'eliminazione delle strategie dominate è più flessibile e consente di affrontare il comportamento razionale emergente in modo iterativo, riflettendo una dinamica più realistica.

---
### Constant-Sum Games
Un gioco composta da due giocatori è un Constant-Sum Game, se per ogni profilo di strategie i payoff dei giocatori soddisfa: $p_1(s) + p_2(s) = k$ 
*(la somma dei payoff tra i 2 giocatori è sempre costante)*
![[Pasted image 20250324170936.png]]

### Zero-Sum Games
Si tratta di un sottoinsieme dei Constant-Sum, in cui la somma dei payoff dei giocatori è sempre 0: $p_1(s) + p_2(s) = 0$ oppure definito come $p_1(s) = -p_2(s)$
![[Pasted image 20250324171135.png]]

> Un gioco Constant-Sum può essere sempre normalizzato e trasformato quindi in uno Zero-Sum Game mantenendo le stesse relazioni tra i payoff dei giocatori.

# Minimax Method
> Metodo di risoluzione per risolvere Zero-Sum Games (più efficiente degli altri metodi per la ricerca del Nash).

**Idea**: Il giocatore sceglierà sempre il peggiore payoff per l'avversario.

**Risoluzione**:
- Per ogni strategia di ciascun giocatore, si marca il payoff peggiore.
- Determinare la strategia che da a ciascun giocatore la miglior peggiore payoff.
- Questa strategia trovata si chiamerà: Minimax Strategy.
- Le strategie Minimax corrispondono ad equilibri di Nash.

**Esempio**:
![[Pasted image 20250324171958.png]]
1.  Peggiori payoff per le strategie dei giocatori:
	- Rowena:
		- Up: 3
		- Down: 1
	- Colin:
		- Left: 0
		- Right: 1
2. Migliori payoff dal punto precedente:
	- Rowena:
		- Up: 3
	- Colin:
		- Right: 1
3. Equilibrio di Nash / Minimax:
	- Up, Right (3, 1)

**NB**: possono esistere più Strategie Minimax!