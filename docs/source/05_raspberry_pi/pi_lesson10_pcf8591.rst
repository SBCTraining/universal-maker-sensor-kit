.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de Raspberry Pi, Arduino et ESP32 de SunFounder sur Facebook ! Plongez plus profondément dans le Raspberry Pi, l'Arduino et l'ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et vos défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & partager** : Échangez des astuces et des tutoriels pour perfectionner vos compétences.
    - **Aperçus exclusifs** : Bénéficiez d'un accès anticipé aux annonces de nouveaux produits et à des aperçus exclusifs.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos produits les plus récents.
    - **Promotions festives et concours** : Participez à nos concours et promotions pendant les fêtes.

    👉 Prêt à explorer et à créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pi_lesson10_pcf8591:

Leçon 10 : Module Convertisseur ADC DAC PCF8591
==================================================

.. note::
   Le Raspberry Pi ne dispose pas de capacités d'entrée analogique, il nécessite donc un module comme le :ref:`cpn_pcf8591` pour lire les signaux analogiques à des fins de traitement.

Dans cette leçon, vous apprendrez à utiliser un Raspberry Pi pour interagir avec le module PCF8591 pour la conversion analogique-numérique et numérique-analogique. Nous verrons comment lire les valeurs analogiques depuis l'entrée AIN0 et les envoyer au DAC (AOUT). Le potentiomètre du module est connecté à AIN0 via des capuchons de connexion, et la LED D2 du module est reliée à AOUT. Ainsi, vous pourrez observer que la luminosité de la LED D2 varie à mesure que vous tournez le potentiomètre.

Composants nécessaires
---------------------------

Pour ce projet, vous aurez besoin des composants suivants.

Il est pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DANS CE KIT
        - Lien
    *   - Kit de capteurs Universal Maker
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
    *   - :ref:`cpn_pcf8591`
        - |link_pcf8591_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. note::
   Dans ce projet, nous avons utilisé la broche AIN0 du module PCF8591, qui est reliée à un potentiomètre sur le module via un capuchon de connexion. **Veuillez vous assurer que le capuchon de connexion est correctement placé sur le module.** Pour plus de détails, consultez le :ref:`schematic <cpn_pcf8591_sch>`.

.. image:: img/Lesson_10_PCF8591_pi_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: Python

   import PCF8591 as ADC  # Import the library for the PCF8591 module
   import time  # Import the time library for adding delays
   
   # Initialize the PCF8591 module at I2C address 0x48.
   # This address is used for communication with the Raspberry Pi.
   ADC.setup(0x48)
   
   try:
       while True:  # Start an infinite loop to continuously monitor the sensor.
           # Read the analog value from the potentiometer connected to AIN0.
           # Channel range from 0 to 3 represents AIN0 to AIN3.
           # The potentiometer's rotation alters the voltage, which is read by the PCF8591.
           potentiometer_value = ADC.read(0)
           print(potentiometer_value)
   
           # Write the value back to AOUT. This will change the brightness of the D2 LED on the module.
           # LED won't light up below 80, so convert '0-255' to '80-255'
           # As the potentiometer is adjusted, the LED's brightness varies proportionally.
           tmp = potentiometer_value*(255-80)/255+80
           ADC.write(tmp)
   
           # Add a short delay of 0.2 seconds to make the loop more manageable.
           time.sleep(0.2)
   
   except KeyboardInterrupt:
       # If a KeyboardInterrupt (CTRL+C) is detected, exit the loop and end the program.
       print("Exit")



Analyse du code
---------------------------

1. **Importation des bibliothèques** :

   Le script commence par importer les bibliothèques nécessaires. La bibliothèque ``PCF8591`` est utilisée pour interagir avec le module ADC/DAC, et ``time`` est utilisé pour créer des délais.

   .. code-block:: python

      import PCF8591 as ADC  # Importation de la bibliothèque pour le module PCF8591
      import time  # Importation de la bibliothèque time pour ajouter des délais

2. **Initialisation du module PCF8591** :

   Le module PCF8591 est initialisé à l'adresse I²C 0x48. Cette étape est cruciale pour établir la communication entre le Raspberry Pi et le module.

   .. code-block:: python

      ADC.setup(0x48)  # Initialisation du module PCF8591 à l'adresse I2C 0x48

3. **Lecture du potentiomètre et écriture dans la LED** :

   Dans un bloc ``try``, une boucle continue ``while True`` lit la valeur du potentiomètre connecté à AIN0 et écrit cette valeur dans le DAC relié à AOUT. Les capuchons de connexion relient le potentiomètre du module à AIN0, et la LED D2 est reliée à AOUT. Veuillez consulter le :ref:`schematic <cpn_pcf8591_sch>` pour plus de détails. La luminosité de la LED varie au fur et à mesure que le potentiomètre est tourné.

   - Utilisez ``ADC.read(channel)`` pour lire l'entrée analogique du canal spécifique. La plage de canaux va de 0 à 3, représentant AIN0 à AIN3.

   - Utilisez ``ADC.write(Value)`` pour définir la sortie analogique de la broche AOUT avec une valeur comprise entre 0 et 255.

   .. raw:: html

      <br/>

   .. code-block:: python

      try:
          while True:  # Lancer une boucle infinie pour surveiller en continu le capteur.
              potentiometer_value = ADC.read(0)
              print(potentiometer_value)
              tmp = potentiometer_value*(255-80)/255+80
              ADC.write(tmp)
              time.sleep(0.2)

4. **Gestion des interruptions clavier** :

   Une ``KeyboardInterrupt`` (comme la touche CTRL+C) permet de quitter proprement la boucle sans générer d'erreurs.

   .. code-block:: python

      except KeyboardInterrupt:
          print("Exit")