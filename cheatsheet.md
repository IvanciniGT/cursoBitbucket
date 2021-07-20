# git init

Crear un repositorio vacio

# git status

- Qué ficheros se han modificado en el workingdir
  cuyos cambios no están controlados en el repositorio
- Qué ficheros se han creado en el workingdir
  que están controlados en el repositorio
- Qué ficheros se han eliminado en el workingdir
  que estaban controlados en el repositorio
- Qué paquete de cambios tengo controlados en el área de staging

# git add NOMBRE_ARCHIVO

- Empezar a controlar un archivo:
   Alta de un fichero en el area de staging
- Cada vez que una serie de cambios hayan sido realizados en un fichero
   y quiera enviar esos cambios a mi repo 

git add * < Añadir todos los archivos/cambios sobre archivos
    del directorio en que me encuente
git add . < Es igual que usar * solo que adicionalmente
    se añadirían archivos ocultos

# git rm --cached NOMBRE_ARCHIVO:
- Los cambios que tengo apuntados en staging, los desapunto

# git rm NOMBRE_ARCHIVO:
- Los cambios que tengo apuntados en staging, los desapunto
- Dejo de controlar un arhivo en el repositorio a partir de ahora
- Lo borro de mi working dir

# git commit -m 'Alta del proyecto'


git config user.name "Ivan"
git config --global user.email "ivan.osuna.ayuste@gmail.com"

# git log
Listado de los paquetes de cambios (commits)
    de mi repositorio
    
# git ls-files
Todos los archivos controlados:
    Archivos que ya están en el repo
    Archivos que tenga apuntados nuevos en el área de staging
    
git branch NOMBRE DE RAMA
    Sirve para crear ramas
git checkout -b NOMBRE DE RAMA
    Sirve para cambiar de commit
        Para cambiar de rama
            Puedo solicitar la creación de una rama
    
    