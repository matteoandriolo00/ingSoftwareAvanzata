## Esercizio: Million Clauses Challenge

L'obiettivo è leggere un file `cnf` e produrre un report statistico nel **minor tempo possibile** (tempo misurato con il comando [`time`](https://www.man7.org/linux/man-pages/man1/time.1.html) e/o [`multitime`](https://github.com/ltratt/multitime) e/o [`hyperfine`](https://github.com/sharkdp/hyperfine)).

Un tipico file CNF si presenta così:
```
c Questo è un commento
p cnf 3 4
1 -2 0
-1 3 0
2 -3 0
1 2 3 0
```

La prima riga iniza con `p` e rappresenta l'header: nell'esempio `3` è il numero di variabili (ciascuna variabile è identificata da un intero) e `4` è il numero di clausole.

Ogni clausola è una sequenza di letterali (numeri interi positivi o negativi) separati da spazio e terminata con `0`.

Il programma deve analizzare il file e restituire:
- conteggio totale delle clausole (per verificare la coerenza con l'header `p cnf`). Le righe che iniziano con `c` devono essere ignorate
- frequenza di ogni variabile: quante volte appare ogni letterale (es. quante volte compare `1` e quante volte `-1`)
- la clausola più lunga: indice (partendo da 1) e numero di letterali contenuti nella clausola con dimensione massima
- densità di letterali: il numero medio di letterali per clausola
- nel caso in cui il file cnf non rispetti le specifiche, deve notificare l'utente (cioè, il programma dovrebbe gestire gli errori e/o eccezioni)

Nell'esempio sopra, il risultato atteso è
```
4
1 2 -1 1 2 2 -2 1 3 2 -3 1
4 3
2.25
```
