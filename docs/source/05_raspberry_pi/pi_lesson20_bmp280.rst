.. note::
    Bonjour, bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans l'univers des Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions festives.

    👉 Prêts à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _pi_lesson20_bmp280:

Leçon 20 : Capteur de température, d'humidité et de pression (BMP280)
=========================================================================

Dans cette leçon, vous apprendrez à connecter et lire les données d'un capteur BMP280 qui mesure la température, l'humidité et la pression à l'aide d'un Raspberry Pi. Vous configurerez le capteur et écrirez un script Python pour mesurer les données environnementales incluant la température, la pression atmosphérique et l'altitude.

Composants nécessaires
--------------------------

Pour ce projet, nous aurons besoin des composants suivants.

Il est certainement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ÉLÉMENTS DE CE KIT
        - LIEN
    *   - Kit universel de capteurs pour créateurs
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 10
    :header-rows: 1

    *   - Présentation des composants
        - Lien d'achat

    *   - Raspberry Pi 5
        - \-
    *   - :ref:`cpn_bmp280`
        - |link_bmp280_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
------------

.. image:: img/Lesson_20_bmp280_pi_bb.png
    :width: 100%


Installation de la bibliothèque
----------------------------------

.. note::
    La bibliothèque adafruit-circuitpython-bmp280 dépend de Blinka, donc assurez-vous que Blinka a été installé. Pour installer les bibliothèques, référez-vous à :ref:`install_blinka`.

Avant d'installer la bibliothèque, assurez-vous que l'environnement Python virtuel est activé :

.. code-block:: bash

   source ~/env/bin/activate

Installez la bibliothèque adafruit-circuitpython-bmp280 :

.. code-block:: bash

   pip install adafruit-circuitpython-bmp280


Exécution du code
---------------------

.. note::
   - Assurez-vous d'avoir installé la bibliothèque Python nécessaire pour exécuter le code selon les étapes "Installation de la bibliothèque".
   - Avant d'exécuter le code, assurez-vous que l'environnement Python virtuel avec Blinka installé est activé. Vous pouvez activer l'environnement virtuel en utilisant une commande comme celle-ci :

     .. code-block:: bash
  
        source ~/env/bin/activate

   - Trouvez le code pour cette leçon dans le répertoire ``universal-maker-sensor-kit-main/pi/``, ou copiez et collez directement le code ci-dessous. Exécutez le code en exécutant les commandes suivantes dans le terminal :

     .. code-block:: bash
  
        python 22_touch_sensor_module.py



.. code-block:: python

   import time
   import board
   
   import adafruit_bmp280
   
   # Créez un objet capteur, communiquant sur le bus I2C par défaut de la carte
   i2c = board.I2C()  # utilise board.SCL et board.SDA
   bmp280 = adafruit_bmp280.Adafruit_BMP280_I2C(i2c, adresse=0x76)
   
   # modifiez ceci pour correspondre à la pression (hPa) au niveau de la mer de votre localisation
   bmp280.pression_niveau_mer = 1013.25
   
   try:
      while True:
         print("\nTemperature: %0.1f C" % bmp280.temperature)
         print("Pressure: %0.1f hPa" % bmp280.pressure)
         print("Altitude = %0.2f meters" % bmp280.altitude)
         time.sleep(2)
   except KeyboardInterrupt:
       print("Exit")  # Sortie sur CTRL+C


Analyse du code
------------------

#. Configuration du capteur

   Importez les bibliothèques nécessaires et créez un objet pour interagir avec le capteur BMP280. ``board.I2C()`` configure la communication I2C. ``adafruit_bmp280.Adafruit_BMP280_I2C(i2c, adresse=0x76)`` initialise le capteur BMP280 avec son adresse I2C.

   Pour plus de détails sur la bibliothèque ``adafruit_bmp280``, veuillez vous référer à |link_Adafruit_CircuitPython_BMP280|.

   .. code-block:: python

      import time
      import board
      import adafruit_bmp280
      i2c = board.I2C()
      bmp280 = adafruit_bmp280.Adafruit_BMP280_I2C(i2c, adresse=0x76)

#. Configuration de la pression au niveau de la mer

   Définissez la propriété ``pression_niveau_mer`` de l'objet BMP280. Cette valeur est nécessaire pour calculer l'altitude.

   .. code-block:: python

      bmp280.pression_niveau_mer = 1013.25

#. Lecture des données en boucle

   Utilisez une boucle ``while True`` pour lire continuellement les données du capteur. ``bmp280.temperature``, ``bmp280.pression``, et ``bmp280.altitude`` lisent respectivement la température, la pression et l'altitude. ``time.sleep(2)`` pause la boucle pendant 2 secondes.

   .. code-block:: python

      try:
         while True:
            print("\nTemperature: %0.1f C" % bmp280.temperature)
            print("Pressure: %0.1f hPa" % bmp280.pressure)
            print("Altitude = %0.2f meters" % bmp280.altitude)
            time.sleep(2)
      except KeyboardInterrupt:
         print("Exit")

#. Gestion des interruptions

   Le bloc ``try`` et ``except KeyboardInterrupt:`` permet au programme de se terminer proprement lorsque vous appuyez sur CTRL+C.

   .. code-block:: python

      try:
         # code de la boucle while ici
      except KeyboardInterrupt:
         print("Exit")