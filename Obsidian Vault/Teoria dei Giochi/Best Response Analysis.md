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

Nel caso in cui **non** è possibile determinare alcun Nash Equilibrium con la Best Response, il gioco non ha equilibri per strategie pure.


> [!NOTE] Ordinal Payoffs 
> L'equilibrio di Nash in strategie pure dipende solo sui payoff "ordinali", non i payoff "reali".
> Nell'immagine sotto non è possibile determinare l'equilibrio se manteniamo come payoff gli effettivi anni di prigione!
> ![[Pasted image 20250321150356.png]]

## Eliminazione Dominated Strategies vs. Best Response
- L'eliminazione iterativa consente di evidenziare il processo decisionale razionale di ciascun giocatore, eliminando ciò che non è razionale da giocare.
- Il metodo delle best response si concentra sui payoff, portando ad essere meno intuitivo o affidabile in situazioni complesse.
- L'eliminazione delle strategie dominate semplifica il problema riducendo lo spazio strategico in caso di situazioni complesse.
- L'equilibrio di Nash non riguarda solo i payoff individuali, ma anche il fatto che ogni giocatore scelga la sua strategia in base a ciò che gli altri giocatori fanno.
- L'eliminazione delle strategie dominate è più flessibile e consente di affrontare il comportamento razionale emergente in modo iterativo, riflettendo una dinamica più realistica.