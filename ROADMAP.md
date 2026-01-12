# ROADMAP

## Outils et méthodes de développement logiciel

### le versioning du code
  1. clone
  2. commit
  3. push
  4. merge
  5. branch
  6. gitignore
  7. push request
  8. add url, remote
  9. rebase
  10. undo a commit
  11. vscode et les commit, plugin 

### le formatage du code
  1. c'est quoi le formatage du code
  2. pourquoi le formatage du code normalisé est important
  3. le formatage du code dans ROS2
  4. les formateurs de code automatique, clang, l'utilisation avec vscode (version python)
  5. Comment vérifier que le code est bien formaté (vérificateur de formatage) (version python et c++)
  6. l'utilisation de pre-commit

### Les tests

  1. pourquoi les tests sont essentiels, pourquoi le test automatique est fondamental
  2. c++/google test
    1. écrire un test
    2. compiler et inclure un test dans cmake
  3. python/pytest
  4. les tests dans ROS
  5. workflow pour les tests

### Reproductibilité / Docker
  
  1. les dépendances en informatique
    1. Le cas de ROS2: exemple avec package.xml, redite dans CMake avec ROS
  2. reproductibilité en c++
  3. reproductibilité en python

### Les workflows git génériques
  1. Présentation de github et gitlab
  2. Présentation de Dagger et Earthly

### Documentation

  1. sphinx
  2. génération automatique de la documentation
  3. publication de la documentation sur le web (github pages)
  4. intégrer le résultats de tests dans la documentation

#### Documenter le code
  1. C++
    2. doxygen

### Outils de vérification et de debug

  1. cppcheck
  2. clang-tidy
  3. valgrind
  4. gdb
  5. vscode et les outils de debug

## Outils spécifiques à la robotique

  0. Visualization avec RViz
  1. Voir les Tf
  2. mettre le robot dans un état avec un topic et le voir dans RViz

  1. Simulation en robotique
  2. Simulation en robotique avec ROS2 et gazebo



## Process visualization RViz avec l'URDF

1. Partir du fichier et identifier/séparer les composants
2. Afficher les composants 1 à 1
3. Les positionner avec RViz
4. Vérifier les angles de rotation et les butées




## Retour des étudiants, éléments à ajouter

Je veux recommencer depuis mon projet sur github ?
  1. clone
  2. installer avec venv et requirements.txt