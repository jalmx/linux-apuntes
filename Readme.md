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

### Comando `chmod` - Cambio de acceso a archivos

El método simbólico y el método octal. El método simbólico es útil para cambiar un conjunto de permisos a la misma vez. El método octal o numérico requiere conocer el valor octal de cada uno de los permisos y requiere que los tres conjuntos de permisos (usuario, grupo, otros) se especifiquen cada vez.

```bash
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

### Más detalles de permisos de archivos y directorios

- El primer carácter indica el `tipo de archivo`.
- Los caracteres `2-4 indican los permisos para el usuario` al que pertenece el archivo.
- Los caracteres `5-7 indican los permisos para el grupo` al que pertenece el archivo.
- Los caracteres `8-10 indican los permisos para "otros"` o lo que se conoce a veces como los permisos del mundo. Esto incluiría todos los usuarios que no sean el propietario del archivo o un miembro del grupo del archivo.

```bash
ls -l /etc/passwd
-rw-r--r--. 1 root root 4135 May 27 21:08 /etc/passwd
```

| Caracter | Tipo de Archivo                                                                                                                                                                                                                                     |
| :------: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|  **-**   | Un archivo normal que puede estar vacío, contener texto o datos binarios.                                                                                                                                                                           |
|  **d**   | Un archivo de directorio que contiene los nombres de otros archivos y enlaces a los mismos.                                                                                                                                                         |
|  **l**   | Un enlace simbólico es un nombre de archivo que hace referencia (apunta) a otro archivo.                                                                                                                                                            |
|  **b**   | Un archivo de bloque es el que se refiere a un dispositivo de hardware de bloque donde los datos se leen en bloques de datos.                                                                                                                       |
|  **c**   | Un archivo de caracteres es aquel que se refiere a un dispositivo de hardware de caracteres, donde se leen los datos un byte a la vez.                                                                                                              |
|  **p**   | Una archivo «pipe» funciona de forma similar al símbolo de barra vertical, lo que permite a la salida de un proceso comunicarse con otro proceso por el archivo «pipe», donde se utiliza la salida de un proceso como entrada para el otro proceso. |
|  **s**   | Un archivo de socket permite que se comuniquen dos procesos, donde se permite a ambos procesos enviar o recibir datos.                                                                                                                              |

Los permisos establecidos en estos archivos determinan el nivel de acceso que un usuario va a tener en el archivo.

| Permiso | Significado relacionado a un archivo                                                                                                                                                                   | Significado relacionado a un directorio                                                                                                                                                                    |
| :-----: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|  **r**  | El proceso puede leer el contenido del archivo, es decir, los contenidos se pueden ver y copiar.                                                                                                       | Los nombres de archivo en el directorio se pueden enumerar, pero otros detalles no están disponibles.                                                                                                      |
|  **w**  | El proceso puede escribir en este archivo, por lo que los cambios se pueden guardar. Ten en cuenta que el permiso `w` realmente requiere el permiso `r` en un archivo para que funcione correctamente. | Los archivos se pueden agregar a un directorio o quitar del mismo. Ten en cuenta que el permiso `w` requiere el permiso `x` en el directorio para que funcione correctamente.                              |
|  **x**  | El archivo se puede ejecutar o correr como un proceso.                                                                                                                                                 | El usuario puede utilizar el comando cd para «entrar» al directorio y utilizar el directorio en una ruta de acceso para acceder a los archivos y, potencialmente, a los subdirectorios de este directorio. |

### Cambio de propietario - Comando `chown`

Inicialmente, el propietario de un archivo es el usuario que lo crea. El comando `chown` se utiliza para cambiar el propietario de los archivos y directorios. Cambiar el usuario propietario requiere acceso administrativo. Un usuario ordinario no puede utilizar este comando para cambiar el usuario propietario de un archivo, ni tan solo para otorgar propiedad de uno de sus propios archivos a otro usuario. Sin embargo, el comando `chown` permite cambiar el grupo propietario, lo cual puede ser realizado por el usuario root o el propietario del archivo.

`chown [OPCIONES] [PROPIETARIO] ARCHIVO`

Se puede hacer el cambio del usuario, grupo o ambos

Solo el cambio del propietario al archivo

```bash
chown ted abc.txt
```

Solo cambia tanto el usario como el grupo

```bash
chown user:group /path/to/file
chown user.group /path/to/file
```

Cambia solo el grupo

```bash
chown :group /path/to/file
chown .group /path/to/file
```

### Método simbolico `chmod`

`chmod nuevo_permiso nombre_de_archivo`

Cuando se especifica el `nuevo_permiso`, comienzas por utilizar uno de los caracteres siguientes para indicar qué conjunto de permisos quieres cambiar:

- `u` = cambiar los permisos del usuario propietario
- `g` = cambiar los permisos del grupo propietario
- `o` = cambiar los permisos de «otros»
- `a` = (*all*) aplicar los cambios a todos los conjuntos de permisos (usuario propietario, grupo propietario y «otros»)

Debe especificar un `+` para agregar un permiso o un `-` para quitar un permiso. Por último, especifica `r` para la lectura `w` para escritura y `x` para ejecución.

Podrías utilizar el carácter `=` en lugar de `-` o `+` para especificar exactamente los permisos que quieres para un conjunto de permisos

**Ejemplos:**

```bash
chmod u+r abc.txt
chmod ug+r,o-w abc.txt
chmod u=r-x abc.txt # al usario se le agrega read se quita write y de agrega exec, es una forma representativa a como se enlistan los permisos
```

### Método númerico `chmod`

| Número | Significado        |
| :----: | ------------------ |
| **4**  | read (leer)        |
| **2**  | write (escribir)   |
| **1**  | execute (ejecutar) |

Usando una combinación de números del 0 al 7, cualquier combinación de permisos posible para leer, escribir y ejecutar se pueden especificar por un conjunto de permisos individuales.

| Valor | Equivalencia |
| :---: | :----------: |
| **7** |     rwx      |
| **6** |     rw-      |
| **5** |     r-x      |
| **4** |     r--      |
| **3** |     -wx      |
| **2** |     -w-      |
| **1** |     --x      |
| **0** |     ---      |

```bash
chmod 754 abc.tx # rwxr-xr-
```

### Comando `umask`

El comando umask es una característica que se utiliza para determinar los permisos predeterminados establecidos al crear un archivo o directorio. Los permisos predeterminados se determinan cuando el valor de umask se resta de los permisos máximos predeterminados permisibles. Los permisos máximos por defecto son diferentes para los archivos y para los directorios:

|    Tipo     | Permisos  |
| :---------: | --------- |
|   archivo   | rw-rw-rw- |
| directorios | rwxrwxrwx |

Al ejercutar el comando 

Usuarios normales

```bash
umask
0002
```

Como `root`

```bash
umask
0022
```

- El primer `0` indica que umask se da como un número octal.
- El segundo `0` indica qué permisos hay que restar de los permisos por defecto de usuario propietario.
- El tercer `0` indica qué permisos hay que restar de los permisos por defecto del grupo propietario.
- El último número `2` indica qué permisos hay que restar de los permisos por defecto de otros.

Para entender cómo funciona `umask`, supongamos que umask se establece en `027` y consideremos lo siguiente:

 | Significado                         |  Valor  |
 | ----------------------------------- | :-----: |
 | File Default (valor predeterminado) |   667   |
 | Umask                               |  -027   |
 | **Resultado**                       | **640** |

La umask `027` significa que, por defecto los archivos nuevos recibirían los permisos `640` o `rw-r-----` tal como se demuestra a continuación:

```bash
umask 027
touch sample
ls -l sample
-rw-r-----. 1 sysadmin sysadmin 0 Oct 28 20:14 sample
```

Debido a que los permisos predeterminados para los directorios son diferentes que para los archivos, una `umask 027` daría lugar a diferentes permisos iniciales sobre los nuevos directorios:

| Significado                              |  Valor  |
| ---------------------------------------- | :-----: |
| Directory Default (valor predeterminado) |   777   |
| Umask                                    |  -027   |
| **Resultado**                            | **750** |

La `umask 027` significa que, por defecto los directorios nuevos recibirían los permisos `750` o `rwxr-x-----` tal como se demuestra a continuación:

```bash
umask 027
mkdir test-dir
ls -ld test-dir
drwxr-x---. 1 sysadmin sysadmin 4096 Oct 28 20:25 test-dir
```

*Cambiar permanentemente la `umask` requiere la modificación del archivo `.bashrc` que se encuentra en el directorio `home` del usuario.*

### Permisos especiales `setuid`

#### El Permiso `setuid`

Cuando el `permiso setuid` se encuentra en un archivo binario ejecutable (un programa), el archivo binario se «ejecuta como» el propietario del archivo, no como el usuario que lo ejecuta. Este permiso se establece en una cierta cantidad de utilidades del sistema para que puedan ser manejados por los usuarios normales, pero ejecutados con los permisos root, proporcionando acceso a los archivos del sistema a los que el usuario normal normalmente no tiene acceso.

Ejecutar el permiso setuid

```bash
chmod u+s file
```

```bash
ls -l /usr/bin/passwd
-rwsr-xr-x 1 root root 31768 Jan 28 2010 /usr/bin/passwd
```

Para agregar el permiso setuid numéricamente, agrega 4000

```bash
chmod 4775 file
```

Retirar el permiso de `sertuid`

```bash
chmod u-s file
```

o

```bash
chmod 0775 file
```

#### El Permiso `setgid` en un Archivo

El permiso `setgid` es similar a `setuid`, pero hace uso de los permisos del grupo propietario. En realidad, hay dos formas de permisos setgid: *`setgid` en un archivo y `setgid` en un directorio*. Cómo funciona el setgid depende de si se establece en un archivo o un directorio.

Permite que un usuario ejecute un archivo binario ejecutable proporcionando un *acceso adicional (temporal) de grupo*.

El comando `wall` puede ejecutar y mandar datos al grupo `tty` gracias a que tiene setgid. Esto no sería posible dado que las terminales `tty?` no permite que `otros` accedan a escribir.

```bash
ls -l /usr/bin/wall
-rwxr-sr-x. 1 root tty 10996 Jul 19  2011 /usr/bin/wall
```

```bash
ls -l /dev/tty?
crw-------. 1 root tty  4, 0 Mar 29  2013 /dev/tty0
crw--w----. 1 root tty  4, 1 Oct 21 19:57 /dev/tty1 #solo a lo que pertenencen al mismo grupo pueden escribir
```

## Creación de un _alias_

Esto se aplica solo a la terminal actual, para que se quede permanente en el usario se debe agregar al archivo `.bashrc` o `.zshrc`, depende el `shell`.

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

Hay tres tipos de comillas que tienen significado especial para el shell Bash: comillas dobles `"`, comillas simples `'` y comilla invertida ` `` `. Cada conjunto de comillas indica al shell que debe tratar el texto dentro de las comillas de una manera distinta a la normal.

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
## Bash Scripting

