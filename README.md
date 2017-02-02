# CodePushDemoApp

- Installer Homebrew
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

- Installer Node et Watchman
$ brew install node watchman

- Installer le client en ligne de commande React Native
$ sudo npm install -g react-native-cli

- Signer le code sous Xcode
$ open ios/mon_projet.xcodeproj/
Aller dans la Target "mon_projet", onglet General, et sélectionner dans Signing la bonne Team (Olivier Huguenot, ou le compte Mobi Rider chez Apple)

- Installer CodePush
$ npm install -g code-push-cli

- Si on a une session GitHub ouverte dans le browser par défaut, faire un logout.

- Créer un compte --- OU --- se logger
$ code-push register
--- OU ---
$ code-push login
Ceci ouvre le navigateur. Il faut se connecter avec le compte GitHub de Mobi Rider (voir ci-dessus)
Une fois l'access-key créée, la C/C dans l'invite de commandes du terminal.
On peut vérifier qu'on est bien connecté au serveur CodePush avec:
$ code-push session list

- Ajouter une app à gérer
$ code-push app add CodePushDemoApp

- "CodePush-ifier" mon projet, dans le répertoire du projet:
$ npm install --save react-native-code-push@latest

- Installation du plugin iOS:
$ code-push deployment ls mon_projet -k
copier la Deployment Key "Staging"
$ react-native link react-native-code-push
coller la Key pour iOS
d'autres façons peut être utilisées, voir https://github.com/Microsoft/react-native-code-push#plugin-installation-ios

- Configuration du plugin iOS:
Si l'étape du dessus a été suivie, c'est déjà fait, sinon voir https://github.com/Microsoft/react-native-code-push#plugin-configuration-ios

- Staging / Production
$ code-push deployment ls mon_projet -k
copier la Deployment Key "Staging", puis ouvrir le projet Xcode:
$ open ios/mon_projet.xcodeproj/
modifier le fichier Info.plist, mettre la Key dans le champ "CodePushDeploymentKey"
Les Deployment Key "Staging" et "Production" servent respectivement à tester des updates sur une app intégrant la Staging Key, et à pousser en Prod chez les users (qui ont la Production Key)
Pour du test, Staging suffit.

- Tester sur iOS device
$ react-native run-ios --device

- Pousser des updates en Staging
Modifier le fichier index.ios.js (genre changer le hello world etc)
$ code-push release-react mon_projet ios

/*
- Tester sur iOS
$ react-native run-ios

- Tester sur iOS device
$ npm install -g ios-deploy --unsafe-perm=true
$ react-native run-ios --device
Attention, il va falloir approuver le développeur dans les réglages du tel:
Réglages > Général > Profils et périphériques > mobile@mobirider.com > Faire confiance
*/
