# SignPDF — application Flutter de signature PDF

Application mobile Flutter (Android / iOS) permettant de :
- sélectionner un PDF depuis le sélecteur de fichiers natif ;
- afficher ses pages ;
- dessiner et enregistrer des signatures manuscrites ;
- positionner une signature sur une page ;
- intégrer la signature dans le PDF exporté ;
- enregistrer le nouveau PDF et le partager.

## Prérequis

- Flutter SDK récent (Dart >= 3.3)
- Android Studio / Android SDK pour Android
- Xcode sur macOS pour compiler iOS

## Installation

À la racine du projet :

```bash
flutter pub get
flutter analyze
flutter run
```

Pour générer un APK :

```bash
flutter build apk --release
```

Pour générer un App Bundle Google Play :

```bash
flutter build appbundle --release
```

Pour iOS (sur macOS avec Xcode) :

```bash
flutter build ios --release
```

## Structure

```text
lib/
  main.dart
  app.dart
  models/
    saved_signature.dart
  screens/
    home_screen.dart
    signature_screen.dart
    pdf_editor_screen.dart
  services/
    signature_storage.dart
    pdf_service.dart
```

## Notes techniques importantes

1. Le traitement des PDF et des signatures est effectué sur l'appareil.
2. Les signatures sont actuellement stockées dans `SharedPreferences` sous forme Base64.
   Pour une version de production, migrer vers un stockage chiffré (Keychain / Android Keystore)
   ou stocker les images dans un répertoire privé avec chiffrement.
3. Le moteur d'édition utilise `syncfusion_flutter_pdf`. Vérifier les conditions de licence
   Syncfusion applicables au projet avant toute distribution commerciale.
4. L'éditeur de cette première version place une signature sur la page actuellement affichée.
   Le positionnement est normalisé par rapport à la page rendue. Le contrôle qualité doit
   inclure des PDF A4, Letter, paysage, pages tournées et documents multi-pages.
5. Le format exporté contient une image de signature intégrée dans le contenu PDF.
   Cela ne crée pas une signature numérique cryptographique/certifiée et ne garantit pas
   à lui seul une signature électronique qualifiée eIDAS.
6. L'importation d'images de signature, le texte libre, les dates, les tampons, l'OCR,
   la gestion de plusieurs signataires et l'historique avancé sont prévus pour les versions suivantes.

## Avant publication

- Tester sur plusieurs versions Android et iOS.
- Ajouter les icônes et les écrans de lancement.
- Ajouter une politique de confidentialité et les mentions légales.
- Vérifier les licences de toutes les dépendances.
- Effectuer des tests sur des PDF chiffrés, endommagés, lourds et avec pages pivotées.
- Faire une revue de sécurité du stockage des signatures.
