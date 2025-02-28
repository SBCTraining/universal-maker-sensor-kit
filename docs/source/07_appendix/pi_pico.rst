.. note:: 
    Bonjour, bienvenue à la communauté de passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres enthousiastes.

    **Pourquoi rejoindre ?**

    - **Support d'expert** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux nouvelles annonces de produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et des promotions lors des fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_pico_w:

Raspberry Pi Pico W
=======================================

.. image:: img/pico_w_side.png
    :width: 60%
    :align: center

Le Raspberry Pi Pico W apporte la connectivité sans fil à la ligne de produits Raspberry Pi Pico les plus vendus. Construit autour de notre plateforme en silicium RP2040, les produits Pico transmettent nos valeurs de haute performance, faible coût et facilité d'utilisation à l'espace des microcontrôleurs.

Le Raspberry Pi Pico W offre une prise en charge du LAN sans fil 802.11 b/g/n 2.4 GHz, avec une antenne intégrée et une certification de conformité modulaire. Il est capable de fonctionner à la fois en modes station et point d'accès. Un accès complet à la fonctionnalité réseau est disponible pour les développeurs C et MicroPython.

Le Raspberry Pi Pico W associe le RP2040 avec 2MB de mémoire flash et une puce d'alimentation prenant en charge des tensions d'entrée de 1.8–5.5V. Il offre 26 broches GPIO, dont trois peuvent fonctionner comme entrées analogiques, sur des plaquettes à trous passants de 0.1” avec des bords moulés.
Le Raspberry Pi Pico W est disponible à l'unité ou en bobines de 480 unités pour l'assemblage automatisé.

Caractéristiques
-------------------

* Format de 21 mm x 51 mm
* Puce microcontrôleur RP2040 conçue par Raspberry Pi au Royaume-Uni
* Processeur double-cœur Arm Cortex-M0+ flexible, fonctionnant jusqu'à 133 MHz
* 264kB de SRAM intégré
* 2MB de flash QSPI embarqué
* LAN sans fil 802.11n 2.4 GHz
* 26 broches GPIO multifonction, dont 3 entrées analogiques
* 2 x UART, 2 x contrôleurs SPI, 2 x contrôleurs I2C, 16 x canaux PWM
* 1 x contrôleur USB 1.1 et PHY, avec support hôte et périphérique
* 8 x machines à états de PIO programmables pour le support de périphériques personnalisés
* Alimentation prise en charge 1.8-5.5V DC
* Température de fonctionnement de -20°C à +70°C
* Module à bords moulés permettant de souder directement sur des cartes porteuses
* Programmation par glisser-déposer utilisant le stockage de masse via USB
* Modes de faible puissance sommeil et dormant
* Horloge précise sur puce
* Capteur de température
* Bibliothèques d'entiers accélérées et à virgule flottante sur puce

Les broches de Pico
-----------------------

.. image:: img/pico_pin.jpg
    :width: 100%
    :align: center

.. raw:: html

    <br/>

.. list-table::
    :widths: 3 5 10
    :header-rows: 1

    *   - Nom
        - Description
        - Fonction
    *   - GP0-GP28
        - Broches d'entrée/sortie polyvalentes
        - Agissent soit en entrée soit en sortie et n'ont pas de fonction fixe propre
    *   - GND
        - Masse de 0 volts
        - Plusieurs broches GND autour du Pico W pour faciliter le câblage.
    *   - RUN
        - Active ou désactive votre Pico
        - Démarrer et arrêter votre Pico W depuis un autre microcontrôleur.
    *   - GPxx_ADCx
        - Entrée/sortie polyvalente ou entrée analogique
        - Utilisée comme une entrée analogique ainsi que comme une entrée ou sortie numérique – mais pas les deux en même temps.
    *   - ADC_VREF
        - Référence de tension pour le convertisseur analogique-numérique (ADC)
        - Une broche d'entrée spéciale qui définit une tension de référence pour toutes les entrées analogiques.
    *   - AGND
        - Masse du convertisseur analogique-numérique (ADC) de 0 volts
        - Une connexion à la terre spéciale pour utilisation avec la broche ADC_VREF.
    *   - 3V3(O)
        - Alimentation de 3.3 volts
        - Une source d'alimentation de 3.3V, la même tension à laquelle votre Pico W fonctionne en interne, générée à partir de l'entrée VSYS.
    *   - 3v3(E)
        - Active ou désactive l'alimentation
        - Active ou désactive l'alimentation 3V3(O), peut également éteindre votre Pico W.
    *   - VSYS
        - Alimentation de 2-5 volts
        - Une broche directement connectée à l'alimentation interne de votre Pico, qui ne peut pas être désactivée sans également éteindre le Pico W.
    *   - VBUS
        - Alimentation de 5 volts
        - Une source d'alimentation de 5 V prise du port micro USB de votre Pico, et utilisée pour alimenter du matériel nécessitant plus de 3.3 V.

Le meilleur endroit pour trouver tout ce dont vous avez besoin pour commencer avec votre Raspberry Pi Pico W est `ici <https://www.raspberrypi.com/documentation/microcontrollers/raspberry-pi-pico.html>`_.

Ou vous pouvez cliquer sur les liens ci-dessous : 

* `Présentation du produit Raspberry Pi Pico W <https://datasheets.raspberrypi.com/picow/pico-w-product-brief.pdf>`_
* `Fiche technique du Raspberry Pi Pico W <https://datasheets.raspberrypi.com/picow/pico-w-datasheet.pdf>`_
* `Commencer avec Raspberry Pi Pico : Développement C/C++ <https://datasheets.raspberrypi.org/pico/getting-started-with-pico.pdf>`_
* `SDK C/C++ Raspberry Pi Pico <https://datasheets.raspberrypi.org/pico/raspberry-pi-pico-c-sdk.pdf>`_
* `Documentation Doxygen de niveau API pour le SDK C/C++ Raspberry Pi Pico <https://raspberrypi.github.io/pico-sdk-doxygen/>`_
* `SDK Python Raspberry Pi Pico <https://datasheets.raspberrypi.org/pico/raspberry-pi-pico-python-sdk.pdf>`_
* `Fiche technique du Raspberry Pi RP2040 <https://datasheets.raspberrypi.org/rp2040/rp2040-datasheet.pdf>`_
* `Conception matérielle avec RP2040 <https://datasheets.raspberrypi.org/rp2040/hardware-design-with-rp2040.pdf>`_
* `Fichiers de conception du Raspberry Pi Pico W <https://datasheets.raspberrypi.com/picow/RPi-PicoW-PUBLIC-20220607.zip>`_
* `Fichier STEP du Raspberry Pi Pico W <https://datasheets.raspberrypi.com/picow/PicoW-step.zip>`_
