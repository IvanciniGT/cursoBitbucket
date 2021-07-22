* git reset
* git revert
* git checkout
* git rebase
* git diff
...
Pull Requests     <<<<<<<<<<<<<<<<<<<<<<<<< MUY IMPORTANTE

* git cherrypeek              <<<<< MUY ESPECIAL. Casos de uso muy restringidos
                                    Me permite tomar un COMMIT que se haya realizado en algun sitio(rama)
                                        y aplicar los cambios de ese commit a otra RAMA

-------------------------------------------

HEAD: Variable que (por defecto) apunta al (último) commit (de la rama) en la que me encuentro....
HEAD: Variable que apunta al commit en el que me encuentro posicionado

ESCENARIO 1


RAMA 1              --- C1 ----- C2 ----- C3 ---- C5*
                                    \
RAMA 2                               -----C5 ---- C6

HEAD (*)


 $ git checkout C3

RAMA 1              --- C1 ----- C2 ----- C3* --- C5
                                    \
RAMA 2                               -----C4 ---- C6



git checkout REF_COMMIT                                                                 <<<<<< Dejar el proyecto en mi working dir como
    Para mover el HEAD usamos el comando CHECKOUT                                               estaba en otro commit.
    Me trae al workingdir el C3, que pasa con el C4 ? Se mantiene en el repo.                  A nivel de repo NO cambia nada.
    PERO me pongo en una posición complicada. ESTOY EN ESTADO DESASOCIADO                      HEAD: SI QUE CAMBIA
                                                                                                >>>> Cambiamos de rama
    Cualquier cambio que hiciera en el código, no lo puedo commitear en la rama 1
    Podría hacer unos cambios.... y generar con esos cambios una rama nueva.
    
    REFCOMMIT:
        ID de un commit
        RAMA -> El ultimo commit de la rama
    
git checkout REF_COMMIT [fichero(s)]                                                    <<<<<< Dejar el fichero en mi working dir como 
    Me trae al workingdir el/los fichero(s) según estaban en C3                                 estaba en un commit anterior.
    Pero no se mueve el HEAD                                                                   A nivel de repo... cambia algo? NO
                                                                                               HEAD: No cambia



ESCENARIO 2

RAMA 1              --- C1 ----- C2 ----- C3 ---- C5*
                                    \
RAMA 2                               -----C5 ---- C6


RAMA 1              --- C1 ----- C2 ----- C3*     C5
                                    \
RAMA 2                               -----C5 ---- C6

HEAD (*)


git reset MODO REF_COMMIT
    MODOS:
        --soft
                Trabaja a nivel del REPOSITORIO
        --mixed <<< POR DEFECTO
                Trabaja a nivel del REPOSITORIO y del AREA DE STAGING (indice)
        --hard
                Trabaja a nivel del REPOSITORIO, del AREA DE STAGING (indice) y del WORKING DIR             <<<< CUIDAO !
    Git reset, elimina (desasocia) los commits posteriores al REF_COMMIT para la rama en la que estoy.
    Los commits que quedan HUERFANOS serán eliminados en algún momento por git de forma AUTOMATICA.
        Git tiene un recolector de basura (por defecto se ejecuta cada 30 dias).
        Para recuperar C%... si un día me hicera falta y aún no se hubiera eliminado, podría usar >>>> git reflog


git reset = git reset --mixed HEAD
    A nivel del repo                NADA TAMPOCO
    A nivel del área de staging     Se borra el area de staging (todos los add/rm son eliminados)
    A nivel del working dir         NADA
            
            PROYECTO:
                src
                target
                
            git init
            git add *
                Meter en staging: src + target     <<<< CAGADA
            git reset                               <<< ARREGLO LA CAGADA
            Me creo un fichero .gitignore
            git add *



RAMA 1              --- C1 ----- C2 ----- C3 ---- C5*
                                    \
RAMA 2                               -----C5 ---- C6

git reset [--mixed] C3
    A nivel del repo                Desasigno C5 (lo marco para su ejecución)
    A nivel del área de staging     Se borra el area de staging (todos los add/rm son eliminados)
    A nivel del working dir         NADA
        
    Proyecto
        creo el archivo 1.... me dan ganas de un cafecito > C1
        vuelvo... y creo el archivo 2... me dan ganas de la sietsa > C2
        Me levanto de la siesta... y modifico ambos archivos.... y me acuesto hasta mañana
            OPCION 1: Hago un C3:
                C0 ---- C1 ---- C2 ---- C3*      Qué aportan esos commits al historial de mi proyecto? NADA
            OPCION 2: 
                Hago un git reset C0
                    C0*      C1 ---- C2 ---- C3      
                            
                    A nivel del repo                Desasigno C1  (lo marco para su ejecución)
                    A nivel del área de staging     Se borra el area de staging (todos los add/rm son eliminados)
                    A nivel del working dir         NADA
                git add *
                Commit Nuevo C1, con toda la info consolidada
                
ESCENARIO 3

RAMA 1              --- C1 ----- C2 ----- C3 ---- C5*
                                    \
RAMA 2                               -----C5 ---- C6

Estando en C5... me doy cuenta que lo último que he hecho ha sido cagada....no vale para nada... nolo quiero

git reset --hard C3
        A nivel del repo                Desasigno C5  (lo marco para su ejecución)
        A nivel del área de staging     Se borra el area de staging (todos los add/rm son eliminados)
        A nivel del working dir         Lo dejo como estaba en C3 <<<< git checkout C3
        
        
GIT REVERT
 
RAMA 1              --- C1 ----- C2 ----- C3 ---- C5*
                                    \
