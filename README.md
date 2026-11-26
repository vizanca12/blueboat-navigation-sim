# Simulateur de Navigation Autonome BlueBoat 🛥️

Environnement de test virtuel développé en Python et Pygame pour le BlueBoat. Il permet de valider les algorithmes de navigation et d'évitement d'obstacles avant leur déploiement sur le bateau réel.

## Contexte

Projet d'Ingénierie en Équipe (PIE) « Bateau IA » de l'ENSTA Paris (Groupe 25, 2025-2026), mené avec l'association TAMEO pour le Monaco Energy Boat Challenge 2026. Ce dépôt contient le simulateur de navigation développé dans ce cadre.

Le rapport final du projet est disponible dans [`docs/rapport_final_PIE.pdf`](docs/rapport_final_PIE.pdf) (sources LaTeX dans [`docs/report/`](docs/report/)).

## 🚀 Fonctionnalités principales

* **Génération de trajectoire** : création automatique d'une route en « 8 » (lemniscate) entre deux points de repère (bouées).
* **Planification d'entrée** : le bateau calcule automatiquement le meilleur point pour rejoindre la trajectoire établie.
* **Évitement d'obstacles** : détection de proximité et calcul en temps réel d'une trajectoire de déviation pour éviter les collisions.
* **Gestion des états** : cycle de mission allant de la recherche de la route jusqu'à l'arrivée au point de destination.

## 📂 Organisation du code

| Fichier / dossier | Contenu |
|---|---|
| `src/blueboat_model.py` | Logique physique et décisionnelle : calculs vectoriels (classe `Vector2`), suivi de points (lookahead) et forces d'évitement |
| `src/test_scenario.py` | Interface et exécution de la simulation : rendu Pygame à 60 FPS, HUD avec télémétrie, progression de la mission et capteurs de proximité |
| `src/Simulation/` | Simulations complémentaires de l'équipe (suivi de trajectoire par spline cubique + Stanley, Dynamic Window Approach, essais RL) sur la carte du port de Monaco |
| `src/Simulation/Pythonrobotics/` | Modules adaptés de [PythonRobotics](https://github.com/AtsushiSakai/PythonRobotics) (Atsushi Sakai, licence MIT) |

## 🛠️ Installation et lancement

Avec le Makefile (crée l'environnement virtuel, installe `pygame-ce` et lance le simulateur) :

```bash
make run
```

Ou manuellement :

```bash
pip install pygame-ce
python src/test_scenario.py
```

## 🔜 Prochaines étapes

L'objectif final de ce simulateur est de servir de base logicielle pour le bateau réel :

* **Communication avec la NVIDIA Jetson** : portage du code pour en faire le module de navigation principal embarqué sur le BlueBoat.
* **Pilotage réel** : conversion des vecteurs de direction calculés ici en commandes moteurs via une liaison série.
* **Intégration ROS 2** : standardisation des données pour une utilisation dans un environnement robotique complet.