Comparaciones

| Comando                   | Descripción                                                                          |
| ------------------------- | ------------------------------------------------------------------------------------ |
| `test –f /dev/ttyS0	0`    | si el archivo existe                                                                 |
| `test ! –f /dev/ttyS0`    | 0 si el archivo no existe                                                            |
| `test –d /tmp`            | 0 si el directorio existe                                                            |
| `test –x `which ls`\`     | sustituir la ubicación de `ls` y luego (probar) `test`, si el usuario puede ejecutar |
| `test 1 –eq 1`            | 0 si tiene éxito la comparación numérica                                             |
| `test ! 1 –eq 1`          | NO – 0 si la comparación falla                                                       |
| `test 1 –ne 1`            | Más fácil, ejecutar test (probar) si hay desigualdad numérica                        |
| `test “a” = “a”`          | 0  si tiene éxito la comparación de cadenas                                          |
| `test “a” != “a”`         | 0  si las cadenas son diferentes                                                     |
| `test 1 –eq 1 –o 2 –eq 2` | `-o` es OR: cualquiera de las opciones pueden ser igual                              |
| `test 1 –eq 1 –a 2 –eq 2` | `-a` es AND: ambas comparaciones deben ser iguales                                   |

### Condicionales 

#### Condicional `if` `elif` `else`

```bash
#!/bin/bash
# script.sh

if [ "$1" = "hello" ]; then
  echo "hello yourself"
elif [ "$1" = "goodbye" ]; then
  echo "nice to have met you"
  echo "I hope to see you again"
else
  echo "I didn't understand that"
fi
```

Ejecucion

```bash
./script.sh hello
hello yourself

./script.sh goodbye
nice to have met you
I hope to see you again

./script.sh
I didn't understand that
```

#### Condicional `case`

```bash
#!/bin/bash

case "$1" in
hello|hi)
  echo "hello yourself"
  ;;
goodbye)
  echo "nice to have met you"
  echo "I hope to see you again"
  ;;
*)
  echo "I didn't understand that"
esac
```

### Loops 

Hay dos loops principales en los scripts del shell: el loop `for` y el loop `while`.

#### Ciclo `for`

```bash
#!/bin/bash

SERVERS="servera serverb serverc"

for S in $SERVERS; do
  echo "Doing something to $S"
done
```
Resultado

```bash
Doing something to servera
Doing something to serverb
Doing something to serverc
```

```bash
#!/bin/bash

for NAME in Sean Jon Isaac David; do
  echo "Hello $NAME"
done

for S in *; do
  echo "Doing something to $S"
done
```
El segundo loop utiliza comodín `*` que es un file glob. El shell expande eso a todos los archivos en el directorio actual.

Resultado:
```bash
Hello Sean
Hello Jon
Hello Isaac
Hello David
Doing something to Readme.md
Doing something to sc.sh
```

*Cuenta la cantidad de palabras en cada archivo*

```bash
for name in /etc/passwd /etc/hosts /etc/group
do
  wc $name
done
```

#### Ciclo `while`

```bash
#!/bin/bash

i=0
while [ $i -lt 10 ]; do
  echo $i
  i=$(( $i + 1))
