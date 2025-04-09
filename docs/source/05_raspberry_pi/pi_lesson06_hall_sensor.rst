.. note:: 

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino & ESP32 di SunFounder su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pi_lesson06_hall_sensor:

Lezione 06: Modulo Sensore Hall
==================================

.. note::
   Il Raspberry Pi non dispone di capacità di input analogico, quindi necessita di un modulo come :ref:`cpn_pcf8591` per leggere i segnali analogici per l'elaborazione.

In questa lezione, impareremo come utilizzare un Raspberry Pi per leggere da un modulo sensore Hall. Imparerai come collegare un modulo fotoresistore al PCF8591 per la conversione analogico-digitale e monitorarne l'uscita in tempo reale usando Python. Inoltre, esplorerai la lettura di valori analogici e la loro interpretazione per rilevare la presenza e il tipo di poli magnetici.

Componenti Necessari
--------------------------

Per questo progetto, abbiamo bisogno dei seguenti componenti.

È decisamente conveniente acquistare un kit completo, ecco il link:

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nome	
        - ARTICOLI IN QUESTO KIT
        - LINK
    *   - Kit Sensori Universale per Makers
        - 94
        - |link_umsk|

Puoi anche acquistarli separatamente dai link qui sotto.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduzione al Componente
        - Link Acquisto

    *   - Raspberry Pi 5
        - |link_rpi5_buy|
    *   - :ref:`cpn_hall`
        - \-
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_06_Hall_Sensor_Module_pi_bb.png
    :width: 100%


Codice
---------------------------

.. code-block:: python

   import PCF8591 as ADC  # Importa il modulo PCF8591
   import time  # Importa time per i ritardi
   
   ADC.setup(0x48)  # Inizializza PCF8591 all'indirizzo 0x48
   
   try:
       while True:  # Lettura continua e stampa
           sensor_value = ADC.read(1) # Leggi dal modulo sensore Hall a AIN1
           print(sensor_value, end="")  # Stampa il dato grezzo del sensore
   
           # Determina la polarità del magnete
           if sensor_value >= 180:
               print(" - South pole detected")   # Determinato come polo sud.
           elif sensor_value <= 80:
               print(" - North pole detected")   # Determinato come polo nord.
   
           time.sleep(0.2)  # Attendi 0.2 secondi prima della prossima lettura
   
   except KeyboardInterrupt:
       print("Exit")  # Uscita con CTRL+C

Analisi del Codice
---------------------------

1. **Importazione delle Librerie**:

   .. code-block:: python
      
      import PCF8591 as ADC  # Importa il modulo PCF8591
      import time  # Importa time per i ritardi

   Questo importa le librerie necessarie. ``PCF8591`` è usato per interagire con il modulo ADC, e ``time`` per implementare i ritardi nel ciclo.

2. **Inizializzazione del Modulo ADC**:

   .. code-block:: python
      
      ADC.setup(0x48)  # Inizializza PCF8591 all'indirizzo 0x48

   Configura il modulo PCF8591. ``0x48`` è l'indirizzo I2C del modulo PCF8591. Questa linea prepara il Raspberry Pi a comunicare con il modulo.

3. **Ciclo Principale per la Lettura dei Dati del Sensore**:

   .. code-block:: python

      try:
          while True:  # Lettura continua e stampa
              sensor_value = ADC.read(1) # Leggi dal modulo sensore Hall a AIN1
              print(sensor_value, end="")  # Stampa il dato grezzo del sensore

   In questo ciclo, ``sensor_value`` viene letto continuamente dal sensore Hall (collegato a AIN1 sul PCF8591). L'istruzione ``print`` emette i dati grezzi del sensore.

4. **Determinare la Polarità del Magnete**:

   .. code-block:: python
      
              # Determina la polarità del magnete
              if sensor_value >= 180:
                  print(" - South pole detected")   # Determinato come polo sud.
              elif sensor_value <= 80:
                  print(" - North pole detected")   # Determinato come polo nord.
 
   Qui, il codice determina la polarità del magnete. Se ``sensor_value`` è 180 o superiore, viene identificato come polo sud. Se è 80 o inferiore, viene considerato polo nord. È necessario modificare questi due valori soglia in base ai risultati effettivi delle misurazioni.

   Il modulo sensore Hall è dotato di un sensore Hall lineare 49E, che può misurare la polarità dei poli nord e sud del campo magnetico e la relativa forza del campo magnetico. Se piazzi il polo sud di un magnete vicino al lato marcato con 49E (il lato con il testo inciso), il valore letto dal codice aumenterà linearmente in proporzione alla forza del campo magnetico applicato. Al contrario, se piazzi un polo nord vicino a questo lato, il valore letto dal codice diminuirà linearmente in proporzione a quella forza del campo magnetico. Per maggiori dettagli, si prega di fare riferimento a :ref:`cpn_hall`.

5. **Ritardo e Gestione delle Eccezioni**:

   .. code-block:: python

      time.sleep(0.2)  # Attendi 0.2 secondi prima della prossima lettura

      except KeyboardInterrupt:
          print("Exit")  # Uscita con CTRL+C



   ``time.sleep(0.2)`` crea un ritardo di 0.2 secondi tra ciascuna iterazione del ciclo per prevenire una velocità di lettura eccessiva. Il blocco ``except`` intercetta un'interruzione da tastiera (CTRL+C) per uscire dal programma in modo ordinato.