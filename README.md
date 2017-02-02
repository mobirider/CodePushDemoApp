# CodePushDemoApp

### Installation software 3rd party

- Installer Homebrew
```sh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

- Installer Node et Watchman
```sh
brew install node watchman
```

- Installer le client en ligne de commande React Native
```sh
sudo npm install -g react-native-cli
```

- Installer CodePush
```sh
npm install -g code-push-cli
```

- Puis
```sh
npm install
```



### Configuration projet

- Signer le code sous Xcode
```sh
open ios/CodePushDemoApp.xcodeproj/
```
Puis aller dans la Target "CodePushDemoApp", onglet General, et sélectionner dans Signing la bonne Team (Olivier Huguenot, ou le compte Mobi Rider chez Apple)

- Si on a une session GitHub ouverte dans le browser par défaut, faire un logout.

- (optionnel) Créer un compte CodePush
```sh
code-push register
```

- Se logger sur CodePush
```sh
code-push login
```
Ceci ouvre le navigateur. Il faut se connecter avec le compte GitHub de Mobi Rider (voir ci-dessus)
Une fois l'access-key créée, la C/C dans l'invite de commandes du terminal.
On peut vérifier qu'on est bien connecté au serveur CodePush avec:
```sh
code-push session list
```

- Ajouter une app à gérer
```sh
code-push app add CodePushDemoApp
```

- Rajouter les sources CodePush au projet, dans le répertoire du projet:
```sh
npm install --save react-native-code-push@latest
```

- Installation du plugin iOS:
Trouver la Deployment Key "Staging"
```sh
code-push deployment ls mon_projet -k
```

```sh
$ react-native link react-native-code-push
```
coller la Key pour iOS
d'autres façons peut être utilisées, voir https://github.com/Microsoft/react-native-code-push#plugin-installation-ios

- Configuration du plugin iOS:
Si l'étape du dessus a été suivie, c'est déjà fait, sinon voir https://github.com/Microsoft/react-native-code-push#plugin-configuration-ios

- Staging / Production
```sh
code-push deployment ls mon_projet -k
```
copier la Deployment Key "Staging", puis ouvrir le projet Xcode:
```sh
open ios/mon_projet.xcodeproj/
```
modifier le fichier Info.plist, mettre la Key dans le champ "CodePushDeploymentKey"
Les Deployment Key "Staging" et "Production" servent respectivement à tester des updates sur une app intégrant la Staging Key, et à pousser en Prod chez les users (qui ont la Production Key)
Pour du test, Staging suffit.

- Tester sur iOS device
```sh
react-native run-ios --device
```

- Pousser des updates en Staging
Modifier le fichier index.ios.js (genre changer le hello world etc), puis:
```sh
code-push release-react mon_projet ios
```
