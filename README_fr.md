# Manuel d'utilisation — DuplicateFinder

> ![Capture d'écran de l'application](capturas/main.png)
> *Vue principale de DuplicateFinder avec la barre de scan et le tableau des résultats.*

---

## Table des matières

1. [Introduction](#1-introduction)
2. [Configuration requise](#2-configuration-requise)
3. [Interface principale](#3-interface-principale)
4. [Sélection des dossiers](#4-selection-des-dossiers)
5. [Modes de détection](#5-modes-de-detection)
6. [Progression du scan](#6-progression-du-scan)
7. [Résultats](#7-resultats)
8. [Actions sur les fichiers](#8-actions-sur-les-fichiers)
9. [Exportation des résultats](#9-exportation-des-resultats)
10. [Préférences](#10-preferences)
11. [Conseils et bonnes pratiques](#11-conseils-et-bonnes-pratiques)

---

## 1. Introduction

**DuplicateFinder** est une application macOS qui trouve et gère les fichiers en double sur votre disque. Elle analyse un ou plusieurs dossiers, calcule une empreinte SHA-256 pour chaque fichier et regroupe les identiques, vous permettant de les examiner, ouvrir, supprimer ou exporter un rapport.

### Fonctionnalités principales

- Analyse récursive de plusieurs dossiers simultanément.
- Deux modes de détection : **Fiable** (basé sur le contenu, SHA-256) et **Rapide** (nom + taille).
- Filtres par taille, extensions et dossiers exclus.
- Tableau triable avec recherche dans les résultats.
- Actions individuelles et par lot : ouvrir, révéler dans le Finder, mettre à la Corbeille ou supprimer définitivement.
- Exportation en CSV et JSON avec tous les emplacements des fichiers en double.
- Interface localisée en 8 langues.

---

## 2. Configuration requise

- **macOS** 14.0 (Sonoma) ou ultérieur.
- **Apple Silicon** ou **Intel**.
- Aucun paquet ou dépendance externe requis.

---

## 3. Interface principale

![Disposition de l'interface](capturas/interfaz.png)

La fenêtre est divisée en trois zones :

| Zone | Description |
|------|-------------|
| **Barre supérieure (ScanView)** | Sélection des dossiers, choix du mode de détection, contrôles de démarrage/annulation. |
| **Barre de statistiques** | Métriques globales (fichiers totaux, doublons, groupes, espace récupérable) et bouton d'exportation. |
| **Tableau des résultats** | Liste triable des groupes de doublons avec recherche. |

---

## 4. Sélection des dossiers

![Sélection des dossiers](capturas/seleccion-carpetas.png)

1. Cliquez sur le bouton **« Choisir un dossier… »** (icône de dossier).
2. La boîte de dialogue standard de macOS s'ouvre. Sélectionnez **un ou plusieurs dossiers** en maintenant ⌘ (Commande).
3. Les dossiers **s'accumulent** dans la liste. Vous pouvez ajouter d'autres dossiers lors de sélections ultérieures.
4. Pour effacer la sélection, cliquez sur le bouton **« Effacer »** (icône ✕) qui apparaît à côté.

> Le bouton **« Lancer le scan »** reste désactivé jusqu'à ce qu'au moins un dossier soit sélectionné. Vous pouvez également glisser un dossier depuis le Finder directement sur la fenêtre.

---

## 5. Modes de détection

DuplicateFinder propose deux modes, sélectionnables via un contrôle segmenté dans la barre supérieure :

| Mode | Description |
|------|-------------|
| **Fiable** | Calcule le haché SHA-256 du **contenu intégral** de chaque fichier. Garantit l'absence de faux positifs, mais est plus lent car il lit chaque fichier. |
| **Nom + Taille** | Compare uniquement le nom (insensible à la casse) et la taille en octets. Très rapide (aucune lecture de fichier), mais peut produire des faux positifs si des fichiers différents partagent le même nom et la même taille. |

> Le mode par défaut est défini dans **Préférences → Détection**.

---

## 6. Progression du scan

Pendant un scan, la barre supérieure affiche la phase en cours :

| Phase | Indicateur |
|-------|------------|
| **Scan en cours…** | Compteur de fichiers traités dans le dossier. |
| **Comparaison…** | Barre de progression avec le nombre de hachés calculés sur le total des candidats. |
| **Calcul en cours…** | Progression de l'insertion en base de données et du calcul des agrégats. |
| **Terminé** | Icône de coche verte. |
| **Annulé** | Icône orange. |

Vous pouvez annuler le scan à tout moment en cliquant sur le bouton **« Annuler »**.

---

## 7. Résultats

![Tableau des résultats](capturas/resultados.png)

Une fois le scan terminé, le tableau des résultats apparaît avec les colonnes suivantes :

| Colonne | Description |
|---------|-------------|
| **Nom** | Nom du fichier avec son icône. |
| **Taille** | Taille de chaque copie. |
| **Copies** | Nombre de doublons pour ce fichier. |
| **Taille × Copies** | Espace total occupé par toutes les copies. |
| **Emplacement** | Chemin complet de chaque copie, avec boutons d'action. |

Vous pouvez **trier** le tableau en cliquant sur n'importe quel en-tête de colonne. Vous pouvez également **rechercher** des fichiers par nom ou chemin à l'aide du champ de recherche en bas.

### Barre de statistiques

Quatre métriques sont affichées au-dessus des résultats :

- **Fichiers totaux** : tous les fichiers scannés.
- **Doublons** : fichiers appartenant à un groupe de doublons.
- **Groupes** : ensembles de fichiers identiques.
- **Récupérable** : espace libéré si toutes les copies en double (moins une par groupe) sont supprimées.

---

## 8. Actions sur les fichiers

Chaque fichier en double dans la colonne « Emplacement » dispose de boutons d'action :

| Bouton | Action |
|--------|--------|
| 👁 (Œil) | Ouvrir le fichier avec l'application par défaut. |
| 📁 (Dossier) | Révéler le fichier dans le Finder. |
| 🗑 (Corbeille) | Mettre à la Corbeille (ou supprimer définitivement, selon les préférences). |

### Suppression par lot

Vous pouvez sélectionner plusieurs fichiers en cochant la case carrée à côté de chacun :

1. Cochez les fichiers que vous souhaitez supprimer.
2. Le bouton **« Supprimer la sélection (N) »** apparaît dans la barre de statistiques.
3. Cliquez dessus pour confirmer et effectuer la suppression.

> Vous pouvez modifier le comportement de suppression dans **Préférences → Général** : activez ou désactivez « Déplacer les fichiers vers la Corbeille ».

---

## 9. Exportation des résultats

Cliquez sur le bouton **« Exporter »** (icône de partage) dans la barre de statistiques et choisissez :

- **CSV** — Fichier texte séparé par des virgules, compatible avec Excel, Numbers et les tableurs.
- **JSON** — Format structuré, idéal pour un traitement programmatique.

Les deux formats incluent **chaque copie de chaque fichier en double** (pas seulement une par groupe), avec les champs : nom, chemin, taille, nombre de copies, espace total occupé et haché SHA-256.

Une boîte de dialogue `NSSavePanel` s'ouvre pour choisir la destination et le nom du fichier.

---

## 10. Préférences

Appuyez sur `⌘,` (Commande + ,) pour ouvrir les préférences, organisées en quatre onglets.

### Général

| Option | Description |
|--------|-------------|
| **N premiers résultats** | Nombre maximal de lignes dans le tableau des résultats (10–100 000). |
| **Déplacer vers la Corbeille** | Lorsqu'activé, les fichiers sont envoyés à la Corbeille au lieu d'être supprimés définitivement. |
| **Stratégie de conservation** | Stratégie pour sélectionner automatiquement la copie à conserver (la plus ancienne, la plus récente ou le chemin le plus court). |
| **Apparence** | Mode clair, sombre ou automatique. |

### Détection

| Option | Description |
|--------|-------------|
| **Mode par défaut** | Mode de détection sélectionné à l'ouverture de l'application. |

### Filtres

| Option | Description |
|--------|-------------|
| **Taille min / max** | Plage de taille en octets. Les fichiers en dehors de cette plage sont ignorés. |
| **Inclure les cachés** | Inclure les fichiers et dossiers cachés (commençant par `.`). |
| **Suivre les liens symboliques** | Lorsqu'activé, les liens symboliques sont suivis pendant le scan. |
| **Extensions autorisées** | Liste séparée par des virgules (ex. `jpg, png, mp4`). Vide = toutes les extensions. |
| **Dossiers exclus** | Liste séparée par des virgules des noms de dossiers ignorés pendant le scan (ex. `node_modules, .git`). |

### Langue

Changez la langue de l'interface parmi les 8 disponibles. L'application peut nécessiter un redémarrage pour que le changement soit pleinement appliqué.

---

## 11. Conseils et bonnes pratiques

1. **Commencez par le mode Rapide** si vous avez beaucoup de dossiers. C'est beaucoup plus rapide et peut trouver la plupart des doublons.
2. **Utilisez le mode Fiable pour les décisions finales** avant de supprimer — surtout lorsque les noms de fichiers ne correspondent pas — pour éviter les faux positifs.
3. **Choisissez des dossiers spécifiques**, pas votre disque entier. Analyser seulement Téléchargements, Documents et Bureau réduit considérablement le temps et le bruit.
4. **Vérifiez les emplacements** dans la colonne « Emplacement » avant de supprimer. Un doublon pourrait se trouver dans un dossier système où il devrait rester.
5. **Exportez un CSV** avant de nettoyer pour conserver un enregistrement des fichiers supprimés.
6. **Configurez des filtres** lorsque vous recherchez des types de fichiers spécifiques (ex. seulement les images `.jpg` et `.png`).
7. **Utilisez le bouton « Effacer »** pour repartir à zéro avec une nouvelle sélection de dossiers sans quitter l'application.

---

> **DuplicateFinder** — [mdc](https://github.com/migueldc-oss/DuplicateFinder)
>
> Documentation générée le 1er juillet 2026.
