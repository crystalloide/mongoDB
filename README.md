## MongoDB : installation, lancement, puis utilisation dans gitpod

### Rappel : nous sommes ici : https://github.com/crystalloide/mongoDB

### Pour ouvrir un environnement Gitpod en ligne avec un simple navigateur web : 

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/crystalloide/mongoDB)

### Pour vérifier - si nécessaire - si des workspaces sont déjà utilisés dans Gitpod :

### https://gitpod.io/workspaces

## 1ère façon d'utiliser MongoDB : via docker : 

#### Pour récupérer la dernière version de l'image mongoDB disponible dans Docker Hub : 

    docker pull mongodb/mongodb-enterprise-server:latest

#### Pour lancer un conteneur à partir de l'image précédente dans Docker Hub :

    docker run --name mongodb -p 27017:27017 -d mongodb/mongodb-enterprise-server:latest

#### Pour voir le conteneur lancé qui exécute le moteur mongoDB : 

    docker ps -a

#### Si on veux installer un client graphique pour intéragir avec le serveur MongDOB lancé : 

#### on peut par exemple utiliser le client Compass à télécharger ici :

    https://www.mongodb.com/try/download/compass

#### Noter que l'URL de votre workspace varie, et il faudra en tenir compte pour configurer notre client :

#### Par exemple dans la présente démo, pour accéder au port 27017, c'était :  

    https://27017-crystalloide-mongodb-lygen7vizjf.ws-eu105.gitpod.io/    

#### Pensez donc çà prendre l'URI correspondante à votre cas actuel

#### Pour arrêter maintenant l'instance lancée : 

    docker stop mongodb

#### On vérifie l'arrêt effectif :     

    docker ps -a

#### Pour aller plus loin : 

#### https://www.mongodb.com/docs/manual/tutorial/install-mongodb-enterprise-with-docker/

## 2nde façon d'utiliser MongoDB : via installation des packages : 

#### On récupère le certificat qui sert à vérifier l'origine des binaires :

    wget -qO- https://www.mongodb.org/static/pgp/server-7.0.asc | sudo tee /etc/apt/trusted.gpg.d/server-7.0.asc

#### On installe l'outil de gestion des certificats GNUPG :

    sudo apt-get install gnupg

#### On installe le lien vers le repository permettant de récupérer les binaires MongoDB :

    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list

#### On effectue un rafraichissement ensuite de l'outil de gestion des packages (apt dans notre cas) :

    sudo apt-get update

#### On installe le package mongosh permettant de lancer un terminal shell en ligne de commandes qui enverra nos commandes vers le serveur mongoDB une fois celui-ci lancé :

    sudo apt-get install -y mongodb-mongosh
    
#### On installe le package mongodb-org qui contient notamment les binaires du serveur mongoDB :

    sudo apt-get install -y mongodb-org

#### On installe les utilitaires pratiques côté réseau (dont netstat) : 

    sudo apt-get install net-tools

#### On créée le répertoire (ici, c'est la valeur par défaut qui est prise) :  

    mkdir data

#### On liste les fichiers et répertoires présents :  

    ls

#### On lance maintenant le moteur NoSQL mongoDB en lui indiquant dans quel répertoire il va stocker les données : 

    mongod --dbpath /workspace/mongoDB/data 

#### Remarque : notre déploiement ne comporte qu'un seul serveur : on parle donc ici de déploiement "stand-alone"

#### Bien entendu, en production, il faudra déployer plusieurs mongoDB travaillant de concert, 

#### les données étants réparties sur chacun d'entre eux pour permette la scalabilité.

#### Remarque : le 1er terminal est désormais occupé par l'exécution du serveur mongoDB, 

#### et si on sort - avec CTRL+C par exemple-, cela revient à stopper l'exécution du serveur mmongoDB. 

#### On pourrait relancer notre serveur en exécution en tâche de fond avec un paramètre comme "-f"  

#### Mais on va simplement lancer un nouveau terminal bash : 

#### Pour cela, cliquer sur "+" en prenant soin de sélectionner "bash" en haut à droite de la 2nde partie de l'écran : 

#### On va maintenant pouvoir se connecter sur le serveur mongoDB 

#### via un terminal en ligne de commande: l'utilitaire "mongosh" récupéré précédemment. 

#### Sans rien préciser d'autre, le client mongosh va prendre alors  les valeurs par défaut : 

#### Il va chercher à joindre le serveur mongoDB en écoute sur "localhost" (ou 127.0.0.1 côté IP) et sur le port "27017" (port d'écoute, valeur par défaut également) :

    mongosh

