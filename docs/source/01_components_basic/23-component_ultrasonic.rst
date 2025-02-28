.. note::

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Approfondissez votre compréhension des Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès en avant-première aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions festives.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_ultrasonic:

Module de Capteur Ultrasonique (HC-SR04)
===========================================

.. image:: img/23_ultrasonic.png
    :width: 350
    :align: center

.. raw:: html

   <br/>

Le module ultrasonique HC-SR04 est un capteur qui peut mesurer des distances de 2 cm à 400 cm en utilisant des ondes ultrasoniques. Il est couramment utilisé dans les projets de robotique et d'automatisation pour détecter des objets et mesurer des distances. Le module est composé d'un émetteur et d'un récepteur ultrasoniques, qui travaillent ensemble pour envoyer et recevoir des ondes ultrasoniques.

.. _cpn_ultrasonic_principle:

Principe
----------------------------
Le module comprend des émetteurs ultrasoniques, un récepteur et un circuit de contrôle. Les principes de base sont les suivants :

1. Utilisez un basculeur IO pour traiter un signal de haut niveau d'au moins 10us.

2. Le module envoie automatiquement huit signaux de 40 kHz et détecte s'il y a un retour de signal d'impulsion.

3. Si le signal revient, passant à haut niveau, la durée de sortie IO haute est le temps écoulé depuis l'émission de l'onde ultrasonique jusqu'à son retour. Ici, la distance testée = (temps haut x vitesse du son (340 m/s) / 2.

Le diagramme de chronométrage est montré ci-dessous.

.. image:: img/23_ultrasonic_principle.png

Vous devez seulement fournir une impulsion courte de 10us pour l'entrée de 
déclenchement pour commencer la mesure, puis le module émet une rafale de 
8 cycles d'ultrasons à 40 kHz et augmente son écho. Vous pouvez calculer la 
distance à travers l'intervalle de temps entre l'envoi du signal de déclenchement 
et la réception du signal d'écho.

.. note::
    Il est recommandé d'utiliser un cycle de mesure supérieur à 60 ms afin de prévenir les collisions de signaux entre le signal de déclenchement et le signal d'écho.

Formule : 
    - us / 58 = centimètres 
    - us / 148 = pouces
    - distance = temps de haut niveau * vitesse du son (340m/s) / 2; 


Exemple
---------------------------
* :ref:`uno_lesson23_ultrasonic` (Arduino UNO)
* :ref:`esp32_lesson23_ultrasonic` (ESP32)
* :ref:`pico_lesson23_ultrasonic` (Raspberry Pi Pico)
* :ref:`pi_lesson23_ultrasonic` (Raspberry Pi)

* :ref:`uno_lesson37_trashcan` (Arduino UNO)

* :ref:`esp32_trashcan` (ESP32)