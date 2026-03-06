# Esercizi Linea di Comando

Risolvere i seguenti esercizi scrivendo un comando con il minor numero di caratteri possibili.
I file si trovano nella cartella `/file`.

# Esercizio 1
I file `v1_deps.txt` e `v2_deps.txt` contengono liste di dipendenze software.
Entrambi sono già ordinati.
Trovare le dipendenze che sono presenti in `v1_deps.txt` ma non in `v2_deps.txt` (cioè che state rimosse nella versione 2).

# Esercizio 2
Il file `users.csv` contiene dati nel formato: `Nome,Cognome,Email,Ruolo`.
Estrarre i valori per `Cognome` e `Email` solo per le prime 10 righe (escludendo l'header).


# Esercizio 3
Il file `access.log` contiene i log di un server web.
Trovare i 5 indirizzi IP che hanno effettuato più richieste.


# Soluzione Esercizio 1
Possibile soluzione: `comm -23 v1_deps.txt v2_deps.txt`

# Soluzione Esercizio 2
Possibile soluzione: `head -n 11 users.csv | tail -n 10 | cut -d',' -f2,3`

# Soluzione Esercizio 3
Possibile soluzione: `cut access.log -d' ' -f1 | sort | uniq -c | sort -nr | head -n 5`
