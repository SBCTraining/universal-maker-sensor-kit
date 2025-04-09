.. note:: 

    Ciao, benvenuto nella Comunità di Appassionati di SunFounder Raspberry Pi & Arduino & ESP32 su Facebook! Immergiti più a fondo in Raspberry Pi, Arduino e ESP32 insieme ad altri entusiasti.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Ottieni accesso anticipato agli annunci di nuovi prodotti e anteprime esclusive.
    - **Special Discounts**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festive.

    👉 Pronto a esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

.. _pi_lesson18_ds18b20:

Lezione 18: Modulo Sensore di Temperatura (DS18B20)
========================================================

In questa lezione, imparerai come utilizzare un Raspberry Pi per leggere i dati della temperatura da un sensore DS18B20. Scoprirai come localizzare il file del dispositivo del sensore, leggere e interpretare i suoi dati grezzi, e convertire questi dati in letture Celsius e Fahrenheit.

Componenti Necessari
----------------------------

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
    *   - :ref:`cpn_ds18b20`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Cablaggio
---------------------------

.. image:: img/Lesson_18_DS18B20_pi_bb.png
    :width: 100%


Codice
---------------------------

.. note::
   Il modulo DS18B20 comunica con il Raspberry Pi utilizzando il protocollo onewire. Prima di eseguire il codice, è necessario abilitare la funzione onewire del Raspberry Pi. Puoi fare riferimento a questo tutorial: :ref:`pi_enable_1wire`. 

.. code-block:: python

   import glob
   import time
   
   # Percorso alla directory che contiene i file di dispositivo per dispositivi 1-wire
   base_dir = "/sys/bus/w1/devices/"
   
   # Trova la prima cartella del dispositivo che inizia con "28", specifica per DS18B20
   device_folder = glob.glob(base_dir + "28*")[0]
   
   # File del dispositivo contenente i dati della temperatura
   device_file = device_folder + "/w1_slave"
   
   
   def read_temp_raw():
       # Legge i dati grezzi della temperatura dal sensore
       f = open(device_file, "r")
       lines = f.readlines()
       f.close()
       return lines
   
   
   def read_temp():
       # Analizza i dati grezzi della temperatura e li converte in Celsius e Fahrenheit
       lines = read_temp_raw()
       # Attende una lettura valida della temperatura
       while lines[0].strip()[-3:] != "YES":
           time.sleep(0.2)
           lines = read_temp_raw()
       equals_pos = lines[1].find("t=")
       if equals_pos != -1:
           temp_string = lines[1][equals_pos + 2 :]
           temp_c = float(temp_string) / 1000.0  # Converti in Celsius
           temp_f = temp_c * 9.0 / 5.0 + 32.0  # Converti in Fahrenheit
           return temp_c, temp_f
   
   
   try:
       # Loop principale per leggere e stampare continuamente la temperatura
       while True:
           temp_c, temp_f = read_temp()
           formatted_output = f"Temperatura: {temp_c:.2f}°C / {temp_f:.2f}°F"
           print(formatted_output)
           time.sleep(1)  # Attendi 1 secondo tra le letture
   except KeyboardInterrupt:
       # Esci dal programma in modo pulito su CTRL+C
       print("Exit")




Analisi del Codice
---------------------------

#. Importazione delle Librerie Necessarie

   La libreria ``glob`` è utilizzata per cercare la cartella del dispositivo del sensore di temperatura. La libreria ``time`` è impiegata per implementare i ritardi nel programma.

   .. code-block:: python

      import glob
      import time

#. Localizzazione del File del Dispositivo del Sensore di Temperatura

   Il codice ricerca la directory del sensore DS18B20 cercando una cartella il cui nome inizia con "28". Il file del dispositivo ``w1_slave`` contiene i dati della temperatura.

   .. code-block:: python

      base_dir = "/sys/bus/w1/devices/"
      device_folder = glob.glob(base_dir + "28*")[0]
      device_file = device_folder + "/w1_slave"

#. Lettura dei Dati Grezzi della Temperatura

   Questa funzione apre il file del dispositivo e ne legge il contenuto. Restituisce i dati grezzi della temperatura sotto forma di elenco di stringhe.

   .. code-block:: python

      def read_temp_raw():
          f = open(device_file, "r")
          lines = f.readlines()
          f.close()
          return lines

#. Analisi e Conversione dei Dati della Temperatura

   La funzione ``read_temp`` richiama ``read_temp_raw`` per ottenere i dati grezzi. Attende una lettura valida della temperatura e poi estrae, analizza e converte la temperatura in Celsius e Fahrenheit.

   .. code-block:: python

      def read_temp():
          lines = read_temp_raw()
          while lines[0].strip()[-3:] != "YES":
              time.sleep(0.2)
              lines = read_temp_raw()
          equals_pos = lines[1].find("t=")
          if equals_pos != -1:
              temp_string = lines[1][equals_pos + 2 :]
              temp_c = float(temp_string) / 1000.0
              temp_f = temp_c * 9.0 / 5.0 + 32.0
              return temp_c, temp_f

#. Ciclo Principale del Programma e Uscita Elegante

   Il blocco ``try`` contiene un loop infinito per leggere e visualizzare continuamente la temperatura. Il blocco ``except`` intercetta un KeyboardInterrupt per uscire dal programma in modo elegante.

   .. code-block:: python

      try:
          while True:
              temp_c, temp_f = read_temp()
              formatted_output = f"Temperature: {temp_c:.2f}°C / {temp_f:.2f}°F"
              print(formatted_output)
              time.sleep(1)
      except KeyboardInterrupt:
          print("Exit")