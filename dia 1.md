# GIT

Sistema de Control de Versión, desarrollado inicialmente por Linus Torwalds.
Linux es un Kernel de SO => Ubuntu, Debian, Redhat, OpenSUSE, Android

## BitBucket, Github, Gitlab

Servicio gestionado de GIT

# SVN, CVS
    Sistemas de control de verisón centralizados

# GIT   
    Sistema de control de versión distribuido
    
Cada usuario que utiliza GIT tiene en local una copia completa del repositorio:

# Repositorio de git? <<<< Una carpeta    > .git

Un almacen de información... para almacenar qué?
    - Archivos
    - Cambios
    - Historial de cambios

# Entorno de trabajo con GIT:

Working dir < Directorio de trabajo
  VVVV     ^^^^^
Indice o Area de staging (es un indice de cambios que está guardado en un fichero dentro de la carpeta .git)
    ES UNICO EN EL PROYECTO. NO HAY 1 POR RAMA
  VVVV
Repositorio LOCAL < .git 
  VVVV
Repositorio(s) REMOTO < .git 


Rama - Branch


Directorio local    SVN
hola.txt            svn add     svn commit

Directorio local    GIT
hola.txt       >     git add     >     git commit     >     git push
                                                                V
                                                            git pull

# Para tener un repo en mi maquina:
- Crear uno nuevo
- Clonar un repo que exista


# Commit?

Paquete de cambios confirmado en el repositorio


# Permisos de Linux
Propietario del archivo
Grupo del archivo
Otras personas
    Lectura   - r 
    Escritura - w
    Ejecución - x 

OWN  GRP  OTH
---  ---  ---
0 No lo tiene
1 Si lo tiene
101 : Lectura y ejecución

BINARIO         DECIMAL
000         >       0
001         >       1
010         >       2
011         >       3
100         >       4
101         >       5
110         >       6
111         >       7
OWN: 6: Lectura y escritura
GRP: 4: Lectura
OTH: 4: Lectura



TRABAJO CON RAMAS
------------------
RAMA? BRANCH
Una rama es una copia que se mantiene en paralelo del repositorio


Archivo 1 > RAMA 1 > Tenga un determino contenido
Archivo 1 > RAMA 2 > Tenga otro contenido

Flujos de trabajo en RAMA:
    GITHUB
    GITLAB
    BITBUCKET
    A nivel de cada empresa 
    - Qué ramas tengo y cómo las uso?

Rama principal: PRINCIPAL, MASTER, MAIN
    En esa rama ESTA TOTAL Y TERMINANTEMENTE PROHIBIDO HACER NI UN COMMIT
    Lo que hay en esa rama debe ser un reflejo fiel de lo que pasa a producción

MASTER_______________________v(n)
   \                        /
    \ SPRINT1 __/ RELEASE1
        \ caracteristica 1
        \ caracteristica 2
        \ caracteristica 3
        \ caracteristica 4
        \ puri
        \ miguel
    
    


git checkout -b RAMA

Crea una rama
    Desde el último commit que tenga en la rama actual. Ese commit... se duplica (como concepto)
Nos posiciona en la rama




Estoy tocando villanos
    Lo tengo con pinzas

Me piden que haga un 
cambio en superheroes
    > desarrollo





Stash:

Un stash es un alacen temporal de cambios sin confirmar

