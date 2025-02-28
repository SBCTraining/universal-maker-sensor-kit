.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder pour Raspberry Pi, Arduino et ESP32 sur Facebook ! Approfondissez vos connaissances sur Raspberry Pi, Arduino et ESP32 avec d'autres amateurs.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et des promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _cpn_l9110:

Module de commande de moteurs L9110
=========================================

Le module de commande de moteurs L9110 est compétent pour piloter deux moteurs simultanément. Il intègre une paire de puces de commande indépendantes L9110S, chaque canal offrant une sortie de courant stable jusqu'à 800mA.

Couvrant une plage de tension de 2,5V à 12V, le module s'accorde parfaitement avec les microcontrôleurs de 3,3V et 5V.

Servant de solution simplifiée, le module de commande de moteurs L9110 facilite le contrôle des moteurs dans un large éventail d'applications.
Grâce à son architecture à deux canaux, il permet l'orchestration indépendante de deux moteurs—idéal pour les projets nécessitant des opérations à deux moteurs.

Avec sa puissante sortie de courant continu, ce module alimente avec assurance des moteurs de petite à moyenne taille, ouvrant la voie à diverses entreprises robotiques, d'automatisation et centrées sur les moteurs. Sa large plage de tension offre en outre une adaptabilité, s'alignant sur diverses configurations d'alimentation électrique.

Conçu avec une facilité d'utilisation à l'esprit, le module propose des bornes d'entrée et de sortie intuitives, simplifiant les connexions aux microcontrôleurs ou dispositifs de contrôle similaires. De plus, il ne lésine pas sur la sécurité—des protections intégrées contre les surintensités et les surtempératures renforcent la fiabilité et la sécurité des opérations moteur.

.. image:: img/37_l9110_module.jpg
    :width: 80%
    :align: center
    
* **B-1A & B-1B(B-2A)**: Broches d'entrée pour contrôler la direction de rotation du moteur B.
* **A-1A & A-1B**: Broches d'entrée pour contrôler la direction de rotation du moteur A.
* **0A & OB(A)**: Broches de sortie du moteur A.
* **0A & OB(B)**: Broches de sortie du moteur B.
* **VCC**: Broche d'entrée d'alimentation (2.5V-12V).
* **GND**: Broche de masse.

**Caractéristiques**

* Puces de contrôle moteur L9110S intégrées
* Contrôle moteur à double canal.
* Contrôle indépendant de la direction de rotation des moteurs.
* Sortie de courant élevée (800mA par canal).
* Large plage de tension (2.5V-12V).
* Design compact.
* Bornes d'entrée et de sortie pratiques.
* Fonctions de protection intégrées.
* Applications polyvalentes.
* Taille du PCB : 29.2mm x 23mm
* Température de fonctionnement : -20°C ~ 80°C
* Indicateur LED de mise sous tension

.. _cpn_l9110_principle:

**Principe de fonctionnement**

Voici la table de vérité du moteur B :

Cette table de vérité montre les différents états du moteur B en fonction des valeurs des broches d'entrée B-1A et B-1B(B-2A). Elle indique la direction de rotation (dans le sens des aiguilles d'une montre ou dans le sens inverse), le freinage ou l'arrêt du moteur B.

.. list-table:: 
    :widths: 25 25 50
    :header-rows: 1

    * - B-1A
      - B-1B(B-2A)
      - État du moteur B
    * - 1
      - 0
      - Rotation dans le sens des aiguilles d'une montre
    * - 0
      - 1
      - Rotation dans le sens inverse des aiguilles d'une montre
    * - 0
      - 0
      - Frein
    * - 1
      - 1
      - Arrêt

Voici la table de vérité du moteur A :

Cette table de vérité montre les différents états du moteur A en fonction des valeurs des broches d'entrée A-1A et A-1B. Elle indique la direction de rotation (dans le sens des aiguilles d'une montre ou dans le sens inverse), le freinage ou l'arrêt du moteur A.

.. list-table:: 
    :widths: 25 25 50
    :header-rows: 1

    * - A-1A
      - A-1B
      - État du moteur A
    * - 1
      - 0
      - Rotation dans le sens des aiguilles d'une montre
    * - 0
      - 1
      - Rotation dans le sens inverse des aiguilles d'une montre
    * - 0
      - 0
      - Frein
    * - 1
      - 1
      - Arrêt

Exemple
---------------------------
* :ref:`uno_lesson31_pump` (Arduino UNO)
* :ref:`esp32_lesson31_pump` (ESP32)
* :ref:`pico_lesson31_pump` (Raspberry Pi Pico)
* :ref:`pi_lesson31_pump` (Raspberry Pi)

* :ref:`uno_lesson34_motor` (Arduino UNO)
* :ref:`esp32_lesson34_motor` (ESP32)
* :ref:`pico_lesson34_motor` (Raspberry Pi Pico)
* :ref:`pi_lesson34_motor` (Raspberry Pi)

* :ref:`uno_lesson07_speed` (Arduino UNO)
* :ref:`pi_lesson07_speed` (Raspberry Pi)

* :ref:`uno_lesson39_soap_dispenser` (Arduino UNO)
* :ref:`uno_lesson45_plant_monitor` (Arduino UNO)
* :ref:`esp32_soap_dispenser` (ESP32)
* :ref:`esp32_plant_monitor` (ESP32)