done
echo "Done counting"
```

Resultado:

```bash
0
1
2
3
4
5
6
7
8
9
Done counting
```

## Hardware

- `arch` Para conocer la arquitectura
- `lscpu` información del CPU y arquitectura
- `cat /proc/cpuinfo` La manera más detallada de obtener la información acerca de tu CPU es visualizando el archivo
- `dmidecode` ver los dispositivos conectados directamente a la tarjeta madre
- `free` ver la información de la RAM, tiene para ver en mega, giga `-m` `-g`
- `lspci` ver todos los dispositivos conectados por un bus PCI
  - `-nn`es para ver más detalles del vendor
  - `-d vendor:device` para ver detalles del dispositivo `lspci -d 15ad:07b0 -vvv` 
- `lsusb` el listado de dispositivos usb
  - `-v` para ver más detalles
- `lshal` te permite ver los dispositivos detectados por HAL.
- `fdisk` manipulate disk partition table
  - `fdisk -l` En lista los discos duros en cilindros
  - `fdisk -cul` en lista los discos en sectores
  - `fdisk -l /dev/sda` Muestra la información de la partición en el primer dispositivo de `sd`
  - `df` manipulate disk partition table
    - `df -l` lo muestra en forma de lista los espacios del disco duro
  - `lsmod` program to show the status of modules in the Linux Kernel

## Gestion de paquetes y procesos

### Debian `.deb`

- `sudo apt-get update` actualizo el sistema
- `sudo apt-cache search keyword` busco paquetes
- `sudo apt-get install package` installar paquetes
- `sudo apt-get upgrade` actualiza a nuevas versiones los paquetes
- `sudo apt-get remove package` Si quieres eliminar todos los archivos de un paquete de software, excepto los archivos de configuración
- `sudo apt-get --purge remove package` Si quieres eliminar todos los archivos de un paquete de software, incluyendo los archivos de configuración
- `dpkg -l` listar los paquetes instalados
- `dpkg -L package`  listar los archivos que componen un paquete especial
- `dpkg -s package` Para consultar un paquete y obtener información o su estado
- `dpkg -S /path/to/file` Para determinar si un determinado archivo fue puesto en el sistema de archivos como el resultado de la instalación de un paquete

### Red Hat `.rpm`

- `yum install package` instala paquetes
- `yum search keyword` busca paquetes
- `yum update package` Si quieres actualizar un paquete de software individual
- `yum remove package` remueve paquetes
- `rpm -qa` Para obtener una lista de todos los paquetes que están instalados actualmente en el sistema ejecuta
- `rpm -ql package` Para listar los archivos que componen un paquete especial
- `rpm -qi package` Para consultar un paquete y obtener información o su estado
- `rpm -qf /path/to/file` Para determinar si un archivo en particular fue puesto en el sistema de archivos como el resultado de la instalación de un paquete

### Procesos

Todo lo relacionado a los procesos se encuentra en el directorio `/proc/sys/`.

El archivo `/proc/sys/kernel/pid_max` define el numero maximo de procesos, cuando llega al topo reinicia y toma los numeros disponibles

- `pstree` display a tree of processes
- `ps`  sólo mostrará los procesos actuales en el shell, snapshot
  - `--forest` indica las ramificaciones de los procesos
  - `aux` para ver todos los procesos del sistema; `ps aux`
  - `-ef` para ver todos los procesos del sistema; `ps -ef`
  - `top` display Linux processes
    - con la tecla `k` activo para eliminar un proceso, con `9` se manda a cerrar de manera forzosa
    - `ps -o pid,tty,time,%cpu,cmd` el argumento `-o` indica las columnas que se van a mostrar
    - `ps -o pid,tty,time,%mem,cmd --sort %mem` la opcion `--sort` los esta enlistando en orden de consumo de memoria
  - `uptime` o `cat /proc/loadavg` ver la carga promedio del sistema
  - `free` sin opciones proporciona una foto de la memoria RAM utilizada en ese momento
    - `free -s 10` actualizaría la salida cada 10 segundos.

### Mandar procesos a segundo plano `&`

Al añadir el signo `&` al final del comando, el proceso se inicia en el segundo plano y permite al usuario mantener el control de la terminal.

```bash
ping localhost > /dev/null &
[1] 158
```

*Esto significa que este proceso tiene un número de trabajo 1 (como lo muestra la salida [1]) y un identificador de proceso (PID) de 158*

Para ver los comandos en ejecucion en la terminal actual

```bash
jobs
[1]+  Running                 ping localhost > /dev/null &
```

Para traerlos a primer plano, se usa el comando `fg` `%` y el numero de `job`

```bash
fg %1
```

Para `suspender` el proceso, no detener se ocupa `ctl+z`, se pausa pero continua como un `job` en la terminal

Para que este proceso continúe ejecutándose en segundo plano, ejecuta el siguiente comando, se usa el comando `bg` `%` y el numero de `job`

```bash
bg %1
```

### Comando `kill` `pkill`

Sirve para eliminar los procesos que estan corriendo

```bash
kill PID 
```

```bash
pkill [opciones] [name_process] 
```

Elimina el proceso con ese ID

```bash
kill 182 
```

Elimina todos todos los procesos sleep

```bash
pkill -15 sleep 
```


## Archivos de registros `logs`

Los demonios que se ejecutan en segundo plano para realizar el registro se llaman `syslogd` y `klogd`. En otras distribuciones, un demonio como el `rsyslogd` en Red Hat y Centos o `systemd journald` en Fedora puede servir para esta función de registro.

Independientemente del nombre del proceso de demonio, los archivos de registro se colocan casi siempre en la estructura del directorio `/var/log`.

|    Archivo     | Contenido                                                                                                                                                                      |
| :------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
|  **boot.log**  | Mensajes generados cuando servicios se inician durante el arranque del sistema.                                                                                                |
|    **cron**    | Mensajes generados por el demonio crond para las tareas que se deben ejecutar en forma recurrente.                                                                             |
|   **dmesg**    | Mensajes generados por el kernel durante el arranque del sistema.                                                                                                              |
|  **maillog**   | Mensajes producidos por el demonio de correo para mensajes de correo electrónico enviados o recibidos                                                                          |
|  **messages**  | Mensajes del kernel y otros procesos que no pertenecen a ninguna otra parte. A veces se denomina `dsyslog` en lugar de `messages` cuando el demonio haya grabado este archivo. |
|   **secure**   | Mensajes de los procesos que requieren autorización o autenticación (por ejemplo, el proceso de inicio de sesión).                                                             |
| **Xorg.0.log** | Mensajes del servidor de ventanas X (GUI).                                                                                                                                     |

Los comandos lastb y last se pueden usar para ver los archivos /var/log/btmp y /var/log/wtmp respectivamente.

## Command `dmesg`

`print or control the kernel ring buffer`

El archivo `/var/log/dmesg` contiene los mensajes del kernel que se produjeron durante el arranque del sistema. El archivo `/var/log/messages` contiene mensajes del kernel que se producen mientras el sistema está corriendo, pero los mensajes se mezclarán con otros mensajes de demonios o procesos.

*Si estuvieras resolviendo problemas con tu dispositivo USB, entonces buscando el texto «USB» con el comando grep siendo sensible a mayúsculas y minúsculas.*

```bash
dmesg | grep -i usb
```

## Red

Archivos para configuraciones de `red`

| Comando                  | Explicación                                                                                                                                                                                                                                                                                                                         |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/etc/hosts`             | Este archivo contiene una tabla de nombres de host para las direcciones IP. Puede utilizarse para complementar un servidor DNS.                                                                                                                                                                                                     |
| `/etc/sysconfig/network` | Este archivo tiene dos configuraciones. La configuración de NETWORK (o «red» en español) puede determinar si la red está activada (yes) o desactivada (no). La configuración de HOSTNAME (O «nombre de host» en español) define un nombre de host de la máquina local.                                                              |
| `/etc/nsswitch.conf`     | Este archivo se puede utilizar para modificar dónde se producen las búsquedas de nombre de host. Por ejemplo, la configuración hosts : files dns buscaría los nombres de host primero en el archivo /etc/hosts y después en el servidor DNS. Si cambias a hosts: dns files, la búsqueda se lleva a cabo primero en el servidor DNS. |

### Comandos para red `ip` `ping` `ss` `dig` `host`

Para ver las interfaces de red

