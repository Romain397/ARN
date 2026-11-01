# ARN — État de l'infrastructure

Point d'avancement : **1er novembre 2026**, fuseau **Europe/Paris**.

## Origine et portée

Ce document consigne les faits rapportés par le responsable du projet pour ce point d'avancement. Les validations du serveur n'ont pas été rejouées pendant cette intervention documentaire. Seuls le dépôt local, son historique et la documentation ont été examinés ; aucun résultat de commande du serveur n'est inventé.

| Statut | Signification |
|---|---|
| **VALIDÉ** | Fonctionnement ou vérification rapporté comme réalisé dans le compte rendu |
| **PRÉPARÉ** | Élément disponible ou préparation effectuée, sans validation du déploiement final |
| **À TESTER** | Vérification ou essai restant à réaliser |
| **NON INSTALLÉ** | Installation non effectuée |
| **BLOQUÉ / RISQUE** | Condition à résoudre avant une opération sensible ; ne prouve pas un échec observé |

## Matériel et systèmes

| Élément | État déclaré au 1er novembre |
|---|---|
| Processeur | AMD Ryzen 9 5900X, 12 cœurs / 24 threads |
| Mémoire | 32 Go de RAM |
| Carte mère | ASUS Prime B450M-A II |
| SSD Ubuntu | Samsung 870 EVO 1 To, dédié à Ubuntu Server et au futur laboratoire |
| SSD Windows | Kingston NVMe 500 Go, réservé à Windows 11 |
| Autres SSD | Deux Samsung réservés aux données Windows et aux jeux |
| Windows 11 | Jeux et utilisation quotidienne |
| Ubuntu Server | 22.04.5 LTS, noyau actuel `5.15.0-202-generic` |
| Virtualisation | **VALIDÉ** : AMD-V et modules KVM opérationnels sur le noyau Ubuntu actuel |

Les SSD Windows, de données et de jeux ne doivent être ni formatés ni modifiés.

## Démarrage sécurisé — configuration figée

L'ensemble suivant est **VALIDÉ** selon le compte rendu et doit rester figé :

- Secure Boot activé.
- Menu rEFInd fonctionnel en **1920 × 1080**, avec deux choix : Windows 11 et Ubuntu Server.
- Ancienne erreur `Invalid Parameter` corrigée.
- GRUB masqué après la sélection d'Ubuntu.
- Ordre UEFI : `0004,0007,0000,0002`.
- Entrée Ubuntu directe `Boot0007` conservée comme secours.
- rEFInd **0.14.2** recompilé avec correction de l'alignement SBAT à `0x10000000`.
- Nouveau rEFInd signé avec une clé MOK ARN enregistrée.
- Shim **16.1** utilisé pour la chaîne rEFInd corrigée.
- Sauvegarde de la configuration de démarrage effectuée sur le SSD Ubuntu.

Le chemin exact de la sauvegarde n'est pas fourni. Le retrouver et en contrôler la disponibilité avant toute future installation ; ne pas consigner de contenu sensible dans Git.

**BLOQUÉ / RISQUE** : toute installation susceptible de changer les chargeurs EFI, rEFInd, GRUB ou l'ordre de démarrage doit être examinée avant exécution. Aucun de ces composants n'est modifié par ce point documentaire.

## Réseau et accès distant

| Élément | Statut | État rapporté ou contrôle restant |
|---|---|---|
| SSH sur Ubuntu | **VALIDÉ** | Accès SSH fonctionnel ; cela ne valide pas à lui seul le chemin Tailscale |
| Tailscale | **VALIDÉ** | Installé, actif et activé au démarrage |
| VPN privé | **VALIDÉ** | Serveur et PC Windows connectés au même VPN |
| Communication extérieure | **VALIDÉ** | Communication Tailscale testée depuis une connexion Internet extérieure |
| SSH via Tailscale | **À TESTER** | Confirmation définitive à retrouver ou test SSH à effectuer depuis l'extérieur |
| Horloge | **VALIDÉ** | Synchronisation NTP active, fuseau Europe/Paris |

Aucune adresse IP personnelle, identité VPN, clé, mot de passe ou donnée d'authentification ne doit figurer dans les comptes rendus versionnés.

## EVE-NG Community

**NON INSTALLÉ** : version ciblée **6.2.0-4 sur Ubuntu Server 22.04**.

| Élément | Statut | Limite de la validation |
|---|---|---|
| Dépôt officiel EVE-NG | **PRÉPARÉ** | Ajout rapporté |
| Paquet EVE-NG `6.2.0-4` | **PRÉPARÉ** | Téléchargé ; pas installé |
| Simulation APT | **VALIDÉ** | 517 nouveaux paquets, aucune suppression et aucune mise à jour ; simulation uniquement |
| Noyau `6.7.5-eveng-6-ksm+` | **PRÉPARÉ** | Téléchargé et extrait |
| Copie du noyau signée ARN | **PRÉPARÉ** | Signature vérifiée avec succès selon le compte rendu |
| Installation et démarrage de ce noyau | **À TESTER** | Copie signée ni installée ni testée au démarrage |
| Modules KVM AMD du noyau Ubuntu actuel | **VALIDÉ** | Ne valide pas les modules du noyau EVE-NG |
| Modules KVM et réseau du noyau EVE-NG | **À TESTER** | Inspection à terminer et signatures à vérifier |
| Scripts d'installation | **BLOQUÉ / RISQUE** | Audit requis avant toute installation |
| Services, accès Web et laboratoires EVE-NG | **À TESTER** | Tests après installation ; aucun succès déclaré à ce stade |

La dernière commande proposée pour vérifier les modules et les scripts EVE-NG **n'a pas été exécutée**. Son texte n'est pas fourni dans ce point d'avancement ; le retrouver et le relire avant exécution.

## Suivi du dépôt

Avant ce point documentaire, la branche locale `main` était propre et alignée sur la référence locale `origin/main`, au commit `35c3df9`. Aucun accès distant n'a été effectué pour confirmer l'état actuel de GitHub.

Le dépôt contient une architecture cible NetOps et un prototype de supervision documenté dans [monitoring/README.md](../monitoring/README.md). Cet historique ne constitue pas une preuve de déploiement de la supervision sur EVE-NG.

La présente intervention concerne uniquement la documentation. Elle n'installe aucun paquet et ne modifie aucun programme, script opérationnel, fichier de configuration système ou de supervision.

## Documents de reprise

- [Préparation EVE-NG, dépendances et risques](ARN-EVE-NG-INSTALLATION.md)
- [Checklist de reprise](ARN-NEXT-STEPS.md)
- [Historique du projet](../CHANGELOG.md)
