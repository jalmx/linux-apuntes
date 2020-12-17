# NDG Linux Unhatched - NDG Linux Unhatched - Español (Notes)

## Primer valor para un archivo

| Símbolo | Tipo de archivo    | Descripción                                                                    |
| ------- | ------------------ | ------------------------------------------------------------------------------ |
| d       | directorio         | Un archivo usado para contener otros archivos.                                 |
| -       | archivo ordinario  | Incluye archivos leíbles, imágenes, archivos binarios, y archivos comprimidos. |
| l       | enlaces simbólicos | Apunta a otro archivo.                                                         |
| s       | socket             | Permite la comunicación entre procesos.                                        |
| p       | tubería (pipe)     | Permite la comunicación entre procesos.                                        |
| b       | archivo bloque     | Usado para comunicaciones con el equipo (hardware).                            |
| c       | archivo carácter   | Usado para comunicaciones con el equipo (hardware)                             |

## Permisos

```
- rw-r--r-- 1 sysadmin sysadmin 647 Dec 20  2017 hello.sh
```

### Propietatio

-`rw-` r--r-- 1 `sysadmin` sysadmin 647 Dec 20 2017 hello.sh

El primer grupo se refiere al usuario que posee el archivo. Si su cuenta actual es la propietaria del archivo, se usará el primer grupo de permisos y los demás permisos no tendrán efecto.

### Grupo

-rw- `r--`r-- 1 sysadmin `sysadmin` 647 Dec 20 2017 hello.sh

El segundo conjunto se refiere al grupo que posee el archivo. Si su cuenta actual no es la del propietario del archivo pero es miembro del grupo que posee el archivo, se aplicarán los permisos del grupo y los demás permisos no tendrán efecto.

### Otros

-rw- r--`r--` 1 sysadmin sysadmin 647 Dec 20 2017 hello.sh

El último grupo es para todos los demás, cualquiera a quien los dos primeros conjuntos de permisos no sean aplicables. Si no es el usuario que posee el archivo o un miembro del grupo que posee el archivo, se le aplicará el tercer conjunto de permisos.

## Tipos de permisos

Tipos de permisos
Un archivo o directorio puede presentar tres permisos diferentes: leer, escribir y ejecutar. La forma en que se aplican estos permisos difiere entre archivos y directorios, como se muestra en la tabla siguiente:

| Permiso                | Efectos sobre los Archivos                                                                                         | Efectos sobre los Directorios                                                                                                                                                                         |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| leer (read) (r)        | Permite que el contenido del archivo sea leído o copiado.                                                          | Sin el permiso para ejecutar, permite obtener un listado poco detallado de los archivos que contiene el directorio. Con el permiso para ejecutar, ls -l proporciona un listado detallado de archivos. |
| escribir (write) (w)   | Permite modificar o reescribir el contenido del archivo.                                                           | Permite añadir o eliminar archivos en un directorio. Para que este permiso funcione, el directorio debe tener permiso para ejecutar.                                                                  |
| ejecutar (execute) (x) | Permite que un archivo funcione como un proceso, aunque archivos script también requerirán el permiso leer (read). | Permite que el usuario se traslade del directorio si en el directorio padre también posee permiso escribir (write).                                                                                   |

### Comando `chmod` Cambio de acceso a archivos

El método simbólico y el método octal. El método simbólico es útil para cambiar un conjunto de permisos a la misma vez. El método octal o numérico requiere conocer el valor octal de cada uno de los permisos y requiere que los tres conjuntos de permisos (usuario, grupo, otros) se especifiquen cada vez.

```
chmod [<COJUNTO DE PERMISOS><ACCIÓN><PERMISOS>]... ARCHIVO
```

#### El método simbólico

**Conjunto de permisos**

| Símbolo | Significado                                                                                 |
| ------- | ------------------------------------------------------------------------------------------- |
| u       | Usuario: El usuario propietario del archivo.                                                |
| g       | Grupo: El grupo propietario del archivo.                                                    |
| o       | Otros: Cualquier otro que no sea el usuario propietario o un miembro del grupo propietario. |
| a       | Todos: Se refiere al usuario, grupo, y todos los demás.                                     |

**Acción**

| Símbolo | Significado                          |
| :-----: | ------------------------------------ |
|    +    | Añadir permiso, si es necesario      |
|    =    | Especificar el permiso exacto        |
|    -    | Eliminar el permiso, si es necesario |

**Permiso**

| Símbolo | Significado        |
| :-----: | ------------------ |
|    r    | leer (read)        |
|    w    | escribir (write)   |
|    x    | ejecutar (execute) |

### Cambio de propietario chown

Inicialmente, el propietario de un archivo es el usuario que lo crea. El comando `chown` se utiliza para cambiar el propietario de los archivos y directorios. Cambiar el usuario propietario requiere acceso administrativo. Un usuario ordinario no puede utilizar este comando para cambiar el usuario propietario de un archivo, ni tan solo para otorgar propiedad de uno de sus propios archivos a otro usuario. Sin embargo, el comando `chown` permite cambiar el grupo propietario, lo cual puede ser realizado por el usuario root o el propietario del archivo.

`chown [OPCIONES] [PROPIETARIO] ARCHIVO`

