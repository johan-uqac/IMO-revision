# Fragments

- Partie d'une interface
- Possible d'en combiner plusieurs pour former une interface complète
- Indépendant et réutilisable, chacun a sa propre logique et son propre cycle de vie, et ses evenements
- Peut être ajouté ou retiré dynamiquement
- Doit être attaché à une activité ou à une autre interface utilisateur (si activité détruite, les fragments sont détruits)
- Chaque action est une transaction, qui peut être annulée ou confirmée

## Cycle de vie

- `onAttach()`: fragment attaché à une activité
- `onCreate()`: fragment créé
- `onCreateView()`: fragment créé et vue associée
- `onActivityCreated()`: activité créée et dessinée

Quand il est détruit:

- `onDestroyView()`: vue détruite
- `onDestroy()`: fragment détruit
- `onDetach()`: fragment détaché

## La classe Fragment

- Hérite de `android.app.Fragment`
- Doit lier le fragment à une vue (layout) avec `onCreateView()`
- - Chargement de la vue avec onCreateView()
- Méthode qui a 2 paramètres: inflater et container pour charger la vue et la vue parente

## Fragment statique

- Déclaré dans le layout de l'activité avec `<fragment>`
- Ne peut pas être ajouté ou retiré dynamiquement

## Fragment dynamique

- Ajouté ou retiré dynamiquement
- Effectué sur des éléments de la vue de l'activité dédiés à cet effet (ex: `FrameLayout`)
- Ajoutés / supprimés / remplacés pendant l'exécution

### Layout à T0

- FragmentManager: gère les fragments de l'activité
- Add: Ajoute un fragment sur la pile à l'intérieur de R.id.fragment_dynamique
- Commit: Valide la transaction

### Concept de transaction

- Un fragment peut être ajouté, remplacé ou supprimé à l'exécution
- Caché ou affiché
- Attaché ou détaché de la structure de l'interface utilisateur

- Une transaction correspond à un ou plusieurs changements sur les fragments en même temps

- Une transaction est créée, construite, complétée et asynchrone

# Persistance

Possible de faire

- Gestion temporaire (Bundle)
- Gestion permanente :
- - Base de données externe (mySQL)
- - Fichiers (XML, JSON, CSV)
- - ORM local
- - Firebase

## SQLite

- Open source
- Pas de serveur
- Stockage local
- Pas de configuration
- Un seul fichier de base de données
- Intégré à Android
- Peu gourmand en mémoire

## SQLiteOpenHelper

- Classe abstraite

### Constructeur

- Context: contexte de l'application
- Nom de la base de données (String)
- CursorFactory: null
- Version de la base de données (int)

### Méthodes

- `onCreate()`: création de la base de données pour la première fois, création des tables

- `onUpgrade()`: mise à jour de la base de données, suppression des tables et recréation

- CRUD

- Cursor: Récypérer le numéro de la colonne via le nom du champ, fermer le curseur après utilisation (mémoire)

# Processus

## Taches asynchrones

- Exécution par l'UI thread
- - Aucun traitement lourd
- - Jamais bloqué

AsyncTask, méthode onPostExectute appelée après l'exécution de la tâche pour libérer l'UI thread

méthode doInBackground() pour exécuter le traitement lourd

## Services

- Exécution en arrière-plan

- Création d'une classe qui hérite de Service
- Déclaration dans le manifest

- Redéfinis les méthodes onStartCommand(), onCreate(), onBind()

## Autres

### Timer

`CountDownTimer(long millisInFuture, long countDownInterval)`

### Alarme

Types:

- RTC: temps réel
- RTC_WAKEUP: temps réel, réveille le téléphone
- ELAPSED_REALTIME: temps écoulé depuis le démarrage du système
- ELAPSED_REALTIME_WAKEUP: temps écoulé depuis le démarrage du système, réveille le téléphone

### Broadcast Receiver

- Réception/Envoi d'événements système ou personnalisés via des intents

### Capteurs

- Accéléromètre, gyroscope, magnétomètre, baromètre, GPS, etc.

### Alerte

- Dialog

### Boule

- Canvas qui grandit au clic
