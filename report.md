# Séminaire 07 - Projet - Journal de bord

[Julien Flückiger]

## Semaine 1 (07.11-13.11)

### temps estimé et temps passé sur le projet et tâches réalisées

| Tâches          | Temps estimé | Temps passé |
| --------------- | ------------ | ----------- |
| Journal de bord | 5min         | 30min       |
| Vue.js          | 10min        | 20min       |
| Bootstrap       | 20min        | 10min       |
| Quiz            | 2h           | 4h          |
| Rapport         | 30min        | 30min       |
| Total           | 3h05         | 5h20        |

### Difficultés rencontrées et solutions trouvées

Bloquer à partir de la consigne: "Afficher le score à la fin du quiz".

Demande de l'aide à un collègue pour savoir ce qu'il fallait faire.

### Explications et réflexions sur le code

**Expliquer le rôle des fichiers suivants :**

1. main.ts :

Ce fichier initialise l’application Vue.js, intègre Bootstrap pour le style et les icônes, configure le routage avec Vue Router et monte l’application sur l’élément racine.

2. main.css :

Ce fichier gère le style des éléments du site.

3. App.vue :

C’est la structure principale du site avec la barre de navigation, appelant les vues (HomeView.vue et AboutView.vue).

4. router/index.ts :

Ce fichier configure et exporte un routeur Vue permettant de naviguer entre la page d’accueil et la page “À propos”.

5. AboutView.vue :

C’est la page d’information.

6. HomeView.vue :

C’est la première page du quiz, qui utilise le fichier Quizform.vue.

7. QuizForm.vue :

Cette page contient toutes les questions du quiz ainsi que le code pour le comptage des points.

**Dans le fichier QuizForm.vue :**

8. Quelles sont les similarités et les différences entre ref et computed ?

Les deux sont réactifs et utilisent “value” pour accéder à leurs valeurs. “ref” sert à gérer les valeurs modifiables, tandis que “computed” est utilisé pour les valeurs dérivées, qui dépendent d’autres valeurs réactives.

9. Que se passe-t-il lorsqu'on clique sur le bouton "Terminer" ?

Le bouton “Terminer” déclenche l’événement “submit” du formulaire associé, vérifie les réponses, calcule le score et affiche le résultat sous forme d’alerte sans recharger la page.

10. Qu'est-ce qu'un v-model ?

Cela lie la valeur d’un champ d’entrée (comme une case à cocher) à une variable du composant. Ainsi, lorsque la valeur de l’élément change, la variable est automatiquement mise à jour, et inversement.

11. À quoi sert le :class="{ disabled: !filled }" ?

Lorsque filled est false (c’est-à-dire si tous les champs ne sont pas remplis), la classe disabled est ajoutée au bouton. Lorsque filled est true (tous les champs sont remplis), la classe est retirée et le bouton devient actif.

### Suite du projet

Peut-être changer les questions pour des questions qui pourront nous êtres utile pour nos cours.

## Semaine 2 (14.11-20.11)

| Tâches           | Temps estimé | Temps passé |
| ---------------- | ------------ | ----------- |
| QuestionRadio    | 1h30         |             |
| QuestionText     | 1h           |             |
| QuestionCheckBox | 30min        |             |
| API              | 1h30         |             |
| Total            | 4h30         |             |

### temps estimé et temps passé sur le projet et tâches réalisées

qweqwe

### Difficultés rencontrées et solutions trouvées

qweqqwe

### Explications et réflexions sur le code

qweqwe

### Suite du projet

qewqweqwe

## Semaine 3 (21.11-27.11)

Tâches: Temps estimé: Temps passé:
qwe 10min 10min

### temps estimé et temps passé sur le projet et tâches réalisées

qweqwe

### Difficultés rencontrées et solutions trouvées

qweqqwe

### Explications et réflexions sur le code

qweqwe

### Suite du projet

qewqweqwe

## Semaine 4 (28.11-04.12)

Tâches: Temps estimé: Temps passé:
qwe 10min 10min

### temps estimé et temps passé sur le projet et tâches réalisées

qweqwe

### Difficultés rencontrées et solutions trouvées

qweqqwe

### Explications et réflexions sur le code

qweqwe

### Suite du projet

qewqweqwe

## Semaine 5 (05.12-11.12)

Tâches: Temps estimé: Temps passé:
qwe 10min 10min

### temps estimé et temps passé sur le projet et tâches réalisées

qweqwe

### Difficultés rencontrées et solutions trouvées

qweqqwe

### Explications et réflexions sur le code

qweqwe

### Suite du projet

qewqweqwe

## Semaine 6 (12.12-18.12)

Tâches: Temps estimé: Temps passé:
qwe 10min 10min

### temps estimé et temps passé sur le projet et tâches réalisées

qweqwe

### Difficultés rencontrées et solutions trouvées

qweqqwe

### Explications et réflexions sur le code

qweqwe

### Suite du projet

qewqweqwe

## Semaine 7 (19.12-25.12)

Tâches: Temps estimé: Temps passé:
qwe 10min 10min

### temps estimé et temps passé sur le projet et tâches réalisées

qweqwe

### Difficultés rencontrées et solutions trouvées

qweqqwe

### Explications et réflexions sur le code

qweqwe

### Suite du projet

qewqweqwe
