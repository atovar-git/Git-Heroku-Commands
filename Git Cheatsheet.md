# Comandos de Github

## 1. Configuración del repositorio LOCAL 🖥️
`git init`  &nbsp;&nbsp; crea repositorio local en la carpeta donde estés parado.  
Puede que pida usuario y contraseña, poner el de GitHub.

`git config user.name "nombre_usuario"`  
`git config user.mail "email_usuario"` &nbsp;&nbsp; el mail de Github.

`git status` &nbsp;&nbsp; indica el estado de los archivos para darle seguimiento.

`git add .`	&nbsp;&nbsp; suma al área de "Staging" todos los archivos del mismo directorio.  
(. = mismo directorio, all = todos los archivos del repositorio sin importar donde estés parado).

`git commit -m "mensaje_del_commit"` &nbsp;&nbsp; agrego los archivos al área de "Producción".

## 2. Conexión entre repositorio LOCAL y REMOTO 🖥️ ↔️ ☁️
Al crear el repositorio GitHub te indica el comando a correr para vincularlo. **Es recomendable seguir dicho script**.  
Algunos de los comandos son:

`git remote add origin "url_repositorio_de_github"` &nbsp;&nbsp; conecto al repositorio remoto. Se agrega a la lista de repositorios REMOTOS vinculados.  
Se hace una vez por repositorio.  
*add origin* significa que el repositorio remoto se llama origin y tiene su URL.

`git remote -v` &nbsp;&nbsp; verifica que quedaron conectados. Muestra una lista de los repositorios REMOTOS vinculados.

`git remote set-url origin "url_NUEVO_repositorio_de_github"` &nbsp;&nbsp; si deseamos cambiar/migrar de repositorio REMOTO podemos ejecutar esta línea.

`git push -u origin master` &nbsp;&nbsp; para subir al repositorio remoto. El -u me permite que luego si quiero realizarlo de nuevo no pongo "origin master".

>## Qué es origin y remote?
>Puede sonar confuso la instrucción git push origin master. Qué hace?  
Básicamente origin es el repositorio remoto (Github). Lo llama de esa manera, abreviado, que tiene su URL.  
El local no lo vemos, no tiene nombre.  
>
>Entonces:  
git push (comando de git para pushear cambios) origin (push al repositorio remoto llamado origin) master (solo pusheará esta rama master LOCAL a master de REMOTO. Si la remota no existe la crea.   
>
>Si alguien hace como un fork (copia del repositorio de Github) se creará otro alias, ya no será el ORIGEN, sino que es una copia (esto sucede en Heroku).   
ORIGIN entonces es nuestro repositorio de Github ORIGINAL, pero "HEROKU" es el repositorio de Heroku.  
De esta forma si hacemos `git remote -v` veremos los REPOSITORIOS remotos VINCULADOS serán:  
>- origin (alias del repositorio remoto) + URL de ESE repositorio (repositorio nuesto original)  
>- heroku (alias del nuevo/copia repositorio remoto) + URL de nuevo/copia repositorio (repositorio copiado por Heroku)  
>
>En conclusión: ORIGIN es el repositorio remoto (abreviación para identificarlo) y se llama origin porque es el repositorio ORIGINAL, de donde salieron otros al hacer forks, como el de Heroku.

## 3. Clonar ⏬
Si ya tenes tu código en el repositorio remoto (cuyo alias es origin) y lo queres copiar a tu máquina local, usar el comando  
`git clone "url_repositorio_de_github"`  
Creará una CARPETA YA con el nombre del repositorio.  
Esto hará que quede vinculado automáticamente al repositorio origin.

## 4. Creación de RAMAS 🔀
Creamos ramas para poder desarrollar sobre la misma sin afectar la original. Una vez finalizado el desarrollo las podremos unir.  

`git checkout -b "nombre_rama_nueva"` &nbsp;&nbsp; crea rama NUEVA. Esta tendrá sus commits.

`git checkout "nombre_rama_existente"` &nbsp;&nbsp; switch entre ramas existentes para poder trabajar en alguna de ellas. Cada una tiene sus propios commits.

## 5. Merge de RAMAS 🈂️
Una vez finalizado el desarrollo sobre alguna de las ramas la unimos con su original.  
**Casi siempre este MERGE se realiza desde la UI de Github ya que debe ser aprobada por otra persona.**  
Si la realizamos localmente usamos:  
`git merge "dev"` &nbsp;&nbsp; ME PARO EN LA RAMA ORIGINAL, y le indico a cuál unirme.

## 6. Ciclo de trabajo 🔃
Luego de un merge y si todo está OK en DEV, vamos a crear nuevamente una rama para seguir trabajando:

### Local:
1. Salgo de mi rama original (mergeada) y paso a la rama dev:  
`git checkout "dev"`  
2. Actualizo dev ya que no tendrá lo que pasó en GitHub:  
`git pull`  
3. Elimino mi rama donde estaba trabajando:  
`git branch  -d "nombre_rama_vieja"`  
4. Creo ahora una nueva rama basándonos en dev que ya tiene todo ok:   
`git checkout "dev"`  
`git checkout  -b "nombre_nueva_rama"`  
5. Ya estamos en el nueva rama:  
`git add .`  
`git commit -m "initial commit"`  
6. Subo al repositorio la nueva rama (vacía por ahora):  
`git push`  
7. Arroja error ya que no existe en GitHub, usar:  
`git push --set-upstream origin "nombre_nueva_rama"` (copiar y pegar de la consola esta linea)
8. **Trabajamos en la rama nueva.**

## 7. Descargando rama de un compañero ⏬
Puede pasar que queremos ver la rama de otro compañero. La rama la vemos en Github pero no la tenemos en local.
- Asegurarnos de pushear todos nuestro cambios a nuestra rama en la que estábamos trabajando para no perder información.
- Ya pusheados nuestros cambios hacemos git pull para descargar todos los cambios que tiene Github. Vemos que aparece un mensaje mostrando una nueva rama que es la de nuestro compañero de origin (Github).
- Hacemos `git checkout "rama_de_mi_compañero"` y listo. Ya Git sabe que estamos trackeando esa rama y podemos ver su contenido.

## 8. Edición en LOCAL y REMOTO (misma parte)
