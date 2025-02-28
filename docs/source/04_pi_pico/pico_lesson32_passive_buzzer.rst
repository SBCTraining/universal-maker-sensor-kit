.. note:: 

    Bonjour et bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, Arduino et ESP32 avec d'autres passionnés.

    **Pourquoi nous rejoindre ?**

    - **Support d'experts** : Résolvez vos problèmes après-vente et défis techniques grâce à l'aide de notre communauté et de notre équipe.
    - **Apprendre et partager** : Échangez des astuces et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Accédez en avant-première aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos derniers produits.
    - **Promotions festives et concours** : Participez à des concours et promotions pendant les fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous dès aujourd'hui !

.. _pico_lesson32_passive_buzzer:

Leçon 32 : Module Buzzer Passif
==================================

Dans cette leçon, vous apprendrez à utiliser un buzzer passif avec le Raspberry Pi Pico W pour jouer des notes individuelles et réaliser des morceaux de musique. Vous découvrirez comment utiliser la modulation de largeur d'impulsion (PWM) pour configurer le buzzer sur la broche GPIO 16 et utiliser la classe "music" de la bibliothèque buzzer_music pour jouer des chansons complètes. Ce cours vous guidera pas à pas pour jouer des notes simples, puis pour exécuter des mélodies complètes telles que "Joyeux anniversaire". Ce projet est idéal pour les débutants, offrant une manière pratique de comprendre les tonalités musicales et d'intégrer des bibliothèques externes en MicroPython sur le Raspberry Pi Pico W.

Composants Requis
--------------------------

Dans ce projet, vous aurez besoin des composants suivants.

Il est certainement plus pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom    
        - Éléments dans ce kit
        - Lien
    *   - Universal Maker Sensor Kit
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction des composants
        - Lien d'achat

    *   - Raspberry Pi Pico W
        - \-
    *   - :ref:`cpn_buzzer`
        - |link_passive_buzzer_module_buy|
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|


Câblage
---------------------------

.. image:: img/Lesson_32_Passive_buzzer_pico_bb.png
    :width: 100%


Code
---------------------------

.. code-block:: python

   import machine
   import time
   
   # Initialiser le PWM sur la GPIO 16 pour le buzzer
   buzzer = machine.PWM(machine.Pin(16))
   
   def tone(pin, frequency, duration):
       """Play a tone on the given pin at the specified frequency and duration."""
       pin.freq(frequency)
       pin.duty_u16(30000)
       time.sleep_ms(duration)
       pin.duty_u16(0)
   
   # Jouer des notes individuelles
   tone(buzzer, 440, 250)  # A4
   time.sleep(0.5)
   tone(buzzer, 494, 250)  # B4
   time.sleep(0.5)
   tone(buzzer, 523, 250)  # C5
   time.sleep(1)
   
   
   
   # Importer la classe music de la bibliothèque buzzer_music pour faciliter la lecture de chansons.
   from buzzer_music import music
   
   # Trouvez une musique sur onlinesequencer.net, cliquez sur éditer, sélectionnez toutes les notes avec CTRL + A puis copiez-les avec CTRL + C
   # Collez la chaîne dans song, en vous assurant de retirer "Online Sequencer:120233:" au début et ";:" à la fin
   # https://onlinesequencer.net/2474257 Joyeux anniversaire (par Sudirth)
   song = "0 G4 3 0;3 G4 1 0;4 A4 4 0;8 G4 4 0;12 C5 4 0;16 B4 8 0;24 G4 3 0;27 G4 1 0;28 A4 4 0;32 G4 4 0;36 D5 4 0;40 C5 8 0;48 G4 3 0;51 G4 1 0;52 G5 4 0;56 E5 4 0;60 C5 4 0;64 B4 4 0;68 A4 4 0;72 F5 3 0;75 F5 1 0;76 E5 4 0;80 C5 4 0;84 D5 4 0;88 C5 8 0"
   
   # Initialiser la classe music avec la chanson et définir la broche du buzzer
   mySong = music(song, pins=[machine.Pin(16)])
   
   # Jouer la musique à l'aide de la classe music.
   while True:
       print(mySong.tick())
       time.sleep(0.04)



Analyse du Code
---------------------------

1. Initialisation

   Importez les modules nécessaires et initialisez le PWM sur une broche GPIO spécifique pour contrôler le buzzer.

   .. code-block:: python

       import machine
       import time

       # Initialiser le PWM sur la GPIO 16 pour le buzzer
       buzzer = machine.PWM(machine.Pin(16))

2. Définition de la fonction tone

   Cette fonction permet de jouer une seule note à une fréquence et une durée spécifiées. Elle règle la fréquence et le cycle de travail (volume) du signal PWM.

   .. code-block:: python

       def tone(pin, frequency, duration):
           """Play a tone on the given pin at the specified frequency and duration."""
           pin.freq(frequency)
           pin.duty_u16(30000)
           time.sleep_ms(duration)
           pin.duty_u16(0)

3. Jouer des notes individuelles

   Ici, la fonction ``tone`` est utilisée pour jouer des notes individuelles. Les paramètres incluent la fréquence de la note (en Hz) et sa durée (en millisecondes).

   .. code-block:: python

       # Jouer des notes individuelles
       tone(buzzer, 440, 250)  # A4
       time.sleep(0.5)
       tone(buzzer, 494, 250)  # B4
       time.sleep(0.5)
       tone(buzzer, 523, 250)  # C5
       time.sleep(1)

4. Utilisation de la bibliothèque buzzer_music

   La bibliothèque ``buzzer_music`` est importée, et une chaîne représentant une chanson est préparée. 

   Vous pouvez trouver de la musique sur onlinesequencer.net, cliquer sur éditer, sélectionner toutes les notes avec CTRL + A, puis les copier avec CTRL + C. Collez la chaîne dans ``song``, en vous assurant de supprimer "Online Sequencer:120233:" au début et ";:" à la fin.

   Pour plus d'informations sur la bibliothèque ``buzzer_music``, veuillez visiter |link_buzzer_music|.

   .. code-block:: python

       # Importer la classe music de la bibliothèque buzzer_music pour faciliter la lecture de chansons.
       from buzzer_music import music

       # https://onlinesequencer.net/2474257 Joyeux anniversaire (par Sudirth)
       song = "0 G4 3 0;3 G4 1 0;4 A4 4 0;8 G4 4 0;12 C5 4 0;16 B4 8 0;24 G4 3 0;27 G4 1 0;28 A4 4 0;32 G4 4 0;36 D5 4 0;40 C5 8 0;48 G4 3 0;51 G4 1 0;52 G5 4 0;56 E5 4 0;60 C5 4 0;64 B4 4 0;68 A4 4 0;72 F5 3 0;75 F5 1 0;76 E5 4 0;80 C5 4 0;84 D5 4 0;88 C5 8 0"

5. Initialisation et lecture de la chanson

   La classe ``music`` est initialisée avec la chaîne de la chanson et la broche GPIO du buzzer. La musique est jouée en boucle à l'aide de la méthode ``tick`` de la classe ``music``.

   .. code-block:: python

       # Initialiser la classe music avec la chanson et définir la broche du buzzer
       mySong = music(song, pins=[machine.Pin(16)])

       # Jouer la musique à l'aide de la classe music.
       while True:
           print(mySong.tick())
           time.sleep(0.04)
