import requests

# URL base dell'API di test
BASE_URL = "https://reqres.in/api/users"

def crea_utente(nome, lavoro):
    """Crea un nuovo utente tramite API"""
    payload = {"name": nome, "job": lavoro}
    response = requests.post(BASE_URL, json=payload)
    if response.status_code == 201:
        return response.json()
    else:
        print("Errore nella creazione utente:", response.status_code)
        return None

def leggi_utente(user_id):
    """Recupera i dati di un utente tramite API"""
    response = requests.get(f"{BASE_URL}/{user_id}")
    if response.status_code == 200:
        return response.json()
    else:
        print("Utente non trovato:", response.status_code)
        return None

def main():
    print("=== Gestione Utenti con API ===")
    
    # Input dall'utente
    nome = input("Inserisci il nome: ")
    lavoro = input("Inserisci il lavoro: ")
    
    # Creiamo un nuovo utente
    utente_creato = crea_utente(nome, lavoro)
    if utente_creato:
        print("\n✅ Utente creato con successo!")
        print("Dettagli:", utente_creato)
        
        # Otteniamo l'ID generato
        user_id = utente_creato["id"]
        
        # Recuperiamo i dati dell'utente
        print("\n🔎 Recupero dati dell'utente con ID:", user_id)
        utente = leggi_utente(user_id)
        
        if utente:
            print("Dati utente trovati:")
            print(utente)

if __name__ == "__main__":
    main()