- `ip -a addr` muestras las interfaces
- `ip addr show` muestras las interfaces
- `routel` o `route` list routes with pretty output format
- `ping` se puede utilizar para determinar si otra máquina es «accesible»
  - `-c` comando para definir cuantos ping lanzara; `-c 4` lanzara 4 pings y termina
- `netstat` Puede utilizarse para mostrar información acerca de conexiones de red, el nuevo comando es `ss`
  - `-i` indica las conexiones de las interfaces de red
  - `-r` muestra el enrutamiento
  - `-tln` para ver los puertos abiertos
    - `-t` indica tcp
    - `-l` indica las que esta escuchando **LISTEN**
    - `-n` indica el numero de puerto
- `dig` DNS lookup utility
  - `dig example.com`
- `host` DNS lookup utility
  - `host example.com`
  - `host 192.168.0.1`
  - `host -t CNAME example.com`
  - `host -t SOA example.com` los registros `SOA` (Start of Authority) indican el servidor principal para el dominio
  - `host -a example.com` da todos los registros del dominio

## Usuarios y cuentas archivos `passwd` `shadow` `group`

### passwd

```
root:x:0:0:root:/root:/bin/bash                                               
daemon:x:1:1:daemon:/usr/sbin:/bin/sh                                         
bin:x:2:2:bin:/bin:/bin/sh                                                    
sys:x:3:3:sys:/dev:/bin/sh                                                    
sync:x:4:65534:sync:/bin:/bin/sync 
```

Formato

```
name:password placeholder:user id:primary group id:comment:home directory:shell
```

La siguiente tabla describe cada uno de estos campos en detalle, usando la primera línea de la salida en el ejemplo anterior `(root:x:0:0:root:/root:/bin/bash)`:

| Campo                |  Ejemplo  | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| -------------------- | :-------: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| name                 |   root    | Es el nombre de la cuenta. Este nombre lo utiliza una persona cuando inicia sesión en el sistema y cuando la propiedad del archivo viene proporcionada por el comando ls -l. Por lo general, el sistema utiliza el ID de usuario (véase abajo) internamente y se proporciona el nombre de cuenta para que a los usuarios regulares se les haga más fácil referirse a la cuenta. Normalmente, la cuenta root es una cuenta administrativa especial. Sin embargo, es importante tener en cuenta que no todos los sistemas tienen una cuenta root, y en realidad, el ID de usuario 0 (cero) proporciona los privilegios administrativos en el sistema.                                                                                                                                                                                                            |
| password placeholder |     x     | Antes, la contraseña se guardaba en esta ubicación, ahora se almacena en el archivo /etc/shadow. La x en el campo del marcador de posición de la contraseña indica al sistema que la contraseña no se almacena aquí, sino más bien en el archivo /etc/shadow.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| user id              |     0     | Cada cuenta tiene asignado un Id. de usuario (UID «User ID» en inglés). El UID es lo que realmente define la cuenta, ya que el nombre de usuario normalmente no es utilizado directamente por el sistema. Por ejemplo, los archivos son propiedad de los UID, no de los nombres de usuario.Algunos UID son especiales. Por ejemplo, el UID 0 le da a la cuenta de usuario privilegios administrativos. Los UID por debajo de 500 (en algunas distribuciones de Linux 1.000) están reservados para las cuentas del sistema. Las cuentas del sistema se tratarán con más detalle más adelante en este capítulo.                                                                                                                                                                                                                                                  |
| primary group id     |     0     | Cada archivo y directorio es propiedad de una cuenta de usuario. Normalmente la persona que crea la cuenta posee el archivo. Además, cada archivo es propiedad de un grupo, normalmente del grupo primario del usuario. A los grupos se les asignan identificadores numéricos al igual que a los usuarios. Cuando un usuario crea un archivo, el archivo es propiedad del UID del usuario y también de un id de grupo (GID «Group ID» en inglés), el GID primario del usuario. Este campo define que GID es el GID primario del usuario. Además, al proporcionar la propiedad del grupo por defecto en un archivo, este campo también indica que el usuario es un miembro del grupo, lo que significa que el usuario tendrá permisos especiales en cualquier archivo que pertenece a este grupo. Los permisos se cubrirán en detalle en un capítulo posterior. |
| comment              |   root    | Este campo puede contener cualquier información sobre el usuario, incluyendo su nombre real (completo) y otra información útil. Este campo también se llama el campo GECOS (General Electric Comprehensive Operating System). El GECOS es un formato predefinido usado raramente para este campo que define una lista de elementos separada por comas, incluyendo el nombre completo del usuario, ubicación de la oficina, número de teléfono e información adicional. El administrador puede modificar la información GECOS con el comando chfn y los usuarios pueden ver esta información con el comando finger.                                                                                                                                                                                                                                             |
| home directory       |   /root   | Este campo define la ubicación del directorio home del usuario. Para los usuarios regulares, esto sería normalmente /home/username donde username se reemplaza con el nombre de usuario del usuario. Por ejemplo, un nombre de usuario bob tendría un directorio home /home/bob. El usuario root tiene normalmente una ubicación diferente para el directorio home: /root. Las cuentas del sistema raramente tienen directorios, ya que normalmente no se utilizan para crear o guardar los archivos.                                                                                                                                                                                                                                                                                                                                                          |
| shell                | /bin/bash | Aquí está ubicado el shell del inicio de la sesión del usuario. De forma predeterminada, el usuario se "ubica en" este shell siempre que el usuario inicia la sesión en un entorno de línea de comandos o abre una ventana de terminal. El usuario luego puede pasar a un shell diferente escribiendo el nombre del shell, por ejemplo: /bin/tcsh. El shell bash (/bin/bash) es el más común para los usuarios de Linux.                                                                                                                                                                                                                                                                                                                                                                                                                                       |

### shadow

```
head /etc/shadow                                           
root:$6$4Yga95H9$8HbxqsMEIBTZ0YomlMffYCV9VE1SQ4T2H3SHXw41M02SQtfAdDVE9mqGp2hr20q
.ZuncJpLyWkYwQdKlSJyS8.:16464:0:99999:7:::                                    
daemon:*:16463:0:99999:7:::                                                   
bin:*:16463:0:99999:7:::                                                      
sys:*:16463:0:99999:7:::                                                      
sync:*:16463:0:99999:7:::                                                     
games:*:16463:0:99999:7:::                                                    
man:*:16463:0:99999:7:::                                                      
lp:*:16463:0:99999:7:::                                                       
mail:*:16463:0:99999:7:::                                                     
news:*:16463:0:99999:7:::   
```

Los campos del archivo `/etc/shadow` son:

```name:password:last change:min:max:warn:inactive:expire:reserved```

Se describre el siguiente registro

```sysadmin:$6$lS6WJ9O/fNmEzrIi$kO9NKRBjLJJTlZD.L1Dc2xwcuUYaYwCTS.gt4elijSQW8ZDp6GLYAx.TRNNpUdAgUXUrzDuAPsYs5YHZNAorI1:15020:5:30:7:60:15050:```

