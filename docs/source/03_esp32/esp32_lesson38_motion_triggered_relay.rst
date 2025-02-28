.. note::

    Bonjour, bienvenue dans la communauté des passionnés de SunFounder Raspberry Pi, Arduino et ESP32 sur Facebook ! Plongez plus profondément dans l'univers du Raspberry Pi, de l'Arduino et de l'ESP32 avec d'autres amateurs.

    **Pourquoi rejoindre ?**

    - **Support d'experts** : Résolvez les problèmes après-vente et les défis techniques avec l'aide de notre communauté et de notre équipe.
    - **Apprendre & Partager** : Échangez des conseils et des tutoriels pour améliorer vos compétences.
    - **Aperçus exclusifs** : Obtenez un accès anticipé aux annonces de nouveaux produits et aux aperçus.
    - **Réductions spéciales** : Profitez de réductions exclusives sur nos nouveaux produits.
    - **Promotions festives et cadeaux** : Participez à des tirages au sort et des promotions de fêtes.

    👉 Prêt à explorer et créer avec nous ? Cliquez sur [|link_sf_facebook|] et rejoignez-nous aujourd'hui !

.. _esp32_motion_triggered_relay:

Leçon 38 : Relais déclenché par mouvement
=========================================

Ce projet vise à contrôler une lumière actionnée par un relais en utilisant un capteur infrarouge passif (PIR).
Lorsque le capteur PIR détecte un mouvement, le relais est activé, allumant ainsi la lumière.
La lumière reste allumée pendant 5 secondes après le dernier mouvement détecté.

.. warning::

    À titre de démonstration, nous utilisons un relais pour contrôler un module LED RGB.
    Cependant, dans des scénarios réels, cela peut ne pas être l'approche la plus pratique.
    
    **Bien que vous puissiez connecter le relais à d'autres appareils dans des applications réelles, une extrême prudence est requise lors de la manipulation de haute tension AC. Une utilisation inappropriée ou incorrecte peut entraîner de graves blessures ou même la mort. Par conséquent, cela est destiné aux personnes qui sont familières et compétentes en matière de haute tension AC. La sécurité doit toujours être une priorité.**

Composants requis
--------------------

Pour ce projet, nous avons besoin des composants suivants.

Il est définitivement pratique d'acheter un kit complet, voici le lien :

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Nom	
        - ARTICLES DANS CE KIT
        - LIEN
    *   - Kit de capteurs universels pour créateurs
        - 94
        - |link_umsk|

Vous pouvez également les acheter séparément via les liens ci-dessous.

.. list-table::
    :widths: 30 20
    :header-rows: 1

    *   - Introduction au composant
        - Lien d'achat

    *   - ESP32 & Carte de développement (:ref:`cpn_esp32_wroom_32e`)
        - |link_esp32_camera_pro_kit_buy|
    *   - :ref:`cpn_pir_motion`
        - \-
    *   - :ref:`cpn_relay`
        - \-
    *   - :ref:`cpn_rgb`
        - \-
    *   - :ref:`cpn_breadboard`
        - |link_breadboard_buy|
        

Câblage
---------

.. image:: img/Lesson_38_Motion_triggered_relay_esp32_bb.png
    :width: 100%


Code
------

.. raw:: html

    <iframe src=https://create.arduino.cc/editor/sunfounder01/5a29dc43-f362-434e-9e5a-f32dcd41b952/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


Analyse du code
------------------

Le projet s'articule autour de la capacité du capteur de mouvement PIR à détecter des mouvements. Lorsqu'un mouvement est détecté, un signal est envoyé à l'Arduino, déclenchant le module de relais, qui à son tour active une lumière. La lumière reste allumée pendant une durée spécifiée (dans ce cas, 5 secondes) après le dernier mouvement détecté, garantissant que la zone reste éclairée pendant une courte période même si le mouvement cesse.

1. **Configuration initiale et déclarations de variables**

    Ce segment définit les constantes et les variables qui seront utilisées tout au long du code. Nous configurons les broches du relais et du PIR ainsi qu'une constante de délai pour le mouvement. Nous avons également une variable pour suivre le dernier temps de mouvement détecté et un drapeau pour surveiller si un mouvement est détecté.

    .. code-block:: arduino
   
        // Définir le numéro de broche pour le relais
        const int relayPin = 19;

        // Définir le numéro de broche pour le capteur PIR
        const int pirPin = 18;

        // Seuil de délai de mouvement en millisecondes
        const unsigned long MOTION_DELAY = 5000;

        unsigned long lastMotionTime = 0;  // Horodatage du dernier mouvement détecté
        bool motionDetected = false;       // Indicateur pour suivre si un mouvement est détecté
        
   

2. **Configuration des broches dans la fonction setup()**

    Dans la fonction ``setup()``, nous configurons les modes des broches pour le relais et le capteur PIR. Nous initialisons également le relais pour qu'il soit éteint au départ.

    .. code-block:: arduino
    
        void setup() {
            pinMode(relayPin, OUTPUT);    // Régler relayPin comme une broche de sortie
            pinMode(pirPin, INPUT);       // Régler la broche PIR comme une entrée
            digitalWrite(relayPin, LOW);  // Éteindre initialement le relais
        }

3. **Logique principale dans la fonction loop()**

    La fonction ``loop()`` contient la logique principale. Lorsque le capteur PIR détecte un mouvement, il envoie un signal ``HIGH``, activant le relais et mettant à jour le ``lastMotionTime``. Si aucun mouvement n'est détecté pendant le délai spécifié (5 secondes dans ce cas), le relais est éteint.
    
    Cette approche garantit que même si le mouvement est sporadique ou bref, la lumière reste allumée pendant au moins 5 secondes après le dernier mouvement détecté, fournissant une durée d'éclairage constante.

    .. code-block:: arduino
    
        void loop() {
            if (digitalRead(pirPin) == HIGH) {
                lastMotionTime = millis();     // Mettre à jour le dernier temps de mouvement
                digitalWrite(relayPin, HIGH);  // Allumer le relais (et donc la lumière)
                motionDetected = true;
            }
    
            // Si un mouvement a été détecté plus tôt et que 5 secondes se sont écoulées, éteindre le relais
            if (motionDetected && (millis() - lastMotionTime >= MOTION_DELAY)) {
                digitalWrite(relayPin, LOW);  // Éteindre le relais
                motionDetected = false;
            }
        }
    
   
