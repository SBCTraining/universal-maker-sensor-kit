.. note:: 

    Ciao, benvenuto nella Comunità degli Appassionati di Raspberry Pi, Arduino & ESP32 di SunFounder su Facebook! Approfondisci la tua conoscenza su Raspberry Pi, Arduino e ESP32 insieme ad altri appassionati.

    **Why Join?**

    - **Expert Support**: Risolvi problemi post-vendita e sfide tecniche con l'aiuto della nostra comunità e del nostro team.
    - **Learn & Share**: Scambia consigli e tutorial per migliorare le tue competenze.
    - **Exclusive Previews**: Accedi in anteprima agli annunci di nuovi prodotti e alle anticipazioni esclusive.
    - **Special Discounts**: Godi di sconti esclusivi sui nostri prodotti più recenti.
    - **Festive Promotions and Giveaways**: Partecipa a giveaway e promozioni festivi.

    👉 Pronto per esplorare e creare con noi? Clicca [|link_sf_facebook|] e unisciti oggi!

Configurazione del tuo Raspberry Pi
======================================

.. _pi_enable_i2c:

Configurazione I2C
-----------------------

Per abilitare la porta I2C sul tuo Raspberry Pi, segui questi passaggi (salta se già abilitato; se non sei sicuro, procedi con le istruzioni).

1. Accedi al tuo Raspberry Pi, apri il Terminale e inserisci il comando seguente per accedere allo Strumento di Configurazione Software di Raspberry Pi. (Puoi anche accedere al terminale tramite SSH.)

   .. code-block:: 

       sudo raspi-config

   .. image:: img/configuration_01.png
       :width: 100%

   .. raw:: html

       <br/><br/>

2. Vai alle **Opzioni di interfaccia**.

   .. note::
      Usa i tasti freccia ``up`` e ``down`` per spostare la selezione evidenziata tra le opzioni disponibili. Premendo il tasto freccia ``Select``, uscirai dal menu delle Opzioni e ti sposterai sui pulsanti ``<Select>`` e ``<Finish>``. Premendo ``left``, tornerai alle opzioni. In alternativa, puoi usare il tasto ``Tab`` per passare tra questi.

   .. image:: img/configuration_02.png
       :width: 100%

   .. raw:: html

       <br/><br/>

3. Seleziona **I2C**.

   .. image:: img/configuration_03.png
       :width: 100%

   .. raw:: html

       <br/><br/>

4. Scegli **<Sì>** per attivare l'interfaccia I2C, poi scegli **<Ok>**.

   .. image:: img/configuration_04.png
       :width: 100%

   .. raw:: html

       <br/><br/>

5. Seleziona **<Finish>** per uscire dallo Strumento di Configurazione Software di Raspberry Pi.

   .. image:: img/configuration_05.png
       :width: 100%

   .. raw:: html

       <br/><br/>

6. Verifica l'indirizzo del dispositivo I2C connesso utilizzando il comando seguente.

   .. code-block:: 

       i2cdetect -y 1      

   .. image:: img/configuration_06.png
       :width: 100%

   Gli indirizzi di eventuali dispositivi I2C connessi saranno mostrati.

   .. image:: img/configuration_07.png
       :width: 100%

   .. raw:: html

       <br/><br/>



.. _pi_enable_1wire:

Configurazione 1-Wire
-----------------------

Per abilitare la porta 1-Wire sul tuo Raspberry Pi, segui questi passaggi (salta se già abilitato; se non sei sicuro, procedi con le istruzioni).


1. Accedi al tuo Raspberry Pi, apri il Terminale e inserisci questo comando per accedere allo Strumento di Configurazione Software di Raspberry Pi. (Puoi anche accedere al terminale tramite SSH.)

   .. code-block:: 

       sudo raspi-config

   .. image:: img/configuration_08.png
       :width: 100%

   .. raw:: html

       <br/><br/>

2. Vai alle **Opzioni di interfaccia**.

   .. note::
      Usa i tasti freccia ``up`` e ``down`` per spostare la selezione evidenziata tra le opzioni disponibili. Premendo il tasto freccia ``destra``, uscirai dal menu delle Opzioni e ti sposterai sui pulsanti ``<Select>`` e ``<Finish>``. Premendo ``left``, tornerai alle opzioni. In alternativa, puoi usare il tasto ``Tab`` per passare tra questi.

   .. image:: img/configuration_09.png
       :width: 100%

   .. raw:: html

       <br/><br/>

3. Seleziona **1-Wire**.

   .. image:: img/configuration_10.png
       :width: 100%

   .. raw:: html

       <br/><br/>

4. Scegli **<Yes>** per attivare l'interfaccia 1-Wire, poi scegli **<Ok>**.

   .. image:: img/configuration_11.png
       :width: 100%

   .. raw:: html

       <br/><br/>

5. Seleziona **<Finish>** per uscire dallo Strumento di Configurazione Software di Raspberry Pi.

   .. image:: img/configuration_12.png
       :width: 100%

   .. raw:: html

       <br/><br/>

6. Seleziona **<yes>** per riavviare il Raspberry Pi.

   .. image:: img/configuration_13.png
       :width: 100%

   .. raw:: html

       <br/><br/>

