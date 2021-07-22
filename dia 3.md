REPO YA EXISTE

Dia 1 - git clone URL

Dia 2 - git pull
        git add FICHERO    # SOLO SI HAY FICHEROS NUEVOS
        git commit -am 'Mensaje'
        git push




CODIGO <<<  Persona 1 + Persona 2



Donde está el repo PRUEBAS ahora mismo?
    Bitbucket: https://bitbucket.org/PERSONA2/pruebas
        desarrollo
        master
    En local en la maquina de Persona 1    /home/ubuntu/environment/curso/ejercicios/pruebas/.git
        desarrollo
        master
        persona 1
    En local en la maquina de Persona 2    /home/ubuntu/environment/curso/ejercicios/compi/.git
        desarrollo
        master
        persona 2 - funcionalidad 1
        persona 2 - funcionalidad 2
        

NO SON IGUALES EN CONTENIDO... 
    pero no solo porque modifique algo y no lo suba.... 
    sino porque hay cosas que yo hago en mi repo que no voy a mandar al remoto
    
    Qué ramas estarán sincronizadas?
        desarrollo
        master











PRUEBAS <<< Persona 2 + Persona 1







METODOLOGIAS AGILES vs METODOLOGIAS CLASICAS (Waterfall)
    SCRUM - SPRINT                
    Cada 2,3, 4 semanas tengo que instalar en prod      |
        Pruebas en otro entorno                         |   AUTOMATIZAR
DEV->OPS. Cultura / Filosifia de la AUTOMATIZACION
    Terraform
CONTENEDORES Estandarización de la distribución e instalación de software
CLOUD

App 
dia 1:    100 usuarios
dia 2:    105 usuarios
dia 3:    130 usuarios
dia 15:   200 usuarios
dia 100  1000 usuarios
dia 300  5000 usuarios


App                                     App Gestion emergencias
dia n   1000                                        10
dia n+1 100000      Black friday                    5
dia n+2 10                                          2000000     < Atentado          Cuando lo necesite ALQUILO
dia n+3 2000000     Cibermonday                     7


Selenium
SoapUI
Postman
JMeter
LoadRunner
UFT
Appium


JENKINS > TravisCI > AzureDevops > Bamboo




----Escenario de ejemplo------

PURI esta trabajando en el fichero prueba1                  > C2
ROSA tambien trabaja en prueba1              > C1  > PUSH

PURI C2   ???
    Sin problema .. donde se hace: EN EL REPO LOCAL
PURI PUSH ???
    Problema: Le va a decir... Eh! que rosa ha hecho un cambio... descargalo primero
    
    git PULL >
        Que no haya conflicto
            Que se genere nuevo commit o que no (A nosotros no da igual... ni me entero)    
        Que si haya conflicto
            Tengo que arreglarlo
            Generar un nuevo COMMIT con el resultado del arreglo de conflictos
        git PUSH
    
    
    
    git config --global credential.helper store   > Almacenar la contraseña y ya no la pide más
    git config --global credential.helper 'cache --timeout=3600'   > Almacenar la contraseña solo durante 1 hora
    
    
Trabajando con git:
    Crear repos 
        Locales
        Bitbucket
    Recuperar repos remotos
    Crear ramas
    Añadir y eliminar archivos
    Commits
    Sincronizarnos entre compañeros push/pull
    Fusionar cambios merge
    Stash
    Tags
    
    
    
Stash : Pila donde se guardan paquetes de cambios
Guardar el paquete 1 de cambios stash[0]
Guardar el paquete 3 de cambios stash[2]


git stash apply stash[1]  -->> Los cambios apuntados en el stash los mete en mi working dir
git stash drop stash[1]   -->> Elimina el paquete de cambios del stash

git stash pop = git stash apply + git stash drop


Fichero1.txt
linea1                  C1
+linea2                 ??

git stash

Que es lo que guardo en el stash: Guardo cambios:


stash[0]:
    En el fichero Fichero1.txt añadir en la linea 2 el texto: "linea2"
    En el fichero Fichero2.txt añadir en la linea 2 el texto: "linea2"
    En el fichero Fichero1.txt reemplazar la linea 2 el texto: "Hola"
    En el fichero Fichero1.txt eliminar la linea 17
    
Esto es lo mismo que se guarda en un COMMIT 


1 Paquete1
0 Paquete 2

git stash clear  BORRAR TODOS LOS STASH


TAGS 

git tag
git tag -l
git tag --list

git tag -a ID_PUBLICO -m 'mensaje descriptivo' ID_COMMIT   <<< le digo un id de commit?
git tag -d ID_PUBLICO 
git tag --show ID_PUBLICO 

Los tags por defecto no se comparten con los repos remotos
git push --tags
git push REPO ID_TAG

---------------
El archivo .gitignore