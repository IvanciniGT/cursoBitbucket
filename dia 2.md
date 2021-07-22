GIT . Trabajamos en 3 zonas:
    - Working dir                   < Carpeta local     < Me da la vista de los archivos que se encuentran en un determinado commit + Modificaciones no controladas por GIT
    - Indice o Area de Staging      < .git/index        < Anotar las modificaciones (Cambios en archivos + Nuevos archivos + Bajas de archivos) que se prepararn para commit 
    - Repositorio Local             < .git              < Guardar Commits
    

ESQUEMA DE UN REPOSITORIO:

-    RAMA 1        C1  ->   C2   ->  C3   ->   C4
                       \
-    RAMA 2                  C5  ->  C6
    
    Commit: Paquete de cambios que puede englobar N archivos que sello y almaceno para su control dentro de UN repositorio.
            Los commits se almacenan en GIT de forma INCREMENTAL !
            
            OBJETIVO: Identificar y controlar un paquete de cambios. Para qué?  >>>> MOTIVOS PARA HACER UN COMMIT
                        - Para ser capaces de revertir un paquete de cambios (Funcionalidad, Bug)
                        - Identificar cúando se hizo un cambio (Funcionalidad, Origen de un bug)
                        - Identificar QUIEN hizo un cambio
                        - Entender cómo va evolucionando el proyecto 
                        - Identificar los cambios que se han introducido desde un determinado momento del tiempo

Archivo1.txt                Archivo1.txt
------------       >>       -------------
Linea 1                     Linea1
                            Linea2 +
--------------------------------------------------------
    VVV                      VVVV
    C1                        C2
    

Crear un repo                                                               git init
Añadir archivos al sistema de control de versión                            git add 
Añadir cambios al sistema de control de versión                             git add
Para controlar un paquete de cambios                                        git commit
Para dejar de seguir un archivo en el sistema de control de versión         git rm
Para eliminar un cambio del sistema de control de versión                   git rm --cached
Para crear una rama                                                         git branch
Para crear una rama                                                         git checkout -b 
Cambiar el commit que visualizo en el working dir                           git checkout 
Fusionar cambios (traer los cambios controlados-COMMIT) de un commit a otro  git merge > En según que casos podía generar un nuevo commit

STASH?          
Un almacen de cambios y ficheros que no están confirmados.
Nos sirve para ocultar del working dir unos determinados cambios TEMPORALMENTE


C(n)  8:00 am
     10:00 am  ->>> Cafecito! --> C(n+1)    CUAL ES EL MOTIVO DE ESTE COMMIT? Copia de seguridad. Esto tiene sentido de cara a controlar la evolución del proyecto?
     13:37 ---> GUAY !!!! Quiero cerrar este paquete de cambios. LISTO !!!
     
REPOSITORIO REMOTO vs LOCAL
Un repositorio local es lo mismo que un repositorio remoto


YO que tengo mi repo y paso datos al TUYO
Para mi quien es el local (EL MIO) y el remoto (el tuyo)
Para ti quien es el local (EL TUYO) y el remoto (el mio)


PURI        - R1            |
    VV   ^^                 |   Repositorio REMOTO - RA - Su misión es:
DIEGO       - R2            |       - Sincronizar paquetes de cambios entre compañer@s
    VV   ^^                 |       - Controlar la evolución del proyecto
CAROLINA    - R3            |       - Servir de copia de seguridad del proyecto
                            |
                            |   Repositorio REMOTO - RB:
                            |       - Un repositorio donde meta solo cambios importantes < Para que 
                                        - Quiero Sincronizar paquetes de cambios entre no compañer@s
                                        - Quiero tener un repo donde el personal (PUEDE SER OTRA EMPRESA) que hace el pase a producción de mi app tome código

La sincronización entre repositorios remotos y locales se hace a nivel de RAMA

Mandar a un repo remoto los commitS realizados sobre UNA RAMA que aún no estén controlados en el REMOTO >                  git push
Traernos de un repo remoto los commitS realizados sobre UNA RAMA que aún no estén controlados en el LOCAL >                git fetch
    Además hace el merge                                                                                                   git pull

Para yo poder mandar commits a una rama de un remoto, tiene que ocurrir que?
    - En el remoto NO PUEDE existir ningún commit en la RAMA en cuestión que YO (LOCAL) no tenga controlado
    
    
RAMA 1 ---- C1----> C2

DIEGO - C1....C2
OMAR  - C1.........C2'
     A priori, a OMAR no le dejará hacer un push
     El tendrá que hacer un fetch... y entoces que ocurre?
        El paquete de cambios C2 se guarda en mi repo local C2 y C2'...y ambos 2 están sobre la MISMA RAMA
        
            C1 --- C2  --- C3
                \_ C2'  __/
        Necesito juntar C2 y C2' en un C3  (Eso es una operación MERGE) <<<<< QUIEN DEBE HACERLO? OMAR... por grande... y tener que hacer curro más dificil
        
        Que habría que hacer después : El push de C3 OMAR 

Que es un git pull? Es un git fetch + git merge

Que pasa si en un merge CUALQUIERA git detecta que hemos tocado exactamente el mismo código de maneras diferentes...
    Se produce un conflicto! MERGING
    

git remote <<<< Nos sirve para controlar LOS repositorios remotos
git remote add NOMBRE URL

