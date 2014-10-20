## Instalación de software

* [Instalación](#/6/1)
* [Desinstalación y actualización](#/6/3)
* [Librerías dinámicas](#/6/5)

note:
Once the program has finished compiling, you can install it.



## Instalación (I)

* Invocamos al comando `make` con el argumento install
```bash
ijfviana@linda:/tmp/as/tar-1.27$ make install
```
* Copiará los ficheros del programa en el directorio indicado
* Si el `make` no hace nada invocamos a la utilidad `install`
```bash
ijfviana@linda:/tmp/as/tar-1.27$ install src/tar
```
* El proceso de instalación suele requerir la modificación de otros ficheros (como scripts de arranque)

note:
* Typically, typing make install as root will do this: The binary program will be copied to a suitable location, such as /usr/local/bin, and the program’s man pages and support files will also be copied to reasonable locations, usually in the /usr/local directory tree.
* If the program is a normal user program, you should then be able to launch it by typing its name, just as you’d run a program installed via a package manager.
* Some programs don’t provide an install target to make—that is, if you type make install, nothing useful will happen. For such programs, you must copy the program file manually.
* The `install` program does the copy job and will automatically adjust ownership and permissions for binaries.
* Typing installprogname/usr/local/bin as root copies progname to /usr/local/bin, changing its ownership to the current effective user ID (root) and its permissions to 0755.



## Instalación (II)

<div class="table-responsive">
<table class="table table-hover table-bordered">
<thead style="background-color:#a8003b; color:white">
<tr>
<th width="530em">Opción </th>
<th>Efecto</th>
</tr>
</thead>
<tbody style="background-color:white;">
<tr>
<td>`-b --backup`</td>
<td>Crea copia de seguridad</td>
</tr>
<tr>
<td>`-gGROUP --group=GROUP`</td>
<td>Cambia el grupo propietario</td>
</tr>
<tr>
<td>`-mMODE --mode=MODE`</td>
<td>Cambia los permisos</td>
</tr>
<tr>
<td>`-oOWNER --owner=OWNER`</td>
<td>Cambia el usuario propietario</td>
</tr>
<tr>
<td>`-s --strip`</td>
<td>Reduce la tabla de símbolos</td>
</tr>
</tbody>
</table>
</div>

note:
several common install options.

Option Effect
-b or --backup Creates a backup of every destination file.
-gGROUP or --group=GROUP Changes the group of the installed files to GROUP rather than to the current group ID.
-mMODE or --mode=MODE Changes the installed files’ mode to MODE.
-oOWNER or --owner=OWNER Changes the owner of the installed files to OWNER rather than to the current user ID.
-s or --strip Strips symbol tables; reduces a binary’s size, but makes debugging harder.
-T or --no-target-directory Treats the destination location as a file rather than as a directory.
-v or --verbose Displays the names of all files and directories as they’re being copied.



## Instalación (III)

<div class="table-responsive">
<table class="table table-hover table-bordered">
<thead style="background-color:#a8003b; color:white">
<tr>
<th width="530em">Opción </th>
<th>Efecto</th>
</tr>
</thead>
<tbody style="background-color:white;">
<tr>
<td>`-T --no-target-directory`</td>
<td>Trata el destino como un fichero</td>
</tr>
<tr>
<td>`-v --verbose`</td>
<td>Mensajes detallados</td>
</tr>
</tbody>
</table>
</div>

note:
several common install options.

Option Effect
-b or --backup Creates a backup of every destination file.
-gGROUP or --group=GROUP Changes the group of the installed files to GROUP rather than to the current group ID.
-mMODE or --mode=MODE Changes the installed files’ mode to MODE.
-oOWNER or --owner=OWNER Changes the owner of the installed files to OWNER rather than to the current user ID.
-s or --strip Strips symbol tables; reduces a binary’s size, but makes debugging harder.
-T or --no-target-directory Treats the destination location as a file rather than as a directory.
-v or --verbose Displays the names of all files and directories as they’re being copied.



## Desinstalación y actualización (I)
### Desinstalación

* Invocamos al comando `make` con el argumento `uninstall`
```bash
ijfviana@linda:/tmp/as/tar-1.27$ make uninstall
```
* Si no hace nada hay que borrar los ficheros manualmente
* *No se puede usar el `make` de otra versión*.

note:
* Typing make uninstall will remove the software, much like using the uninstall feature of RPM or the Debian package manager.
* If you use the Makefile from a different version of the program than you have installed, you might not remove the right files.
* If the software doesn’t support a make uninstall operation, you’ll have to delete the files manually.



## Desinstalación y actualización (II)
### Actualización

* Hacer una copia de la versión actual
* Desinstalar la versión actual
* Obtener el código de la nueva versión
* Compilar e instalar la nueva versión

note:
* Uninstall the old software, and then install the new version.
* This procedure ensures that you’ll remove all the old files and install the relevant new files.
* Be sure to back up any configuration files and verify that your configuration is correct after you install the new version, though.



## Librerías dinámicas (I)

<a class="fancybox" href="img/librerias_dinamicas.png" data-fancybox-group="gallery" title="Librerías dinámicas">
<img height="550px" src="img/librerias_dinamicas.redimensionado640x480.png" alt="Librerías dinámicas">
</a>

note:
* La invocación al comando make install implica no solo la instalación de ejecutable sino de librerías dinámicas
* Cuando se ejecuta la aplicación las librerías se van cargando en memoria (si no estaba) conforme se necesite



## Librerías dinámicas (II)

* Podemos usar el comando `ldd` para saber las librerías que cargará un ejecutable

```bash
ijfviana@vagalume:~/$ ldd /usr/bin/vi
	linux-vdso.so.1 =>  (0x00007ffff15fe000)
	libtinfo.so.5 => /lib/x86_64-linux-gnu/libtinfo.so.5 (0x00007fae06e40000)
	libselinux.so.1 => /lib/x86_64-linux-gnu/libselinux.so.1 (0x00007fae06c21000)
	libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007fae06860000)
	libdl.so.2 => /lib/x86_64-linux-gnu/libdl.so.2 (0x00007fae0665c000)
	/lib64/ld-linux-x86-64.so.2 (0x00007fae0708b000)
```

note:
* ldd  prints  the  shared  libraries  required by each program or shared library specified on the command line.



## Librerías dinámicas (III)

<a class="fancybox" href="img/ld-so.png" data-fancybox-group="gallery" title="Librerías dinámicas">
<img height="550px" src="img/ld-so.redimensionado640x480.png" alt="Librerías dinámicas">
</a>

note:
*  ld.so loads the shared libraries needed by a program, prepares the program to run, and then runs it.



## Librerías dinámicas (IV)

<a class="fancybox" href="img/ld-so-2.png" data-fancybox-group="gallery" title="Librerías dinámicas">
<img src="img/ld-so-2.redimensionado640x480.png" alt="Librerías dinámicas">
</a>

note:
*  The necessary shared libraries needed by the program are  searched  for in the following order
  1 Using the environment variable LD_LIBRARY_PATH
  2 From  the  cache file /etc/ld.so.cache which contains a compiled list of candidate libraries previously found  in  the  augmented library  path.
  3 In the default path /lib, and then /usr/lib.



## Librerías dinámicas (V)

<a class="fancybox" href="img/ldconfig.png" data-fancybox-group="gallery" title="Librerías dinámicas">
<img src="img/ldconfig.redimensionado640x480.png" alt="Librerías dinámicas">
</a>

note:
* ldconfig  creates,  updates,  and removes the necessary links and cache (for use by the run-time linker,  ld.so)  to  the  most  recent  shared libraries  found  in
 * the directories specified on the command line,
 * in the file /etc/ld.so.conf,
 * and in the trusted directories (/usr/lib  and
       /lib).



## Librerías dinámicas (VI)

``` bash
ijfviana@vagalume:/etc$ cat  ld.so.conf
include /etc/ld.so.conf.d/*.conf
```

``` bash
ijfviana@vagalume:/etc/ld.so.conf.d$ ls
i386-linux-gnu_GL.conf	libc.conf	       x86_64-linux-gnu_GL.conf
i686-linux-gnu.conf	x86_64-linux-gnu.conf  zz_i386-biarch-compat.conf
```

``` bash
ijfviana@vagalume:/etc/ld.so.conf.d$ cat x86_64-linux-gnu_GL.conf
/usr/lib/x86_64-linux-gnu/mesa
/usr/lib/pxpress/lib
/usr/lib/i386-linux-gnu/mesa
/usr/lib32/pxpress/lib
```