## Creación de un _alias_

```bash
alias nombre_alias="comando combinado"
```

**Ejemplo:**

```bash
alias mycal="cal 2014"
```

## Comando `w`

- `w` : display who is logged in and what they are doing

`user@domain:~$ w`

Resultado

```bash
17:15  up 1 day,  7:27, 2 users, load averages: 2.34 2.31 2.31
USER     TTY      FROM              LOGIN@  IDLE WHAT
Xizuth   console  -                Sat09   31:26 -
Xizuth   s000     -                17:15       - w
```

## Comando `grep`

El comando `grep` es un filtro de texto que busca líneas en una entrada y devolverá aquellas que coincidan con un patrón determinado

Opciones:
- `-c` Imprime cuantas coincidencia en la busqueda
- `-n` muestra los números de la línea originales
- `-l` en lista los archivos que en su contenido contiene el patron
- `-v` Todas las líneas que no contengan el patron
- `-i` ignora mayusculas y minusculas del patron en la busqueda, mostrando en donde se encuentra
- `-w` la busqueda debe coincidir exacto con el patron

```bash
grep [OPCIONES] PATRÓN [ARCHIVO]
```

Ejemplo:

```bash
grep sysadmin passwd
```

salida:

```bash
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```

Obtiene las coincidencias de la busqueda

```bash
grep -c bash /etc/passwd
```

Imprimer las lineas con el numero de linea en donde esta el archivo

```bash
grep -n bash /etc/passwd
```

Imprimer los directorios que coinciden

```bash
grep -l linux /etc/*
```

Todas las líneas que no contengan *nologin* en el archivo `/etc/passwd`

```bash
grep -v nologin /etc/passwd
```

Listado de las líneas de los archivos en el directorio `/etc` que contengan cualquier tipo de letra (mayúscula o minúscula) del patrón de caracteres `linux`

```bash
grep -i linux /etc/*
```

Listado de las líneas de los archivos en el directorio `/etc` que contengan el patrón de la palabra `linux`

```bash
grep -w linux /etc/*
```



## Comando `ls`

En lista los archivos y carpetas de uno o más directorios

En lista dentro de la carpeta donde se ubica:

```bash
sysadmin@localhost:~/Documents$ ls
```

En lista dentro de la carpeta que se pasa como argumento:

```bash
sysadmin@localhost:~$ ls Documents
```

En lista dentro de las carpetas que se pasa como argumento:

```bash
sysadmin@localhost:~$ ls /etc/ppp /etc/ssh
```

**Flags**

```bash
ls -l #lista
ls -a # muestra ocultos
ls -r #invierte el orden
```

## Comandos de historiales

### Comando `date`

Fecha

```bash
sysadmin@localhost:~$ date
Sun Nov  1 00:40:28 UTC 2015
```

### Comando `cal`

Calendario

```bash
sysadmin@localhost:~$ cal
   November 2020
Su Mo Tu We Th Fr Sa
 1  2  3  4  5  6  7
 8  9 10 11 12 13 14
15 16 17 18 19 20 21
22 23 24 25 26 27 28
29 30
```

### Comando (history)

Historial de comandos

```bash
sysadmin@localhost:~$ history
    1  date
    2  ls
    3  cal 5 2015
    4  history
```

## Instrucciones de control

Las instrucciones de control te permiten utilizar varios comandos a la vez o ejecutar comandos adicionales, dependiendo del éxito de un comando anterior. Normalmente estas instrucciones de control se utilizan en scripts o secuencias de comandos, pero también pueden ser utilizadas en la línea de comandos.

### Punto y coma `;`

El punto y coma puede utilizarse para ejecutar varios comandos, uno tras otro. Cada comando se ejecuta de forma independiente y consecutiva; no importa el resultado del primer comando, el segundo comando se ejecutará una vez que el primero haya terminado, luego el tercero y así sucesivamente.

```bash
cal ; echo "hola" ; ls -l ssh*
 November 2020
Su Mo Tu We Th Fr Sa
 1  2  3  4  5  6  7
 8  9 10 11 12 13 14
15 16 17 18 19 20 21
22 23 24 25 26 27 28
29 30

hola
total 160
-rw-r--r-- 1 root root 125749 Jan 13  2016 moduli
-rw-r--r-- 1 root root   1669 Jan 13  2016 ssh_config
-rw------- 1 root root    668 Mar 14  2016 ssh_host_dsa_key
-rw-r--r-- 1 root root    607 Mar 14  2016 ssh_host_dsa_key.pub
-rw------- 1 root root    227 Mar 14  2016 ssh_host_ecdsa_key
-rw-r--r-- 1 root root    179 Mar 14  2016 ssh_host_ecdsa_key.pub
-rw------- 1 root root   1675 Mar 14  2016 ssh_host_rsa_key
-rw-r--r-- 1 root root    399 Mar 14  2016 ssh_host_rsa_key.pub
-rw-r--r-- 1 root root    302 Jan 10  2011 ssh_import_id
-rw-r--r-- 1 root root   2489 Mar 14  2016 sshd_config
```

### Doble amperson `&&` [`AND`]

