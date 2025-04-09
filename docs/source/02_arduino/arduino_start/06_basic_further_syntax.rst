.. note::

    Ciao e benvenuto nella community Facebook per gli appassionati di SunFounder Raspberry Pi, Arduino ed ESP32! Approfondisci le tue conoscenze su Raspberry Pi, Arduino ed ESP32 insieme ad altri appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche con l’aiuto della community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anticipazioni.
    - **Sconti speciali**: Approfitta di sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni natalizie e giveaway.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti oggi stesso!

Regole di scrittura degli sketch
====================================


Se chiedi a un amico di accendere la luce, puoi dire "Accendi la luce", oppure "Luce accesa, amico", usando qualsiasi tono tu voglia.

Ma se vuoi che sia la scheda Arduino a eseguire qualcosa per te, devi rispettare le regole della programmazione Arduino per scrivere i comandi correttamente.

Questo capitolo contiene le regole fondamentali del linguaggio Arduino e ti aiuterà a capire come tradurre il linguaggio naturale in codice.

Ovviamente, è un processo che richiede tempo per essere assimilato e rappresenta spesso la parte più soggetta a errori per i principianti, quindi se sbagli spesso, non preoccuparti: basta provare ancora qualche volta.


Punto e virgola ``;``
-----------------------

Proprio come quando scriviamo una lettera e mettiamo il punto alla fine della frase per indicarne la conclusione, nel linguaggio Arduino si utilizza il ``;`` per segnalare la fine di un comando.

Prendiamo come esempio il classico "lampeggio del LED integrato". Uno sketch corretto dovrebbe apparire così:

Esempio:

.. code-block:: C

    void setup() {
        // inserisci qui il tuo codice di setup, verrà eseguito una sola volta:
        pinMode(13,OUTPUT); 
    }

    void loop() {
        // inserisci qui il tuo codice principale, verrà eseguito ripetutamente:
        digitalWrite(13,HIGH);
        delay(500);
        digitalWrite(13,LOW);
        delay(500);
    }

Ora osserviamo i due sketch seguenti e proviamo a indovinare se verranno correttamente riconosciuti da Arduino prima di eseguirli.

Sketch A:

.. code-block:: C
    :emphasize-lines: 8,9,10,11

    void setup() {
        // inserisci qui il tuo codice di setup, verrà eseguito una sola volta:
        pinMode(13,OUTPUT); 
    }

    void loop() {
        // inserisci qui il tuo codice principale, verrà eseguito ripetutamente:
        digitalWrite(13,HIGH)
        delay(500)
        digitalWrite(13,LOW)
        delay(500)
    }

Sketch B:

.. code-block:: C
    :emphasize-lines: 8,9,10,11,12,13,14,15,16

    void setup() {
        // inserisci qui il tuo codice di setup, verrà eseguito una sola volta:
        pinMode(13,OUTPUT);
    }
    
    void loop() {
        // inserisci qui il tuo codice principale, verrà eseguito ripetutamente:
        digitalWrite(13,
    HIGH);  delay
        (500
        );
        digitalWrite(13,
        
        LOW);
                delay(500)
        ;
    }

Il risultato è che **Sketch A** genera un errore mentre **Sketch B** funziona.

* Gli errori in **Sketch A** sono dovuti alla mancanza del ``;``. Anche se il codice sembra corretto, Arduino non riesce a interpretarlo.
* **Sketch B**, pur sembrando scritto "contro l’essere umano", funziona perché l’indentazione, gli a capo e gli spazi all’interno delle istruzioni non hanno alcun significato per Arduino: per il compilatore, appare identico all’esempio funzionante.

Tuttavia, evita di scrivere il codice come in **Sketch B**, perché saranno le persone a leggerlo e modificarlo: non crearti inutili difficoltà.


Parentesi graffe ``{}``
--------------------------

Le ``{}`` sono elementi fondamentali del linguaggio di programmazione Arduino e devono sempre comparire in coppia.
Una buona pratica consiste nello scrivere immediatamente la parentesi graffa di chiusura dopo quella di apertura, posizionando poi il cursore tra le due per inserire le istruzioni.



Commento ``//``
-----------------

Il commento è la parte dello sketch che il compilatore ignora. Viene solitamente usato per spiegare il funzionamento del programma.

Se scriviamo due barre oblique in una riga di codice, tutto ciò che segue fino alla fine della riga viene ignorato dal compilatore.

Quando creiamo un nuovo sketch, questo contiene già due commenti. Rimuoverli non ha alcun effetto sul funzionamento del programma.

