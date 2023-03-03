Cosas de Heroku:

Para vincular Git a Heroku:
heroku git:remote -a example-app
De esta forma ya podemos pasar el código de git a Heroku. Heroku SOLO DEPLOYEA lo que se pushee a SU MASTER/MAIN.
git remote -v (Para ver si quedó vinculado)

Para deployar el código:
git push heroku main (OJO NOSOTROS USAMOS SUBCARPETAS, en teoría dice que el .git debe estar en la raiz pero nosotro susamos subcarpetas, ver el word para ver cómo deployar usando subcarpetas)

Para deployar otra rama LOCAL que no sea main a MAIN de HEROKU:
git push heroku testbranch:main (recordar lo que hace este comando pushea A la rama master del repo heroku la rama local testbranch. Si no se especifica ":" pushea la rama coincidente. Si se pushea a otra que no sea main de Heroku no funcionará.

Multiples ambientes:
Nosotros podemos tener dev, test and prod: dev es nuestra máquina local, test es un app de Heroku con sus variables de entorno y PROD es OTRA APP de Heroku.
Mediante git push podemos pushear nuestras ramas locales (diferentes a main) al repositorio de Heroku correspondiente).

Para resetear el git de Heroku ejecutar:
heroku plugins:install heroku-repo (instala este plugin por única vez)
heroku repo:reset --app appname (borra elgit de Heroku)

No se recomienda implementar repositorios grandes de más de 600 MB. Ejecutar heroku apps:info le muestra el tamaño de su repositorio.

-----------------------------------------------------

Procfiles
Necesita un Procfile en la carpeta raiz (donde está el package.json) indicando el comando a ejecutar de la aplicación para iniciarla. 
Generalmente web: npm start. Y correrá el script START del package.json. PERO podemos correr un script usando release: my_script (release phase) y luego nuestra web: npm start.
Igualmente si no tenemos un Procfile Heroku identifica la app y la ejecuta.

OJO!! MUY  IMPORTANTE: se puede hacer uso de las variables de entorno en este Procfile. 
De esta forma podemos definir en una app EN SU ENTORNO la VARIABLE DE ENTORNO NODE_ENV = test, por lo que correrá el script de test con sus correspondientes variables de entorno, sería por ejemplo web: npm $NODE_ENV

Podemos correr la app como sabemos llamando al script del package.json desde la consola, pero es CONVENIENTE usar 
heroku local 
para correrlo ya que será lo mismo que correrá el host.
Como mencionamos éste correrá el Procfile y cargará sus variables de entorno definidas en el .env en el process.env. RECORDAR QUE PUEDE USAR LA VARIABLES DE ENTORNO DEFINIDAD en Heroku previamente.
RECORDAR ESTE .ENV no debe subirse a control de versiones ya que tiene passwords a aplicaciones. PARA ESO SE USAN las variables de entorno definidas en Heroku para test y PROD.

Para acceder a la consola del heroku tenemos varios comandos, ej:
heroku config muestra las variables de entorno definidas
heroku ps, muestra la cantidad de servidores (container/procesadores(DYNOS en Heroku)) que ejecutan la app. Por ejemplo web.x muestran su script que corrió (npm start)
heroku ps::restart reinicia el servidor
heroku logs, muestra el log de ejecución del servidor
heroku ps bash abre la consola para poder ejecutar un comando en su consola

-----------------------------------------
Manejo de ambientes en Heroku:

Como ya mencionamos:
Nosotros podemos tener dev, test and prod: dev es nuestra máquina local, test es un app de Heroku con sus variables de entorno y PROD es OTRA APP de Heroku.
Mediante git push podemos pushear nuestras ramas locales (diferentes a main) al repositorio de Heroku correspondiente).
De esta forma se manejan los ambientes por separado.
Obviamente debemos configurar cada ambiente con sus variables de entorno, addons, etc.
RECORDAR que siempre se pushea a la rama master de ese ambiente, pudiendo seleccionar cualquiera LOCAL.

Existen los que se llaman piplines en el cual se agregan apps que indican que estado es, si dev, stage o prod.
Estas sirven para deployar directamente de una ambiente a otra. Ejemplo de test a prod (hay un botón que hace el deploy automático PROMOTE).

ES PRIMORDIAL RECORDAR QUE:
git push heroku main pushea los cambios ocales de main a la rama main de heroku.
Debemos usar para los ambientes:
git push heroku testbranch:main pushea la rama local testbrahc a la rama master de heroku
La diferencia con los ambientes es que ahora ya tendremos otro nombre para el repo remoto, no es heroku sino será stageing o production. Para esto debemos crear la app segun indica la documentación y vincularla con ese nombre. POR DEFECTO PONE TODO HEROKU pero debemos cambiarla.
git push staging master de esta forma pusheamos los cambios a staging repo.
Conviene usar la rama LOCAL test para pasar los cambios a la rama master de STAGING (en lugar de siempre master a master).











