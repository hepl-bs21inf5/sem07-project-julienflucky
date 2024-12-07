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

- Bloquer à partir de la consigne: "Afficher le score à la fin du quiz".

- Demande de l'aide à un collègue pour savoir ce qu'il fallait faire.

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

&nbsp;

## Semaine 2 (14.11-20.11)

### temps estimé et temps passé sur le projet et tâches réalisées

| Tâches                  | Temps estimé | Temps passé |
| ----------------------- | ------------ | ----------- |
| QuestionRadio           | 1h30         | 45min       |
| QuestionText            | 1h           | 2h          |
| API                     | 1h30         | 15min       |
| QuestionCheckBox(Bonus) | 30min        | -           |
| Rapport                 | 30min        | 30min       |
| Total                   | 5h           | 3h30        |

### Difficultés rencontrées et solutions trouvées

- Un peu de la peine avec le QuestionText pour savoir quoi mettre dedans exactement, mais après m'être document j'ai trouvé les solutions.

### Explications et réflexions sur le code

**Question 1: Quelle est la différence entre un prop et un modèle (v-model) ?**

- Un prop est un mécanisme qui permet de passer unidirectionnellement des données d'un composant père à un composant fils.
- Un modèle permet de lier bidirectionnellement une donnée entre un composant père et un composant fils.

**Question 2: Comment rendre la propriété placeholder optionnelle ?**

- Il faudrait définir une valeur par défaut dans defineProps dans QuestionText.vue.

### Suite du projet

- Toujours changé les questions pour des questions utiles, mais j'imagine que ça sera pour la fin plutôt.
- Faire un bouton pour le QuizTrivia et une correction avec une notification mais je ne sais pas si c'est vraiment utile.
- Faire le QuestionCheckBox Bonus.

&nbsp;

## Semaine 3 (21.11-27.11)

### temps estimé et temps passé sur le projet et tâches réalisées

| Tâches  | Temps estimé | Temps passé |
| ------- | ------------ | ----------- |
| Réponse | 1h30         | 1h          |
| Score   | 30min        | 30min       |
| Rapport | 30min        | 45min       |
| Total   | 2h30         | 2h15        |

### Difficultés rencontrées et solutions trouvées

- Je ne comprenais pas pourquoi quand je cochais une case ça enlevait les celle d'avant, je ne pouvais cocher qu'une case des QuestionRadio parmis les trois. Après j'ai compris que je devais changer la valeur dans les crochets de correctAnswers.

- Sur la page du site, le score augmente malgré que les réponses soient fausses. Et dans réponses correctes, ça renvoie la réponse cochée et non la réponse correcte. Je vais demander de l'aide.
  Solution après avoir demandé de l'aide: changer le v-model dans QuestionRadio et QuestionText pour value.

### Explications et réflexions sur le code

**Question 1: À quoi sert l'option immediate: true dans le watch ? Que se passe-t-il si on l'enlève ou si on met immediate: false ?**

- Immediate: true permet d'exécuter immédiatement la fonction de rappel sans attendre que la propriété observée change.
  La fonction du watch s'exécute dès l'initialisation, même sans changement initial de value.

Exemple:
watch(
value,
(newValue) => {
if (newValue === null) {
modelValue.value = QuestionState.Empty
} else {
modelValue.value = QuestionState.Fill
}
},
{ immediate: true },
)

- Sans immediate ou avec un immediate: false, la focntiom sera exécutée qu'en réponse à un changement de la propriété observée.

**Question 2: Proposer une autre manière de calculer le score (réécrire la fonction du computed) et comparer les deux méthodes.**

- Une autre façon de calculer le score serait d'utiliser reduce (qui parcourt un tableau et accumule une valeur finale en appliquant une fonction à chaque élément) à la place de filter, en accumulant un compteur chaque fois qu'un état est QuestionState.Correct, ce qui évite de créer un tableau intermédiaire et peut être plus performant pour de grandes listes.

### Suite du projet

Faire en sorte que les boutons marchent.

&nbsp;

## Semaine 4 (28.11-11.12)

### temps estimé et temps passé sur le projet et tâches réalisées

| Tâches                  | Temps estimé | Temps passé |
| ----------------------- | ------------ | ----------- |
| Etats                   | 1h30         | 1h          |
| Boutons                 | 1h           | 45min       |
| Réponses immuables      | 30min        | 20min       |
| Rapport                 | 30min        | 45min       |
| Nouvel nav barre(Bonus) | 30min        | 30min       |
| Total                   | 3h30         | 3h20        |

### Difficultés rencontrées et solutions trouvées

- Aucune.

### Explications et réflexions sur le code

**Question 1: Comment pourrait-on réécrire la ligne suivante sans l'opérateur ternaire (avec des if et else) ?**

"model.value =
value.value === props.answer ? QuestionState.Correct : QuestionState.Wrong;"

- if (value.value === props.answer) {
  model.value = QuestionState.Correct;
  } else {
  model.value = QuestionState.Wrong;
  }

**Question 2: Comment pourrait-on réécrire autrement la logique du watch sur value ?**

- On pourrait réécrire la logique du watch en utilisant un opérateur ternaire pour directement assigner la valeur, ce qui simplifie et réduit le code.

Par exemple:
watch(
value,
(newValue) => {
model.value = newValue === null ? QuestionState.Empty : QuestionState.Fill;
},
{ immediate: true },
);

### Suite du projet

Peut-être améliorer la partie Trivia pour qu'elle marche avec des boutons et calcule de score etc.

&nbsp;

## Semaine 5 (12.12-18.12)

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

&nbsp;

## Semaine 6 (19.12-25.12)

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
