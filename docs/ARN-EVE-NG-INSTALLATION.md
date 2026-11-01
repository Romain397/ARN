# ARN — Préparation de l'installation EVE-NG

Point d'avancement : **1er novembre 2026**. Cible : **EVE-NG Community 6.2.0-4 sur Ubuntu Server 22.04**.

## État de référence

**EVE-NG est NON INSTALLÉ.** Les éléments ci-dessous proviennent du compte rendu du responsable du projet ; aucune commande d'installation ou de vérification du serveur n'a été exécutée pendant cette mise à jour documentaire.

La configuration de démarrage validée est décrite dans [ARN-STATUS.md](ARN-STATUS.md). Elle doit rester figée, avec Secure Boot actif, le noyau Ubuntu `5.15.0-202-generic` fonctionnel et l'entrée Ubuntu directe `Boot0007` conservés comme secours.

## Préparation réalisée et dépendances

| Élément | Statut | Résultat rapporté |
|---|---|---|
| Dépôt officiel EVE-NG | **PRÉPARÉ** | Dépôt ajouté |
| Paquet Community `6.2.0-4` | **PRÉPARÉ** | Téléchargé |
| Résolution APT simulée | **VALIDÉ** | 517 nouveaux paquets, 0 suppression, 0 mise à jour |
| Noyau `6.7.5-eveng-6-ksm+` | **PRÉPARÉ** | Téléchargé et extrait |
| Copie du noyau signée avec la clé ARN | **PRÉPARÉ** | Signature vérifiée avec succès |
| KVM AMD sur le noyau Ubuntu actuel | **VALIDÉ** | Modules disponibles et virtualisation opérationnelle |

Le détail des 517 paquets n'a pas été fourni. Le nombre décrit la simulation rapportée, pas une liste de dépendances figée ni des paquets déjà installés. Avant l'installation future, conserver une sortie assainie de la résolution APT et examiner tout changement par rapport à cette référence.

La copie signée du noyau EVE-NG **n'est pas le noyau installé et n'a pas été testée au démarrage**. La vérification de cette signature ne valide ni les signatures des modules, ni leur chargement, ni le fonctionnement d'EVE-NG.

## Contrôles encore nécessaires

Tous les contrôles de cette section sont **À TESTER** :

1. Terminer l'inspection des modules du noyau EVE-NG extrait.
2. Identifier les modules KVM AMD et réseau nécessaires, puis vérifier leurs signatures et leur compatibilité avec les exigences Secure Boot de la machine.
3. Auditer les scripts d'installation du paquet noyau et du paquet EVE-NG : opérations sur les disques, SSH, services, réseau, fichiers de démarrage et éventuels redémarrages.
4. Déterminer si les scripts préservent la copie signée, le noyau Ubuntu de secours et la chaîne de démarrage fonctionnelle.
5. Préparer une procédure d'installation et de retour au noyau Ubuntu, compatible avec la configuration de démarrage figée.

La dernière commande proposée pour l'inspection des modules et des scripts **n'a pas encore été exécutée**. Son texte et ses résultats ne sont pas disponibles ici. Retrouver la commande, vérifier sa portée avant de la lancer et consigner ensuite uniquement les résultats réellement obtenus et assainis.

## Risques et conditions préalables

| Statut | Point à traiter | Condition avant de poursuivre |
|---|---|---|
| **BLOQUÉ / RISQUE** | Signature du noyau seule insuffisante pour valider l'ensemble | Examiner séparément les modules KVM et réseau ; prévoir ensuite leurs tests de chargement |
| **BLOQUÉ / RISQUE** | Effets des scripts sur le démarrage | Audit préalable et procédure préservant Secure Boot, EFI, rEFInd, GRUB et le secours Ubuntu |
| **BLOQUÉ / RISQUE** | `install-eve.sh` contient des opérations sensibles sur les disques et SSH | Ne pas exécuter sans audit ; documenter les effets et leur compatibilité avec les contraintes ARN |
| **BLOQUÉ / RISQUE** | Disques Windows, données et jeux à préserver | Aucune opération de formatage ou modification sur ces SSD |
| **BLOQUÉ / RISQUE** | Accès distant après installation | Confirmer SSH par Tailscale et anticiper les effets des scripts sur SSH et le réseau |
| **À TESTER** | Disponibilité de la sauvegarde de démarrage | Retrouver la sauvegarde sur le SSD Ubuntu et vérifier qu'elle est exploitable |

Ces risques signalent des contrôles manquants ; aucun échec de démarrage ou de module n'est déclaré. Si l'audit montre qu'une étape requiert de modifier la configuration de démarrage figée, suspendre cette étape et documenter le conflit avant toute intervention.

## Séquence future envisagée

Cette séquence est **à réaliser ultérieurement**, après résolution des points préalables. Elle ne constitue pas une autorisation d'installation dans le cadre de la tâche documentaire.

1. Achever l'inspection des modules, vérifier leurs signatures et auditer les scripts.
2. Écrire la procédure détaillée préservant Secure Boot, les chargeurs fonctionnels, les SSD Windows et le noyau Ubuntu de secours ; prévoir le retour à l'état fonctionnel.
3. Installer EVE-NG Community 6.2 selon cette procédure, après validation des conditions préalables.
4. Tester le démarrage et les modules du noyau EVE-NG dans ces conditions, en consignant les résultats réels.
5. Configurer les services et le réseau EVE-NG.
6. Vérifier l'accès Web depuis le réseau local puis via Tailscale, sans exposition directe sur Internet.
7. Tester KVM et des laboratoires réseau, avec des critères de réussite et des résultats documentés.
8. Valider l'installation finale, la sauvegarder et mettre à jour les documents de suivi.

**Ne pas exécuter `apt install eve-ng` pour le moment. Ne pas exécuter `install-eve.sh` sans audit. Ne pas désactiver Secure Boot, remplacer les chargeurs EFI fonctionnels ou modifier rEFInd / GRUB pendant cette tâche.**

## Traces à conserver lors de la reprise

Pour chaque contrôle effectivement réalisé, noter la date, la version ou le composant concerné, la commande relue, le résultat assaini, les limites et la prochaine action. Un test ne passe à **VALIDÉ** qu'après sa réalisation ; une préparation ne vaut pas installation.

Ne versionner aucune clé privée MOK, aucun certificat sensible, mot de passe, jeton, adresse IP personnelle ou fichier système contenant des secrets. Les artefacts de signature et les sauvegardes système restent hors du dépôt.

La [checklist de reprise](ARN-NEXT-STEPS.md) suit l'ordre de travail et les conditions de passage.