#### Pour afficher la version du moteur mongoDB : 

    db.version();
    
#### Affichage de la version de mongoDB : 

    test> db.version();
    7.0.5

#### Affichage des commandes disponibles avec l commande "help" : 

    help

#### Affichage en retour :  
    
    Shell Help:

    use                                        Set current database
    show                                       'show databases'/'show dbs': Print a list of all available databases.
                                               'show collections'/'show tables': Print a list of all collections for current database.
                                               'show profile': Prints system.profile information.
                                               'show users': Print a list of all users for current database.
                                               'show roles': Print a list of all roles for current database.
                                               'show log <type>': log for current connection, if type is not set uses 'global'
                                               'show logs': Print all logs.

    exit                                       Quit the MongoDB shell with exit/exit()/.exit
    quit                                       Quit the MongoDB shell with quit/quit()
    Mongo                                      Create a new connection and return the Mongo object. Usage: new Mongo(URI, options [optional])
    connect                                    Create a new connection and return the Database object. Usage: connect(URI, username [optional], password [optional])
    it                                         result of the last line evaluated; use to further iterate
    version                                    Shell version
    load                                       Loads and runs a JavaScript file into the current shell environment
    enableTelemetry                            Enables collection of anonymous usage data to improve the mongosh CLI
    disableTelemetry                           Disables collection of anonymous usage data to improve the mongosh CLI
    passwordPrompt                             Prompts the user for a password
    sleep                                      Sleep for the specified number of milliseconds
    print                                      Prints the contents of an object to the output
    printjson                                  Alias for print()
    convertShardKeyToHashed                    Returns the hashed value for the input using the same hashing function as a hashed index.
    cls                                        Clears the screen like console.clear()
    isInteractive                              Returns whether the shell will enter or has entered interactive mode

    For more information on usage: https://docs.mongodb.com/manual/reference/method



#### Utilisation de la commande db.help() : 

    db.help();


