---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## C Language fundamentals
drawings:
  persist: false
transition: slide-left
title: Fondamentaux du langage C
mdc: true
hideInToc: true
---

# Fondamentaux du langage C

---

<Toc maxDepth=2 />

---

# Mise en place de l'environnement de travail

- C: langage compilé
- Nécessite un compilateur
- Le binaire résultant est spécifique à la plateforme

---

## Environnement Windows

- Télécharger et installer [MSYS2](https://www.msys2.org/)
- Ouvrir un terminal MSYS2
- Installer le compilateur `gcc` et l'outil `make` avec la commande suivante:

```bash
pacman -S mingw-w64-x86_64-gcc mingw-w64-x86_64-make
```

---

## Environnement Linux (Ubuntu)

- Installer le compilateur `gcc` et l'outil `make` avec la commande suivante:

```bash
sudo apt install gcc make
```

---

## Environnement MacOS

- Installer [Homebrew](https://brew.sh/)
- Installer le compilateur `gcc` et l'outil `make` avec la commande suivante:

```bash
brew install gcc make
```

---

## Premier programme

Créer un fichier `hello.c` avec le contenu suivant:

```c
#include <stdio.h>

int main(void) {
    printf("Hello, world!\n");
    return 0;
}
```

---

Compiler le programme avec la commande suivante:

```bash
gcc -o hello hello.c
```

- `-o` permet de spécifier le nom du binaire résultant, `hello` dans notre cas.
- `hello.c` est le fichier source à compiler.

Exécuter le programme avec la commande suivante:

```bash
$ ./hello
Hello, world!
```

---

## Éditeur de texte

Pour écrire du code, il est recommandé d'utiliser un éditeur de texte adapté à la programmation.

- [Visual Studio Code](https://code.visualstudio.com/)
- [CLion](https://www.jetbrains.com/clion/)
- [Vim](https://www.vim.org/)

On va considérer Visual Studio Code pour la suite du cours.

---

## Extensions Visual Studio Code

- [C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)

---

# Langage C

## Histoire

Le langage C a été créé en 1972 par Dennis Ritchie au sein des laboratoires Bell pour le développement du système d'exploitation Unix, initialement écrit en assembleur (PDP-11).

Le langage C a été conçu pour permettre la portabilité du système d'exploitation Unix sur différentes architectures matérielles.

---

## Motivations

Le C est un langage de programmation de bas niveau, c'est-à-dire qu'il permet de manipuler directement la mémoire de l'ordinateur.

Il est donc possible de programmer des applications très performantes en C.

Il est cependant plus haut niveau que l'assembleur, et permet d'être indépendant de l'architecture matérielle. De ce fait, il est possible de porter un programme écrit en C sur différentes architectures.

---

## Portage

Puisque le langage C définit une syntaxe haut niveau pour décrire un programme, il est possible de porter le même programme sur n'importe quelle architecture pour laquelle un compilateur C a été développé.

Il est même possible de porter un programme vers une autre architecture que l'actuelle, en utilisant ce qu'on appelle un *cross-compiler*. P.ex. compiler un programme à destination de Windows depuis un système Linux.

Le compilateur a comme rôle de traduire les instructions C haut niveau vers un langage de plus bas niveau, compréhensible par la machine elle-même.

---

## Caractéristiques

- Langage compilé
- Typage statique
- Typage faible
- Impératif (procédural)

---
layout: image-right
image: /images/Compilation-Process-in-C.png
---

## Langage naturel vs langage de programmation vs langage machine

- Langage naturel: langage parlé par les humains
- Langage de programmation: langage compris par les ordinateurs (C, Java, Python, etc.)
- Langage machine: langage compris par les processeurs (binaire)

---

## Syntaxe

Exemple de code en C:

```c
#include <stdio.h> // macro pour importer stdio; gère les entrées-sorties (pour le print)

/**
* Fonction main
* Elle prend deux paramètres:
*   - argc: int (nombre entier)
*   - argv: char** (tableaux de chaîne de caractères)
* et retourne un int.
*/
int main(int argc, char* argv[]) { // début de la fonction
  int a; // création de la variable `a`
  a = 42; // assignation de `a` avec la valeur `42`
  printf("Bonjour %d", a); // affichage de "Bonjour {a}"
} // fin de la fonction
```

Chaque instruction doit se terminer par un `;`. Les accolades `{}` définissent la portée des variables, i.e. une variable définie à l'intérieur d'une scope (`{}`) n'est plus accessible en dehors.

---

### Variables

Une variable permet de stocker une valeur en mémoire, et peut être modifiée à tout moment pendant l'exécution du code.

Elle possède une portée (emplacements où elle est valide) et un type (int, char, float, ...).

Les variables sont essentielles dans le code car elles permettent de stocker des valeurs temporaires lors de l'exécution d'un programme.

---

```c
int a = 42;
char b[] = "Bonjour tout le monde";
```

`a` et `b` sont toutes les deux des variables, resp. de type `int` et `char[]`

```c
void foo(int p, int q) { ... }
```

`p` et `q` sont aussi des variables, mais qui résident dans la fonction `foo`.

---

```c {|2|5|} {lines:true}
{
  int a = 42;
}

int b = 2*a;
```

Ici le compilateur emmet une erreur car la variable `a` n'est pas valide lorsqu'on essaie de la lire.

<v-click>

```c {lines:true}
int a = 42;

{
  int b = 2*a;
}
```

Ce code provoque-t-il une erreur de compilation?

</v-click>
<v-click>

Non, car `a` est encore valide dans la scope de `b`.

</v-click>

---

# Commentaires

Les commentaires de fonctions sont essentiels pour expliquer le but et le fonctionnement d'une fonction dans un programme.

## Exemple 1 : Fonction d'addition

```c
/**
 * Cette fonction ajoute deux nombres entiers.
 *
 * @param a Le premier nombre à ajouter
 * @param b Le deuxième nombre à ajouter
 * @return La somme des deux nombres
 */
int addition(int a, int b) {
    return a + b;
}
```

Ce commentaire explique brièvement ce que fait la fonction addition, quelles sont ses paramètres et ce qu'elle renvoie.

---
hideInToc: true
---

## Exemple 2 : Fonction de recherche dans un tableau

```c
/**
 * Recherche un élément donné dans un tableau d'entiers.
 *
 * @param tableau Le tableau dans lequel effectuer la recherche
 * @param taille La taille du tableau
 * @param cible L'élément que l'on recherche
 * @return L'index de l'élément trouvé ou -1 s'il n'est pas présent.
 */
int rechercherElement(int tableau[], int taille, int cible) {
    for (int i = 0; i < taille; i++) {
        if (tableau[i] == cible) {
            return i;
        }
    }
    return -1; // Élément non trouvé
}
```

Ce commentaire décrit la fonction rechercherElement, ses paramètres, ce qu'elle renvoie, et comment elle gère les cas où l'élément recherché n'est pas trouvé.

---
hideInToc: true
---

## Exemple 3 : Fonction pour calculer la factorielle

```c
/**
 * Calcule la factorielle d'un nombre entier positif.
 *
 * @param n Le nombre pour lequel calculer la factorielle
 * @return La factorielle de n, -1 en cas d'erreur.
 */
int calculerFactorielle(int n) {
    if (n < 0) {
        return -1; // Erreur : factorielle de nombre négatif
    }

    int resultat = 1;
    for (int i = 1; i <= n; i++) {
        resultat *= i;
    }

    return resultat;
}
```

Ce commentaire explique la fonction calculerFactorielle, sa restriction sur les nombres négatifs, et son comportement en cas d'erreur.
