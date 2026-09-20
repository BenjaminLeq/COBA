<div align="center">

# COBA

### Générateur local de codes-barres pour Windows

![Version](https://img.shields.io/badge/version-2.2-2563EB)
![AutoIt](https://img.shields.io/badge/AutoIt-3.3.16.1-5C9BD5)
![Plateforme](https://img.shields.io/badge/plateforme-Windows_10%2F11-0078D4?logo=windows11&logoColor=white)
![Architecture](https://img.shields.io/badge/architecture-x64-6B7280)
![Portable](https://img.shields.io/badge/installation-portable-047857)

**Créez, prévisualisez et exportez des codes-barres Code 128 et Code 39, sans installation et sans service en ligne.**

</div>

---

COBA est un utilitaire Windows conçu pour générer rapidement des codes-barres à l'unité ou par lot. Le calcul, l'aperçu et les exports sont réalisés entièrement sur le poste : aucune donnée saisie n'est envoyée sur Internet.

L'application tient dans un seul fichier `COBA.exe`. Elle ne nécessite ni police de codes-barres, ni bibliothèque supplémentaire, ni programme d'installation.

<p align="center"><img width="917" height="739" alt="1" src="https://github.com/user-attachments/assets/be29cc02-6461-435d-a55a-2ed8de779abc" /></p>

## Fonctionnalités

- aperçu actualisé automatiquement après chaque modification ;
- Code 128 avec sélection optimisée des jeux A, B et C ;
- Code 39 avec checksum Mod 43 facultatif ;
- texte lisible facultatif, centré sous le symbole ;
- largeur du module et hauteur des barres configurables ;
- export PNG en 203, 300 ou 600 DPI ;
- export SVG vectoriel aux dimensions physiques exactes ;
- génération par lot depuis la première colonne d'un fichier CSV ;
- progression, annulation et journal des erreurs pour les lots ;
- mémorisation des derniers paramètres et du dernier dossier ;
- aide intégrée décrivant chaque réglage ;
- autotests internes du moteur d'encodage au démarrage.

## Formats pris en charge

| Format | Usage conseillé | Caractéristiques |
|---|---|---|
| **Code 128 automatique** | références, inventaire, logistique, identifiants | compact, jeux A/B/C sélectionnés automatiquement, caractères ASCII |
| **Code 39** | équipements existants, références alphanumériques simples | lettres majuscules, chiffres et caractères spéciaux limités, checksum Mod 43 facultatif |
| **PNG** | bureautique, impression à résolution connue | 203, 300 ou 600 DPI ; module ajusté au pixel le plus proche |
| **SVG** | PAO, impression et redimensionnement | vectoriel, indépendant du DPI, dimensions exprimées en millimètres |

> Le SVG est recommandé lorsqu'un code-barres doit être redimensionné ou intégré dans une mise en page destinée à l'impression.

## Téléchargement et démarrage

### Configuration requise

- Windows 10 ou Windows 11 ;
- système 64 bits ;
- droits d'écriture dans le dossier choisi pour les exports.

### Installation

1. Ouvrez la section **Releases** du dépôt GitHub.
2. Téléchargez `COBA.exe` depuis la dernière version disponible.
3. Placez-le dans un dossier accessible en écriture, par exemple `Documents\COBA`.
4. Lancez `COBA.exe`.

La release contient uniquement l'exécutable :

```text
COBA.exe
```

Aucune installation n'est nécessaire. Pour supprimer complètement COBA, fermez l'application, supprimez l'exécutable puis, si vous ne souhaitez pas conserver les préférences, le dossier `%LOCALAPPDATA%\COBA`.

> **Avertissement SmartScreen**  
> Selon la configuration du poste, Microsoft Defender SmartScreen peut afficher un avertissement au premier lancement d'un exécutable non signé. Vérifiez que le fichier provient bien de la page Releases officielle du projet avant de l'autoriser.

## Utilisation

1. Saisissez le texte ou le numéro dans **Données à encoder**.
2. Choisissez la symbologie et les dimensions souhaitées.
3. Activez si nécessaire **Afficher le texte sous le code-barres**.
4. Vérifiez l'aperçu, actualisé automatiquement.
5. Cliquez sur **Exporter PNG** ou **Exporter SVG**.

| Action | Résultat |
|---|---|
| **Exporter PNG** | crée une image matricielle avec la résolution sélectionnée |
| **Exporter SVG** | crée une image vectorielle aux dimensions physiques exactes |
| **Générer un lot** | traite la première colonne d'un fichier CSV |
| **Ouvrir le dossier** | ouvre le dernier dossier d'export utilisé |
| **Effacer** | vide la saisie et retire l'aperçu courant |
| **Aide** | ouvre la documentation intégrée des paramètres |

Le raccourci `Ctrl+S` ouvre directement l'export PNG lorsqu'un aperçu valide est disponible.

## Comprendre les paramètres

| Paramètre | Description | Conseil |
|---|---|---|
| **Symbologie** | définit la norme utilisée pour encoder la valeur | privilégiez Code 128 sauf contrainte particulière |
| **Module** | largeur de l'élément le plus fin | augmentez-la si le lecteur a des difficultés |
| **Hauteur** | hauteur physique des barres, hors marges et texte | adaptez-la au format de l'étiquette |
| **Résolution** | densité de pixels du fichier PNG | choisissez le DPI natif de l'imprimante |
| **Checksum Mod 43** | caractère de contrôle facultatif du Code 39 | activez-le seulement si le système destinataire l'attend |
| **Texte sous le code-barres** | affiche la valeur lisible sous les barres | utile pour l'identification manuelle |

### Module et résolution

Une largeur exprimée en millimètres ne correspond pas toujours à un nombre entier de pixels. Pour le PNG, COBA arrondit donc le module au pixel le plus proche et affiche sa largeur réelle sous l'aperçu.

| Résolution | Usage courant |
|---|---|
| **203 DPI** | imprimantes thermiques d'étiquettes |
| **300 DPI** | imprimantes classiques et bureautique |
| **600 DPI** | impression haute définition |

Le SVG ne subit pas cet arrondi : ses dimensions restent indépendantes du DPI sélectionné.

## Génération par lot

La fonction **Générer un lot** produit plusieurs codes-barres à partir de la première colonne d'un fichier CSV ou texte.

### Préparer le fichier

Dans Excel, utilisez **Fichier → Enregistrer sous → CSV UTF-8 (*.csv)**. Renommer simplement un fichier `.xlsx` en `.csv` ne convertit pas son contenu et COBA le refusera.

Exemple avec en-tête :

```csv
reference
PLOP123
MLOM456
TEST232
```

### Lancer le traitement

1. Cliquez sur **Générer un lot**.
2. Sélectionnez le fichier CSV.
3. Indiquez si sa première ligne est un en-tête.
4. Choisissez si une version SVG doit aussi être créée.
5. Sélectionnez le dossier de destination.

Une fenêtre indique l'avancement et permet d'annuler. Les lignes vides sont ignorées. Les lignes refusées sont consignées dans `COBA_erreurs.txt` dans le dossier de destination.

## Données et fichiers créés

| Élément | Emplacement ou comportement |
|---|---|
| Images PNG et SVG | dossier choisi lors de l'export |
| Dossier initial `exports` | créé à côté de l'exécutable lorsqu'il est accessible en écriture |
| Préférences | `%LOCALAPPDATA%\COBA\settings.ini` |
| Journal de lot | `COBA_erreurs.txt`, uniquement lorsqu'une erreur est rencontrée |
| Données saisies | traitées uniquement en mémoire sur le poste |

COBA n'intègre aucun mécanisme de télémétrie, de compte utilisateur ou de communication réseau.

## Limites actuelles

- le Code 128 accepte les caractères ASCII et limite la saisie à 120 caractères ;
- le Code 39 limite la saisie à 60 caractères ;
- les lots utilisent uniquement la première colonne du fichier ;
- les retours à la ligne intégrés dans une cellule CSV ne sont pas pris en charge ;
- EAN-13, UPC-A, GS1-128, QR Code et Data Matrix ne sont pas disponibles ;
- COBA ne commande pas directement une imprimante d'étiquettes.

## Dépannage

### Les listes de paramètres sont vides

Utilisez la dernière version disponible dans les Releases. Depuis la version 2.2 corrigée, toute préférence vide ou invalide est automatiquement remplacée par une valeur par défaut.

### Le fichier CSV est refusé

Vérifiez qu'il s'agit d'un véritable fichier CSV UTF-8. Un classeur Excel renommé conserve son format interne `.xlsx` et ne peut pas être lu comme du texte.

### Le code-barres est trop grand

Réduisez la largeur du module, la hauteur ou le DPI. La longueur de la valeur saisie influence également la largeur finale du symbole.

### Le lecteur ne reconnaît pas le code-barres

- vérifiez que le lecteur prend en charge la symbologie choisie ;
- évitez de recadrer les marges blanches autour du symbole ;
- imprimez l'image à sa taille réelle, sans adaptation automatique à la page ;
- essayez un module plus large ;
- désactivez le checksum Mod 43 si le système destinataire ne l'attend pas.

## Signaler un problème

Ouvrez une issue sur le dépôt GitHub en indiquant :

- la version de COBA et de Windows ;
- la symbologie et les paramètres utilisés ;
- une valeur d'exemple sans donnée confidentielle ;
- le message d'erreur exact ;
- une capture d'écran si elle facilite le diagnostic.

## Auteur

COBA est développé par **Benjamin Lequeux**.

---

<div align="center">

**COBA 2.2 — Génération locale de codes-barres pour Windows**

</div>
