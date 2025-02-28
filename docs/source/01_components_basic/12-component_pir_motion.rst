.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans les univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_pir_motion:

Module de Détection de Mouvement PIR (HC-SR501)
====================================================

.. image:: img/12_pir_module.png
    :width: 300
    :align: center


Le capteur de mouvement infrarouge passif (PIR) est un capteur qui détecte les mouvements. Il est couramment utilisé dans les systèmes de sécurité et les systèmes d'éclairage automatique. Le capteur dispose de deux fentes qui détectent le rayonnement infrarouge. Lorsqu'un objet, tel qu'une personne, passe devant le capteur, celui-ci détecte un changement dans la quantité de rayonnement infrarouge et déclenche un signal de sortie.

Spécifications
---------------------------
* Tension d'alimentation : 5V~20V; 
* Sortie : Par défaut basse ; devient haute lorsqu'une personne passe.
* Temps de retard : 5~200s (réglable)
* Temps de blocage : 8s
* Portée de détection : <120°, jusqu'à 7 mètres (réglable)
* Mode de déclenchement : L Déclenchement non répétable, H Déclenchement répétable
* Taille du PCB : 32 x 24mm
* Taille de la lentille : 23mm
* Température de fonctionnement : -15~+70℃


Brochage
---------------------------
* **VCC** : C'est l'entrée d'alimentation positive du contrôle principal.
* **GND** : Connexion à la terre.
* **DO** : Sortie numérique. Par défaut basse ; devient haute lorsqu'une personne passe.

Principe
---------------------------
Le capteur PIR est divisé en deux fentes connectées à un amplificateur différentiel. Lorsqu'un objet stationnaire se trouve devant le capteur, les deux fentes reçoivent la même quantité de rayonnement et la sortie est nulle. Lorsqu'un objet en mouvement se trouve devant le capteur, l'une des fentes reçoit plus de rayonnement que l'autre, ce qui fait fluctuer la sortie haut ou bas. Ce changement de tension de sortie est le résultat de la détection de mouvement.

.. image:: img/12_pir_working_principle.jpg
    :width: 500
    :align: center

Après le câblage du module de détection, il y a une initialisation d'une minute. Pendant l'initialisation, le module peut émettre une sortie 0 à 3 fois à intervalles. Ensuite, le module sera en mode veille. Veuillez éloigner toute source de lumière et d'autres sources d'interférence de la surface du module afin d'éviter les erreurs de fonctionnement causées par le signal interférant. Il est même préférable d'utiliser le module sans trop de vent, car le vent peut également interférer avec le capteur.

.. image:: img/12_pir_module_back.png
    :width: 350
    :align: center

.. raw:: html
    
    <br/><br/> 

Réglage de la Distance
^^^^^^^^^^^^^^^^^^^^^^^^^
En tournant le bouton du potentiomètre de réglage de distance dans le sens des aiguilles d'une montre, la portée de la distance de détection augmente, et la distance maximale de détection est d'environ 0 à 7 mètres. Si vous le tournez dans le sens inverse des aiguilles d'une montre, la portée de la distance de détection diminue, et la distance minimale de détection est d'environ 0 à 3 mètres.

Réglage du Délai
^^^^^^^^^^^^^^^^^^^^
En tournant le bouton du potentiomètre de réglage du délai dans le sens des aiguilles d'une montre, vous verrez également le délai de détection augmenter. Le maximum du délai de détection peut atteindre jusqu'à 300s. Au contraire, si vous le tournez dans le sens inverse des aiguilles d'une montre, vous pouvez raccourcir le délai avec un minimum de 5s.

Deux Modes de Déclenchement
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Choisir différents modes en utilisant le capuchon de cavalier.

* H : Mode de déclenchement répétable, après la détection du corps humain, le module émet un niveau haut. Pendant la période de délai suivante, si quelqu'un entre dans la portée de détection, la sortie restera à un niveau haut.
* L : Mode de déclenchement non répétable, émet un niveau haut lorsqu'il détecte le corps humain. Après le délai, la sortie passe automatiquement du niveau haut au niveau bas.

Exemple
---------------------------
* :ref:`uno_lesson12_pir_motion` (Arduino UNO)
* :ref:`esp32_lesson12_pir_motion` (ESP32)
* :ref:`pico_lesson12_pir_motion` (Raspberry Pi Pico)
* :ref:`pi_lesson12_pir_motion` (Raspberry Pi)

* :ref:`uno_lesson40_motion_triggered_relay` (Arduino UNO)
* :ref:`uno_iot_intrusion_alert_system` (Arduino UNO)
* :ref:`esp32_motion_triggered_relay` (ESP32)
* :ref:`esp32_iot_intrusion_alert_system` (ESP32)