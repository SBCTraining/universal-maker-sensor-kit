.. note::
    Bonjour et bienvenue dans la communauté Facebook des passionnés de SunFounder Raspberry Pi, Arduino, et ESP32 ! Plongez plus profondément dans l'univers des Raspberry Pi, Arduino, et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux nouvelles annonces de produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions de vacances.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_esp32_wroom_32e:

ESP32 WROOM 32E
==================

L'ESP32 WROOM-32E est un module polyvalent et puissant construit autour du chipset ESP32 d'Espressif. Il offre un traitement bicœur, une connectivité Wi-Fi et Bluetooth intégrée, et dispose d'une large gamme d'interfaces périphériques. Connu pour sa faible consommation d'énergie, ce module est idéal pour les applications IoT, permettant une connectivité intelligente et des performances robustes dans des formats compacts.

.. image:: img/esp32_wroom_32e.png
    :width: 60%
    :align: center


Caractéristiques clés :

* **Puissance de traitement** : Il est équipé d'un microprocesseur bicœur Xtensa® 32 bits LX6, offrant évolutivité et flexibilité.
* **Capacités sans fil** : Avec le Wi-Fi 2,4 GHz intégré et le Bluetooth en mode dual, il est parfaitement adapté aux applications exigeant une communication sans fil stable.
* **Mémoire et stockage** : Il est doté d'une SRAM abondante et d'un stockage flash haute performance, répondant aux besoins de stockage de programmes utilisateurs et de données.
* **GPIO** : Offrant jusqu'à 38 broches GPIO, il prend en charge une variété de dispositifs externes et de capteurs.
* **Consommation d'énergie faible** : Plusieurs modes d'économie d'énergie sont disponibles, ce qui le rend idéal pour les scénarios alimentés par batterie ou à efficacité énergétique.
* **Sécurité** : Des fonctionnalités de chiffrement et de sécurité intégrées garantissent que les données des utilisateurs et leur vie privée sont bien protégées.
* **Polyvalence** : Des appareils ménagers simples aux machines industrielles complexes, le WROOM-32E offre des performances cohérentes et efficaces.

En résumé, l'ESP32 WROOM-32E offre non seulement des capacités de traitement robustes et diverses options de connectivité, mais aussi une gamme de fonctionnalités qui en font un choix privilégié dans les secteurs de l'IoT et des dispositifs intelligents.

* |link_esp32_datasheet|

.. _esp32_pinout:

Schéma des broches
---------------------

L'ESP32 présente certaines limitations d'utilisation des broches en raison du partage de certaines fonctionnalités sur des broches spécifiques. Lors de la conception d'un projet, il est judicieux de planifier soigneusement l'utilisation des broches et de vérifier les conflits potentiels pour garantir un fonctionnement correct et éviter les problèmes.


.. image:: img/esp32_pinout.jpg
    :width: 100%
    :align: center

Voici certaines des restrictions et considérations clés :

* **ADC1 et ADC2** : ADC2 ne peut pas être utilisé lorsque le WiFi ou le Bluetooth est actif. Cependant, ADC1 peut être utilisé sans restrictions.
* **Broches de démarrage** : GPIO0, GPIO2, GPIO5, GPIO12 et GPIO15 sont utilisées pour le démarrage pendant le processus de boot. Il convient de ne pas connecter de composants externes qui pourraient interférer avec le processus de boot sur ces broches.
* **Broches JTAG** : GPIO12, GPIO13, GPIO14 et GPIO15 peuvent être utilisées comme broches JTAG pour le débogage. Si le débogage JTAG n'est pas nécessaire, ces broches peuvent être utilisées comme GPIO normales.
* **Broches tactiles** : Certaines broches prennent en charge les fonctionnalités tactiles. Ces broches doivent être utilisées avec précaution si vous souhaitez les utiliser pour la détection tactile.
* **Broches d'alimentation** : Certaines broches sont réservées aux fonctions liées à l'alimentation et doivent être utilisées en conséquence. Par exemple, évitez de tirer un courant excessif des broches d'alimentation comme 3V3 et GND.
* **Broches uniquement en entrée** : Certaines broches sont uniquement en entrée et ne doivent pas être utilisées comme sorties.


.. _esp32_strapping:

Broches de strapping
-----------------------

L'ESP32 dispose de cinq broches de strapping :

.. list-table::
    :widths: 5 15
    :header-rows: 1

    *   - Broches de Strapping
        - Description
    *   - IO5
        - Par défaut en pull-up, le niveau de tension de IO5 et IO15 affecte le timing de l'esclave SDIO.
    *   - IO0
        - Par défaut en pull-up, si mis à bas, il entre en mode téléchargement.
    *   - IO2
        - Par défaut en pull-down, IO0 et IO2 feront entrer l'ESP32 en mode téléchargement.
    *   - IO12(MTDI)
        - Par défaut en pull-down, si mis à haut, l'ESP32 ne démarrera pas normalement.
    *   - IO15(MTDO)
        - Par défaut en pull-up, si mis à bas, le journal de débogage ne sera pas visible. De plus, le niveau de tension de IO5 et IO15 affecte le timing de l'esclave SDIO.

Le logiciel peut lire les valeurs de ces cinq bits depuis le registre "GPIO_STRAPPING". Pendant la libération du reset du système du chip (power-on-reset, reset du watchdog RTC et brownout reset), les verrous des broches de strapping échantillonnent le niveau de tension comme bits de strapping de "0" ou "1", et conservent ces bits jusqu'à ce que le chip soit alimenté ou éteint. Les bits de strapping configurent le mode de boot du dispositif, la tension de fonctionnement de VDD_SDIO et d'autres paramètres système initiaux.

Chaque broche de strapping est connectée à sa résistance de pull-up/pull-down interne pendant le reset du chip. En conséquence, si une broche de strapping n'est pas connectée ou si le circuit externe connecté est à haute impédance, la pull-up/pull-down interne faible déterminera le niveau d'entrée par défaut des broches de strapping.

Pour changer les valeurs des bits de strapping, les utilisateurs peuvent appliquer des résistances de pull-down/pull-up externes, ou utiliser les GPIOs du MCU hôte pour contrôler le niveau de tension de ces broches lors de l'allumage de l'ESP32.

Après la libération du reset, les broches de strapping fonctionnent comme des broches à fonction normale.
Reportez-vous au tableau suivant pour une configuration détaillée du mode de boot par les broches de strapping.

.. image:: img/esp32_strapping.png
   :width: 100%
   :align: center

* FE : front descendant, RE : front montant
* Le firmware peut configurer les bits de registre pour changer les paramètres de "Tension de l'LDO interne (VDD_SDIO)" et "Timing de l'esclave SDIO", après le démarrage.
* Le module intègre un flash SPI de 3,3 V, donc la broche MTDI ne peut pas être mise à 1 lorsque le module est alimenté.