El símbolo de ampersand doble `&&` actúa como un operador "y" lógico. Si el primer comando tiene éxito, entonces el segundo comando (a la derecha de la `&&`) también se ejecutará. Si el primer comando falla, entonces el segundo comando no se ejecutará.

```bash
sysadmin@localhost:~$ ls /etc/xml && echo success
catalog  catalog.old  xml-core.xml  xml-core.xml.old
success
sysadmin@localhost:~$ ls /etc/junk && echo success
ls: cannot access /etc/junk: No such file or directory
```

### Doble pipe `||` [`OR`]

La línea vertical doble `||` es un operador lógico "o".
Con la línea vertical doble, si el primer comando se ejecuta con éxito, el segundo comando es omitido. Si el primer comando falla, entonces se ejecutará el segundo comando. En otras palabras, esencialmente estás diciendo al shell, "O bien ejecuta este primer comando o bien el segundo".

```bash
sysadmin@localhost:~$ ls /etc/xml || echo failed
catalog  catalog.old  xml-core.xml  xml-core.xml.old
sysadmin@localhost:~$ ls /etc/junk || echo failed
ls: cannot access /etc/junk: No such file or directory
failed
```

## Variables de entorno

- `env` : muestra todas las variables de entorno
- `export`: agrega la variable como variable de entorno
  - `export mivariable`
  - `export mivariable2="contenido de la variable"`
- `unset`: elimina la variable de entorno
  - `unset mivariable`

**HISTSIZE**

```BASH
HISTSIZE=5000 #estoy cambiando cuantos comandos guarda el historial de comandos
```

**PATH**

Define en qué directorios el shell buscará los comandos.

```bash
echo $PATH
/Users/Xizuth/.nvm/versions/node/v12.14.0/bin:/opt/local/bin:/opt/local/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/opt/X11/bin:/Users/Xizuth/.nvm/versions/node/v12.14.0/bin:/opt/local/bin:/opt/local/sbin
```

el shell primero busca el comando en el directorio `/home/sysadmin/bin`. Si el comando se encuentra en ese directorio, entonces se ejecuta. Si no es encontrado, el shell buscará en el directorio `/usr/local/sbin`.

## Alias

Un alias puede utilizarse para asignar comandos más largos a secuencias más cortas. Cuando el shell ve un alias ejecutado, sustituye la secuencia más larga antes de proceder a interpretar los comandos.

Los nuevos alias se pueden crear introduciendo alias `name=command` (o «alias nombre=comando» en español), donde nombre es el nombre que quieres dar a el alias y comando es el comando que quieres que se ejecute cuando se ejecuta el alias.

```bash
sysadmin@localhost:~$ alias lh='ls -Shl'
sysadmin@localhost:~$ lh /etc/ppp
total 0
drwxr-xr-x 1 root root 10 Jan 29  2015 ip-down.d
drwxr-xr-x 1 root root 10 Jan 29  2015 ip-up.d
```

## Globbing

| Nombre        | Simbolo | Aplicación                           | Descripción                                                                                                                                                                                                                                 |
| ------------- | ------- | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Asterisco     | \*      | `echo /etc/t*`                       | El asterisco se utiliza para representar cero o más de cualquier carácter en un nombre de archivo.                                                                                                                                          |
| Interrogación | ?       | `echo /etc/t???????`                 | El signo de interrogación representa cualquier carácter único.                                                                                                                                                                              |
| Corchetes     | [ ]     | `echo /etc/[gu]*` `echo /etc/[a-d]*` | Los corchetes se utilizan para coincidir con un carácter único representando un intervalo de caracteres que pueden coincidir con los caracteres. mostrará todos los archivos que comiencen con cualquier letra entre e incluyendo `a` y `d` |
| Exclamación   | !       | `echo [!DP]*`                        | El signo de exclamación se utiliza en conjunto con los corchetes para negar un intervalo. Por ejemplo, el comando echo [!DP]\* mostrará cualquier archivo que no comienza con `D` o `P`.                                                    |

 `sysadmin@localhost:~$ echo /etc/*???????????????????? /etc/bindresvport.blacklist /etc/ca-certificates.conf `
  - **\*** : 0 o más carácteres
  - **?** : 1 coincidencia
  - **[ ]** : coincide con el contenido
    - [gu] : coinciede con las letras _gu_
    - [a-d] : invertvalos
      - `sysadmin@localhost:~$ echo /etc/[gu]* /etc/gai.conf /etc/groff /etc/group /etc/group- /etc/gshadow /etc/gshadow- /etc/ucf.conf /etc/udev /etc/ufw /etc/update-motd.d /etc/updatedb.conf`
  - **!** : negación
    - `echo [!DP]*`: que no comience con DP
  - **" "** : texto dentro de la comillas
    - `echo "hola"`
    - `sysadmin@localhost:~$ echo "The path is $PATH" The path is /usr/bin/custom:/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games`
  - **\\** : escapa carácteres
    - `sysadmin@localhost:~$ echo The service costs \$100 and the path is $PATH The service costs $100 and the path is /usr/bin/custom:/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games`
  - **\` \`** : Las comillas invertidas se utilizan para especificar un comando dentro de un comando, un proceso de sustitución del comando. Esto permite un uso muy potente y sofisticado de los comandos.
    - sysadmin@localhost:~\$ echo Today is \`date\`
      Today is Mon Nov 2 03:40:04 UTC 2015`