#### Affichage en retour :     


    Database Class:

    getMongo                                   Returns the current database connection
    getName                                    Returns the name of the DB
    getCollectionNames                         Returns an array containing the names of all collections in the current database.
    getCollectionInfos                         Returns an array of documents with collection information, i.e. collection name and options, for the current database.
    runCommand                                 Runs an arbitrary command on the database.
    adminCommand                               Runs an arbitrary command against the admin database.
    aggregate                                  Runs a specified admin/diagnostic pipeline which does not require an underlying collection.
    getSiblingDB                               Returns another database without modifying the db variable in the shell environment.
    getCollection                              Returns a collection or a view object that is functionally equivalent to using the db.<collectionName>.
    dropDatabase                               Removes the current database, deleting the associated data files.
    createUser                                 Creates a new user for the database on which the method is run. db.createUser() returns a duplicate user error if the user already exists on the database.
    updateUser                                 Updates the user’s profile on the database on which you run the method. An update to a field completely replaces the previous field’s values. This includes updates to the user’s roles array.
    changeUserPassword                         Updates a user’s password. Run the method in the database where the user is defined, i.e. the database you created the user.
    logout                                     Ends the current authentication session. This function has no effect if the current session is not authenticated.
    dropUser                                   Removes the user from the current database.
    dropAllUsers                               Removes all users from the current database.
    auth                                       Allows a user to authenticate to the database from within the shell.
    grantRolesToUser                           Grants additional roles to a user.
    revokeRolesFromUser                        Removes a one or more roles from a user on the current database.
    getUser                                    Returns user information for a specified user. Run this method on the user’s database. The user must exist on the database on which the method runs.
    getUsers                                   Returns information for all the users in the database.
    createCollection                           Create new collection
    createEncryptedCollection                  Creates a new collection with a list of encrypted fields each with unique and auto-created data encryption keys (DEKs). This is a utility function that internally utilises ClientEnryption.createEncryptedCollection.
    createView                                 Create new view
    createRole                                 Creates a new role.
    updateRole                                 Updates the role’s profile on the database on which you run the method. An update to a field completely replaces the previous field’s values.
    dropRole                                   Removes the role from the current database.
    dropAllRoles                               Removes all roles from the current database.
    grantRolesToRole                           Grants additional roles to a role.
    revokeRolesFromRole                        Removes a one or more roles from a role on the current database.
    grantPrivilegesToRole                      Grants additional privileges to a role.
    revokePrivilegesFromRole                   Removes a one or more privileges from a role on the current database.
    getRole                                    Returns role information for a specified role. Run this method on the role’s database. The role must exist on the database on which the method runs.
    getRoles                                   Returns information for all the roles in the database.
    currentOp                                  Runs an aggregation using $currentOp operator. Returns a document that contains information on in-progress operations for the database instance. For further information, see $currentOp.
    killOp                                     Calls the killOp command. Terminates an operation as specified by the operation ID. To find operations and their corresponding IDs, see $currentOp or db.currentOp().
    shutdownServer                             Calls the shutdown command. Shuts down the current mongod or mongos process cleanly and safely. You must issue the db.shutdownServer() operation against the admin database.
    fsyncLock                                  Calls the fsync command. Forces the mongod to flush all pending write operations to disk and locks the entire mongod instance to prevent additional writes until the user releases the lock with a corresponding db.fsyncUnlock() command.
    fsyncUnlock                                Calls the fsyncUnlock command. Reduces the lock taken by db.fsyncLock() on a mongod instance by 1.
    version                                    returns the db version. uses the buildinfo command
    serverBits                                 returns the db serverBits. uses the buildInfo command
    isMaster                                   Calls the isMaster command
    hello                                      Calls the hello command
    serverBuildInfo                            returns the db serverBuildInfo. uses the buildInfo command
    serverStatus                               returns the server stats. uses the serverStatus command
    stats                                      returns the db stats. uses the dbStats command
    hostInfo                                   Calls the hostInfo command
    serverCmdLineOpts                          returns the db serverCmdLineOpts. uses the getCmdLineOpts command
    rotateCertificates                         Calls the rotateCertificates command
    printCollectionStats                       Prints the collection.stats for each collection in the db.
    getProfilingStatus                         returns the db getProfilingStatus. uses the profile command
    setProfilingLevel                          returns the db setProfilingLevel. uses the profile command
    setLogLevel                                returns the db setLogLevel. uses the setParameter command
    getLogComponents                           returns the db getLogComponents. uses the getParameter command
    cloneDatabase                              deprecated, non-functional
    cloneCollection                            deprecated, non-functional
    copyDatabase                               deprecated, non-functional
    commandHelp                                returns the db commandHelp. uses the passed in command with help: true
    listCommands                               Calls the listCommands command
    getLastErrorObj                            Calls the getLastError command
    getLastError                               Calls the getLastError command
    printShardingStatus                        Calls sh.status(verbose)
    printSecondaryReplicationInfo              Prints secondary replicaset information
    getReplicationInfo                         Returns replication information
    printReplicationInfo                       Formats sh.getReplicationInfo
    printSlaveReplicationInfo                  DEPRECATED. Use db.printSecondaryReplicationInfo
    setSecondaryOk                             This method is deprecated. Use db.getMongo().setReadPref() instead
    watch                                      Opens a change stream cursor on the database
    sql                                        (Experimental) Runs a SQL query against Atlas Data Lake. Note: this is an experimental feature that may be subject to change in future releases.
    checkMetadataConsistency                   Returns a cursor with information about metadata inconsistencies


#### Pour afficher les databases existantes : (Et oui, il y en a déjà !)

    show dbs;
    
#### Affichage de la liste des databases : 

    admin   40.00 KiB
    config  60.00 KiB
    local   40.00 KiB    

#### Pour pouvoir passer des commandes d'administration, on doit préalablement aller sur la database "admin" : 

    use admin;

#### Pour afficher maintenant les collections présentes dans la database "admin" : 

    show collections;
    
#### Affichage des collections présentes dans la database "admin" :    

    system.version
    
#### On se connecte sur la database "local" ensuite : 

    use local;
 
#### On affiche -et on constate- qu'il n'y a pour le moment qu'une seule collection existante  : 

    show collections;
    
#### Affichage des collections présentes dans la database "local" :     

    startup_log
   
#### Pour afficher quelques informations utiles : 

    db.startup_log.find().limit(10);

#### Pour afficher quelques informations utiles en format plus agréable/ pratique :

    db.startup_log.find().limit(10).pretty;

#### Pour sortir du client shell mongosh : 
    quit

#### Pour exécuter une commande en la passant en paramètre de mongosh :  
    mongosh --host 127.0.0.1:27017 --eval "db.hostInfo()"
    
#### Noter que l'URL de votre workspace varie et qu'il faudra donc peut-être en tenir compte selon vos usages souhaités

#### Dans mon cas, pour accéder au port 27017, c'était :  

#### https://27017-crystalloide-mongodb-lygen7vizjf.ws-eu105.gitpod.io/

## Fin du TP
