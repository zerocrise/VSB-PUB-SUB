# VSB-PUB-SUB
Pattern pub/sub
Guida al Test su Rete Locale
Per testare la federazione tra broker e lo scambio di oggetti, segui questi passaggi. Supponiamo di avere due PC (o due terminali sullo stesso PC con IP diversi/localhost).
IP di esempio:
PC 1 (Broker A): 192.168.1.10
PC 2 (Broker B): 192.168.1.11
Passo 1: Compilazione
Su entrambe le macchine (assicurati di avere JDK installato):
bash
1
Passo 2: Avvio Broker A (PC 1)
Questo broker ascolta i client sulla 5000 e i peer sulla 5001.
bash
1
Passo 3: Avvio Broker B (PC 2) e Collegamento ad A
Questo broker si avvia e si collega automaticamente a BrokerA come peer.
bash
1
(Nota: l'ultimo argomento dice a BrokerB di connettersi all'indirizzo IP di BrokerA sulla porta peer).
Passo 4: Test del Subscriber (Su PC 2, collegato a Broker B)
Un client si collega a Broker B e aspetta messaggi.
bash
1
Passo 5: Test del Publisher (Su PC 1, collegato a Broker A)
Un client si collega a Broker A e pubblica.
bash
1
Scrivi un messaggio (es. "Ciao Rete Locale") e premi Invio.
Risultato Atteso
Il Publisher invia l'oggetto a Broker A.
Broker A vede che non ha subscriber locali per "news", ma ha un Peer (Broker B).
Broker A serializza l'oggetto e lo invia via TCP a Broker B.
Broker B riceve l'oggetto, controlla i suoi subscriber locali.
Broker B invia l'oggetto al Client Subscriber.
Il terminale del Subscriber stampa: >>> RICEVUTO: [news] Ciao Rete Locale (Da: User-...)
