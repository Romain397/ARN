# Historique du projet ARN

Les entrées du 14 et du 15 octobre 2026 sont reconstituées à partir de l'historique Git et de la documentation existante. Le point du 1er novembre consigne l'état rapporté à cette date ; il ne date pas individuellement les opérations effectuées sur le serveur.

## 2026-11-01 — Dual-boot stable et préparation EVE-NG 6.2

- **VALIDÉ**, selon le compte rendu : dual-boot Windows 11 / Ubuntu Server 22.04.5 LTS, Secure Boot actif, rEFInd 0.14.2 corrigé et signé, shim 16.1, GRUB masqué, ordre UEFI et secours Ubuntu conservés. Configuration de démarrage figée et sauvegardée sur le SSD Ubuntu.
- **VALIDÉ**, selon le compte rendu : AMD-V et KVM sur le noyau Ubuntu `5.15.0-202-generic`, SSH sur Ubuntu, Tailscale actif au démarrage, communication VPN depuis l'extérieur, NTP et fuseau Europe/Paris.
- **À TESTER** : confirmation définitive de SSH via Tailscale ; une communication VPN validée ne confirme pas seule SSH.
- **PRÉPARÉ** : dépôt officiel ajouté, paquet EVE-NG Community `6.2.0-4` téléchargé, noyau `6.7.5-eveng-6-ksm+` extrait et copie signée ARN dont la signature a été vérifiée.
- **VALIDÉ** : simulation APT rapportée avec 517 nouveaux paquets, aucune suppression et aucune mise à jour ; aucune installation réelle.
- **NON INSTALLÉ** : EVE-NG. La copie signée du noyau EVE-NG n'est ni installée ni testée au démarrage.
- **BLOQUÉ / RISQUE** : installation en attente de l'inspection des modules, de la vérification de leurs signatures, de l'audit des scripts et d'une procédure préservant Secure Boot. La dernière commande proposée d'inspection n'a pas été exécutée.
- Documentation : création de [l'état de référence](docs/ARN-STATUS.md), de [la préparation EVE-NG](docs/ARN-EVE-NG-INSTALLATION.md), de [la checklist de reprise](docs/ARN-NEXT-STEPS.md) et du présent historique. README relié au suivi, processeur corrigé en Ryzen 9 5900X et rôle EVE-NG précisé comme prévu, non installé.
- Intervention limitée à la documentation : aucune nouvelle validation du serveur, aucune modification opérationnelle et aucun push sur GitHub.

## 2026-10-15 — Supervision et alertes

- Commit `35c3df9` : ajout de Blackbox Exporter, Alertmanager, règles d'alerte et provisioning Grafana à la stack de supervision.
- Documentation du prototype sur le portable et du scénario de validation par arrêt de Grafana, notification Discord puis résolution, dans [monitoring/README.md](monitoring/README.md). Aucun nouveau test effectué au titre du point du 1er novembre et aucun déploiement sur EVE-NG déduit de cet historique.

## 2026-10-14 — Initialisation et premier prototype

- Commit `a7eb1f8` : ajout de la licence.
- Commits `1bd75be` et `1ba3218` : structure du dépôt, documentation de l'architecture cible et suivi de l'initialisation.
- Commit `7b7377b` : premiers fichiers Docker Compose et Prometheus du prototype de supervision.
- Commit `74eb875` : mise à jour du README.
