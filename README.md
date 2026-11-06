# ombrefer-online

Version web du jeu de rôle [Les Cryptes d'Ombrefer](https://github.com/alexandrefelmy-dev/Les-Cryptes-d-Ombrefer), avec un moteur en Java.

## Prérequis

Java 25 (JDK), Maven et Git.

## Installation sous Windows

Dans PowerShell. Ouvre un nouveau terminal après chaque installation, sinon les nouvelles commandes ne sont pas reconnues.

1. Installe Git, le JDK et VS Code :

   ```powershell
   winget install Git.Git
   winget install EclipseAdoptium.Temurin.25.JDK
   winget install Microsoft.VisualStudioCode
   ```

2. Installe Maven avec [Scoop](https://scoop.sh), car Maven n'est pas proposé par winget :

   ```powershell
   Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
   Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
   scoop install main/maven
   ```

3. Vérifie les installations :

   ```powershell
   java -version
   mvn -v
   git --version
   ```

4. Déclare ton identité Git, à faire une seule fois par PC :

   ```powershell
   git config --global user.name "Ton nom"
   git config --global user.email "ton-email"
   ```

5. Dans VS Code, ajoute l'extension **Extension Pack for Java**.

## Récupérer le projet et lancer les tests

```powershell
git clone https://github.com/alexandrefelmy-dev/ombrefer-online.git
cd ombrefer-online
git switch feature/game-character
mvn test
```

Le résultat attendu est `BUILD SUCCESS`.