| Campo       | Ejemplo           | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ----------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| name        | sysadmin          | Este es el nombre de la cuenta, que coincide con el nombre de cuenta en el archivo /etc/passwd.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| password    | \$6\$.........rI1 | El campo passwd contiene la contraseña cifrada de la cuenta. Esta cadena muy larga (que está truncada en el ejemplo a la izquierda de esta celda) es un cifrado unidireccional, lo que significa que no puede "revertirse" para determinar la contraseña original. Mientras que los usuarios habituales tienen contraseñas encriptadas en este campo, las cuentas del sistema tendrán un carácter de * en este campo. Verás más detalles sobre las cuentas de sistema más adelante en este capítulo.                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| last change | 15020             | Este campo contiene un número que representa la última vez que la contraseña fue cambiada. El número 15020 es el número de días desde el 01 de enero de 1970 (llamada la Época) y el último día en el que la contraseña de la cuenta fue cambiada. Este valor se genera automáticamente cuando se modifica la contraseña del usuario. Este valor es importante ya que se utiliza por característica de envejecimiento de la contraseña proporcionado por el resto de los campos de este archivo.                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| min         | 5                 | Este es uno de los campos del envejecimiento de la contraseña; un valor distinto de cero en este campo indica que después de que un usuario cambiara su contraseña, la contraseña no se puede cambiar otra vez por un número específico de días (5 en este ejemplo). Este campo es importante cuando se utiliza el campo max (véase abajo). Un valor de cero en este campo significa que el usuario siempre puede cambiar su contraseña.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| max         | 5                 | Este campo se utiliza para obligar a los usuarios a cambiar regularmente sus contraseñas. Un valor de 30 en este campo significa que el usuario debe cambiar su contraseña al menos cada 30 días para evitar que su cuenta quede «bloqueada» Ten en cuenta que si el campo min se establece en 0, el usuario puede restablecer inmediatamente su contraseña al valor original, anulando el propósito de obligar al usuario a cambiar su contraseña cada 30 días. Así que, si se establece el campo max, normalmente se establece también el campo min. Por ejemplo, un min:max de 5:60 se refiere a que el usuario debe cambiar su contraseña cada 60 días y, después de cambiarla, el usuario debe esperar 5 días antes de que pueda cambiar su contraseña otra vez. Si el campo max se establece a 99999, el valor máximo posible, entonces el usuario esencialmente nunca debe cambiar su contraseña (porque 99999 días son aproximadamente 274 años). |
| warn        | 7                 | Si se establece el campo max, el campo warn indica que al usuario se le «advertirá» cuando se acerca el plazo máximo max. Por ejemplo, si se establece warn a 7, entonces en cualquier momento durante los 7 días anteriores al plazo max se le advertirá al usuario que cambie su contraseña durante el proceso del inicio de sesión. El usuario sólo se advierte en el inicio de sesión, por lo que algunos administradores prefieren establecer el campo de advertencia a un valor alto para proporcionar una mayor probabilidad de tener una advertencia emitida.Si el plazo máximo max se establece al valor de 99999, entonces el campo warn es esencialmente inútil                                                                                                                                                                                                                                                                                |
| inactive    | 60                | Si el usuario hace caso omiso a las advertencias y se excede el plazo max para la contraseña, se bloqueará su cuenta. En tal caso, el campo inactive proporciona al usuario un período de «gracia» en el que puede cambiar su contraseña, pero sólo durante el proceso del inicio de sesión. Si el campo inactive viene establecido a un valor de 60, el usuario tiene 60 días de gracia para cambiar la contraseña a una nueva. Si no lo hace, entonces necesitará que el administrador restablezca la contraseña para el usuario.                                                                                                                                                                                                                                                                                                                                                                                                                       |
| expire      | 15050             | Este campo representa el número de días a partir del 01 de enero del 1970 y el día en el que la cuenta «vencerá». Una cuenta vencida se bloqueará, no se borra, lo que significa que el administrador puede restablecer la contraseña para desbloquear la cuenta. Las cuentas con fechas de vencimiento normalmente se ofrecen a los empleados temporales o contratistas. La cuenta caducará automáticamente después del último día laboral del usuario. Cuando un administrador establece este campo, se utiliza una herramienta para convertir una fecha real en una fecha de «Época». En Internet hay varios convertidores disponibles.                                                                                                                                                                                                                                                                                                                |
| reserved    |                   | Actualmente este campo no se utiliza y está reservado para su uso futuro.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |

### Archivo `group` Comando `groups`

Ubicación `/etc/group`
El archivo /etc/group es un archivo delimitado por dos puntos con los siguientes campos:

- `groups` retorna los grupos del usuario actual

```
group_name:password_placeholder:GID:user_list
```

La siguiente tabla describe los campos del archivo /etc/group con más detalle, utilizando una línea que describe a una cuenta de grupo típica:

```
mail:x:12:mail,postfix
```

| Campo                |   Ejemplo    | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| -------------------- | :----------: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| group_name           |     mail     | Este campo contiene el nombre del grupo. Igual que en el caso de los nombres de usuario, para las personas es más fácil recordar los nombres de grupo. El sistema utiliza típicamente IDs de grupos (GID) en lugar de nombres de grupo.                                                                                                                                                                                                                                                                                                |
| password_placeholder |      x       | Aunque hay contraseñas para grupos, raramente se utilizan en Linux. Si el administrador creará una contraseña de grupo, se almacenaría en un archivo diferente (/etc/gshadow) ya que la contraseña de grupo ya no se almacena en el archivo /etc/group. La x en este campo se utiliza para indicar que la contraseña no se almacena en este archivo. Las contraseñas de grupo están más allá del alcance de este curso.                                                                                                                |
| GID                  |      12      | Cada grupo está asociado con un ID de grupo único (GID) que se coloca en este campo.                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| user_list            | mail,postfix | Este último campo se utiliza para indicar quién es un miembro del grupo. Mientras que la pertenencia a un grupo primario se define en el archivo /etc/passwd, los usuarios que se asignan a los grupos adicionales tendrían su nombre de usuario en este campo del archivo /etc/group. En este caso, los usuarios mail y postfix son miembros secundarios del grupo mail. Es muy común para un nombre de usuario aparecer también como un nombre del grupo. También es común que un usuario pertenezca a un grupo con el mismo nombre. |

### Comando `getent`

Otra técnica para recuperar la información del usuario que se encuentra normalmente en los archivos `/etc/passwd` y `/etc/shadow`, `/etc/group` es utilizar el comando `getent`

```bash
getent [passwd | shadow | group] [user]
```

Ejemplo:

```bash
getent passwd sysadmin
```

```bash
getent shadow root
```

```bash
getent group mail
```

 *El signo `!` que aparece en el campo de la contraseña (segundo campo) del archivo shadow, muestra que la contraseña para student no fue configurada.*

### Cambiando de grupo los archivos - Comando `chgrp`

Para cambiar al grupo propietario de un archivo existente se puede utilizar el comando `chgrp group_name file`

Si quieres cambiar el grupo propietario de un archivo existente, puedes utilizar el comando chgrp. Como un usuario sin privilegios administrativos, el comando chgrp puede utilizarse solamente para cambiar el grupo propietario del archivo a un grupo del que el usuario ya sea miembro. Como usuario `root`, el comando chgrp puede utilizarse para cambiar el grupo propietario de cualquier archivo a cualquier grupo.

- `-R` La opcion de recursividad para cambiar todos los archivos de grupo

Cambio al grupo `games` el archivo sample

```bash
chgrp games sample
```

### Comando `stat`

 El comando stat muestra información más detallada acerca de un archivo.

