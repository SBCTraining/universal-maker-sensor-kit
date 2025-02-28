.. note:: 
    Bonjour, bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes post-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux avant-premières.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêts à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _cpn_mpu6050:

Module Gyroscope & Accéléromètre (MPU6050)
===============================================================

.. image:: img/05_mpu6050_1.png
    :width: 300
    :align: center

.. raw:: html

   <br/>

Le MPU-6050 est un dispositif de suivi de mouvement à 6 axes (combinant un gyroscope à 3 axes et un accéléromètre à 3 axes). Il détecte les changements de mouvement, d'accélération et de rotation. Il est couramment utilisé dans la robotique, les manettes de jeux et d'autres dispositifs électroniques nécessitant une détection de mouvement. Sa haute précision et son coût réduit en font un favori dans la communauté DIY.

Principe
---------------------------
Un module de capteur MPU-6050 est composé d'un accéléromètre à 3 axes et d'un gyroscope à 3 axes.

Ses trois systèmes de coordonnées sont définis comme suit :

Placez le MPU6050 à plat sur une table, assurez-vous que la face avec l'étiquette est vers le haut et qu'un point sur cette surface est dans le coin supérieur gauche. Ensuite, la direction verticale vers le haut est l'axe z du capteur. La direction de gauche à droite est considérée comme l'axe X. En conséquence, la direction de l'arrière vers l'avant est définie comme l'axe Y.

.. image:: img/05_mpu_2.png
    :width: 300
    :align: center

Accéléromètre à 3 axes
^^^^^^^^^^^^^^^^^^^^^^^^^^
L'accéléromètre fonctionne sur le principe de l'effet piézoélectrique, la capacité de certains matériaux à générer une charge électrique en réponse à une contrainte mécanique appliquée.

Imaginez ici une boîte cuboïdale contenant une petite balle à l'intérieur, comme sur l'image ci-dessus. Les parois de cette boîte sont faites de cristaux piézoélectriques. Lorsque vous inclinez la boîte, la balle est forcée de se déplacer dans la direction de l'inclinaison, due à la gravité. La paroi avec laquelle la balle entre en collision crée de petits courants piézoélectriques. Il y a en tout, trois paires de parois opposées dans un cuboïde. Chaque paire correspond à un axe dans l'espace 3D : les axes X, Y et Z. Selon le courant produit par les parois piézoélectriques, nous pouvons déterminer la direction de l'inclinaison et son amplitude.

.. image:: img/05_mpu_3.png
    :width: 800
    :align: center

Nous pouvons utiliser le MPU6050 pour détecter son accélération sur chaque axe coordonné (dans l'état de bureau stationnaire, l'accélération de l'axe Z est de 1 unité de gravité, et les axes X et Y sont à 0). S'il est incliné ou dans une condition de poids nul/surpoids, la lecture correspondante changera.

Il existe quatre gammes de mesure qui peuvent être sélectionnées par programmation : +/-2g, +/-4g, +/-8g, et +/-16g (2g par défaut) correspondant à chaque précision. Les valeurs vont de -32768 à 32767.

La lecture de l'accéléromètre est convertie en une valeur d'accélération en mappant la lecture de la plage de lecture à la plage de mesure.

Accélération = (Donnée brute de l'axe de l'accéléromètre / 65536 * plage d'accélération à échelle complète) g

Prenons l'axe X comme exemple, lorsque la donnée brute de l'accéléromètre de l'axe X est 16384 et que la plage est sélectionnée comme +/-2g :

Accélération le long de l'axe X = (16384 / 65536 * 4) g =1g

Gyroscope à 3 axes
^^^^^^^^^^^^^^^^^^^^
Les gyroscopes fonctionnent sur le principe de l'accélération de Coriolis. Imaginez qu'il y a une structure en forme de fourche qui est en mouvement constant de va-et-vient. Elle est maintenue en place à l'aide de cristaux piézoélectriques. Chaque fois que vous essayez d'incliner cet agencement, les cristaux subissent une force dans la direction de l'inclinaison. Ceci est causé par l'inertie de la fourche en mouvement. Les cristaux produisent ainsi un courant en accord avec l'effet piézoélectrique, et ce courant est amplifié.

.. image:: img/05_mpu_4.png
    :width: 800
    :align: center

Le gyroscope a également quatre types de gammes de mesure : +/- 250, +/- 500, +/- 1000, +/- 2000. La méthode de calcul et l'accélération sont essentiellement cohérentes.

La formule pour convertir la lecture en vitesse angulaire est la suivante :

Vitesse angulaire = (Donnée brute de l'axe du gyroscope / 65536 * plage du gyroscope à échelle complète) °/s

Pour l'axe X, par exemple, la donnée brute de l'accéléromètre de l'axe X est 16384 et la plage est +/- 250°/s :

Vitesse angulaire le long de l'axe X = (16384 / 65536 * 500)°/s =125°/s

Exemple
---------------------------
* :ref:`uno_lesson05_mpu6050` (Arduino UNO)
* :ref:`esp32_lesson05_mpu6050` (ESP32)
* :ref:`pico_lesson05_mpu6050` (Raspberry Pi Pico)
* :ref:`pi_lesson05_mpu6050` (Raspberry Pi Pi)

* :ref:`uno_lesson52_tilt_direction_indicator` (Arduino UNO)




