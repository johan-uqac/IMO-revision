# Examen Partiel Informatique Mobile

## Introduction

| Plateforme | Langage       | IDE            | Avantage majeur        | Inconvénient majeur | Environnement       | Part de marché | Gain potentiel |
| ---------- | ------------- | -------------- | ---------------------- | ------------------- | ------------------- | -------------- | -------------- |
| Android    | Java / Kotlin | Android Studio | Coût de mise en prod   | Potentiel gain      | Windows, Mac, Linux | +++++          | ----           |
| iOS        | Swift / Obj-C | Xcode          | Support et maintenance | Coût de dev         | Mac                 | ----           | ++++           |

Pourquoi pas multiplateforme ?

**POUR** :

- Coût de développement
- Moins de développeurs
- Maintenance
- UX uniforme
- Marketing
- Mise en marché plus simple

**CONTRE** :

- Perte de spécificité de chaque plateforme
- Performance
- Intégration de fonctionnalités natives plus complexe et longue
- Perte d'UX

## Android

Créé en 2003 et racheté en 2005 par Google. Open Source. Gratuit. SDK Android 1.0 en 2008. Logo appelé BugDroid

Problème de fragmentation. Plusieurs versions d'Android en circulation. Plusieurs constructeurs. Plusieurs surcouches constructeurs.

Basé sur le kernel Linux. Séparation de l'OS et des applications.

Android est un framework.

### Liberté

Les applications s'exécutent dans un environnement contraint :

- Mémoire limitée
- CPU limité
- Affichage
- Stockage

### Architecture

1. Applications
2. Framework Android : Gestionnaire de ressources / notifications, ...
3. Bibliothèques : Composants système
4. Android Runtime : VM ART
5. Kernel Linux : Gestion de la mémoire / processus

#### VR ART

A l'origine : Dalvik

Depuis Android 5.0 : ART (Android Runtime) parce que Oracle a attaqué Google pour violation de brevets.

AOT (Ahead Of Time) : Compilation à l'installation plutôt qu'à l'exécution :

- Meilleures performances
- Meilleure garbage collector
- Amélioration du dev et des logs

### Gradle

- Gestion des dépendances
- Automatisation de la compilation, création et déploiement de l'APK

## Structure

**Manifest** : Spécificités de l'application

**Dossier res** : Icones (drawable/mipmap) Layout/menu (xml des interfaces) Values (strings, colors, styles)

### Paramètres

- **minSdkVersion** : Version minimale d'Android
- **targetSdkVersion** : Version cible d'Android
- **compileSdkVersion** : Version de l'API Android pour compiler l'application

## Environnement

### Internationalisation

- **Strings** : Fichier XML dans res/values

Nom du fichier : res/values-<locale>/strings.xml

Locale : fr, en, es, ... suivi d'un -r pour les régions : fr-rCA, fr-rFR, ...

Pareil pour les styles / themes / layouts

## Layouts

- **LinearLayout** : Alignement horizontal ou vertical, espace parent, poids (flexbox), gravity marge / padding
- **RelativeLayout** : Positionnement relatif, alignement, alignParent, toRightOf, ...
- **TableLayout** : Tableau
- **ScrollView** : Ne peut contenir que un seul enfant
- **GridLayout** : Grille
- **ConstraintLayout** : Contrainte par rapport aux autres éléments

## Widgets

### Implémentation

android:onClick="onClick" : Appel de la méthode onClick dans le code Java

### Listener

```java
bouton.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        // Code
    }
});
```

Via lambda :

```java
bouton.setOnClickListener((View v) -> {
    // Code
});
```

### Widgets connus

- **Button** : Bouton
- **TextView** : Texte
- **EditText** : Champ de texte, inputType (text, password, email, ...)
- **ImageView** : Image
- **ImageButton** : Image cliquable
- **CheckBox** : Case à cocher
- **RadioButton** : Bouton radio (bouton rond)
- **Switch** : Interrupteur (on/off)

## Cycle de vie

### Activités

- Possède une fenêtre pour l'interface graphique
- Plusieurs écrans = plusieurs activités
- Chaque activité gère son cycle de vie et peut appeler d'autres activités

### Etats

- Active
- En pause
- Arrêt
- Mort

### Evénements

- **onCreate** : Création de l'activité, appelée lors du chargement de l'activité, savedInstanceState pour récupérer les données de sauvegarde
  - **Rotation** = Recréation de l'activité et réappel de onCreate
- **onResume** : Mise à jour de l'interface
- **onRestart** : Reconnexion de la bdd
- **onPause** : Mise en pause de l'activité, arreter les timers / faire des sauvegardes
- **onStop** : Arrêt de l'activité, libérer les ressources
- **onDestroy** : Destruction de l'activité, libérer les ressources

### Bundle

- **onSaveInstanceState** : Sauvegarde des données
- **onRestoreInstanceState** : Restauration des données

Ne pas mettre de fichiers / bdd / image / video / web
Mettre focus / entrée importante

- **PersistableBundle** : Sauvegarde des données persistantes dans un fichier sur le disque

## Notifications

NotificationManager : Référence sur le service

Construite avec un builder

```java
NotificationCompat.Builder builder = new NotificationCompat.Builder(this, "channelId")
    .setSmallIcon(R.drawable.ic_launcher_foreground)
    .setContentTitle("Titre")
    .setContentText("Texte")
    .setPriority(NotificationCompat.PRIORITY_DEFAULT);
```

## Intents

- Asynchrone
- Lancer un composant (activité, app, ...)
- Possibilité de passer des données via extra

Quitter avec finish() pour revenir à l'activité précédente

Possible de quitter avec un _resultCode_
