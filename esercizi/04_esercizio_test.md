# Esercizio Testing

Considerare il seguente codice:
```Python
import time

class TTLCache:
    """
    Una cache in memoria con limite di capacità e scadenza temporale (Time-To-Live).
    Implementa una politica di rimozione LRU (Least Recently Used) quando è piena.
    """
    def __init__(self, capacity: int, ttl_seconds: int):
        if capacity <= 0:
            raise ValueError("La capacità deve essere maggiore di zero.")
        if ttl_seconds <= 0:
            raise ValueError("Il TTL deve essere maggiore di zero.")
            
        self.cache : 'dict[str,tuple[int, float]]' = {} 
        self.access_order : 'list[str]' = [] 
        self.capacity = capacity
        self.ttl_seconds = ttl_seconds

    def _cleanup_expired(self) -> None:
        """Metodo interno per rimuovere le chiavi scadute."""
        current_time = time.time()
        keys_to_remove : 'list[str]' = []
        for key, (_, insert_time) in self.cache.items():
            if current_time - insert_time > self.ttl_seconds:
                keys_to_remove.append(key)
                
        for key in keys_to_remove:
            del self.cache[key]
            if key in self.access_order:
                self.access_order.remove(key)

    def get(self, key : str) -> int | None:
        """Recupera un valore dalla cache, aggiornando il suo stato di accesso."""
        self._cleanup_expired()
        
        if key in self.cache:
            # Aggiorna l'ordine di accesso per la politica LRU
            self.access_order.remove(key)
            self.access_order.append(key)
            
            value, insert_time = self.cache[key]
            return value
            
        return None

    def put(self, key : str, value : int) -> None:
        """Inserisce o aggiorna un valore nella cache."""
        self._cleanup_expired()
        
        if key in self.cache:
            # Se la chiave esiste, la rimuovo dall'ordine attuale per rimetterla in fondo
            self.access_order.remove(key)
        elif len(self.cache) >= self.capacity:
            # Rimuovi il meno recentemente utilizzato (il primo della lista)
            lru_key = self.access_order.pop(0)
            del self.cache[lru_key]
            
        # Salva il valore e il tempo di inserimento
        self.cache[key] = (value, time.time())
        self.access_order.append(key)
        
    def clear(self):
        """Svuota completamente la cache."""
        self.cache.clear()
        self.access_order.clear()

# esempio di utilizzo
def main():
    cache = TTLCache(capacity=2, ttl_seconds=5)
    
    cache.put("a", 1)
    print(cache.get("a"))  # Output: 1
    
    time.sleep(6)  # Attendi che il TTL scada
    print(cache.get("a"))  # Output: None (scaduto)
    
    cache.put("b", 2)
    cache.put("c", 3)
    print(cache.get("b"))  # Output: 2
    print(cache.get("c"))  # Output: 3
    
    cache.put("d", 4)  # Rimuove "b" (LRU)
    print(cache.get("b"))  # Output: None (rimosso)
    print(cache.get("c"))  # Output: 3
    print(cache.get("d"))  # Output: 4

if __name__ == "__main__":
    main()
```

Implementare una suite di test per la classe `TTLCache`.

Form per il caricamento dell'esercizio: [https://forms.gle/DVS5GsMkShX5C5V48](https://forms.gle/DVS5GsMkShX5C5V48)

## Parte 2
Considerare i seguenti file per il test:
- Test 1: [https://drive.google.com/file/d/11-A8aUTszsEfycZgLiiy4wQOBhPtw8Pi/view?usp=sharing](https://drive.google.com/file/d/11-A8aUTszsEfycZgLiiy4wQOBhPtw8Pi/view?usp=sharing)
- Test 2: [https://drive.google.com/file/d/1WLyX6pNHX3t0wtRQZvHl5dAQLmr4VEs6/view?usp=sharing](https://drive.google.com/file/d/1WLyX6pNHX3t0wtRQZvHl5dAQLmr4VEs6/view?usp=sharing)
- Test 3: [https://drive.google.com/file/d/18ZWvMUkkXiMFYTNhFiRFcXtyCl3MLRlw/view?usp=sharing](https://drive.google.com/file/d/18ZWvMUkkXiMFYTNhFiRFcXtyCl3MLRlw/view?usp=sharing)
- Test 4: [https://drive.google.com/file/d/1_YibPmJUENPL6gbar4XSXwtTL9QyC_wd/view?usp=sharing](https://drive.google.com/file/d/1_YibPmJUENPL6gbar4XSXwtTL9QyC_wd/view?usp=sharing)

Scrivere una valutazione per ciascuno dei 4 come illustrato nel form seguente: [https://forms.gle/NqAsXDrWS8RUbCyB7](https://forms.gle/NqAsXDrWS8RUbCyB7)