## Agente e ambiente

L'agente e' un sistema che percepisce l'ambiente tramite **sensori** e agisce su di esso tramite **attuatori**.

### Caratteristiche dell'ambiente

![Imgur](https://i.imgur.com/IMrCMEx.png)
![Imgur](https://i.imgur.com/j5FeDdh.png)

Spesso alcuni ambienti sono stocastici perche' parzialmente osservabili e quindi non viene compreso appieno il determinismo.

### Qualche nozione

L'approccio **forte** e' quello di imitare il ragionamento umano, l'approccio **debole** e' trovare un algoritmo che funziona per un determinato problema.

L'ambiente puo' avere vari *stati*, che cambiano a seconda delle *azioni*. L'*obiettivo* e' uno *stato goal*. La *soluzione* e' una serie di azioni o che portano all'obiettivo.

### Problema

Un problema di ricerca e' definibile come una tupla di 4 elementi:
1. Stato iniziale
2. Funzione successore: dato uno stato e un'azione calcola lo stato successivo
3. Test obiettivo: determina se lo stato e' uno stato goal
4. Funzione di costo del cammino: assegna un costo a un percorso

## Albero/grafo di ricerca

- ogni nodo corrisponde a uno stato
- i nodi figli si ricavano tramite la funzione successore
- la radice e' lo stato iniziale
- e' un grafo se si puo' arrivare allo stesso stato con piu' percorsi

Formalmente:

G = ({n<sub>i</sub>}, {e<sub>ij</sub>})

c<sub>ij</sub>: costo dell'arco e<sub>ij</sub>

## Strategie di ricerca

```
frontiera = nodi non terminali e non espansi
b = branching factor (figli medi di un nodo)
m = profondita' massima
```

Quale nodo espandere per continuare la ricerca?

Criteri:
1. Completezza: garanzia di trovare una soluzione, se esiste
2. Ottimalità: garanzia di trovare una soluzione ottima (a costo minimo)
3. Complessità temporale: quanto tempo occorre per trovare una soluzione
4. Complessità spaziale: quanta memoria occorre per effettuare la ricerca

Approcci:
- blind: analizzano solo la struttura del problema per cercare la soluzione
- informati: usano informazioni aggiuntive derivate dalla ricerca

### Ricerca in ampiezza

Trova la soluzione ottimale solo se il costo e' funzione monotona crescente della profondita'. Frontiera come coda FIFO. Complessita' esponenziale O(b<sup>m</sup>).

### Ricerca a costo uniforme

Mantiene la frontiera ordinata in base al costo. Non contano la profondita' ma solo il costo dei percorsi. E' uguale alla ricerca in ampiezza se il costo di ogni azione e' uguale.

### Ricerca in profondita'

Si espande il nodo piu' profondo. La frontiera e' uno stack. Complessita' spaziale O(b * m) se si scoprono tutti i figli (senza backtracking), O(m) se si scopre solo un figlio. Complessita' temporale peggiore esponenziale. L'ottimalita' non e' garantita.

C'e' la variante **limitata** in cui si espande fino a una profondita' *l* ma non ha senso perche' si perde la completezza.

### Iterative deepening depth-first search

A ogni iterazione si fa una ricerca in profondita' limitata con una profondita' diversa. La complessita' temporale e' esponenziale come in quella in ampiezza, ma non visita il d+1 livello.

E' meglio quando lo spazio di ricerca e' ampio e la profondita' della soluzione non e' prevedibile.

### Ricerca bidirezionale

Due ricerche:
- una dallo stato iniziale
- una dallo stato goal

Termina quando le due ricerche si incontrano.

Se ci sono tanti stati goal, si cerca uno stato di comodo, ovvero raggiungibile in un passo da tutti gli stati goal.

Complessita' temporale e spaziale ottime: O(b<sup>d/2</sup>)