git push NOMBRE_REMOTO
git pull|fetch NOMBRE_REMOTO

La misma RAMA en 2 repositorios puede tener DISTINTOS NOMBRES

LOCAL                           REMOTO 1
    desarrollo  -------------->    development
    
    
Ivan    ---> 10:55 am: Cafecito + COMMIT. Ivan tiene su código sin acabar... de hecho ni compila: EN UNA RAMA MIA... EN MI REPO sin hacer push
Miguel  ---> 10:56 am: COMMIT con su funcionalidad LISTA



Por parejas

Omar - Maricarmen
Puri - Rosa
Carolina - Diego
Enrique - Miguel
Fernando - Marian

----------------------------

Cada pareja trabaja en 2 repositorios mismo proyecto
1º REPO: CODIGO DE UN PROGRAMA
2º REPO: Pruebas automatizadas


REPO CODIGO
    MAIN
    DESARROLLO
    TU_NOMBRE

REPO PRUEBAS
    DEFINITIVAS
    DESARROLLO
    TU_NOMBRE        
    
Cada uno:
1º Llevar el Commit ivan => desarrollo
    MERGE: Normal ... si ya existiera 
                            desarrollo
    Existe desarrollo? NO
    1º crear desarrollo...
        desde la rama ivan....
            Ya en automatico entra el 
                commit ultimo que tengo en ivan
2º Crear un repo remoto
    BITBUCKET | GITHUB | GITLAB
3º Alta del remoto en el local
4º Mandar la rama desarrollo al remoto


En cualquier servicio que ofrezca la posibilidad de crear repos remotos:
    BITBUCKET | GITHUB | GITLAB
    Al crear un repositorio tengo 2 opciones:
        Inicializarlo con un commit
            Añadir un README
                      .gitignore
        No inicializarlo con un commit
        
        
        
PROCEDIMIENTO PARA CREAR UN REPO:
1 - Creo un repo local => remoto
        Para poder hacer esto me tengo que asegurar que el remoto no
            contenga nada inicialmente
            
        git init
            crear ARCHIVOS
        git add ARCHIVOS
        git commit -m 'MENSAJITO'
            crear el REPO REMOTO  en BITBUCKET | GITHUB | GITLAB
                PERO OJO!!!! VACIO
        git remote add NOMBRE_REMOTO URL 
        git push NOMBRE_REMOTO
        
2 - Creo un repo REMOTO => local
        Creo el REPO en REMOTO... con contenido
            README + .gitignore
        git clone URL_REMOTO carpeta_local
        * NOTA:
        Si yo ahora quiero subir cambios al remoto, como lo hago?
            crear ARCHIVOS
        git add ARCHIVOS
        git commit -m 'MENSAJITO'
        git push => Sobre que remoto?
            El remoto ha sido añadido (git remote add)
                AUTOMATICAMENTE al hacer el git clone
                EL NOMBRE_REMOTO se asigna automaticamente: ORIGIN
                
                
https://bitbucket.org/ivanciniGT/pruebas
git remote rm bitbucket
git remote add bitbucket https://bitbucket.org/PuriCope/codigo.git 
git push bitbucket


ME descargo el repo de mi compi
    git clone

¿Que ramas me ha traido?


https://bitbucket.org/ivanciniGT/pruebas

$ git remote rm origin
$ git remote add origin https://bitbucket.org/ivanciniGT/pruebas
$ git push > ERROR
    gt push --upstream origin desarrollo
 > USUARIO: MI_USUARIO
 > PASSWORD: VUESTRO_PASSWORD
    Forbiden  : NO TENEMOS PERMISOS PARA ESCRIBIR EN ESE REPO
    
Nuestro compi hizo el repo PUBLICO y por tanto podía verlo, y descargarlo
    PRO NO PUEDO ESCRIBIR EN EL
    
Si fuera privado:
    Al hacer el git clone URL
    Me habría pedido credenciales ... y me habria dado: FORBIDEN: No estoy autorizado
    
De verdad quiero yo que cualquiera toque mi repo?
    NO
Quien quiero que toque el repo del proyecto?
    Los integrantes del equipo?
        SEGURO !!!!! NI DE COÑA !!!!!
    
    PURI commit a la rama master???
    
    Quien puede controlar (editar el repo) PRIVILEGIADOS 1,2-3 personas
    
    GIT No disponemos de permisos a nivel de carpeta ni archivo
    
    Si quiero que los integrantes del equipo hagan cambios... pero ni de coña les voy a dejar controlar el repo
    
    
    
    
    GIT CHECKOUT me pone en el working dir (en mi carpeta) los ficheros que quiera YO (por defecto todos) tal y
        como estaban en un determinado commit (por defecto el último)
    
    git checkout COMMIT_ID ficheros
    git checkout RAMA ficheros  => Ultimo commit de la RAMA
    
    CHECKOUT TRABAJA SOBRE el WORKING DIR
    
    git revert CAMBIA MI REPO y mi working dir
    
    Fichero1.txt    > Fichero1.txt   > REVERT > Fichero1.txt
    Linea1              Linea1                      Linea1
                        Linea2
    C1                      C2                      C3
    
                                        RESET > Eliminar el C2 del repo... opcionalmente se modificará el working dir (Reset HARD) <<< PELIGROSO
                                                                                                                                Puedo perder datos