RAMA 2                               -----C5 ---- C6

Quiero revertir los cambios que hice en C5... pero no quiero que se borren del historial. Motivos
    - Por si un día quiero volver a utilizarlo.... y lo tengo bien empaquetadito: cherrypeek
    - Para saber que camino no deberíamos tomar
    
git revert REF_COMMIT HEAD~2

RAMA 1              --- C1 ----- C2 ----- C3 ---- C5 ---- C7* (que sería igual a C2)
                                    \
RAMA 2                               -----C5 ---- C6

Qué contendría C7? 
    Tendría un paquete de cambios que ANULEN lo que ha hecho C3 y C5
    C3: Añadir el fichero 7.txt
    C5: Modificar la linea 37 del fichero 4.txt
    C7: Eliminar el fichero 7.txt
        Modificar la linea 37 del fichero 4.txt para que se quede como estaba en C2

HEAD~2        2 commits anteriores al HEAD
HEAD^^        2 commits anteriores al HEAD

RESET a donde voy ? C3... cual se queda?   C3
REVERT quien quiero revertir? C3 ... cual se queda? C7 que es igual a C2


ESCENARIO 4 - git rebase: Nos hace un merge por cambio de base
El rebase implica reescribir el historial de mi proyecto

RAMA Desarrollo                 C0 -------------------------------- C7 -- C8
                                  \                               /      /
RAMA Funcionalidad 1               -- C1 ----- C2 ----- C3 ---- C5*     /
                                                 \                     /
RAMA Funcionalidad 2                               -----C5 ---- C6 ----

Dos ramas que han ido evolucionando.
En un momento dado quiero fusionar cambios


RAMA Funcionalidad 1               -- C1 ----- C2 ----- C3 ---- C5* ---- C7   MERGE TRADICIONAL
                                                 \                      /   
RAMA Funcionalidad 2                               -----C5 ---- C6 ----

-----

RAMA Desarrollo                 C0 -----------------------------------------------------------C7 ??? MERGE? FastForward 
                                    \                                                        /
RAMA Funcionalidad 1                 -- C1 ----- C2 ----- C3 ---- C5*                       /
                                                                    \                      /
RAMA Funcionalidad 2                                                   -----C5 ---- C6 ----   REBASE

-----

RAMA Desarrollo                 C0 
                                    \                                                       
RAMA Funcionalidad 1                  -- C1 ----- C2 ----- C3 ---- C5*                   
                                                                    \                     
RAMA Funcionalidad 2                                                   -----C5 ---- C6 



En RAMA 2, en C6, tengo todo


REPOSITORIO
C1:
    11+ public static int suma( int a, int b ){
    12+     return a+b;
    13+ }

C2:
    8+ \n
    12+ \n
        /**
         * Funcion que suma
         * @param a: Numero 1 a sumar
         * @param b: Numero 2 a sumar
         * @return El resultado de sumar los numeros
         */
    21+ \n
    
    
    
A nivel de working dir:
    reset --hard
    checkout
    
    
>>>>> COMMIT SUMA  >>>> COMMIT RESTA

1- Quitar el commit de la resta
    git reset --hard  >>> desvincular LA RESTA y dejarla en el LIMBO.... (no se por cuanto tiempo)
    git revert        >>> Generar un commit nuevo que anule resta
        Mantengo resta por si las moscas
2- Ir a un commit anterior...
    git checkout HEAD~1    >>>>> Va un commit pa' tras.... PERO OJO!!!!No puedo hacer commits despues..
                 HEAD^                                                  Porque estoy en un estado desasociado
                                                                PD: Seguro que no puedo hacer commits?
                                                                    Podría hacer un commit, en una NUEVA RAMA
                                                                    
                                                                    
 --- SUMA >> RESTA >> CONTRA_RESTA  >> Nuevo commit con mas cosas
 
 
 --- SUMA  >> Nuevo commit con mas cosas    RESTA 
 

 --- SUMA >>>> RESTA            >>> AMBAS FUNCIONES
            \  MULTIPLICACION   / 
            
            
 --- SUMA >>>> RESTA                        /   FAST FORWARD
                      \  MULTIPLICACION    /


git diff                                    >>>> Cambios en WD sin INDEXAR (ADD STAGING)
git diff --cached                           >>>> Cambios entre INDICE(STAGING) y el ULTIMO COMMIT


git diff HEAD^ HEAD                         >>>> Compara commits
git diff b9e0ac8  HEAD src/main/java/curso/App.java     Compara los cambios de un fichero entre commits
git diff b9e0ac8  HEAD                      >>>> Compara los cambios TODOS entre commits

git diff master..nuevarama                  >>>> Compara ramas (Los finales de cada rama)



--------------------------------------------------------------------------

PULL REQUEST: BITBUCKET + GITHUB
MERGE REQUEST: GITLAB


Alquien (Un equipo) tiene un repo... que controla...es decir:
    SOLO ellos pueden hacer commits a ese repo

Alguien (del mismo equipo o no) quiere trabajar contra ese repo:
    FORKING > Una copia paralela del repositorio original... pero mia, de mi pertenencia
                    NO EN LOCAL... SINO EN EL REMOTO
                    
        Clonarme en local mi repo FORKEADO
            Hago cambios
            Los subo al remoto MIO, a mi FORKING
            Creo un pull request y lo mando
            
        El responsable del otro repo, puede aprobar o no mis cambios
        
    
REPO MAESTRO PROYECTO
    main
    ^^^^^^
REPO FORKEADO DONDE PUEDE TRABAJAR MAS GENTE