### Las Comillas

Hay tres tipos de comillas que tienen significado especial para el shell Bash: comillas dobles `"`, comillas simples `'` y comilla invertida ` ` `. Cada conjunto de comillas indica al shell que debe tratar el texto dentro de las comillas de una manera distinta a la normal.

#### Comillas Dobles

Las comillas dobles detendrán al shell de la interpretación de algunos metacaracteres, incluyendo los comodines. Dentro de las comillas dobles, el asterisco es sólo un asterisco, un signo de interrogación es sólo un signo de interrogación y así sucesivamente. Esto significa que cuando se utiliza el segundo comando `echo` más abajo, el shell BASH no convierte el patrón de globbing en nombres de archivos que coinciden con el patrón:

```bash
sysadmin@localhost:~$ echo /etc/[dp]*
/etc/DIR_COLORS /etc/DIR_COLORS.256color /etc/DIR_COLORS.lightbgcolor /etc/PackageKit
sysadmin@localhost:~$ echo "/etc/[DP]*"
/etc/[DP]*
```

#### Comillas Simples

Las comillas simples evitan que el shell interprete algunos caracteres especiales. Esto incluye comodines, variables, sustitución de comando y otro metacarácter que aún no hemos visto.

```bash
sysadmin@localhost:~$ echo The car costs $100
The car costs 00
sysadmin@localhost:~$ echo 'The car costs $100'
The car costs $100
```

#### Barra Diagonal Inversa (\\)

Si colocas una barra diagonal invertida \ antes del otro carácter, tratará al otro carácter como un carácter de "comillas simples". El tercer comando más abajo muestra cómo utilizar el carácter \, mientras que los otros dos muestran cómo las variables serían tratadas si las pones entre las comillas dobles y simples:

```bash
sysadmin@localhost:~$ echo "The service costs $100 and the path is $PATH"
The service costs 00 and the path is /usr/bin/custom:/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games

sysadmin@localhost:~$ echo 'The service costs $100 and the path is $PATH'
The service costs $100 and the path is $PATH

sysadmin@localhost:~$ echo The service costs \$100 and the path is $PATH
The service costs $100 and the path is /usr/bin/custom:/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
```

#### Comilla Invertida `

Las comillas invertidas se utilizan para especificar un comando dentro de un comando, un proceso de sustitución del comando. Esto permite un uso muy potente y sofisticado de los comandos.

```bash
sysadmin@localhost:~$ date
Mon Nov  2 03:35:50 UTC 2015
```

```bash
sysadmin@localhost:~$ echo Today is `date`
Today is Mon Nov 2 03:40:04 UTC 2015
```

### Manual o información de comandos `Man`

Para buscar todos los tipos de archivo

```bash
man -f passwd
```

```bash
whatis passwd
```

```bash
passwd (5)           - the password file
passwd (1)           - change user password
passwd (1ssl)        - compute password hashes
```

Para entrar a ver el manual de `passwd` a nivel `file`, se usa el comando `man` con el `nivel` y el `command`:

```bash
man 5 passwd
```

### Encontrar por palabra clave

```bash
man -k passwd
```

#### `apropos`

search the manual page names and descriptions

```bash
apropos command
```

Estos dos comandos hacen lo mismo

```bash
man -k passwd
```

o

```bash
apropops passwd
```

**salida:**

```bash
chgpasswd (8)        - update group passwords in batch mode
chpasswd (8)         - update passwords in batch mode
gpasswd (1)          - administer /etc/group and /etc/gshadow
pam_localuser (8)    - require users to be listed in /etc/passwd
passwd (1)           - change user password
passwd (1ssl)        - compute password hashes
passwd (5)           - the password file
update-passwd (8)    - safely update /etc/passwd, /etc/shadow and /etc/group
```

#### Comando `info`

El comando `info` también proporciona documentación sobre funciones y comandos del sistema operativo. El objetivo de este comando es ligeramente diferente de las páginas `man`: *proporcionar un recurso de documentación que proporciona una estructura lógica*, facilitando la lectura de la documentación.

```bash
info passwd
```

```bash
info apt
```

### Opcion `--help`

Esto es útil para aprender el uso básico de un comando

#### Encontrar archivos `whereis` `locate`

```bash
sysadmin@localhost:~$  ps --help
```

#### Readme del sistema

Estos archivos de documentación se suelen llamar archivos "readme" , ya que los archivos tienen nombres como README o readme.txt. La ubicación de estos archivos puede variar según la distribución que estés utilizando. Ubicaciones típicas incluyen `/usr/share/doc` y `/usr/doc`.

### Comando `whereis` o `Locate`

`locate - find files by name`

El comando `whereis` está diseñado para encontrar de manera específica las páginas `man` y los comandos. Si bien esto es útil, hay veces en las que quieras encontrar un archivo o directorio, no sólo archivos de comandos o páginas mas.

Para encontrar cualquier archivo o directorio, puede utilizar el comando `locate`. Este comando buscará en una base de datos de todos los archivos y directorios que estaban en el sistema cuando se creó la base de datos. Por lo general, el comando que genera tal base de datos se ejecuta por la noche.

