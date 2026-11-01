# ARN — Checklist de reprise

État de référence : **1er novembre 2026**. Reprise prévue : **2 novembre 2026**, fuseau **Europe/Paris**.

## Point de départ

- **VALIDÉ** : dual-boot Windows 11 / Ubuntu Server, Secure Boot actif, rEFInd fonctionnel et KVM AMD sur le noyau Ubuntu actuel.
- **PRÉPARÉ** : paquets EVE-NG Community `6.2.0-4`, noyau `6.7.5-eveng-6-ksm+` extrait et copie signée dont la signature a été vérifiée.
- **NON INSTALLÉ** : EVE-NG ; la copie signée du noyau EVE-NG n'est ni installée ni testée au démarrage.
- **À TESTER** : confirmation définitive de SSH via Tailscale, inspection des modules EVE-NG et vérification de leurs signatures.
- **BLOQUÉ / RISQUE** : installation en attente de l'audit des scripts et d'une procédure préservant Secure Boot et la configuration de démarrage figée.

Ces états reprennent le compte rendu fourni ; ils ne résultent pas de nouveaux tests du serveur. Lire [l'état de référence](ARN-STATUS.md) et [la préparation EVE-NG](ARN-EVE-NG-INSTALLATION.md) avant toute opération.

## Première séance de reprise — contrôles préalables

- [ ] Confirmer le contexte du serveur : Ubuntu Server 22.04.5 LTS et noyau de référence `5.15.0-202-generic` ; consigner tout écart observé sans modifier le démarrage.
- [ ] Retrouver la sauvegarde de démarrage sur le SSD Ubuntu et contrôler sa disponibilité.
- [ ] Retrouver une preuve de SSH par Tailscale depuis l'extérieur ou effectuer ce test ; distinguer une communication VPN réussie d'une session SSH réussie.
- [ ] Retrouver la dernière commande proposée d'inspection des modules et scripts, **encore non exécutée**, et relire sa portée avant exécution.
- [ ] Terminer l'inspection des modules du noyau EVE-NG extrait.
- [ ] Vérifier les signatures des modules KVM AMD et réseau nécessaires ; documenter ce qui est vérifié et ce qui reste incertain.
- [ ] Analyser les scripts du paquet noyau et du paquet EVE-NG, notamment les effets sur les disques, SSH, les services, le réseau et le démarrage.
- [ ] Auditer `install-eve.sh` sans l'exécuter ; relever les opérations sensibles sur les disques et SSH.
- [ ] Retrouver le détail de la simulation APT et préparer une nouvelle vérification avant installation si nécessaire ; comparer avec les 517 nouveaux paquets, 0 suppression, 0 mise à jour rapportés.
- [ ] Rédiger une procédure d'installation et de retour au noyau Ubuntu fonctionnel, compatible avec Secure Boot, les chargeurs EFI, rEFInd, GRUB et l'ordre UEFI figés.

## Condition de passage à l'installation

- [ ] Résoudre ou documenter chaque risque identifié dans les modules et les scripts ; ne pas poursuivre en présence d'un conflit avec les contraintes ARN.
- [ ] Vérifier que la procédure conserve le noyau Ubuntu actuel, l'entrée `Boot0007` de secours et la sauvegarde de démarrage.
- [ ] Vérifier que la procédure ne formate ni ne modifie les SSD Windows, de données et de jeux.
- [ ] Valider la procédure détaillée avant toute installation réelle.

**Arrêt avant cette étape tant que ces conditions ne sont pas remplies.** La tâche du 1er novembre est documentaire : elle n'autorise pas l'exécution d'`apt install eve-ng` ni une modification système.

## Après validation de la procédure — travaux futurs

- [ ] Installer EVE-NG Community 6.2.0-4 sur Ubuntu Server selon la procédure validée.
- [ ] Tester le démarrage du noyau EVE-NG signé et les modules requis avec Secure Boot actif ; consigner les résultats réels.
- [ ] Configurer et vérifier les services ainsi que le réseau EVE-NG.
- [ ] Tester l'accès Web sur le réseau local.
- [ ] Tester l'accès Web via Tailscale depuis l'extérieur, sans exposition directe sur Internet.
- [ ] Tester KVM et des laboratoires réseau ; consigner les scénarios et leurs résultats.
- [ ] Valider et sauvegarder l'installation finale ; documenter le retour au secours Ubuntu.
- [ ] Mettre à jour les statuts et le [changelog](../CHANGELOG.md) à partir des seuls travaux réellement effectués.

## Traçabilité de chaque séance

- [ ] Dater les contrôles, noter les versions et conserver des preuves assainies ; laisser les tests non réalisés en **À TESTER**.
- [ ] Vérifier le diff et l'absence d'adresses IP personnelles, de clés privées MOK, de certificats sensibles, de mots de passe et de jetons avant chaque commit.
- [ ] Préserver les changements sans rapport avec la séance et sélectionner explicitement les fichiers à versionner.
- [ ] Conserver le commit local jusqu'à autorisation explicite de push sur GitHub.
