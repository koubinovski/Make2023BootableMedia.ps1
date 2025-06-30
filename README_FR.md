# Make2023BootableMedia – Version compatible PCA 2023

## 📌 Description
Ceci est une version modifiée du script `Make2023BootableMedia.ps1` de Microsoft.  
Il permet de créer une **clé USB ou un CD/DVD amorçable** à partir d’**ISOs Windows Insider**, même si le Secure Boot exige des exécutables EFI signés avec **PCA 2023**.

## ❗ Pourquoi ce script est nécessaire
Les ISOs Windows Insider récentes contiennent encore des chargeurs (`bootx64.efi`, `bootmgr.efi`) signés avec le certificat **PCA 2011**.  
Microsoft applique désormais des mises à jour de Secure Boot qui **révoquent ces signatures** via la liste DBX, notamment après la faille CVE-2020-0689.

Conséquences :
- Échec du démarrage sur les systèmes exigeant PCA 2023
- Écran noir ou retour au BIOS avec les ISOs officielles

## ✅ Ce que fait ce script
- Remplace le chargeur EFI par `bootmgfw_EX.efi` (signé PCA 2023)
- Prend en charge les supports **formatés en NTFS** (fichiers `install.wim` > 4 Go)
- Supprime le bloc de signature Authenticode pour éviter les erreurs d'exécution

## 🛠 Prérequis
- Un système avec le Secure Boot **mis à jour pour PCA 2023**
- Une ISO Insider Windows (via UUP Dump, Microsoft, etc.)

## 📦 Dépendances
Pour exécuter correctement le script, les éléments suivants doivent être installés :

- **PowerShell 5.1 ou supérieur**
- **Droits administrateur**
- Accès aux fichiers suivants :
  - Le fichier `bootmgfw_EX.efi` signé PCA 2023
  - Une ISO Insider valide (`.iso`)
  - Une clé USB ou un CD/DVD

Dépendances supplémentaires :
- Le **Windows ADK (Assessment and Deployment Kit)** doit être installé  
- Le **module complémentaire Windows PE Add-on for ADK** est également nécessaire  
  Ces composants fournissent des outils comme `oscdimg.exe`, `copype.cmd` et les fichiers du boot PE requis.

👉 Vous pouvez télécharger l’ADK et le module PE ici :  
https://learn.microsoft.com/fr-fr/windows-hardware/get-started/adk-install

## 📅 Utilisation
```powershell
.\Make2023BootableMedia.ps1 -MediaPath D:\ -ISOSourcePath C:\ISO\Win11_Insider.iso
```
> Pour afficher toutes les options :  
> `Get-Help .\Make2023BootableMedia.ps1 -Detailed`

## 📟 Licence
Ce projet est distribué sous la licence [BSD-2-Clause-Patent](./LICENSE), également utilisée par Microsoft.  
Elle inclut une clause de brevet pour les contributions couvertes.  
Voir [LICENSE](./LICENSE) pour les conditions complètes.

## ✏️ Auteur et modifications
Modifié et maintenu par **Yoann Deferi** (alias **koubinovski**) – Juin 2025  
Script original publié par Microsoft dans le dépôt [`secureboot_objects`](https://github.com/microsoft/secureboot_objects).

👉 [Read in English](./README.en.md)
