.. note:: 

    Ciao, benvenuto nella community SunFounder su Facebook dedicata agli appassionati di Raspberry Pi, Arduino ed ESP32! Approfondisci l’uso di Raspberry Pi, Arduino ed ESP32 insieme ad altri utenti appassionati.

    **Perché unirsi?**

    - **Supporto esperto**: Risolvi problemi post-vendita e difficoltà tecniche grazie all’aiuto della community e del nostro team.
    - **Impara e condividi**: Scambia suggerimenti e tutorial per migliorare le tue competenze.
    - **Anteprime esclusive**: Accedi in anticipo agli annunci sui nuovi prodotti e alle anteprime.
    - **Sconti speciali**: Goditi sconti esclusivi sui nostri prodotti più recenti.
    - **Promozioni festive e giveaway**: Partecipa a promozioni festive e concorsi a premi.

    👉 Pronto a esplorare e creare con noi? Clicca su [|link_sf_facebook|] e unisciti subito!

.. _set_up_your_raspberry_pi:

Configura il tuo Raspberry Pi
===============================

Se hai uno schermo
---------------------------

Se possiedi uno schermo, sarà facile interagire con il Raspberry Pi.

**Componenti necessari**

* Qualsiasi modello di Raspberry Pi  
* 1 * Alimentatore  
* 1 * Scheda Micro SD  
* 1 * Alimentatore per schermo  
* 1 * Cavo HDMI  
* 1 * Schermo  
* 1 * Mouse  
* 1 * Tastiera

#. Inserisci la scheda SD con il sistema operativo Raspberry Pi nello slot micro SD situato nella parte inferiore del Raspberry Pi.

#. Collega mouse e tastiera.

#. Collega lo schermo alla porta HDMI del Raspberry Pi e assicurati che lo schermo sia alimentato e acceso.

   .. note::

      Se utilizzi un Raspberry Pi 4, collega lo schermo alla porta HDMI0 (la più vicina alla porta di alimentazione).

#. Usa l’alimentatore per accendere il Raspberry Pi. Dopo alcuni secondi, verrà mostrato il desktop del sistema operativo Raspberry Pi.

   .. image:: img/set_up_01.png
       :align: center

   .. raw:: html

       <br/>

#. Puoi avviare un browser web sul sistema Raspberry Pi e accedere a questa pagina del tutorial. In questo modo sarà facile copiare ed eseguire i comandi nel Terminale.

   .. image:: img/set_up_02.png
       :align: center

.. raw:: html

   <br/>

.. _no_screen:

Se non hai uno schermo
---------------------------

Se non hai un monitor, puoi accedere da remoto al tuo Raspberry Pi.

**Componenti necessari**

* Qualsiasi modello di Raspberry Pi  
* 1 * Alimentatore  
* 1 * Scheda Micro SD

Puoi utilizzare il comando SSH per accedere alla shell Bash del Raspberry Pi, che è l’interfaccia predefinita di Linux. Con la shell puoi svolgere la maggior parte delle operazioni tramite semplici comandi nei sistemi Unix/Linux.

Se preferisci non utilizzare la riga di comando, puoi sfruttare la funzione desktop remoto per accedere all’ambiente desktop del Raspberry Pi senza dover collegare uno schermo fisico.

Consulta i seguenti tutorial dettagliati per ciascun sistema operativo.


.. toctree::
   :maxdepth: 1

   03_a_remote_macosx
   03_b_remote_windows
   03_c_remote_linux

