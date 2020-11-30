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

### Cambio de acceso a archivos (chmod)

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

Fecha

```bash
sysadmin@localhost:~$ date
Sun Nov  1 00:40:28 UTC 2015
```

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

Historial de comandos

```bash
sysadmin@localhost:~$ history
    1  date
    2  ls
    3  cal 5 2015
    4  history
```

# Lista de comandos

- `w` : display who is logged in and what they are doing
- `whoami` : display effective user id
- `chmod` : cambia el nivel de acceso a los archivos
- `id` : return user identity
- `cat` (ver achivos pequeños), less, more : ver archivos planos
- `head`, tails : ver archivos con delimitación de lineas
  - head -n 5 archivo.ext (muestra las primero 5 lineas)
  - `head -n 10 archivo.txt`
- `cp` : copiar
  - `cp [OPCIONES] ORIGEN DESTINO`
- `dd` : copiar particiones, discos, etc a nivel de _bits_
  - `dd if=/dev/sda of=/dev/sdb` -- clonar un disco duro
- `mv` : mover o cambiar nombre
- `ls`
- `history`
- `cal`
- `date`
- `grep`
- `echo`: se utiliza para mostrar la salida en la terminal
- `env` : muestra todas las variables de entorno
- `export`: agrega la variable como variable de entorno
  - `export mivariable`
  - `export mivariable2="contenido de la variable"`
- `unset`: elimina la variable de entorno
  - `unset mivariable`
- `which`
- `type`
- `alias`: me muestra todos los alias
- Globbing (comodines):
  - `sysadmin@localhost:~$ echo /etc/*???????????????????? /etc/bindresvport.blacklist /etc/ca-certificates.conf `
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

## Variables

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

### Globbing

| Nombre        | Simbolo | Aplicación                           | Descripción                                                                                                                                                                                                                                 |
| ------------- | ------- | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Asterisco     | \*      | `echo /etc/t*`                       | El asterisco se utiliza para representar cero o más de cualquier carácter en un nombre de archivo.                                                                                                                                          |
| Interrogación | ?       | `echo /etc/t???????`                 | El signo de interrogación representa cualquier carácter único.                                                                                                                                                                              |
| Corchetes     | [ ]     | `echo /etc/[gu]*` `echo /etc/[a-d]*` | Los corchetes se utilizan para coincidir con un carácter único representando un intervalo de caracteres que pueden coincidir con los caracteres. mostrará todos los archivos que comiencen con cualquier letra entre e incluyendo `a` y `d` |
| Exclamación   | !       | `echo [!DP]*`                        | El signo de exclamación se utiliza en conjunto con los corchetes para negar un intervalo. Por ejemplo, el comando echo [!DP]\* mostrará cualquier archivo que no comienza con `D` o `P`.                                                    |

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

#### Comilla Invertida

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

Puede que quieras **empezar listando cuántos archivos coincidirán**. Lo puedes hacer mediante la opción `-c` del comando `locate`:

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

### Trucos

Para generar archivos y carpetas con un patron

``` bash
mkdir {2000..2020}-{1..9}
```

Creara carpertas con la nomeclatura 2000-1 hasta 2020-9, todas las combinaciones posibles