```bash
sysadmin@localhost:~$ whereis ls
ls: /bin/ls /usr/share/man/man1/ls.1.gz
```

```bash
sysadmin@localhost:~$ locate ls
/bin/false
/bin/ls
/bin/lsblk
/bin/lsmod
/etc/initramfs-tools
```

Puede que quieras empezar listando **cuántos archivos coincidirán**. Lo puedes hacer mediante la opción `-c` del comando `locate`:

```bash
sysadmin@localhost:~$ locate -c passwd
97
```

**Para limitar la salida aún más, coloca un carácter** `\` delante del término de búsqueda. Este carácter limita la salida a los nombres de archivo que coincidan exactamente con el término:

```bash
sysadmin@localhost:~$ locate -b "\passwd"
/etc/passwd
/etc/cron.daily/passwd
/etc/pam.d/passwd
/usr/bin/passwd
/usr/share/doc/passwd
/usr/share/lintian/overrides/passwd
```

Los archivos que creaste hoy normalmente no los vas a poder buscar con el comando `locate`. Si tienes acceso al sistema como usuario root (con la cuenta del administrador de sistema), puede actualizar manualmente la base de datos `locate` ejecutando el comando `updatedb`. Los usuarios regulares no pueden actualizar el archivo de base de datos.

#### `updatedb`

```bash
updatedb
```

`updatedb - update a database for mlocate`

### Comando `ls`

- `-S` ordena por size
- `-R` muestra todo los archivos, inlcuyendo los subdirectorios
- `-t` ordena por fecha
- `--full-time` visualiza la fecha y la hora completas (incluyendo horas, segundos, minutos...):
- `-r` los ordena de forma inversa


### Comando copiar `cp`

`cp` - copy files and directories

```bash
cp [fuente] [destino]
```

Argumentos

- `-v` verboso
- `-i` al copiar verificar si existe, en caso de existir pregunta si se desea sobreescribir
- `-n` se pasa para indicar que no sobreescriba
  - `cp -i -n archivo.txt archivo.copy`
- `-r` copia el directorio completo
  - `cp -r /usr/share/doc /home/usuario/`


### Comando mover `mv`

Mueve y renombra archivos

`mv [fuente] [destino]`

**Aplican los mismos argumento que `cp`**, no tiene la opcion `r` recursividad

### Comando eliminar `rm`

`rm [archivo]`

argumentos

- `-i` confirma eliminar el archivo
- `-r` borra la carpeta

### Enlances duros y simbolicos `ln`

Permite hacer referencias a directorios o archivos

```bash
ln <opciones> <ruta origen> <ruta destino>
```
Donde:

`<ruta origen>` es la ruta del directorio o archivo original.
`<ruta destino>` el la ruta en la que se realizará el enlace.

Argumentos:

- `-s` crea un enlace simbólico
- `-f` o `--force` elimina un objeto de destino en caso de que ya exista.
- `-i` o `--interactive` pregunta si se eliminará un objeto de destino.

Enlace duro

```bash
ln ~/original ~/copia
```
Enlace simbolico

```bash
ln -s ~/ejemplo_1 ~/simbolico_1
```

### Comando `stat`

El comando `stat` permite desplegar los datos generales de un objeto.

```bash
stat <opciones> <ruta>
```

```bash
stat Documents
```

Salida
```
File: `Documents/'
  Size: 4096            Blocks: 8          IO Block: 4096   directory
Device: 3000c2h/3145922d        Inode: 9049952     Links: 2
Access: (0755/drwxr-xr-x)  Uid: ( 1001/sysadmin)   Gid: ( 1001/sysadmin)
Access: 2020-01-10 21:53:30.476732135 +0000
Modify: 2016-03-14 17:34:24.000000000 +0000
Change: 2020-01-10 21:53:30.436732017 +0000
 Birth: -
```

### Comando `file`

El comando file regresa el tipo de archivo que se consulta.

```bash
file <ruta>
```

```bash
file .bashrc
.bashrc: ASCII English text
```

### Comando `tree`


Este comando permite desplegar la estructura de archivos y subdirectorios de un directorio dado.

```bash
tree <opciones> <ruta>
```

Argumentos:
- `-L #` Define el número de niveles de subdirectorios a los que accederá. # indica con un entero hasta que nivel se mostrará.
- `-a` para desplegar los archivos y directorios ocultos.

Muesta el arbol a 1 nivel

```bash
tree -L 1
```

Muesta el arbol a 1 nivel y los archivos ocultos

```bash
tree -aL 1
```

Muestra los directorios a su máximo nivel

