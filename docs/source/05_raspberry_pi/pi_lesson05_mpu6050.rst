.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez encore plus profondément dans l'univers du Raspberry Pi, Arduino et ESP32 aux côtés d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et vos défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour perfectionner vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et à des aperçus.
    - **Réductions spéciales** : Bénéficiez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à nos concours et promotions spéciales durant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pi_lesson05_mpu6050:

Leçon 05 : Module Gyroscope & Accéléromètre (MPU6050)
==========================================================

Dans cette leçon, vous apprendrez à interfacer le Raspberry Pi avec le MPU6050, un capteur qui intègre un gyroscope à 3 axes et un accéléromètre. Vous découvrirez comment mesurer l'accélération, l'orientation et la rotation. Ce projet vous offrira une expérience pratique en lecture de données de capteurs, en utilisation de Python pour l'interaction avec le matériel et en compréhension des bases de la communication I2C. Vous apprendrez également à capturer en continu l'accélération sur trois axes, la vitesse de rotation et la température à partir du capteur. C'est un excellent point de départ pour les débutants désireux de se plonger dans l'univers des capteurs et du suivi de mouvement avec le Raspberry Pi.

Composants nécessaires
--------------------------

Pour ce projet, vous aurez besoin des composants suivants.

Il est très pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DANS CE KIT
        - Lien
    *   - Kit de capteurs Universal Maker
        - 94
        - |link_umsk|

Vous pouvez aussi acheter les composants séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - Raspberry Pi 5
        - \-
    *   - :ref:`cpn_mpu6050`
        - |link_mpu6050_buy|


Câblage
---------------------------

.. image:: img/Lesson_05_mpu6050_pi_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   # Importation de la classe mpu6050 et de la fonction sleep des modules respectifs.
   from mpu6050 import mpu6050
   from time import sleep
   
   # Initialisation du capteur MPU-6050 avec l'adresse I2C 0x68.
   sensor = mpu6050(0x68)
   
   # Boucle infinie pour lire continuellement les données du capteur.
   while True:
       # Récupérer les données de l'accéléromètre.
       accel_data = sensor.get_accel_data()
       # Récupérer les données du gyroscope.
       gyro_data = sensor.get_gyro_data()
       # Récupérer les données de température.
       temp = sensor.get_temp()
   
       # Afficher les données de l'accéléromètre.
       print("Accelerometer data")
       print("x: " + str(accel_data['x']))
       print("y: " + str(accel_data['y']))
       print("z: " + str(accel_data['z']))
   
       # Afficher les données du gyroscope.
       print("Gyroscope data")
       print("x: " + str(gyro_data['x']))
       print("y: " + str(gyro_data['y']))
       print("z: " + str(gyro_data['z']))
   
       # Afficher la température en Celsius.
       print("Temp: " + str(temp) + " C")
   
       # Pause de 0.5 seconde avant le prochain cycle de lecture.
       sleep(0.5)


Analyse du code
---------------------------

#. Importation des bibliothèques

   La classe ``mpu6050`` est importée depuis la bibliothèque ``mpu6050``, et la fonction ``sleep`` provient du module ``time``. Ces importations sont nécessaires pour interagir avec le capteur MPU-6050 et introduire des délais dans le code.

   Pour plus d'informations sur la bibliothèque ``mpu6050``, veuillez consulter |link_mpu6050_python_driver|.

   .. code-block:: python

      from mpu6050 import mpu6050
      from time import sleep

#. Initialisation du capteur

   Une instance de la classe ``mpu6050`` est créée avec l'adresse I2C 0x68 (l'adresse par défaut du capteur MPU-6050). Cette étape initialise le capteur pour la lecture des données.

   .. code-block:: python

      sensor = mpu6050(0x68)

#. Boucle infinie pour une lecture continue

   Une boucle infinie (``while True``) est utilisée pour lire en continu les données du capteur. Cela est courant dans les applications basées sur des capteurs où une surveillance constante est nécessaire.

   .. code-block:: python

      while True:

#. Lecture des données du capteur

   À l'intérieur de la boucle, les données de l'accéléromètre, du gyroscope et du capteur de température sont récupérées à l'aide des méthodes ``get_accel_data``, ``get_gyro_data`` et ``get_temp`` de l'instance de la classe ``mpu6050``. Ces méthodes retournent les données du capteur sous un format facilement exploitable.

   .. code-block:: python

      accel_data = sensor.get_accel_data()
      gyro_data = sensor.get_gyro_data()
      temp = sensor.get_temp()

#. Affichage des données du capteur

   Les données récupérées sont ensuite affichées. Les données de l'accéléromètre et du gyroscope sont accessibles sous forme de valeurs de dictionnaire (axes x, y, z), et la température est directement affichée en tant que valeur en Celsius.

   .. code-block:: python

      print("Accelerometer data")
      print("x: " + str(accel_data['x']))
      print("y: " + str(accel_data['y']))
      print("z: " + str(accel_data['z']))

      print("Gyroscope data")
      print("x: " + str(gyro_data['x']))
      print("y: " + str(gyro_data['y']))
      print("z: " + str(gyro_data['z']))

      print("Temp: " + str(temp) + " C")

#. Délai entre les lectures

   Enfin, un délai de 0,5 seconde est ajouté grâce à ``sleep(0.5)``, afin de ne pas surcharger le Raspberry Pi avec des lectures de données trop rapides.

   .. code-block:: python

      sleep(0.5)