---
title: Configuration de la carte SD
---

Cette page est destinée à préparer votre carte SD pour votre appareil. Au cours de ce processus, nous formaterons la carte SD et vérifierons qu'il n'y a pas d'erreurs sur la carte.

::: danger

Assurez-vous de sauvegarder le contenu de votre carte SD AVANT de continuer. Toutes les données de votre carte SD seront EFFACÉES pendant le processus.

:::

::::: tabs

:::: tab name="Windows" os="windows"

### Section I - Formatage de votre carte SD avec SD Formatter

::: tip

Cette section formate la carte SD selon les spécifications de la SD Card Association. Cela peut résoudre de nombreux problèmes pouvant survenir lors de l'exécution d'applications homebrews.

:::

::: danger

Toutes les cartes SD de 64 Go ou plus seront formatées en `exFAT` au cours de ce processus. Vous _devez_ suivre la section II pour reformater en `FAT32`.

:::

1. Téléchargez la dernière version de [SD Formatter](https://www.sdcard.org/downloads/formatter/sd-memory-card-formatter-for-windows-download/)
   - Si le lien ci-dessus ne fonctionne pas pour vous, téléchargez [depuis archive.org](https://web.archive.org/web/20220626204124/https://www.sdcard.org/downloads/formatter/sd-memory-card-formatter-for-windows-download/)
   - Acceptez les conditions générales d'utilisation pour lancer le téléchargement
1. Exécutez `SD Card Formatter Setup` (le fichier `.exe`) avec les droits d'administrateur dans le fichier `.zip` téléchargé, puis installez le programme
1. Exécutez `SD Card Formatter` à partir du menu Démarrer avec les droits d'administrateur
1. Sélectionnez votre carte SD
1. Assurez-vous que la case `Quick Format` (« formatage rapide ») est cochée
1. Lancez le processus de formatage

### Section II - Formatage de votre carte SD avec GUIFormat

Cette section formate les cartes SD supérieures à 32 Go en FAT32.

::: tip

Si votre carte SD a une capacité de 32 Go ou moins, passez à la section III.

:::

1. Téléchargez la dernière version de [GUIFormat](http://ridgecrop.co.uk/index.htm?guiformat.htm)
   - Cliquez sur l'image du site pour télécharger l'application
1. Exécutez GUIFormat avec les droits d'administrateur
1. Sélectionnez votre lettre de lecteur
1. Définissez l'unité de taille d'allocation (`Allocation size unit`) à `32768`
   - Si cette taille est trop grande pour votre SD, définissez-la à la plus haute qui fonctionne
1. Assurez-vous que la case `Quick Format` (« formatage rapide ») est cochée
1. Lancez le processus de formatage

![](https://user-images.githubusercontent.com/1000503/83831499-8f330b80-a6b5-11ea-9ab9-ec2196150751.png)

### Section III - Vérification des erreurs
1. Allez dans la fenêtre des propriétés de votre carte SD
   - `Explorateur Windows` -> `Ce PC` -> Clic droit sur votre carte SD -> `Propriétés`
1. Dans l'onglet Outils, sélectionnez `Vérifier maintenant`
1. Cochez à la fois `Réparer automatiquement les erreurs de système de fichiers` et `Rechercher et tenter une récupération des secteurs défectueux`
1. Lancez le processus de vérification

Cette opération permet de scanner la carte SD et de corriger les erreurs qu'elle trouve.

### Section IV - Vérification de la lecture/écriture de la carte SD

1. Téléchargez et extrayez [l'archive h2testw](http://www.heise.de/ct/Redaktion/bo/downloads/h2testw_1.4.zip) n'importe où sur votre ordinateur
   - Si le lien ci-dessus ne fonctionne pas pour vous, téléchargez [depuis archive.org](https://web.archive.org/web/20210912045431/http://www.heise.de/ct/Redaktion/bo/downloads/h2testw_1.4.zip)
   - Elle peut également être extraite sur un périphérique externe tant qu'il ne s'agit pas de votre carte SD
1. Avec votre carte SD insérée dans votre ordinateur, exécutez `h2testw.exe`
1. Sélectionnez la langue dans laquelle vous souhaitez voir h2testw. Étant donné qu'il n'est pas disponible en français, les noms anglais seront utilisés et traduits pour ce guide
1. Définissez la lettre de lecteur de votre carte SD en tant que cible
1. Assurez-vous que `All available space` (« Tout l'espace disponible ») est sélectionné
1. Cliquez sur `Write + Verify` (« Écrire + Vérifier »)
- Attendez que le processus se termine

::: tip

Si le test affiche le résultat `Test finished without errors` (« Test terminé sans erreur »), votre carte SD est saine et vous pouvez supprimer tous les fichiers `.h2w` sur votre carte SD.

:::

::: danger

Si le test donne d'autres résultats, votre carte SD est peut-être corrompue ou endommagée et vous devrez peut-être la remplacer !

:::

::::

:::: tab name="Linux" os="other"

::: tip

Si TWiLight Menu++ ne démarre pas après avoir suivi cette méthode, veuillez plutôt suivre la méthode Windows, soit en redémarrant sous Windows, soit en exécutant une machine virtuelle Windows

:::

### Section I - Formatage de votre carte SD
1. Assurez-vous que votre carte SD n'est **pas** insérée dans votre machine Linux
1. Lancez le terminal Linux
1. Tapez `watch "lsblk"`
1. Insérez votre carte SD dans votre machine Linux
1. Observez le résultat. Cela devrait ressembler à quelque chose comme cela :
```
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
mmcblk0     179:0    0   3,8G  0 disk
└─mmcblk0p1 179:1    0   3,7G  0 part /run/media/user/FFFF-FFFF
```
1. Prenez note du nom de l'appareil. Dans notre exemple ci-dessus, c'était `mmcblk0p1`
  + Si `RO` est réglé sur 1, assurez-vous que l'interrupteur de verrouillage n'est pas glissé vers le bas
1. Appuyez sur CTRL + C pour quitter le menu
1. Suivez les instructions relatives à la capacité de votre carte SD :
    - 2 Go ou moins : `sudo mkdosfs /dev/(nom de l'appareil ci-dessus) -s 64 -F 16`
         - Cela crée une seule partition FAT16 avec une taille de cluster de 32 ko sur la carte SD
    - 4 Go ou plus : `sudo mkdosfs /dev/(nom de l'appareil ci-dessus) -s 64 -F 32`
         - Cela crée une seule partition FAT32 avec une taille de cluster de 32 ko sur la carte SD

### Section II - Utilisation de F3
1. Téléchargez et extrayez [l'archive F3](https://github.com/AltraMayor/f3/archive/v7.2.zip) n'importe où sur votre ordinateur.
1. Lancez le terminal dans le dossier F3
1. Exécutez `make` pour compiler F3
1. Avec votre carte SD insérée et montée, exécutez `./f3write <le point de montage de votre carte SD>`
   - Attendez que le processus soit terminé. Regardez ci-dessous pour un exemple de sortie du terminal :
   ```
   $ ./f3write /media/michel/6135-3363/
   Free space: 29.71 GB
   Creating file 1.h2w ... OK!
   ...
   Creating file 30.h2w ... OK!
   Free space: 0.00 Byte
   Average Writing speed: 4.90 MB/s
   ```
1. Exécutez `./f3read <le point de montage de votre carte SD>`
- Attendez que le processus soit terminé. Regardez ci-dessous pour un exemple de sortie du terminal :
   ```
   $ ./f3read /media/michel/6135-3363/
                     SECTORS      ok/corrupted/changed/overwritten
   Validating file 1.h2w ... 2097152/        0/      0/      0
   ...
   Validating file 30.h2w ... 1491904/        0/      0/      0

      Data OK: 29.71 GB (62309312 sectors)
   Data LOST: 0.00 Byte (0 sectors)
               Corrupted: 0.00 Byte (0 sectors)
      Slightly changed: 0.00 Byte (0 sectors)
            Overwritten: 0.00 Byte (0 sectors)
   Average Reading speed: 9.42 MB/s
   ```

___

::: tip

Si le test affiche le résultat `Data LOST: 0.00 Byte (0 sectors)` votre carte SD est saine et vous pouvez supprimer tous les fichiers `.h2w` sur votre carte SD.

:::

::: danger

Si le test donne d'autres résultats, votre carte SD est peut-être corrompue ou endommagée et vous devrez peut-être la remplacer !

:::

::::

:::: tab name="macOS" os="macos"

### Section I - Formatage de votre carte SD avec SD Formatter

::: tip

Cette section formate la carte SD selon les spécifications de la SD Card Association. Cela peut résoudre de nombreux problèmes pouvant survenir lors de l'exécution d'applications homebrews.

:::

::: danger

Toutes les cartes SD de 64 Go ou plus seront formatées en `exFAT` au cours de ce processus. Vous _devez_ suivre la section II pour reformater en `FAT32`.

:::

1. Téléchargez la dernière version de [SD Formatter](https://www.sdcard.org/downloads/formatter/sd-memory-card-formatter-for-mac-download/)
   - Acceptez les conditions générales d'utilisation pour lancer le téléchargement
1. Exécutez `Install SD Card Formatter` (le fichier `.mpkg`) dans le fichier `.zip` téléchargé
1. Exécutez `SD Card Formatter`
1. Sélectionnez votre carte SD
1. Assurez-vous que la case `Quick Format` (« formatage rapide ») est cochée
1. Lancez le processus de formatage

### Section II - Formatage de votre carte SD avec l'Utilitaire de disque

Cette section formate les cartes SD supérieures à 32 Go en FAT32.

::: tip

Si votre carte SD a une capacité de 32 Go ou moins, passez à la section III.

:::

#### OS X El Capitan (10.11) et versions ultérieures

1. Lancez l'application Utilitaire de disques
1. Sélectionnez `Afficher tous les appareils` dans le panneau `Présentation` en haut à gauche
1. Sélectionnez votre carte SD dans la barre latérale
   - Assurez-vous de choisir le bon périphérique, sinon vous risquez d'effacer accidentellement le mauvais lecteur !
1. Cliquez sur `Effacer` en haut
1. Assurez-vous que le `Format` est défini à `MS-DOS (FAT32)`
   - De El Capitan (10.11) à Catalina (10.15) choisissez `MS-DOS (FAT)`
1. Assurez-vous que `Schéma` est réglé sur `Master Boot Record`
   - Si `Schéma` n'apparaît pas, cliquez sur `Annuler` et assurez-vous de choisir le périphérique au lieu d'un volume
1. Cliquez sur `Effacer`, puis cliquez sur `Fermer`

#### OS X Yosemite (10.10) et versions antérieures
1. Lancez l'application Utilitaire de disques
1. Sélectionnez votre carte SD dans la barre latérale
   - Assurez-vous de choisir le bon périphérique, sinon vous risquez d'effacer accidentellement le mauvais lecteur !
1. Cliquez sur `Partitionner` en haut
   - Si `Partitionner` n'apparaît pas, assurez-vous de choisir le périphérique au lieu d'un volume
1. Assurez-vous que la `Configuration de volume` est définie à `1 partition`
1. Assurez-vous que le `Format` est défini à `MS-DOS (FAT)`
1. Depuis le bouton Options (en dessous de la table de partitions), sélectionnez `Master Boot Record`.
1. Cliquez sur `OK` -> `Appliquer` -> `Partition`

### Section III - Utilisation de F3
1. Ouvrez le terminal
1. Installez F3 depuis brew en exécutant `brew install f3`
   - Si vous n'avez pas brew, installez-le en suivant les instructions de [brew.sh](https://brew.sh)
1. Avec votre carte SD insérée et montée, exécutez `./f3write <le point de montage de votre carte SD>`
   - Attendez que le processus soit terminé. Regardez ci-dessous pour un exemple de sortie du terminal :
   ```
   $ f3write /Volumes/SD\ CARD
   Free space: 29.71 GB
   Creating file 1.h2w ... OK!
   ...
   Creating file 30.h2w ... OK!
   Free space: 0.00 Byte
   Average Writing speed: 4.90 MB/s
   ```
1. Exécutez `f3read <le point de montage de votre carte SD>`
   - Attendez que le processus soit terminé. Regardez ci-dessous pour un exemple de sortie du terminal :
   ```
   $ f3read /Volumes/SD\ CARD
                     SECTORS      ok/corrupted/changed/overwritten
   Validating file 1.h2w ... 2097152/        0/      0/      0
   ...
   Validating file 30.h2w ... 1491904/        0/      0/      0

      Data OK: 29.71 GB (62309312 sectors)
   Data LOST: 0.00 Byte (0 sectors)
               Corrupted: 0.00 Byte (0 sectors)
      Slightly changed: 0.00 Byte (0 sectors)
            Overwritten: 0.00 Byte (0 sectors)
   Average Reading speed: 9.42 MB/s
   ```

___

::: tip

Si le test affiche le résultat `Data LOST: 0.00 Byte (0 sectors)` votre carte SD est saine et vous pouvez supprimer tous les fichiers `.h2w` sur votre carte SD.

:::

::: danger

Si le test donne d'autres résultats, votre carte SD est peut-être corrompue ou endommagée et vous devrez peut-être la remplacer !

:::

::::

:::::

::: tip

Vous pouvez maintenant restaurer le contenu de votre carte SD et continuer.

:::

