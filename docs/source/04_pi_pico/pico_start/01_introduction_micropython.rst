.. note:: 

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers de Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et à des promotions festives.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

Introduction à MicroPython
======================================

MicroPython est une implémentation logicielle d'un langage de programmation largement compatible avec Python 3, écrit en C, optimisé pour fonctionner sur un microcontrôleur.

MicroPython comprend un compilateur Python pour bytecode et un interpréteur d'exécution de ce bytecode. L'utilisateur est confronté à une invite interactive (le REPL) pour exécuter immédiatement les commandes prises en charge. Une sélection de bibliothèques Python de base est incluse ; MicroPython intègre des modules qui donnent au programmeur accès au matériel de bas niveau.

* Référence : `MicroPython - Wikipedia <https://en.wikipedia.org/wiki/MicroPython>`_

L'histoire commence ici
--------------------------------

Tout a changé en 2013 lorsque Damien George a lancé une campagne de financement participatif (Kickstarter).

Damien était étudiant de premier cycle à l'université de Cambridge et un programmeur de robotique passionné. Il voulait réduire le monde de Python d'une machine de gigaoctets à un kilooctet. Sa campagne Kickstarter visait à soutenir son développement pendant qu'il transformait son concept en une mise en œuvre achevée.

MicroPython est soutenu par une communauté diversifiée de Pythonistas qui ont un vif intérêt à voir le projet réussir.

Outre les tests et le soutien de la base de code, les développeurs ont fourni des tutoriels, des bibliothèques de code et le portage du matériel, permettant ainsi à Damien de se concentrer sur d'autres aspects du projet.

* Référence : `realpython <https://realpython.com/micropython/>`_


Pourquoi MicroPython ?
-------------------------

Bien que la campagne Kickstarter originale ait lancé MicroPython en tant que carte de développement "pyboard" avec STM32F4, MicroPython prend en charge de nombreuses architectures de produits basées sur ARM. Les ports principaux pris en charge sont ARM Cortex-M (de nombreuses cartes STM32, TI CC3200/WiPy, cartes Teensy, série Nordic nRF, SAMD21 et SAMD51), ESP8266, ESP32, PIC 16 bits, Unix, Windows, Zephyr et JavaScript.
De plus, MicroPython permet une rétroaction rapide. Cela est dû au fait que vous pouvez utiliser REPL pour entrer des commandes de manière interactive et obtenir des réponses. Vous pouvez même modifier le code et l'exécuter immédiatement au lieu de traverser le cycle code-compiler-télécharger-exécuter.

Bien que Python offre les mêmes avantages, pour certaines cartes microcontrôleurs comme le Raspberry Pi Pico, elles sont petites, simples et disposent de peu de mémoire pour exécuter le langage Python en totalité. C'est pourquoi MicroPython a évolué, conservant les principales fonctionnalités de Python et en ajoutant de nouvelles pour travailler avec ces cartes microcontrôleurs.

Vous apprendrez ensuite à installer MicroPython sur le Raspberry Pi Pico.
