.. note:: 

    Ciao! Benvenuto nella community Facebook dedicata agli appassionati di SunFounder, Raspberry Pi, Arduino ed ESP32! Unisciti a noi per approfondire l’universo di Raspberry Pi, Arduino ed ESP32 insieme ad altri maker e appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e sfide tecniche grazie all’aiuto della nostra community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Ricevi in anteprima annunci e anticipazioni sui nuovi prodotti.
    - **Sconti speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e omaggi**: Partecipa a giveaway e iniziative promozionali durante le festività.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _cpn_mpu6050:

Modulo Giroscopio & Accelerometro (MPU6050)
===============================================================

.. image:: img/05_mpu6050_1.png
    :width: 300
    :align: center

.. raw:: html

   <br/>

L’MPU-6050 è un dispositivo di tracciamento del movimento a 6 assi (combina un giroscopio a 3 assi e un accelerometro a 3 assi). È in grado di rilevare variazioni di movimento, accelerazione e rotazione. È ampiamente utilizzato in robotica, controller per videogiochi e altri dispositivi elettronici che richiedono il rilevamento del movimento. La sua elevata precisione e il basso costo lo rendono particolarmente popolare tra gli appassionati del fai-da-te.

Principio di funzionamento
------------------------------
Il modulo MPU-6050 è composto da un accelerometro a 3 assi e un giroscopio a 3 assi.

I suoi tre sistemi di coordinate sono definiti come segue:

Posiziona l'MPU6050 su una superficie piana, con la faccia con l’etichetta rivolta verso l’alto e il punto situato nell’angolo in alto a sinistra. In questa configurazione, la direzione verticale verso l’alto rappresenta l’asse Z del chip. La direzione da sinistra a destra è l’asse X. Di conseguenza, la direzione dal retro verso il fronte è definita come asse Y.

.. image:: img/05_mpu_2.png
    :width: 300
    :align: center

Accelerometro a 3 assi
^^^^^^^^^^^^^^^^^^^^^^^^
L’accelerometro funziona secondo il principio dell’effetto piezoelettrico, ovvero la capacità di alcuni materiali di generare una carica elettrica in risposta a uno stress meccanico.

Immagina una scatola cuboidale contenente una piccola sfera, come mostrato nell’immagine sopra. Le pareti della scatola sono fatte di cristalli piezoelettrici. Quando inclini la scatola, la gravità spinge la sfera a muoversi nella direzione dell'inclinazione. La parete contro cui urta la sfera genera una debole corrente piezoelettrica. Esistono tre coppie di pareti opposte nella scatola, ciascuna delle quali corrisponde a un asse nello spazio tridimensionale: X, Y e Z. In base alla corrente generata dalle pareti piezoelettriche, possiamo determinare la direzione e l'entità dell’inclinazione.

.. image:: img/05_mpu_3.png
    :width: 800
    :align: center

Possiamo usare l’MPU6050 per rilevare l’accelerazione lungo ciascun asse (in stato statico su una scrivania, l’accelerazione sull’asse Z è pari a 1 unità gravitazionale, mentre sugli assi X e Y è 0). In caso di inclinazione o condizioni di microgravità/sovrappeso, i valori cambieranno di conseguenza.

È possibile selezionare quattro intervalli di misura via software: +/-2g, +/-4g, +/-8g e +/-16g (predefinito: 2g), ognuno con la propria precisione. I valori letti variano tra -32768 e 32767.

La lettura dell’accelerometro viene convertita in un valore di accelerazione mappando il valore letto all’intervallo selezionato.

Accelerazione = (Dati grezzi dell’accelerometro / 65536 * Intervallo scala piena) g

Ad esempio, se i dati grezzi dell’accelerometro sull’asse X sono 16384 e l’intervallo è +/-2g:

Accelerazione lungo l’asse X = (16384 / 65536 * 4) g = 1g

Giroscopio a 3 assi
^^^^^^^^^^^^^^^^^^^^^^^
I giroscopi si basano sul principio dell’accelerazione di Coriolis. Immagina una struttura a forma di forcella in movimento oscillante costante, tenuta in posizione da cristalli piezoelettrici. Quando si cerca di inclinare questa struttura, i cristalli sperimentano una forza nella direzione dell’inclinazione, dovuta all’inerzia del movimento. Di conseguenza, i cristalli generano una corrente secondo l’effetto piezoelettrico, che viene poi amplificata.

.. image:: img/05_mpu_4.png
    :width: 800
    :align: center

Anche il giroscopio offre quattro intervalli di misura: +/-250, +/-500, +/-1000, +/-2000. Il metodo di calcolo è sostanzialmente simile a quello dell’accelerazione.

La formula per convertire la lettura in velocità angolare è:

Velocità angolare = (Dati grezzi del giroscopio / 65536 * Intervallo scala piena) °/s

Ad esempio, se i dati grezzi del giroscopio sull’asse X sono 16384 e l’intervallo selezionato è +/-250°/s:

Velocità angolare sull’asse X = (16384 / 65536 * 500)°/s = 125°/s



Esempi
---------------------------
* :ref:`uno_lesson05_mpu6050` (Arduino UNO)
* :ref:`esp32_lesson05_mpu6050` (ESP32)
* :ref:`pico_lesson05_mpu6050` (Raspberry Pi Pico)
* :ref:`pi_lesson05_mpu6050` (Raspberry Pi Pi)

* :ref:`uno_lesson52_tilt_direction_indicator` (Arduino UNO)




