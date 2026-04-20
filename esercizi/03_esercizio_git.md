# Esercizio GIT
## 1. Preparazione
**Ruoli:**
* **1 Integration Manager (Maintainer):** responsabile del repository "ufficiale"
* **I rimanenti sono Sviluppatori (Developer):** responsabili dell'implementazione delle feature

Obiettivo: implementare una calcolatrice (in Python o in un qualsiasi altro linguaggio) che legga una serie di numeri da tastiera ed esegua l'operazione richiesta.

---

## 2. Setup del Progetto
1.  **Manager:** inizializza un repository locale con `git init`, crea un file `README.md` dove descrive il contenuto del repository e un file con una funzione base (in un qualsiasi linguaggio)
2.  **Manager:** carica il progetto su una piattaforma online (es. GitHub, GitLab, Bitbucket, ...) in un repository pubblico ed aggiunge i colleghi come collaboratori
3.  **Developer:** eseguono il `git clone` del repository per ottenere la loro copia locale

---

## 3. Sviluppo in Parallelo
Ogni membro del gruppo deve lavorare su un **branch separato** per simulare lo sviluppo di diverse funzionalità:

* **Sviluppatori** 
    * Ciascuno crea un branch: `git checkout -b <nome>` (al posto di `<nome>` utilizzare il nome che si preferisce). Tutti i nomi devono essere diversi
    * Ciascuno modifica il file aggiunto al punto 2.1 aggiungendo le funzionalità che preferisce
    * Esegue `git add` e `git commit`

* **Manager:** 
    * Crea un branch `fix-readme`
    * Corregge un errore nel testo del `README.md`
    * Esegue il merge immediato sul branch `main`

---

## 4. Integrazione e Gestione Conflitti
Il Manager deve ora integrare tutto il lavoro nel branch principale (`main`) e risolvere i conflitti con l'aiuto di tutti.

---

## 5. Conclusione e Discussione
Al termine dell'attività, rispondere a queste domande:
1.  Ci sono stati conflitti? Se sì, come sono stati risolti?
2.  Ci sono stati vantaggi a lavorare su branch diversi invece che tutti su `main`?