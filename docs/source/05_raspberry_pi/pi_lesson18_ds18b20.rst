    Bonjour et bienvenue dans la communauté Facebook des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder ! Plongez plus profondément dans l'univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des cadeaux et promotions de vacances.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _pi_lesson18_ds18b20:

Leçon 18 : Module de capteur de température (DS18B20)
=======================================================

Dans cette leçon, vous apprendrez à utiliser un Raspberry Pi pour lire les données de température d'un capteur de température DS18B20. Vous comprendrez comment localiser le fichier de périphérique du capteur, lire et analyser ses données brutes, et convertir ces données en lectures Celsius et Fahrenheit.

Composants nécessaires
----------------------

Pour ce projet, nous aurons besoin des composants suivants.

Il est certainement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ÉLÉMENTS DE CE KIT
        - LIEN
    *   - Kit de capteurs universel pour créateurs
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - Raspberry Pi 5
        - \-
    *   - :ref:`cpn_ds18b20`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
----------

.. image:: img/Lesson_18_DS18B20_pi_bb.png
    :width: 100%


Code
--------

.. note::
   Le module DS18B20 communique avec le Raspberry Pi en utilisant le protocole onewire. Avant de lancer le code, vous devez activer la fonction onewire du Raspberry Pi. Vous pouvez vous référer à ce tutoriel : :ref:`pi_enable_1wire`.

.. code-block:: python

   import glob
   import time
   
   # Chemin vers le répertoire contenant les fichiers de périphérique pour les dispositifs 1-wire
   base_dir = "/sys/bus/w1/devices/"
   
   # Trouve le premier dossier de périphérique qui commence par "28", spécifique au DS18B20
   device_folder = glob.glob(base_dir + "28*")[0]
   
   # Fichier de périphérique contenant les données de température
   device_file = device_folder + "/w1_slave"
   
   
   def read_temp_raw():
       # Lit les données brutes de température du capteur
       f = open(device_file, "r")
       lines = f.readlines()
       f.close()
       return lines
   
   
   def read_temp():
       # Analyse les données brutes de température et les convertit en Celsius et Fahrenheit
       lines = read_temp_raw()
       # Attend une lecture de température valide
       while lines[0].strip()[-3:] != "YES":
           time.sleep(0.2)
           lines = read_temp_raw()
       equals_pos = lines[1].find("t=")
       if equals_pos != -1:
           temp_string = lines[1][equals_pos + 2 :]
           temp_c = float(temp_string) / 1000.0  # Convertit en Celsius
           temp_f = temp_c * 9.0 / 5.0 + 32.0  # Convertit en Fahrenheit
           return temp_c, temp_f
   
   
   try:
       # Boucle principale pour lire et afficher continuellement la température
       while True:
           temp_c, temp_f = read_temp()
           formatted_output = f"Temperature: {temp_c:.2f}°C / {temp_f:.2f}°F"
           print(formatted_output)
           time.sleep(1)  # Attente de 1 seconde entre les lectures
   except KeyboardInterrupt:
       # Sortie du programme en douceur sur CTRL+C
       print("Exit")




Analyse du code
-------------------

#. Importation des bibliothèques nécessaires

   La bibliothèque ``glob`` est utilisée pour rechercher le dossier de périphérique du capteur de température. La bibliothèque ``time`` est utilisée pour implémenter des délais dans le programme.

   .. code-block:: python

      import glob
      import time

#. Localisation du fichier de périphérique du capteur de température

   Le code recherche le répertoire du capteur DS18B20 en cherchant un nom de dossier commençant par "28". Le fichier de périphérique ``w1_slave`` contient les données de température.

   .. code-block:: python

      base_dir = "/sys/bus/w1/devices/"
      device_folder = glob.glob(base_dir + "28*")[0]
      device_file = device_folder + "/w1_slave"

#. Lecture des données brutes de température

   Cette fonction ouvre le fichier de périphérique et lit son contenu. Elle renvoie les données brutes de température sous forme de liste de chaînes.

   .. code-block:: python

      def read_temp_raw():
          f = open(device_file, "r")
          lines = f.readlines()
          f.close()
          return lines

#. Analyse et conversion des données de température

   La fonction ``read_temp`` appelle ``read_temp_raw`` pour obtenir les données brutes. Elle attend une lecture de température valide puis extrait, analyse et convertit la température en Celsius et en Fahrenheit.

   .. code-block:: python

      def read_temp():
          lines = read_temp_raw()
          while lines[0].strip()[-3:] != "YES":
              time.sleep(0.2)
              lines = read_temp_raw()
          equals_pos = lines[1].find("t=")
          if equals_pos != -1:
              temp_string = lines[1][equals_pos + 2 :]
              temp_c = float(temp_string) / 1000.0
              temp_f = temp_c * 9.0 / 5.0 + 32.0
              return temp_c, temp_f

#. Boucle principale du programme et sortie en douceur

   Le bloc ``try`` contient une boucle infinie pour lire et afficher continuellement la température. Le bloc ``except`` intercepte un KeyboardInterrupt pour quitter le programme en douceur.

   .. code-block:: python

      try:
          while True:
              temp_c, temp_f = read_temp()
              formatted_output = f"Temperature: {temp_c:.2f}°C / {temp_f:.2f}°F"
              print(formatted_output)
              time.sleep(1)
      except KeyboardInterrupt:
          print("Exit")