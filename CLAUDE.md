# Ombrefer Online : notes de reprise

Ce fichier garde le contexte du projet d'une session et d'un PC à l'autre.

## Rôle de Claude

Lire `prompt.md` et s'y conformer : mentor pédagogique, réponses en français, petites étapes, indices plutôt que solution complète, vérification de la compréhension. Ne pas écrire à ma place le code du projet, sauf si je le demande ou si cela me débloque vraiment.

## Travail sur plusieurs PC

Je travaille sous Ubuntu et sous Windows. Au début d'une session sur un PC, vérifier `java -version`, `mvn -v`, `git config user.name` et `git config user.email`, et m'avertir de tout prérequis manquant avant de commencer le code. La procédure d'installation est dans `README.md`. Sous Windows, donner les commandes pour PowerShell.

## Projet

Version web de mon jeu Python [Les Cryptes d'Ombrefer](https://github.com/alexandrefelmy-dev/Les-Cryptes-d-Ombrefer), qui reste un dépôt séparé et peut continuer à évoluer. Le dépôt Python sert de référence pour les règles. Une nouvelle règle qui me plaît devient une issue ici : on ne cherche pas à garder les deux versions identiques.

## Architecture et choix techniques

- Moteur de jeu en Java pur, sans lien avec le web ni la base de données.
- API Spring Boot, ajoutée en semaine 3, qui charge l'état, applique l'action, enregistre et répond.
- PostgreSQL et Flyway, interface HTML/CSS/JS.
- Java 25, Spring Boot 4.1, Maven, JUnit 6, WireMock.
- Le code et ses commentaires sont en anglais.

Décisions à respecter :

- Pas de `input()` dans le moteur : chaque action du joueur est une requête HTTP.
- Le générateur de hasard est passé au moteur, pour que les tests puissent rejouer une partie.
- Les monstres sont importés d'Open5e vers la base, jamais appelés pendant une partie.
- Open5e : filtrer avec `document__slug=wotc-srd`, convertir les valeurs à l'échelle du jeu, lire l'Open Gaming License avant de publier.
- La classe s'appelle `GameCharacter`, pas `Character`, qui entre en conflit avec `java.lang.Character`.

## Feuille de route indicative

| Semaine | Objectif | Critère de validation |
|---|---|---|
| 1 | Java et combat en console | `mvn test` réussit, PV jamais négatifs, critique testé |
| 2 | Moteur complet, CI, pre-commit Java | Une partie entière rejouée à l'identique dans un test |
| 3 | API HTTP | Erreurs 400 et 404 propres, tests d'API |
| 4 | PostgreSQL et migrations | La partie survit à un redémarrage |
| 5 | Interface web et classement | Une partie complète au navigateur |
| 6 | Import Open5e et mock WireMock | Tests sans réseau, cas 404, 500 et timeout simulés |
| 7 | Docker, environnements dev, recette et prod simulés, Dev Container | Base inaccessible de l'extérieur, même image partout |
| 8 | Documentation sur GitHub Pages, bilan | Site publié par la CI, release `v1.0` |

Ce calendrier est un repère, pas une date limite. Prolongements facultatifs : comptes avec mot de passe, plusieurs instances, Kubernetes local, nouveaux contenus.

## État au 2026-11-07

Fait :

- Java 25 et Maven installés sur le premier PC.
- Projet Maven et `FirstTest` en place, PR #2 fusionnée.
- Branche `feature/game-character` créée et poussée.

Prochaine étape : écrire `GameCharacter` (issue #1), pas encore commencée.

- Classe : `src/main/java/com/ombrefer/engine/GameCharacter.java`
- Tests : `src/test/java/com/ombrefer/engine/GameCharacterTest.java`
- Attributs privés : `name`, `maxHp`, `currentHp`, `attack`
- Méthodes : constructeur `(String name, int maxHp, int attack)`, `isAlive()`, `takeDamage(int)`, `int heal(int)`, `getCurrentHp()`
- Avancer une méthode à la fois, avec son test, puis supprimer `FirstTest.java`.

Petites tâches en attente :

- Renommer l'issue #1 avec `GameCharacter`.
- Créer le milestone de la semaine 1 s'il n'existe pas.
- Retirer la ligne `Java` de `.gitignore`.

## Questions auxquelles je dois encore répondre

1. Pourquoi `input()` en plein combat ne peut pas fonctionner tel quel sur un serveur web ?
2. Pourquoi `FirstTest` est dans `src/test/java` et pas dans `src/main/java` ?
3. Que se passe-t-il avec `takeDamage(-5)`, et comment le tester ?
4. Quelle langue pour la documentation, français ou anglais ?

## Mon niveau

- Python et programmation orientée objet pratiqués, Java nouveau.
- pre-commit et pull request compris dans l'ensemble.
- Workflow GitHub Actions : confondu avec une feuille de route le 2026-11-06, à revérifier.