```bash
stat Documents/                                           
File: `Documents'
Size: 4096            Blocks: 8          IO Block: 4096   directory
Device: c7h/199d        Inode: 73669082    Links: 2                
Access: (0755/drwxr-xr-x)  Uid: ( 1001/sysadmin)   Gid: ( 1001/sysadmin)
Access: 2020-01-10 21:37:13.450191690 +0000
Modify: 2016-03-14 17:34:24.000000000 +0000
Change: 2020-01-10 21:37:13.414190649 +0000
Birth: -
```

### Comando `id`

El comando `id` informará la identidad actual, tanto por nombre del usuario como por el identificador de usuario

- `id` : return user identity

- `id` muestra la identificacion del usuario actual
- `id [user]` da los datos del *user*; `id root`
- `id -g` da el grupo primario de usuario actual
- `id -G` da todos los grupos del usuario actual
- `cat /etc/group | grep sysadmin` filta para mostrar los grupos del usario que se le paso

### Comando `su` `sudo` `visudo`

- su: `change user ID or become superuser`
- sudo: `execute a command as another user`
- visudo: `edit the sudoers file`

- `su -` o `su -l [user]` o `su - root` inicias sesion con el usario en forma root
- `sudo` permite a un usuario ejecutar comandos que necesite privilegios `root`
- `visudo` entra a modificar y configurar los usuarios que pueden ejecutar acciones `sudo`

### Archivo `visudo`

Al activar este comando se abre un editor y se modica el archivo `/etc/sudoers`, lo cual define quien puede ejecutar comandos `sudo`

``` bash
sudo visudo

# User privilege specification
root    ALL=(ALL:ALL) ALL
usuario ALL=(ALL:ALL) ALL
```

## Comando `who` `w` `last`

### Comnado `who`

Muestra una lista de usuarios que están conectados actualmente en el sistema, desde dónde están conectados y cuándo iniciaron sesión.

Opciones;

- `-b` mostrará la última vez que el sistema se inició (fue arrancado)
- `-r` mostrará el tiempo en el cual el sistema haya alcanzado un cierto nivel ejecución

Ejemplo: 

```bash
who -b -r
system boot  	2013-10-11 09:54
run-level 5    2013-10-11 09:54
```

```bash
who
root     	tty2        2013-10-11 10:00
sysadmin	tty1        2013-10-11 09:58 (:0)
sysadmin 	pts/0       2013-10-11 09:59 (:0.0)
sysadmin 	pts/1       2013-10-11 10:00 (example.com)
```

| Columna  |            Ejemplo             | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | :----------------------------: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| username |              root              | Esta columna indica el nombre del usuario que inició la sesión. Ten en cuenta que por "sesión" nos referimos a «cualquier proceso de inicio de sesión y cualquier ventana de la terminal abierta».                                                                                                                                                                                                                                                                                                                                                                                                                            |
| terminal |              tty2              | Esta columna indica en qué ventana de terminal está trabajando el usuario. Si el nombre de la terminal inicia con tty , entonces esto es una indicación de un inicio de sesión local, está es una terminal de línea de comandos regular. Si el nombre de la terminal inicia con pts, entonces esto indica que el usuario está usando una pseudo terminal o corriendo un proceso que actúa como la terminal. Esto puede significar que el usuario tiene una aplicación de terminal corriendo en X Windows, como gnome-terminal o xterm o pueden haber usado un protocolo de red para conectarse al sistema, como ssh o telnet. |
| date     | 2013-10-11 10:00 (example.com) | Esto indica cuándo inició sesión el usuario. Después de la fecha y la hora en que el usuario inició sesión en el sistema, puede aparecer alguna información de localización. Si la información de localización contiene un nombre de host, nombre de dominio o dirección IP, entonces el usuario inició sesión remotamente. Si hay dos puntos y un número, entonces esto indica que han hecho un inicio de sesión gráfico local. Si no se muestra información de localización en la última columna, entonces esto significa que el usuario inició sesión mediante un proceso de línea de comandos local.                      |

### Comandos `w` `whoami`

Proporciona una lista más detallada sobre los usuarios que actualmente están en el sistema que el comando `who`. También proporciona un resumen del estado del sistema.

- `w` sesiones en la maquina
- `whoami` : display effective user id

```bash
w                                                       
23:45:49 up 84 days,  7:34,  2 users,  load average: 0.07, 0.13, 0.12          
USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU WHAT            
sysadmin pts/0                     23:11    5.00s  0.14s  0.01s ssh localhost   
sysadmin pts/1    localhost        23:39    5.00s  0.00s  0.00s w 
```

| Column | Ejemplo     | Descipción                                                                                                             |
| ------ | ----------- | ---------------------------------------------------------------------------------------------------------------------- |
| USER   | root        | Esta columna indica el nombre del usuario que inició la sesión.                                                        |
| TTY    | tty2        | Esta columna indica en qué ventana de terminal el usuario está trabajando.                                             |
| FROM   | example.com | Desde dónde inició sesión el usuario.                                                                                  |
| LOGIN@ | 10:00       | Cuándo inició sesión el usuario.                                                                                       |
| IDLE   | 43:44       | Cuánto tiempo el usuario ha estado inactivo desde la ejecución del último comando.                                     |
| JCPU   | 0.01s       | El tiempo total de cpu (s=segundos) utilizado por todos los procesos (programas) ejecutados desde el inicio de sesión. |
| PCPU   | 0.01s       | El tiempo total de cpu para el proceso actual.                                                                         |
| WHAT   | -bash       | El proceso actual que está ejecutando el usuario.                                                                      |
### Comando `last` `lastb`

- `show listing of last logged in users`

- `last` muestra cuando ingreso un usuario con exito
- `lastb` muestra cuantas veces fallaron al ingresar

Muestra el historial de logues en el sistema.
*El comando last lee la historia completa de la sesión desde el archivo* `/var/log/wtmp`

## Creacion de usuarios y grupos

### Grupos

Ver los grupos a los que pertener un usuario

```bash
grep root /etc/group # despliega todos los grupos a los que pertence el usuario
root:x:0:
```

o

```bash
getent group root #solo muestra el grupo principal
root:x:0:
```

#### Comando `groupadd`

El comando `groupadd` puede ser ejecutado por el usuario `root` para crear un nuevo grupo

Opciones:

- `-g` indica el id del grupo: si no se indica, el pone automaticamente uno GID
- `-r` se forza a un GID para la zona de procesos internos; es decir, a grupos reservados para el sistema

``` bash
groupadd -g [group_id] [name_group]
```

``` bash
groupadd -g 506 research
```

**Modificar un grupo `groupmod`**

Opciones:

 - `-n` Se puede utilizar para cambiar el nombre del grupo
 - `-g` cambiar el GID para el grupo.

Si se modica el GID se pierde el acceso al aunque tenga el mismo nombre, porque todo esta refenciado hacia el GID, no al nombre del grupo

Cambiar el nombre de `sales` a `marketing`

```bash
groupmod -n marketing sales
```
Encontrar archivos huerfanos; es decir, sin grupo

```bash
find / -nogroup 
```

**Eliminar grupos `groupdel`**

 Eliminar un grupo con el comando groupdel, ten en cuenta que los archivos que pertenecen a ese grupo se convertirán en `huérfanos`.
Sólo se puede eliminar a los grupos suplementarios, por lo que si un grupo es el grupo primario para cualquier usuario, no se puede eliminar. El administrador puede modificar qué grupo es el grupo primario del usuario, por lo que un grupo que estaba siendo utilizado como un grupo primario se puede transformar en un grupo suplementario y luego se puede eliminar.

```bash
groupdel [name_group]
```

```bash
groupdel clerks
```

### Comando `newgrp`

- `log in to a new group`

Es para cambiar al grupo primario del usario actual; una vez hecho el cambio verificar si cambio el grupo primario con el comando `id`. Ahora al crear documentos y arhivos, el grupo primario sera el nuevo asignado. El cambio del grupo es temporal hasta cerrar la sesión.

```bash
newgrp [name_group]
```

```bash
newgrp research
```

*Se requieren privilegios administrativos para cambiar permanentemente el grupo primario del usuario. El usuario root ejecutaría el comando `usermod -g groupname username`.*

### Comando `chgrp` `stat`

Si quieres cambiar el grupo propietario de un archivo existente, puedes utilizar el comando `chgrp`



### Agregar usuarios - Comando `useradd`

Opciones

- `-u` UID user id, debe ser unico es arriba de 1000 y abajo para servicios del sistema (depende la distro y revisar el archivo `passwd`)
- `-m` crea la carpeta de home
- `-g` nombre del grupo, normalmente el mismo nombre que el usuario,
- `-d` define el path del home del usuario
- `-G` grupos adicionales, separados por comas sin espacios; `grupo1,grupo2`; deben existir primero los grupos
- `-c` Comentario, normalmente el nombre completo de la persona o servicio
- Al final el nombre del usuario

Creando un usuario con `useradd`

```bash
 useradd -m xizuth #crea el usuario con todo por defecto y crea el directorio del home