.. code-block:: C
    :emphasize-lines: 2,7

    void setup() {
        // inserisci qui il tuo codice di setup, verrà eseguito una sola volta:

    }

    void loop() {
        // inserisci qui il tuo codice principale, verrà eseguito ripetutamente:

    }


I commenti sono molto utili nella programmazione. Ecco alcuni esempi d’uso comuni:

* Uso A: Spiegare a te stesso o ad altri cosa fa una determinata sezione di codice.

.. code-block:: C

    void setup() {
        pinMode(13,OUTPUT); // Imposta il pin 13 in modalità output, controlla il LED integrato
    }

    void loop() {
        digitalWrite(13,HIGH); // Accende il LED integrato impostando il pin 13 su HIGH
        delay(500); // Mantiene lo stato per 500 ms
        digitalWrite(13,LOW); // Spegne il LED integrato
        delay(500); // Mantiene lo stato per 500 ms
    }

* Uso B: Disabilitare temporaneamente alcune istruzioni (senza eliminarle) per poi riattivarle al bisogno. Utile durante il debug per localizzare errori.

.. code-block:: C
    :emphasize-lines: 3,4,5,6

    void setup() {
        pinMode(13,OUTPUT);
        // digitalWrite(13,HIGH);
        // delay(1000);
        // digitalWrite(13,LOW);
        // delay(1000);
    }

    void loop() {
        digitalWrite(13,HIGH);
        delay(200);
        digitalWrite(13,LOW);
        delay(200);
    }    

.. note:: 
    Usa la scorciatoia ``Ctrl+/`` per commentare o decommentare rapidamente il tuo codice.

Commento ``/**/``
------------------

Funziona come ``//``, ma può estendersi su più righe. Una volta che il compilatore incontra ``/*``, ignorerà tutto fino a trovare ``*/``.

Esempio 1:

.. code-block:: C
    :emphasize-lines: 1,8,9,10,11

    /* Lampeggio */

    void setup() {
        pinMode(13,OUTPUT); 
    }

    void loop() {
        /*
        Il codice seguente fa lampeggiare il LED integrato
        Puoi modificare il numero in delay() per cambiare la frequenza del lampeggio
        */
        digitalWrite(13,HIGH); 
        delay(500); 
        digitalWrite(13,LOW); 
        delay(500);
    }


``#define``
--------------

Si tratta di uno strumento utile del C++.

.. code-block:: C

    #define identifier token-string

Il compilatore sostituisce automaticamente ``identifier`` con ``token-string`` durante la compilazione. Viene spesso utilizzato per definire costanti.

Ecco un esempio di sketch che utilizza ``define``, migliorando la leggibilità del codice:

.. code-block:: C
    :emphasize-lines: 1,2

    #define ONBOARD_LED 13
    #define DELAY_TIME 500

    void setup() {
        pinMode(ONBOARD_LED,OUTPUT); 
    }

    void loop() {
        digitalWrite(ONBOARD_LED,HIGH); 
        delay(DELAY_TIME); 
        digitalWrite(ONBOARD_LED,LOW); 
        delay(DELAY_TIME);
    }

Per il compilatore, questo codice equivale a:

.. code-block:: C

    void setup() {
        pinMode(13,OUTPUT); 
    }

    void loop() {
        digitalWrite(13,HIGH); 
        delay(500); 
        digitalWrite(13,LOW); 
        delay(500);
    }

Possiamo vedere che ``identifier`` viene sostituito e non esiste realmente all'interno del programma.
Pertanto, ci sono alcune accortezze da tenere a mente quando lo si utilizza:

1. Una ``token-string`` può essere modificata solo manualmente e non può essere trasformata in altri valori tramite operazioni aritmetiche nel programma.

2. Evita di utilizzare simboli come ``;``. Ad esempio:

.. code-block:: C
    :emphasize-lines: 1

    #define ONBOARD_LED 13;

    void setup() {
        pinMode(ONBOARD_LED,OUTPUT); 
    }

    void loop() {
        digitalWrite(ONBOARD_LED,HIGH); 
    }

Il compilatore lo interpreterà così, generando un errore:

.. code-block:: C
    :emphasize-lines: 2,6

    void setup() {
        pinMode(13;,OUTPUT); 
    }

    void loop() {
        digitalWrite(13;,HIGH); 
    }

.. note:: 
    Una convenzione comune per ``#define`` è scrivere ``identifier`` tutto in maiuscolo per evitare confusione con le variabili.