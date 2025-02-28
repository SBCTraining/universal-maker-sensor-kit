.. note:: 
    Bonjour, bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_flame:

Module Capteur de Flamme
============================

.. image:: img/03_flame_module.png
    :width: 400
    :align: center

.. raw:: html

   <br/>

.. tip::
   Gardez une distance spécifique entre le capteur et la flamme pour éviter les dommages dus aux hautes températures.

.. note::
   **Avis** : En raison d'une erreur de production, certains des capteurs de flamme inclus dans nos kits peuvent être la version à 3 broches, qui manque de la sortie analogique (AO). Cette version convient à la plupart des projets et n'affecte pas l'utilisation générale. Si vous avez besoin de la version à 4 broches, veuillez contacter notre service clientèle à service@sunfounder.com. Nous fournirons un remplacement gratuit pour répondre à vos besoins.

Le capteur de flamme est un capteur capable de détecter la présence de feu ou de flammes. Le capteur de flamme fonctionne sur la base du rayonnement infrarouge. Le photodiode IR détectera le rayonnement IR de tout corps chaud. Cette valeur est ensuite comparée à une valeur de référence. Une fois que le rayonnement atteint la valeur seuil, le capteur change sa sortie en conséquence. Il est largement utilisé dans les systèmes de détection d'incendie dans les maisons et les industries.

Le capteur de flamme fonctionne sur le principe de la détection infrarouge (IR). Le capteur dispose d'un récepteur IR qui détecte le rayonnement IR émis par les flammes. Lorsqu'un feu brûle, il émet une petite quantité de lumière infrarouge, cette lumière est reçue par le photodiode (récepteur IR) sur le module du capteur. Ensuite, nous utilisons un amplificateur opérationnel pour vérifier un changement de tension à travers le récepteur IR, de sorte que si un feu est détecté, la broche de sortie (DO) donnera 0V(LOW), et si il n'y a pas de feu, la broche de sortie sera à 5V(HIGH).

Spécifications
---------------------------
* Tension d'alimentation : 3,3V - 5V
* Taille du PCB : 31 x 14mm
* Type de signal de sortie : DO et AO
* Angle de détection : 60 degrés


Brochage
---------------------------
* **VCC** : C'est l'entrée d'alimentation positive provenant du contrôle principal.
* **GND** : Connexion à la terre.
* **DO** : Sortie numérique. Elle indique la présence d'une flamme. Lorsque le rayonnement infrarouge dépasse la valeur seuil (réglée par le potentiomètre), DO devient LOW ; sinon, il reste HIGH.
* **AO** : Sortie analogique. Elle génère une tension de sortie qui est inversement proportionnelle à l'intensité du rayonnement infrarouge (taille de la flamme). Ainsi, un rayonnement infrarouge plus élevé entraînera une tension plus basse, tandis qu'un rayonnement infrarouge plus faible entraînera une tension plus élevée.


Schéma
---------------------------

.. image:: img/03_flame_module_schematic.png
    :width: 100%
    :align: center

.. raw:: html

   <br/>

Exemple
---------------------------
* :ref:`uno_lesson03_flame` (Arduino UNO)
* :ref:`esp32_lesson03_flame` (ESP32)
* :ref:`pico_lesson03_flame` (Raspberry Pi Pico)
* :ref:`pi_lesson03_flame` (Raspberry Pi)
* :ref:`uno_iot_flame` (Arduino UNO)