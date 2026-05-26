TP 11 — Localisation d’un smartphone et envoi des coordonnées vers un serveur distant
Projet LocalisationSmartphone – Mon application de suivi GPS

J’ai développé ce projet dans le cadre d’un travail pratique. L’objectif était de créer une application Android capable de récupérer les coordonnées GPS d’un téléphone et de les envoyer en temps réel à un serveur distant. Les données sont stockées dans une base MySQL. L’architecture est séparée en deux parties : l’application mobile native (Java) et un backend PHP structuré en couches (modèle, DAO, service).

Objectifs pédagogiques que je me suis fixés

- Récupérer la latitude, la longitude, l’altitude et la précision via le GPS du smartphone.
- Gérer correctement les permissions Android liées à la localisation et à l’état du téléphone.
- Faire communiquer l’application mobile avec un service web grâce à des requêtes HTTP POST (j’ai utilisé Volley).
- Mettre en place une architecture backend professionnelle (DAO, Service, Modèle).
- Assurer un stockage persistant des données de géolocalisation.

Architecture du projet

1. Côté mobile (Android)

L’application est écrite en Java. Voici les composants que j’ai utilisés :

- LocationManager et LocationListener : pour écouter activement les changements de position.
- TelephonyManager : pour identifier l’appareil de manière unique (IMEI / ANDROID_ID).
- Volley : pour envoyer les données au serveur en méthode POST.
- AndroidX : pour la compatibilité et les interfaces modernes.

2. Côté serveur (PHP / MySQL)

J’ai organisé le backend de façon modulaire :

- un dossier classe/ avec l’entité Position.php (le modèle).
- un dossier connexion/ qui gère la connexion à MySQL via PDO.
- un dossier dao/ contenant l’interface IDao.php (opérations CRUD).
- un dossier service/ avec PositionService.php qui implémente la logique d’accès aux données.
- un script createPosition.php qui reçoit les données envoyées par l’application mobile.

Configuration et installation (ce que j’ai fait)

Base de données

- J’ai créé une base nommée "localisation" sous MySQL.
- J’ai exécuté le script de création de la table "position" (champs : id, latitude, longitude, date_position, imei).

Serveur PHP

- J’ai copié le dossier "localisation" dans le répertoire racine de mon serveur (par exemple htdocs sous XAMPP).
- J’ai vérifié les paramètres de connexion dans connexion/Connexion.php (host, dbname, login, mot de passe).

Application Android

- J’ai ouvert le projet dans Android Studio.
- Dans MainActivity.java, j’ai mis à jour la variable "insertUrl" avec l’adresse IP de mon serveur. Pour l’émulateur, j’utilise 10.0.2.2.
- J’ai compilé et lancé l’application sur un téléphone réel ou un émulateur.

Utilisation – comment ça marche

1. Je lance l’application. Elle me demande les permissions (localisation et état du téléphone). Je les accepte.
2. J’active le GPS de l’appareil.
3. Dès qu’un changement de position est détecté (selon les seuils de distance et de temps que j’ai configurés), l’application envoie automatiquement les données au serveur.
4. Je peux vérifier dans phpMyAdmin que les nouvelles lignes apparaissent bien dans la table "position".

Bonnes pratiques que j’ai suivies

- Je me suis assuré que le smartphone et le serveur sont sur le même réseau local (pour les tests).
- Côté PHP, j’ai utilisé des requêtes préparées pour éviter les injections SQL.
- J’ai systématiquement vérifié l’état du fournisseur GPS avant de demander des mises à jour de position.

Remarques personnelles

Ce projet m’a permis de comprendre l’enchaînement complet entre une application Android, un serveur PHP et une base MySQL. C’est une base solide pour des applications de géolocalisation plus complexes (suivi de flotte, journal de bord, etc.). Si vous reprenez ce code, pensez à bien adapter l’URL du serveur et à gérer les cas où le GPS n’est pas disponible.

Voilà, c’est le README que j’ai écrit pour mon projet LocalisationSmartphone.