```bash
tree ./
.
|-- Desktop
|-- Documents
|-- Downloads
|-- Music
|-- Pictures
|-- Public
|-- Templates
`-- Videos
8 directories, 0 files
```

### Comando `du`

Este comando despliega el tamaño que ocupa un directorio.

```bash
du <opciones> <ruta>
```

Argumentos:

- `-m` permite desplegar el tamaño de los directorios en MB.

Desplegara el contenido y el peso de la carpeta

```bash
du -m Documents
```

### Compresion de archivos `gzip` y `gunzip`

Para comprimir archivos

`gzip [archivo]`

Argumentos:
- `-l` conocer el porcentaje de compresion
  - `gzip -l [archivo].gz`
- `-d` descomprimir
  - `gzip -l [archivo].gz`

Descomprimir archivos

```bash
gzip -d [archivo].gz
```

```bash
gunzip [archivo].gz
```

### Empaquetamiento _tarballs_ `tar` (Tape ARchive )

`Tar` tiene 3 modos que deberás conocer:

- **Crear**: hacer un archivo nuevo de una serie de archivos
- **Extraer**: sacar uno o más archivos de un archivo
- **Listar**: mostrar el contenido del archivo sin extraer

Empaqueta, se la da un nombre y los archivos o carpeta

`tar -cf [nombre_pkg].tar [files...]`

#### Empaqueta y lo comprime con **`gzip`**

```bash
tar -czf [nombre_pkg].tar.gz  [files...]
```

```bash
tar -czf [nombre_pkg].tgz  [files...]
```

```bash
tar -rvf [archivo].tar [file_to_add]
```


Argumentos:

- `-c` creacion
- `-f` que se le pasara el nombre
- `-t` listar documentos en el archivo en el archivo empaquetado
- `-z` que use **gzip** para la tarea
- `j` que use **bzip2** para la tarea
- `x` para descomprimir
- `-r` recursividad (para agregar mas archivos a un *tar*)


#### Empaquetado y lo comprime con **bzip2**

```bash
tar -cjf [nombre_pack].tar.bz2  [nombre_archivos]
```

```bash
tar -cjf [nombre_pack].tbz  [nombre_archivos]
```

```bash
tar -cjf [nombre_pack].tbz2  [nombre_archivos]
```

**En listar el contenido de un `tar` comprimido**

```bash
tar -tf access_logs.tgz
```

```bash
tar -tvf access_logs.tgz
```

```bash
tar -tjf access_logs.tbz
```

```bash
tar -tzf access_logs.tgz
```

#### Descomprimiendo los `tar`

```bash
tar -xjf access_logs.tbz
```

```bash
tar -xzf access_logs.tar.gz
```

Si sólo quieres algunos documentos del archivo empaquetado puedes agregar sus nombres al final del comando, pero por defecto deben coincidir exactamente con el nombre del archivo o puedes utilizar un patrón:

```bash
tar -xjvf [archivo_comprimido].tbz [path/exacta_file]
```

```bash
tar -xzvf [archivo_comprimido].tgz [path/exacta_file]
```

#### Zip

Compresion de archivos

```bash
zip -r [nombre_compress].zip [archivos...]
```

- `-r` recursividad

El listado de los archivos en el `zip` se realiza por el comando `unzip` y la opción `–l` (listar):

```bash
unzip -l logs.zip
```

**Para descomprimir**

```bash
unzip [archivo].zip
```

### Pipe ( | )

Se utilizarse para enviar la salida de un comando a otro. Se utiliza a menudo para refinar los resultados de un comando inicial.

Múltiples barras verticales pueden utilizarse consecutivamente para unir varios comandos. Si se unen tres comandos con la barra vertical, la salida del primer comando se pasa al segundo comando. La salida del segundo comando se pasa al tercer comando. La salida del tercer comando se imprime en la pantalla.

En lugar de mostrar la salida del comando anterior, poner la barra vertical junto al comando `head` muestra sólo las primeras diez líneas:

```bash
ls /etc | head
```

Despliega el listado de archivo, enumera las lineas y saca las ultimas 5 lineas

```bash
ls -l /etc/ppp | nl | tail -5
```

## Redirección de I/O

Entras, salidas y errores estandars

- STDIN
- STDOUT
- STDERR

Rederigir hacia un archivo, lo crea y escribe `>`

```bash
echo "Line 1" > example.txt
```

Rederigir hacia un archivo, lo crea y agrega `>>`

```bash
echo "Line 1" >> example.txt
```

Puedes redirigir el STDERR de una manera similar a la STDOUT. STDOUT es también conocida como secuencia o canal («stream» o «channel» en inglés) #1. Al STDERR se asigna la secuencia #2.

- Canal 1 STDOUT
- Canal 2 STDERR

```bash
ls /fake 2> error.txt
cat error.txt
ls: cannot access /fake: No such file or directory # mensaje del archivo
```

Guardar todo lo que **no marca error**

```bash
ls /fake /etc/ppp > example.txt
```

Guardar todo lo **marca error**

```bash
ls /fake /etc/ppp 2> error.txt
```

Las salidas *STDOUT* y *STDERR* pueden enviarse a un archivo mediante el uso de `&>` un conjunto de caracteres que significan «ambos `1>` y `2>`»

```bash
ls /fake /etc/ppp &> all.txt
```

La salida aparece en el archivo con todos los mensajes *STDERR* en la parte superior y todos los mensaje *STDOUT* debajo de todos los mensajes de *STDERR*.

**Enviando a archivos distintos**, `example.txt` guarda los *STDOUT* y `error.txt` guarda los *STDERR*; no importa el órden:

```bash
 ls /fake /etc/ppp > example.txt 2> error.txt
