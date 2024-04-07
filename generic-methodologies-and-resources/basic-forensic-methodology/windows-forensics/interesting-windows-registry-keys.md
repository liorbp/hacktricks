# Clés de registre Windows intéressantes

### Clés de registre Windows intéressantes

<details>

<summary><strong>Apprenez le piratage AWS de zéro à héros avec</strong> <a href="https://training.hacktricks.xyz/courses/arte"><strong>htARTE (Expert Red Team AWS HackTricks)</strong></a><strong>!</strong></summary>

Autres façons de soutenir HackTricks :

* Si vous souhaitez voir votre **entreprise annoncée dans HackTricks** ou **télécharger HackTricks en PDF**, consultez les [**PLANS D'ABONNEMENT**](https://github.com/sponsors/carlospolop) !
* Obtenez le [**swag officiel PEASS & HackTricks**](https://peass.creator-spring.com)
* Découvrez [**La famille PEASS**](https://opensea.io/collection/the-peass-family), notre collection exclusive de [**NFT**](https://opensea.io/collection/the-peass-family)
* **Rejoignez le** 💬 [**groupe Discord**](https://discord.gg/hRep4RUj7f) ou le [**groupe Telegram**](https://t.me/peass) ou **suivez-nous** sur **Twitter** 🐦 [**@hacktricks_live**](https://twitter.com/hacktricks_live)**.**
* **Partagez vos astuces de piratage en soumettant des PR aux** [**HackTricks**](https://github.com/carlospolop/hacktricks) et [**HackTricks Cloud**](https://github.com/carlospolop/hacktricks-cloud) dépôts GitHub.

</details>


### **Version de Windows et Informations sur le propriétaire**
- Situées dans **`Software\Microsoft\Windows NT\CurrentVersion`**, vous trouverez la version de Windows, le Service Pack, l'heure d'installation et le nom du propriétaire en toute simplicité.

### **Nom de l'ordinateur**
- Le nom d'hôte se trouve sous **`System\ControlSet001\Control\ComputerName\ComputerName`**.

### **Paramètres de fuseau horaire**
- Le fuseau horaire du système est stocké dans **`System\ControlSet001\Control\TimeZoneInformation`**.

### **Suivi de l'heure d'accès**
- Par défaut, le suivi de l'heure d'accès est désactivé (**`NtfsDisableLastAccessUpdate=1`**). Pour l'activer, utilisez :
`fsutil behavior set disablelastaccess 0`

### Versions de Windows et Service Packs
- La **version de Windows** indique l'édition (par exemple, Home, Pro) et sa version (par exemple, Windows 10, Windows 11), tandis que les **Service Packs** sont des mises à jour comprenant des correctifs et parfois de nouvelles fonctionnalités.

### Activation de l'heure d'accès
- Activer le suivi de l'heure d'accès permet de voir quand les fichiers ont été ouverts pour la dernière fois, ce qui peut être crucial pour l'analyse forensique ou la surveillance du système.

### Détails des informations réseau
- Le registre contient des données étendues sur les configurations réseau, y compris les **types de réseaux (sans fil, câble, 3G)** et les **catégories de réseaux (Public, Privé/Domicile, Domaine/Travail)**, qui sont essentiels pour comprendre les paramètres de sécurité réseau et les autorisations.

### Mise en cache côté client (CSC)
- **CSC** améliore l'accès aux fichiers hors ligne en mettant en cache des copies de fichiers partagés. Différents paramètres **CSCFlags** contrôlent la manière dont les fichiers sont mis en cache, ce qui affecte les performances et l'expérience utilisateur, notamment dans les environnements avec une connectivité intermittente.

### Programmes de démarrage automatique
- Les programmes répertoriés dans diverses clés de registre `Run` et `RunOnce` sont lancés automatiquement au démarrage, ce qui affecte le temps de démarrage du système et peut potentiellement être des points d'intérêt pour identifier des logiciels malveillants ou indésirables.

### Shellbags
- Les **Shellbags** stockent non seulement les préférences des vues de dossiers, mais fournissent également des preuves forensiques de l'accès à des dossiers même si le dossier n'existe plus. Ils sont inestimables pour les enquêtes, révélant l'activité de l'utilisateur qui n'est pas évidente par d'autres moyens.

### Informations et forensique sur les périphériques USB
- Les détails stockés dans le registre sur les périphériques USB peuvent aider à retracer quels périphériques étaient connectés à un ordinateur, liant potentiellement un périphérique à des transferts de fichiers sensibles ou à des incidents d'accès non autorisés.

### Numéro de série du volume
- Le **Numéro de série du volume** peut être crucial pour suivre l'instance spécifique d'un système de fichiers, utile dans des scénarios forensiques où l'origine des fichiers doit être établie sur différents appareils.

### **Détails de l'arrêt**
- L'heure d'arrêt et le compteur (ce dernier uniquement pour XP) sont conservés dans **`System\ControlSet001\Control\Windows`** et **`System\ControlSet001\Control\Watchdog\Display`**.

### **Configuration réseau**
- Pour des informations détaillées sur l'interface réseau, consultez **`System\ControlSet001\Services\Tcpip\Parameters\Interfaces{GUID_INTERFACE}`**.
- Les heures de première et dernière connexion réseau, y compris les connexions VPN, sont enregistrées sous différents chemins dans **`Software\Microsoft\Windows NT\CurrentVersion\NetworkList`**.

### **Dossiers partagés**
- Les dossiers partagés et les paramètres se trouvent sous **`System\ControlSet001\Services\lanmanserver\Shares`**. Les paramètres de mise en cache côté client (CSC) dictent la disponibilité des fichiers hors ligne.

### **Programmes démarrant automatiquement**
- Les chemins comme **`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Run`** et des entrées similaires sous `Software\Microsoft\Windows\CurrentVersion` détaillent les programmes configurés pour s'exécuter au démarrage.

### **Recherches et chemins saisis**
- Les recherches de l'Explorateur et les chemins saisis sont suivis dans le registre sous **`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer`** pour WordwheelQuery et TypedPaths, respectivement.

### **Documents récents et fichiers Office**
- Les documents récents et les fichiers Office consultés sont notés dans `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs` et des chemins spécifiques aux versions Office.

### **Éléments les plus récemment utilisés (MRU)**
- Les listes MRU, indiquant les chemins de fichiers et les commandes récents, sont stockées dans diverses sous-clés `ComDlg32` et `Explorer` sous `NTUSER.DAT`.

### **Suivi de l'activité utilisateur**
- La fonction User Assist enregistre des statistiques détaillées d'utilisation des applications, y compris le nombre d'exécutions et l'heure de la dernière exécution, à **`NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\{GUID}\Count`**.

### **Analyse des Shellbags**
- Les Shellbags, révélant des détails d'accès aux dossiers, sont stockés dans `USRCLASS.DAT` et `NTUSER.DAT` sous `Software\Microsoft\Windows\Shell`. Utilisez **[Shellbag Explorer](https://ericzimmerman.github.io/#!index.md)** pour l'analyse.

### **Historique des périphériques USB**
- **`HKLM\SYSTEM\ControlSet001\Enum\USBSTOR`** et **`HKLM\SYSTEM\ControlSet001\Enum\USB`** contiennent des détails riches sur les périphériques USB connectés, y compris le fabricant, le nom du produit et les horodatages de connexion.
- L'utilisateur associé à un périphérique USB spécifique peut être identifié en recherchant les ruches `NTUSER.DAT` pour le **{GUID}** du périphérique.
- Le dernier périphérique monté et son numéro de série de volume peuvent être retracés via `System\MountedDevices` et `Software\Microsoft\Windows NT\CurrentVersion\EMDMgmt`, respectivement.

Ce guide condense les chemins et méthodes cruciaux pour accéder à des informations détaillées sur le système, le réseau et l'activité utilisateur sur les systèmes Windows, visant la clarté et la facilité d'utilisation.



<details>

<summary><strong>Apprenez le piratage AWS de zéro à héros avec</strong> <a href="https://training.hacktricks.xyz/courses/arte"><strong>htARTE (Expert Red Team AWS HackTricks)</strong></a><strong>!</strong></summary>

Autres façons de soutenir HackTricks :

* Si vous souhaitez voir votre **entreprise annoncée dans HackTricks** ou **télécharger HackTricks en PDF**, consultez les [**PLANS D'ABONNEMENT**](https://github.com/sponsors/carlospolop) !
* Obtenez le [**swag officiel PEASS & HackTricks**](https://peass.creator-spring.com)
* Découvrez [**La famille PEASS**](https://opensea.io/collection/the-peass-family), notre collection exclusive de [**NFT**](https://opensea.io/collection/the-peass-family)
* **Rejoignez le** 💬 [**groupe Discord**](https://discord.gg/hRep4RUj7f) ou le [**groupe Telegram**](https://t.me/peass) ou **suivez-nous** sur **Twitter** 🐦 [**@hacktricks_live**](https://twitter.com/hacktricks_live)**.**
* **Partagez vos astuces de piratage en soumettant des PR aux** [**HackTricks**](https://github.com/carlospolop/hacktricks) et [**HackTricks Cloud**](https://github.com/carlospolop/hacktricks-cloud) dépôts GitHub.

</details>