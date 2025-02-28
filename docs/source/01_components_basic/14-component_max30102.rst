.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_max30102:

Module Capteur de Pouls et de Taux d'Oxygène Sanguin (MAX30102)
==================================================================

.. image:: img/14_gy_max30102_module.png
    :width: 200
    :align: center

.. raw:: html

   <br/>

Le MAX30102 est un module capteur avancé conçu pour le suivi du rythme cardiaque et des niveaux d'oxygène sanguin (SpO2). Fabriqué par Maxim Integrated, il combine la photopléthysmographie et le monitorage du rythme cardiaque dans un boîtier compact, le rendant populaire pour les applications de santé et de fitness portables.

Spécifications
---------------------------
* Type de puce : MAX30102
* Longueur d'onde de crête des LED : 660nm/880nm
* Tension d'alimentation : 3.3V ou 5V
* Type de signal de détection : Signal de réflexion optique (PPG)
* Interface de signal de sortie : Interface I2C
* Taille du PCB : 14 x 14mm
* Température de fonctionnement : -40 ~ +85℃

Brochage
---------------------------
* **VCC** : C'est l'entrée d'alimentation positive du contrôle principal.
* **GND** : Connexion à la terre.
* **SCL** : Broche d'horloge série pour l'interface I2C.
* **SDA** : Broche de données série pour l'interface I2C.
* **INT** : Broche d'interruption du CI.

Principe
---------------------------

Le MAX30102 est un capteur qui combine un oxymètre de pouls et un moniteur de fréquence cardiaque. C'est un capteur optique qui mesure l'absorption du sang pulsatile à travers un photodétecteur après avoir émis deux longueurs d'onde lumineuses provenant de deux LED - une rouge et une infrarouge. Cette combinaison particulière de couleurs de LED est conçue pour permettre la lecture des données au bout du doigt.

Le MAX30102 fonctionne en projetant les deux lumières sur le doigt ou le lobe de l'oreille (ou essentiellement n'importe où la peau n'est pas trop épaisse, permettant aux deux lumières de pénétrer facilement le tissu) et en mesurant la quantité de lumière réfléchie à l'aide d'un photodétecteur. Cette méthode de détection des pulsations par la lumière s'appelle la Photopléthysmographie.

Le fonctionnement du MAX30102 peut être divisé en deux parties : Mesure du rythme cardiaque et Oxymétrie de pouls (mesure du niveau d'oxygène dans le sang).

Mesure du rythme cardiaque
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
L'hémoglobine oxygénée (HbO2) dans le sang artériel a la caractéristique d'absorber la lumière IR. Plus le sang est rouge (plus l'hémoglobine est élevée), plus la lumière IR est absorbée. À mesure que le sang est pompé à travers le doigt à chaque battement de cœur, la quantité de lumière réfléchie change, créant une onde changeante à la sortie du photodétecteur. En continuant à projeter de la lumière et à prendre des lectures de photodétecteur, vous commencez rapidement à obtenir une lecture du pouls cardiaque (HR).


Oxymétrie de pouls
^^^^^^^^^^^^^^^^^^^^
L'oxymétrie de pouls est basée sur le principe que la quantité de lumière ROUGE et IR absorbée varie selon la quantité d'oxygène dans votre sang.

Exemple
---------------------------
* :ref:`uno_lesson14_max30102` (Arduino UNO)
* :ref:`esp32_lesson14_max30102` (ESP32)
* :ref:`pico_lesson14_max30102` (Raspberry Pi Pico)
* :ref:`pi_lesson14_max30102` (Raspberry Pi)

* :ref:`uno_lesson41_heartrate_monitor` (Arduino UNO)
* :ref:`esp32_heartrate_monitor` (ESP32)