```

Crea el usuario especificando varios detalles

```bash
 useradd -u 1000 -g users -G wheel,research -c 'Jane Doe' jane 
```

Se observan los paramentros establecidos para cuando se agregaran usuarios

```bash
useradd -D 
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
```

| Campo             |  Ejamplo  | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ----------------- | :-------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| GROUP             |    100    | En las distribuciones que no usan UPG, este será el grupo principal de forma predeterminada para un usuario nuevo, si no se ha especificado uno con el comando `useradd`. Este normalmente es el grupo de «users» con un GID de 100. Esta configuración afecta a la configuración por defecto del archivo `/etc/passwd`  bob:<span>x</span>:600:<mark>600</mark>:bob:/home/bob:/bin/bash <br> La opción `-g` para el comando `useradd` permite utilizar un grupo principal diferente al predeterminado, cuando se crea una nueva cuenta de usuario.                                                                                                                                              |
| HOME              |   /home   | El directorio /home es el directorio base predeterminado, en el cuál se creará un nuevo directorio home del usuario. Esto significa que un usuario con un nombre de cuenta de bob tendría un directorio de /home/bob. Esta configuración afecta a la configuración por defecto del archivo /etc/passwd  <br> bob:<span>x</span>:600:600:bob:<mark>/home</mark>/bob:/bin/bash <br> La opción `-b` para el comando `useradd` permite utilizar un directorio base diferente al predeterminado, cuando se crea una nueva cuenta de usuario.                                                                                                                                                          |
| INACTIVE          |    -1     | Este valor representa el número de días después de que caduca la contraseña hasta que la cuenta será deshabilitada. Un valor de `-1` significa que esta función no está habilitada por defecto y no se proporciona ningún valor «inactivo» para las nuevas cuentas por defecto. Esta configuración afecta a la configuración por defecto del archivo `/etc/shadow`  <br>bob:pw:15020:5:30:7:<mark>60</mark>:15050: <br> La opción `-f` para el comando `useradd` permite utilizar un valor INACTIVE diferente al predeterminado, cuando se crea una nueva cuenta de usuario.                                                                                                                     |
| EXPIRE            |           | Por defecto, no hay ningún valor para la fecha de caducidad. Generalmente, una fecha de vencimiento se configura para una cuenta individual, no a todas las cuentas. Por ejemplo, si tuvieras un contratista que fuese contratado para trabajar hasta el final del día 01 de noviembre de 2013, podrías asegurarte de que no pueda iniciar sesión después de esa fecha, utilizando el campo de EXPIRE. Esta configuración afecta a la configuración por defecto del archivo `/etc/shadow`  <br>bob:pw:15020:5:30:7:60:<mark>15050</mark>: <br>La opción `-e` para el comando `useradd` permite utilizar un valor EXPIRE diferente al predeterminado, cuando se crea una nueva cuenta de usuario. |
| SHELL             | /bin/bash | El valor de SHELL indica el shell por defecto para los usuarios cuando inician sesión en el sistema. Esta configuración afecta a la configuración por defecto del archivo `/etc/passwd`  <br> bob:<span>x<span>:600:600:bob:/home/bob:<mark>/bin/bash</mark> <br> La opción `-s` para el comando `useradd` permite utilizar un shell de inicio de sesión diferente al predeterminado, cuando se crea una nueva cuenta de usuario.                                                                                                                                                                                                                                                                |
| SKEL              | /etc/skel | El valor SKEL determina qué directorio «esqueleto» tendrá su contenido copiado en el directorio home de los usuarios nuevos. El contenido de este directorio se copia en el directorio `home` del usuario nuevo y el nuevo usuario recibe la propiedad de los nuevos archivos. Esto proporciona a los administradores una manera fácil de «rellenar» una nueva cuenta de usuario con los archivos de configuración clave. La opción `-k` para el comando `useradd` permite utilizar un directorio SKEL diferente al predeterminado, cuando se crea una nueva cuenta de usuario.                                                                                                                  |
| CREATE_MAIL_SPOOL |    yes    | El «mail spool» es un archivo donde se coloca el correo entrante. Actualmente el valor para crear un mail spool es `yes`, lo que significa que los usuarios por defecto están configurados con la capacidad de recibir y guardar correo local. Si no piensas usar el correo local, este valor puede cambiarse a no.                                                                                                                                                                                                                                                                                                                                                                              |

Para modificar uno de los valores por defecto del `useradd`, el archivo `/etc/default/useradd` puede editarse con un editor de texto. Otra técnica (más segura) es usar el comando `useradd -D`.

Aquí esta editando la opción `INACTIVE`

```bash
useradd -D -f 30
GROUP=100
HOME=/home
INACTIVE=30
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
```

### Comando `usermod`

El comando `usermod` ofrece muchas opciones para modificar una cuenta de usuario existente. 
Tiene casi las mismas opciones que `useradd`

| Opción corta        | Opción larga                  | Descripción                                                                                   |
| ------------------- | ----------------------------- | --------------------------------------------------------------------------------------------- |
| `-c`                | `COMMENT`                     | Establecer el valor del campo GECOS o comentario a COMMENT.                                   |
| `-d`  `HOME_DIR`    | `--home` `HOME_DIR`           | Establecer un nuevo directorio home para el usuario.                                          |
| `-e`  `EXPIRE_DATE` | `--expiredate ` `EXPIRE_DATE` | Configurar la fecha de caducidad de la cuenta a EXPIRE_DATE.                                  |
| `-f`  `INACTIVE`    | `--inactive ` `INACTIVE`      | Configurar la cuenta para permitir acceso INACTIVE días después de que la contraseña caduque. |
| `-g`  `GROUP`       | `--gid ` `GROUP`              | Establecer GROUP como grupo primario.                                                         |
| `-G`  `GROUPS`      | `--groups ` `GROUPS`          | Establecer grupos adicionales a una lista especificada en GROUPS.                             |
| `-a`                | `--append`                    | Añadir grupos adicionales del usuario especificados por -G.                                   |
| `-h`                | `--help`                      | Mostrar la ayuda para usermod.                                                                |
| `-l` `NEW_LOGIN`    | `--login` `NEW_LOGIN`         | Cambiar el nombre de inicio de sesión del usuario.                                            |
| `-L`                | `--lock`                      | Bloquear la cuenta de usuario.                                                                |
| `-s` `SHELL`        | `--shell` `SHELL`             | Especificar el shell de inicio de sesión para la cuenta.                                      |
| `-u` `NEW_UID`      | `--uid` `NEW_UID`             | Especificarque el UID del usuario sea NEW_UID.                                                |
| `-U`                | `--unlock`                    | Desbloquear la cuenta de usuario.                                                             |

*Agrego un usuario a otro grupo*; estoy agregando a `jane` al grupo `develomenent`

```bash
usermod -aG development jane
```

### Comando `userdel`

Eliminar un usuario del sistema. Borrar un usuario sin borrar su directorio home significa que los archivos del directorio home del usuario son ahora huérfanos.

Opciones:

  - `-r` elimina su directorio `home`

Solo elimina el usuario sin eliminar ningun archivo

```bash
userdel jane
```

Elimina al usuario y su directorio

```bash
userdel jane -r
```

**Archivo `/etc/login.defs`**

El archivo `/etc/login.defs` también contiene valores que se aplicarán por defecto a los nuevos usuarios que vayas a crear con el comando `useradd`. A diferencia del `/etc/default/useradd`, que puede ser actualizado con el comando useradd `-D`, el archivo `/etc/login.defs` generalmente lo edita directamente el administrador para modificar sus valores.

Con esta linea se extrae lo importante, evidiendo el relleno

```bash
grep -Ev '^#|^$' /etc/login.defs
MAIL_DIR          /var/spool/mail
PASS_MAX_DAYS     99999
PASS_MIN_DAYS     0
PASS_MIN_LEN      5
PASS_WARN_AGE     7
UID_MIN           500
UID_MAX           60000
GID_MIN           500
GID_MAX           60000
CREATE_HOME       yes
UMASK             077
USERGROUPS_ENAB   yes
ENCRYPT_METHOD    SHA512
MD5_CRYPT_ENAB    no
```

| Campo           | Ejemplo         | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| MAIL_DIR        | /var/mail/spool | El directorio en el que se crea el archivo mail spool del usuario.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| PASS_MAX_DAYS   | 99999           | Esta configuración determina el número máximo de días en los que un usuario podrá utilizar la misma contraseña. Puesto que por defecto viene configurado el valor de 99999 días o más de 200 años, significa que los usuarios nunca tienen que cambiar su contraseña. Las organizaciones con políticas eficaces para el mantenimiento de contraseñas seguras comúnmente cambian este valor a 60 o 30 días. Esta configuración afecta a la configuración por defecto del archivo `/etc/shadow`  bob:pw:15020:5:<mark>30</mark>:7:60:15050:                    |
| PASS_MIN_DAYS   | 0               | Con esto configurado a un valor predeterminado de 0 (cero), el tiempo más corto que un usuario tiene que mantener una contraseña es de cero días, lo que significa que inmediatamente después de configurar la contraseña, se puede cambiar. Si el valor `PASS_MIN_DAYS` se estableció en 3 días, después de establecer una nueva contraseña, el usuario tendría que esperar tres días antes de que pueda cambiarla otra vez. Esta configuración afecta a la configuración por defecto del archivo `/etc/shadow`  bob:pw:15020:<mark>3</mark>:30:7:60:15050: |
| PASS_MIN_LEN    | 5               | Esto indica el número mínimo de caracteres que debe contener una contraseña.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| PASS_WARN_AGE   | 7               | Este es el valor predeterminado para el campo de advertencia. Cuando un usuario se acerca al número máximo de días durante los que puede usar su contraseña, el sistema comprobará si es hora de empezar a avisar al usuario sobre cambiar su contraseña durante el inicio de sesión. Esta configuración afecta a la configuración por defecto del archivo `/etc/shadow` bob:pw:15020:3:30:<mark>7</mark>:60:15050:                                                                                                                                          |
| UID_MIN         | 500             | El `UID_MIN` determina el primer UID que se asignará a un usuario ordinario. Cualquier usuario con un UID menor que este valor, ya sea para una cuenta del sistema o bien para la cuenta de root.                                                                                                                                                                                                                                                                                                                                                            |
| UID_MAX         | 60000           | Un `UID` técnicamente podría tener un valor de más de 4 billones. Para la máxima compatibilidad se recomienda dejarlo en su valor predeterminado de 60000.                                                                                                                                                                                                                                                                                                                                                                                                   |
| GID _MIN        | 500             | El `GID_MIN` determina el primer `GID` que se asignará a un grupo ordinario. Cualquier grupo con un `GID` menor que este valor, ya sea para un grupo del sistema o bien para el grupo de root.                                                                                                                                                                                                                                                                                                                                                               |
| GID _MAX        | 60000           | Un `GID` igual que un `UID` técnicamente podría tener un valor de más de 4 billones. Cualquier valor que utilices para tu `UID_MAX` debes utilizar para `GID_MAX` para soportar UPG.                                                                                                                                                                                                                                                                                                                                                                         |
| CREATE_HOME     | yes             | Este valor determina si se crea o no un nuevo directorio para el usuario, al crear su cuenta.                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| UMASK           | 077             | Este `UMASK` funciona en el momento que se crea el directorio `home` del usuario; determinará cuáles serán los permisos predeterminados de este directorio. Utilizando el valor predeterminado de `077` para `UMASK` significa que sólo el usuario propietario tendrá algún tipo de permiso para acceder a su directorio.                                                                                                                                                                                                                                    |
| USERGROUPS_ENAB | yes             | En las distribuciones que cuentan con un grupo privado para cada usuario, como se muestra en este ejemplo CentOS, el `USERGROUPS_ENAB` tendrá un valor de `yes`. Si no se utiliza la UPG en la distribución, entonces esto tendrá un valor no.                                                                                                                                                                                                                                                                                                               |
| ENCRYPT_METHOD  | SHA512          | El método de cifrado que se utiliza para cifrar las contraseñas de los usuarios en el archivo `/etc/shadow`. El valor de `ENCRYPT_METHOD` anula la configuración de `MD5_CRYPT_ENAB`.                                                                                                                                                                                                                                                                                                                                                                        |
| MD5_CRYPT_ENAB  | no              | Este ajuste obsoleto originalmente permitía al administrador especificar el uso del cifrado de contraseñas `MD5` en lugar del cifrado original `DES`. Ahora es reemplazado por el valor de `ENCRYPT_METHOD`.                                                                                                                                                                                                                                                                                                                                                 |

### Cambiando la contraseña de un usuario

Ejecutando el comando `passwd [name_user]`, si todo sale bien, se actualiza el archivo `etc/shadow`

## Trucos

Para generar archivos y carpetas con un patron

``` bash
mkdir {2000..2020}-{1..9}
```

Creara carpertas con la nomeclatura 2000-1 hasta 2020-9, todas las combinaciones posibles

## Propiedades de archivos

Los usuarios poseen los archivos que crean. Mientras que esta propiedad puede cambiarse, esta función requiere privilegios administrativos. Aunque la mayoría de los comandos generalmente muestran al usuario propietario como un nombre, el sistema operativo en realidad asociará la propiedad del usuario con el UID para ese nombre de usuario. Cada archivo también tiene un grupo propietario.

## Extras

Especificación de la estructura de archivos

https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html

## Lista de comandos que aun no tienen seccion

- `dd` : copiar particiones, discos, etc a nivel de _bits_
  - `dd if=/dev/sda of=/dev/sdb` -- clonar un disco duro
- `which`
- `type` para conocer el tipo de un comando
  - `type ls`
- `nl` : regresa numero de lineas que contiene un archivo
