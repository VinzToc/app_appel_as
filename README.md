# 🏃 Application AS Lycée - Scanner QR Code

Application web pour gérer les présences de l'Association Sportive via scan de QR codes.

## 📋 Installation

### Étape 1 : Configuration de Google Sheets

1. Ouvrez votre Google Sheets : https://docs.google.com/spreadsheets/d/1bpIpkrsn0Fo_EKbQoyFaa654Ei1CSJRqtYU--Z9RIBM/edit?usp=sharing

2. Ajoutez les en-têtes dans la première ligne :
   - Colonne A : **N°**
   - Colonne B : **DATE**
   - Colonne C : **NOM**
   - Colonne D : **PRENOM**
   - Colonne E : **CLASSE**

3. Ouvrez l'éditeur de script :
   - Menu **Extensions** > **Apps Script**

4. Supprimez tout le code existant et collez le contenu du fichier `apps-script.gs`

5. Cliquez sur **Déployer** > **Nouveau déploiement**

6. Cliquez sur l'icône ⚙️ à côté de "Sélectionner le type" et choisissez **Application Web**

7. Configurez :
   - **Description** : Scanner AS Lycée
   - **Exécuter en tant que** : Moi
   - **Qui a accès** : Tout le monde
   
8. Cliquez sur **Déployer**

9. **IMPORTANT** : Copiez l'URL de déploiement qui ressemble à :
   ```
   https://script.google.com/macros/s/AKfycby.../exec
   ```

10. Autorisez l'application (cliquez sur "Autoriser l'accès")

### Étape 2 : Configuration de l'application HTML

1. Ouvrez le fichier `index.html`

2. Remplacez la ligne 237 :
   ```javascript
   const GOOGLE_SCRIPT_URL = 'https://script.google.com/macros/s/YOUR_DEPLOYMENT_ID/exec';
   ```
   
   Par votre URL de déploiement obtenue à l'étape 1.9

### Étape 3 : Publier sur GitHub Pages

1. Créez un nouveau dépôt sur GitHub

2. Uploadez le fichier `index.html`

3. Allez dans **Settings** > **Pages**

4. Sous "Source", sélectionnez **main** branch

5. Cliquez sur **Save**

6. Votre application sera disponible à l'adresse :
   ```
   https://votre-nom-utilisateur.github.io/nom-du-depot/
   ```

## 📱 Format des QR Codes

Les QR codes doivent contenir les informations au format suivant :
```
NOM|PRENOM|CLASSE
```

**Exemples :**
- `DUPONT|Marie|2nde A`
- `MARTIN|Lucas|1ère S`
- `BERNARD|Sophie|Terminale ES`

### Générer des QR Codes

#### Option 1 : Saisie individuelle
Remplissez le formulaire pour chaque élève et cliquez sur "Générer le QR Code".

#### Option 2 : Import fichier CSV
1. Préparez un fichier CSV avec vos données élèves
2. Les colonnes doivent être organisées ainsi :
   - **Colonne B** : NOM
   - **Colonne C** : PRENOM
   - **Colonne O** : CLASSE
3. Cliquez sur "Choisir un fichier" et sélectionnez votre CSV
4. Vérifiez l'aperçu des données détectées
5. Cliquez sur "Générer tous les QR Codes"

**Format CSV accepté :**
- Séparateur : point-virgule (;) ou virgule (,)
- La première ligne (en-têtes) est ignorée
- Exemple de structure :

```csv
ID;NOM;PRENOM;...autres colonnes...;CLASSE
1;DUPONT;Marie;...;2nde A
2;MARTIN;Lucas;...;1ère S
```

Un fichier d'exemple `exemple-eleves.csv` est fourni.

#### Option 3 : Saisie manuelle multiple
Collez une liste d'élèves au format : `NOM|PRENOM|CLASSE` (un par ligne).

### Sites pour générer des QR Codes manuellement
- https://www.qr-code-generator.com/
- https://www.qr-code-monkey.com/

Collez le texte au format ci-dessus et générez le QR code pour chaque élève.

## 🎯 Utilisation

1. Ouvrez l'application sur votre smartphone

2. Cliquez sur **"Démarrer le scan"**

3. Autorisez l'accès à la caméra

4. Pointez la caméra vers le QR code de l'élève

5. L'application :
   - Scanne automatiquement le QR code
   - Enregistre la présence dans Google Sheets
   - Affiche une confirmation
   - Ajoute l'élève à la liste des présents

6. Continuez à scanner les QR codes des autres élèves

7. Cliquez sur **"Arrêter"** quand vous avez terminé

## ✨ Fonctionnalités

### Application principale (index.html)
- ✅ Scan automatique des QR codes
- ✅ Enregistrement en temps réel dans Google Sheets
- ✅ Compteur de présents
- ✅ Liste des élèves scannés
- ✅ Prévention des doublons
- ✅ Design responsive (mobile-first)
- ✅ Numérotation automatique
- ✅ Date automatique du jour

### Générateur de QR Codes (qr-generator.html)
- ✅ Saisie individuelle d'élèves
- ✅ Import fichier CSV (colonnes B, C, O)
- ✅ Aperçu avant génération
- ✅ Saisie manuelle multiple
- ✅ Génération en masse
- ✅ Impression de tous les QR codes
- ✅ Design responsive

## 🔧 Dépannage

**La caméra ne s'active pas :**
- Vérifiez les autorisations de votre navigateur
- Utilisez HTTPS (obligatoire pour la caméra)

**Les données ne s'enregistrent pas :**
- Vérifiez que l'URL du Google Script est correcte
- Vérifiez que le déploiement est accessible à "Tout le monde"
- Regardez les logs dans Apps Script (Exécutions)

**QR Code non reconnu :**
- Vérifiez le format : NOM|PRENOM|CLASSE
- Assurez-vous que le QR code est net et bien éclairé

## 📊 Structure du Google Sheets

| N° | DATE     | NOM      | PRENOM | CLASSE    |
|----|----------|----------|--------|-----------|
| 1  | 06/02/26 | DUPONT   | Marie  | 2nde A    |
| 2  | 06/02/26 | MARTIN   | Lucas  | 1ère S    |
| 3  | 06/02/26 | BERNARD  | Sophie | Term ES   |

## 📄 Licence

Ce projet est libre d'utilisation pour les établissements scolaires.

## 📦 Fichiers fournis

- **index.html** : Application de scan QR code pour l'appel
- **qr-generator.html** : Générateur de QR codes pour les élèves
- **apps-script.gs** : Script à installer dans Google Sheets
- **exemple-eleves.csv** : Fichier CSV d'exemple avec la structure correcte
- **README.md** : Ce guide d'utilisation

---

**Développé pour l'Association Sportive**
