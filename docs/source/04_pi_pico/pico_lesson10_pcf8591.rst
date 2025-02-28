.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l’univers du Raspberry Pi, Arduino et ESP32 avec d’autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d’experts** : Résolvez les problèmes après-vente et les défis techniques avec l’aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et concours** : Participez à des concours et promotions spéciales.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd’hui !

.. _pico_lesson10_pcf8591:

Leçon 10 : Module Convertisseur ADC DAC PCF8591
==================================================

Dans cette leçon, vous apprendrez à connecter le Raspberry Pi Pico W au module convertisseur ADC DAC PCF8591 en utilisant MicroPython. Vous établirez une connexion I2C, initialiserez le module PCF8591 et lirez des valeurs analogiques depuis ses canaux. Cette session pratique approfondira votre compréhension de la conversion analogique-numérique et de la communication I2C sur le Raspberry Pi Pico W. Le potentiomètre du module est connecté à AIN0 à l’aide de fils de connexion, et la LED D2 du module est reliée à AOUT, de sorte que vous pourrez observer la variation de la luminosité de la LED D2 en fonction de la rotation du potentiomètre.

Composants Requis
--------------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est plus pratique d’acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - Éléments dans ce kit
        - Lien
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Vous pouvez aussi les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - Raspberry Pi Pico W
        - \-
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_10_PCF8591_Module_bb.png
    :width: 100%


Code
---------------------------

.. note::

    * Ouvrez le fichier ``10_pcf8591_module.py`` dans le dossier ``universal-maker-sensor-kit-main/pico/Lesson_10_PCF8591_Module`` ou copiez ce code dans Thonny, puis cliquez sur "Run Current Script" ou appuyez simplement sur F5 pour l'exécuter. Pour un tutoriel détaillé, veuillez consulter :ref:`open_run_code_py`.

    * Vous devez utiliser le fichier ``PCF8591.py``, vérifiez s'il a été chargé sur le Pico W. Pour un tutoriel détaillé, consultez :ref:`add_libraries_py`.

    * N’oubliez pas de sélectionner l’interpréteur "MicroPython (Raspberry Pi Pico)" dans le coin inférieur droit.

.. code-block:: python

   from machine import I2C, Pin
   import time
   from PCF8591 import PCF8591
   
   # Configuration de la connexion I2C sur les broches 20 (SDA) et 21 (SCL)
   i2c = I2C(0, sda=Pin(20), scl=Pin(21))
   
   # Initialisation du module PCF8591 à l'adresse 0x48
   pcf8591 = PCF8591(0x48, i2c)  # Ajustez l'adresse si nécessaire
   
   # Vérification de la connexion du module PCF8591
   if pcf8591.begin():
       print("PCF8591 found")
   
   # Boucle principale pour lire les valeurs analogiques
   while True:
       # Lire et afficher la valeur analogique du canal AIN0
       AIN0 = pcf8591.analog_read(PCF8591.AIN0)
       print("AIN0 ", AIN0)  # PCF8591.CHANNEL_0 peut aussi être utilisé
       # Les autres canaux peuvent être lus en décommentant les lignes suivantes
       # print("AIN1 ", pcf8591.analog_read(PCF8591.AIN1))
       # print("AIN2 ", pcf8591.analog_read(PCF8591.AIN2))
       # print("AIN3 ", pcf8591.analog_read(PCF8591.AIN3))
   
       # Écrire la valeur sur AOUT. Cela changera la luminosité de la LED D2 sur le module.
       pcf8591.analog_write(AIN0)
   
       # Attendre 0,2 secondes avant la prochaine lecture
       time.sleep(0.2)


Analyse du Code
---------------------------

#. Importation des Bibliothèques et Configuration de l'I2C

   - Le module ``machine`` est importé pour utiliser la communication I2C et la classe ``Pin``.
   - Le module ``time`` est importé pour ajouter des délais dans le programme.
   - La bibliothèque ``PCF8591`` est importée pour interagir facilement avec le module PCF8591. Pour plus d'informations sur la bibliothèque ``PCF8591``, consultez |link_PCF8591_micropython_library|.

   .. raw:: html

      <br/>

   .. code-block:: python

      from machine import I2C, Pin
      import time
      from PCF8591 import PCF8591

#. Initialisation de la Connexion I2C

   La communication I2C est initialisée en utilisant les broches SDA (Données Série) et SCL (Horloge Série). Le Raspberry Pi Pico W utilise les GPIO 20 et 21 à cet effet.

   .. code-block:: python

      i2c = I2C(0, sda=Pin(20), scl=Pin(21))

#. Initialisation du Module PCF8591

   Le module PCF8591 est initialisé avec son adresse I2C (0x48). Cette adresse peut nécessiter un ajustement en fonction de la configuration du module.

   .. code-block:: python

      pcf8591 = PCF8591(0x48, i2c)  # Ajustez l'adresse si nécessaire

#. Vérification de la Connexion

   Le programme vérifie si le module PCF8591 est correctement connecté.

   .. code-block:: python

      if pcf8591.begin():
          print("PCF8591 found")

#. Boucle Principale pour Lire les Valeurs Analogiques

   - Le programme entre dans une boucle infinie et lit continuellement la valeur analogique du canal AIN0.
   - La fonction ``analog_read`` est utilisée pour lire la valeur d’un canal spécifié.
   - La fonction ``analog_write`` est utilisée pour écrire la valeur sur AOUT.
   - Les fils de connexion relient le potentiomètre du module à AIN0, et la LED D2 est connectée à AOUT. Ainsi, la luminosité de la LED change en fonction de la rotation du potentiomètre. Consultez le schéma du module PCF8591 :ref:`schematic <cpn_pcf8591_sch>` pour plus de détails.
   - Un délai de 0,2 seconde est ajouté entre chaque lecture pour stabiliser la sortie.

   .. raw:: html

      <br/>

   .. code-block:: python

      while True:
          # Lire et afficher la valeur analogique du canal AIN0
          AIN0 = pcf8591.analog_read(PCF8591.AIN0)
          print("AIN0 ", AIN0)  # PCF8591.CHANNEL_0 peut aussi être utilisé
          # Les autres canaux peuvent être lus en décommentant les lignes suivantes
          # print("AIN1 ", pcf8591.analog_read(PCF8591.AIN1))
          # print("AIN2 ", pcf8591.analog_read(PCF8591.AIN2))
          # print("AIN3 ", pcf8591.analog_read(PCF8591.AIN3))
      
          # Écrire la valeur sur AOUT. Cela changera la luminosité de la LED D2 sur le module.
          pcf8591.analog_write(AIN0)
      
          # Attendre 0,2 secondes avant la prochaine lecture
          time.sleep(0.2)