```

**STDIN**

Con `cat` se queda esperando recibir datos, pero al recibirlos, el resultado lo devuelve a la salida.

```bash
cat
```

Con `cat > new.txt` lo que se escribe los manda al archivo

```bash
cat > new.txt
```

### Comando `tr`

Transforma o borrar caracteres. Lo que escribe lo convierte a mayúsculas

```bash
tr 'a-z' 'A-Z'
watch how this works
WATCH HOW THIS WORKS
```

Para transformar todos los caracteres de un archivo a mayusculas

``` bash
tr 'a-z' 'A-Z' < example.txt
```

Para transformar todo a mayusculas de un archivo y la salida mandarlo a otro archivo

```bash
tr 'a-z' 'A-Z' < example.txt > newexample.txt
```

### Comando `find`

Search for files in a directory hierarchy

``` bash
find [directorio de inicio] [opción de búsqueda] [criterio de búsqueda] [opción de resultado]
```

```bash
find [starting directory] [search option] [search criteria] [result option]
```

Opciones
  - `-name` para agregar el nombre del archivo, no afecta mayúsculas y minúsculas
  - `-ls` imprime la descripción como si fuera el comando `ls -l`
  - `-size` busca por tamaño de archivo. Tamaño en bytes (c), kilobytes (k), megabytes (M) o gigabytes (G)
  - `-maxdepth`	Permite al usuario especificar la profundidad en la estructura de los directorios a buscar. Por ejemplo, `-maxdepth 1` significaría sólo buscar en el directorio especificado y en sus subdirectorios inmediatos.
  - `-mmin`	Devuelve los archivos que fueron modificados según el tiempo de modificación en minutos. Por ejemplo, `-mmin 10` coincidirá con los archivos que fueron modificados hace 10 minutos.
  - `-type`	Devuelve los archivos que coinciden con el tipo de archivo. Por ejemplo, `-type f` devuelve los archivos que son archivos regulares. `d`para directorios


Buscar un archivo `hosts` por su nombre en todo el sistema y los errores tirarlos a la basura

```bash
find /etc -name hosts 2> /dev/null
```

Despliega los archivos como si era con el comando `ls -l` y los errores los manda a la basuca

```bash
find /etc -name hosts -ls 2> /dev/null
```

La búsqueda de archivos en la estructura de directorios `/etc` con el tamaño exacto de `10 bytes`:

```bash
find /etc -size 10c -ls 2>/dev/null
```

Buscará todos los archivos en la estructura de directorio `/usr` que su tamaño sea mayor a `100 megabytes`; se usa `+` o `-` para indicar si son mayores que o menores que la cantidad:

```bash
find /usr -size +100M -ls 2> /dev/null
```

```bash
find /etc -size 10c -type f -ls 2>/dev/null
```

## Vizualización de archivos `cat` `less` `more` `head` `tails`

- `cat` visualización de archivos pequeños
- `less` visualización de archivos avanzado
- `more` Este comando ha existido desde los primeros días de UNIX.
- `head`, `tails` : ver archivos con delimitación de lineas
  - `head -n 5 archivo.ext` (muestra las primero 5 lineas)
  - `head -n 10 archivo.txt`
  - `head -5 archivo.txt`

**Enfocado a `less`**

- Ventana hacia adelante	`Barra espaciadora`
- Ventana hacia atrás	`b`
- Línea hacia adelante	`Enter`
- Salir	`q`
- Ayuda	`h`

**`tail`**

Puedes ver los cambios en vivo en los archivos mediante la opción -f del comando tail. Esto es útil cuando quieres seguir cambios en un archivo mientras están sucediendo.

```bash
tail -f /var/log/mail.log
```

### Comando `sort` Ordenar archivos o entradas (STDIN)

Puede utilizarse el comando sort para reorganizar las líneas de archivos o entradas en orden alfabético o numérico basado en el contenido de uno o más campos. Los campos están determinados por un separador de campos contenido en cada línea, que por defecto son espacios en blanco (espacios y tabuladores).

Opciones:
- `-n` ordena por numeros
- `-r` invierte el orden
- `-t` se puede agregar el separador `-t,`, `-t:`
- `-k` se indica el campo por el cual se va a ordenar

Ordena por numeros y despues por letra en orden ascendente

```bash
sort archivo
```

El separador es `:`, se invierte el orden `-r` con base al campo 3 `-k3`
```bash
sort -t: -n -r -k3 mypasswd
```

Puede que quieras ordenar primero por el apellido (campo #2), luego el nombre (campo #1) y luego por edad (campo #3). Esto se puede hacer con el siguiente comando:

```bash
sort -t: -k2 -k1 -k3n filename
```

### Comando `wc`

`print newline, word, and byte counts for each file`

El comando `wc` permite que se impriman hasta tres estadísticas por cada archivo, así como el total de estas estadísticas, siempre que se proporcione más de un nombre de archivo.

Opciones:
- `-l` imprime el numero de lineas que tiene el archivo
- `-m` imprime el numero de caracteres
- `-c` imprime el peso en bytes del archivo

Imprime la cantidad de lineas, caracteres y peso en bytes del archivo

```bash
wc /etc/passwd
```

Imprime la suma de cantidad de lineas, caracteres y peso en bytes de los archivos, maximo puede imprimir de 2 archivos

```bash
wc /etc/passwd /etc/passwd-
```

```bash
wc /etc/passwd -l
```

Forma de uso:

Indica el número de arhivos que tiene el directorio `etc`

```bash
ls /etc/ | wc -l
```

### Comando `cut`

`remove sections from each line of files`

Puede extraer columnas de texto de un archivo o entrada estándar. El uso primario del comando `cut` es para trabajar con los archivos delimitados de las bases de datos.

Opciones:
- `-d` delimitador, por defaul `tab` es el delimitador; `-d:`
- `-f` Los campos a mostrar, al estar delimitado selecciona esos campos; `-f1,5-7`
- `-c` selecciona los carecteres; `-c1-11,50-`

```bash
cut -d: -f1,5-7 passwd
```

```bash
ls -l | cut -c1-11,50-
```

## Expresiones regulares

Es una colección de caracteres *«normales»* y *«especiales»* que se utilizan para que coincida con un patrón simple o complejo. Los caracteres normales son caracteres alfanuméricos que coinciden con ellos mismos.

| Expresión Regular | Coincidencias                                                                                                                                                                                             |
| :---------------: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|       **.**       | Cualquier carácter individual                                                                                                                                                                             |
|      **[ ]**      | **Una lista o rango** de caracteres que coinciden con un carácter, a menos que el primer carácter sea el símbolo de intercalación ^, lo que entonces significa cualquier carácter que no esté en la lista |
|      **\***       | ***El carácter previo* que se repite cero o más veces**                                                                                                                                                   |
|       **^**       | **El texto siguiente** debe aparecer al **principio de la línea**                                                                                                                                         |
|       **$**       | **El texto anterior** debe aparecer al **final de la línea**                                                                                                                                              |

Coincide el patron porque busca que comience con `a` y los `..` indica que hay 2 caracteres más cual sea

```bash
echo abcddd > example
sysadmin@localhost:~$ grep --color 'a..' example
`abc`ddd
```

Busca 2 palabras, la primera que contenga `a` o `b`, y la segunda letra en el rango de `a` hasta `d`

```bash
grep --color '[ab][a-d]' example
`ab`cddd
```

Busca el patron donde primero exista cualquier letra que no este en rango `a` a `c`, contigua a una `d`

```bash
grep --color '[^abc]d' example.txt
abc`dd`d
```

Busca que contenga la letra `d` seguido de ningun o mas del mismo caracter

```bash
grep --color 'd*' example.txt
abc`ddd`
```

Busca todas las coincidencia con la letra `a`

```bash
grep  'a' example
`a`bcddd
xyz`a`bc
```

Busca solo las que comienzan con `a`

```bash
grep  '^a' example
`a`bcddd
```

Buscará todas las palabras que terminan con `c`

```bash
grep "c$" example
xyzab`c`
```

Busca la coincidencia de la letra `cd` y que se repita la `d`

```bash
grep "cd*" example
ab`cddd`
xyzab`c`
ab`cd`*
```

Si queremos seleccionar con el `*` en la busqueda, se debe escapar el caracter

```bash
grep "cd\*" example
ab`cd*`
```

### Expresiones regulares Extendidas

Para aplicar las expresiones extendidas se aplica la opcion `-E`
|   RE   | Significado                                                                           |
| :----: | ------------------------------------------------------------------------------------- |
| **?**  | Coincide con el carácter anterior cero o una vez más, así que es un carácter opcional |
| **+**  | Coincide con el carácter anterior repetido una o más veces                            |
| **\|** | Alternación o como un operador lógico                                                 |

Haz coincidir `colo` seguido por cero o un carácter `u`

```bash
grep -E 'colou?r' example
```

Coincide con uno o más `d` caracteres

```bash
grep -E 'd+' example
```

Coincide con `gray` o `grey`

```bash
grep -E 'gray|grey' example
```

## Comando `xargs`

El comando `xargs` se utiliza para construir y ejecutar líneas de comandos de una entrada estándar. Este comando es muy útil cuando se necesita ejecutar un comando con una lista de argumentos muy larga, que en algunos casos puede resultar en un error si la lista de argumentos es demasiado larga.

Su objetivo es construir la línea de comandos para que un comando se ejecute las menos veces posibles con tantos argumentos como sea posible, en lugar de ejecutar el comando muchas veces con un argumento cada vez.

Opciones

- `-0`  desactiva la cadena de fin de archivo, permitiendo el uso de los argumentos que contengan espacios, comillas o barras diagonales inversas.

```bash
ls | xargs rm
```

## Trucos

Para generar archivos y carpetas con un patron

``` bash
mkdir {2000..2020}-{1..9}
```

Creara carpertas con la nomeclatura 2000-1 hasta 2020-9, todas las combinaciones posibles

## Extras

Especificación de la estructura de archivos

https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html

## Lista de comandos

- `whoami` : display effective user id
- `id` : return user identity
- `dd` : copiar particiones, discos, etc a nivel de _bits_
  - `dd if=/dev/sda of=/dev/sdb` -- clonar un disco duro
- `grep`
- `echo`: se utiliza para mostrar la salida en la terminal
- `which`
- `type`
- `nl` : regresa numero de lineas que contiene un archivo
