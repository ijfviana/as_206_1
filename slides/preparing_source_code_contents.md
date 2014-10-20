## Introducción

* [Obtención del código fuente](#/4/1)
* [Desempaquetar el código fuente](#/4/2)
* [Leer la documentación](#/4/5)

note:
* The first step in compiling source code is to obtain it and understand the author’s directions on using it.
* Source code can be obtained from a variety of places.
* Although there are some common practices in source code distribution, there are few rules that you can rely upon to be true in all cases.
* You must be prepared todo different things to install different source packages.



## Obtención del código fuente

<a class="fancybox" href="img/obtener_fuentes.png" data-fancybox-group="gallery" title="Introducción">
<img height="550px" src="img/obtener_fuentes.redimensionado640x480.png" alt="Introducción">
</a>

note:
* If you’re looking for software to perform some task but don’t know its name, though, you may want to check out an open source repository site, such as
 * SourceForge (https://sourceforge.net),
 * Google Code (http://code.google.com),
 * Freshmeat (http://freshmeat.net).



## Desempaquetar el código fuente

<a class="fancybox" href="img/extensiones.png" data-fancybox-group="gallery" title="Introducción">
<img height="550px" src="img/extensiones.redimensionado640x480.png" alt="Introducción">
</a>

note:
* Sometimes program Web sites provide multiple packages intended for different platforms.
* Linux source code tarballs (files created with the tar utility) usually come in files with names that end in
  * .tgz --> compressed with gzip
  * .tar.gz --> compressed with gzip
  * .tbz -->  compressed with bzip2
  * .tbz2 --> compressed with bzip2
  * .tar.bz2 --> compressed with bzip2
  * .zip --> compressed with PkZip (not tarballs)
* If you see a source RPM file, which has a name that ends in .src.rpm, and if you have an RPM-based distribution, you can download it and generate a binary RPM.
* Source RPMs are converted into binary RPMs by typing rpmbuild --rebuildaprogram-1.2.3.src.rpm, where aprogram-1.2.3.src.rpm is the source RPM’s filename.
* The binary RPM will be stored in a location that is specified about a dozen lines above the end of the resulting output.
* You should not follow the normal source code compilation and installation instructions when installing a source RPM.



## Desempaquetar el código... (II)

* Extraer un paquete comprimido con [`gzip`](http://linux.die.net/man/1/gzip)
```bash
ijfviana@vagalume:~$ tar xzf simplesamlphp-1.10.0.tar.gz
ijfviana@vagalume:~$ tar -xzf simplesamlphp-1.10.0.tar.gz
ijfviana@vagalume:~$ gunzip -c simplesamlphp-1.10.0.tgz   | tar xv
ijfviana@vagalume:~$ tar simplesamlphp-1.10.0.tar.gz
simplesamlphp-1.10.0/
simplesamlphp-1.10.0/attributemap/
simplesamlphp-1.10.0/attributemap/addurnprefix.php
simplesamlphp-1.10.0/attributemap/facebook2name.php
simplesamlphp-1.10.0/attributemap/feide-oid.php
simplesamlphp-1.10.0/attributemap/linkedin2name.php
```
* Extraer un paquete comprimido con [`bzip`](http://linux.die.net/man/1/bzip2)
```bash
ijfviana@vagalume:~$ tar xjf simplesamlphp-1.10.0.tar.bz
ijfviana@vagalume:~$ tar xjzf simplesamlphp-1.10.0.tar.bz
simplesamlphp-1.10.0/
simplesamlphp-1.10.0/attributemap/
simplesamlphp-1.10.0/attributemap/addurnprefix.php
simplesamlphp-1.10.0/attributemap/facebook2name.php
```

note:
*  To uncompress any type of tarball, you use the tar utility, passing it the -x (or --extract) operation name along with
 * either -z (--gzip)
 * or -j (--bzip2)
* if the tarball was compressed and -f (--file) to specify the filename.
* You may want to add -v (--verbose) to see a list of filenames as they’re extracted. The final command might look like this:
$ tar xvzf aprogram-1.2.3.tgz
* The leading dash (-) can be, and often is, omitted when using single-character options with the tar program.
* Some people prefer to call gunzip or bunzip2 separately, piping the result through tar:
$ gunzip -c aprogram-1.2.3.tgz | tar xv



## Desempaquetar el código... (III)
* Ver el contenido de un fichero fuente sin descomprimir (`-t`, `--list`)
```bash
ijfviana@vagalume::/usr/src$ tar tf simplesamlphp-1.10.0.tar.gz
simplesamlphp-1.10.0/
simplesamlphp-1.10.0/attributemap/
simplesamlphp-1.10.0/attributemap/addurnprefix.php
simplesamlphp-1.10.0/attributemap/facebook2name.php
simplesamlphp-1.10.0/attributemap/feide-oid.php
simplesamlphp-1.10.0/attributemap/linkedin2name.php
```

note:
* Tarballs are conventionally built such that, when they’re extracted, they create a subdirectory, usually with the same name as the tarball, and all files are placed within the new directory.
* This isn’t always true, though, and it’s often not true of .zip files.
* If you want to be sure that a tarball will extract neatly into a new subdirectory, you can use the -t (--list) operation
* You can extract a source tarball where you want but you may prefer to extract the tarball into a subdirectory of `/usr/src`.
* By default, `/usr/src` is normally writeable only by root, so you may need to acquire superuser.



## Leer la documentación

* Fichero de documentación
```bash
ijfviana@linda:/tmp/as/simplesamlphp-1.10.0$ ls
attributemap  config-templates  extra     metadata-templates  templates
bin           COPYING           INSTALL   modules             www
cert          data              lib       NEWS
CHANGELOG     dictionaries      log       README
config        docs              metadata  schemas
```
* Hay que leer los ficheros `README` e `INSTALL` para consultar las instrucciones específicas de cada software

note:
* Once you’ve extracted the source code, you should type ls in the source code directory to view the files it contains.
* In most cases, you’ll find several documentation files:
  * COPYING (the license text),
  * CHANGELOG (a history of technical changes to the software),
  * NEWS (another history of changes, this one less technical),
  * README (general documentation), and INSTALL (instructions on installing the software).
* Documentation files like these usually have entirely uppercase names, but this isn’t always true.
* You should be sure to read the general documentation (README) and installation instructions (INSTALL) before proceeding with any source code compilation or installation procedure.
* Although most programs follow a similar procedure, the actions required are not completely standardized. You may find that the software you want to install requires some unusual steps
