# Introducción a la infraestructura virtual: concepto y soporte físico

## Ejercicio 1
**Consultar en el catálogo de alguna tienda de informática el precio de un ordenador tipo servidor y calcular su coste de amortización a cuatro y siete años. Consultar [este artículo en Infoautónomos sobre el tema.](https://infoautonomos.eleconomista.es/consultas-a-la-comunidad/988/)**

El servidor utilizado de ejemplo es [este](https://www.pccomponentes.com/servidor-hp-proliant-ml110-gen10-intel-xeon-3106-16gb).

## Ejercicio 2
**Usando las tablas de precios de servicios de alojamiento en Internet "clásicos", es decir, que ofrezcan _Virtual Private Servers_ o servidores físicos, y de proveedores de servicios en la nube, comparar el coste durante un año de un ordenador con un procesador estándar (escogerlo de forma que sea el mismo tipo de procesador en los dos vendedores) y con el resto de las características similares (tamaño de disco duro equivalente a transferencia de disco duro) en el caso de que la infraestructura comprada se usa solo el 1% o el 10% del tiempo.**

## Ejercicio 3
**En general, cualquier ordenador con menos de 5 ó 6 años tendrá estos flags. ¿Qué modelo de procesador es? ¿Qué aparece como salida de esa orden? Si usas una máquina virtual, ¿qué resultado da? ¿Y en una Raspberry Pi o, si tienes acceso, [el procesador del móvil](https://stackoverflow.com/questions/26239956/how-to-get-specific-information-of-an-android-device-from-proc-cpuinfo-file)?**

Mi ordenador personal tiene un procesador de la familia Intel, concretamente un Intel Core i7.

Al usar la orden

```bash
egrep '^flags.*(vmx|svm)' /proc/cpuinfo
```

la salida es la que se muestra en la siguiente captura:

![egrep '^flags.\*(vmx|svm)' /proc/cpuinfo](img/egrep-vmx.png)

Esta misma línea se repite un total de 8 veces debido al número de CPUs. Como se puede comprobar, el flag de virtualización en el core que se muestra (y en los 7 restantes también) está activo, puesto que de lo contrario el comando no daría lugar a salida alguna. Además, se puede ver que la última "palabra" en rojo corresponde justamente con **vmx**.

Por otro lado, en una máquina virtual (en este caso una que ya tenía instalada y que usa una distribución de Kali-Linux), la salida del mismo comando no se muestra, es decir, en la máquina virtual no está activo el flag como se puede observar en la imagen.

![egrep en Kali-Linux](img/egrep-vm.png)

Puesto que no dispongo de una RasPi, he utilizado mi teléfono móvil, un Samsung con 4 cores con un modelo de procesador Samsung Exynos 8890. En este caso, al ejecutar el comando

```bash
cat /proc/cpuinfo
```

no se observa una bandera de virtualización como las mencionadas en el temario.

![/proc/cpuinfo](img/cpuinfo.jpg)

Ninguna de las banderas activas representan la virtualización, sino otras propiedades relacionadas con operaciones de punto flotante, de enteros...

## Ejercicio 4
1. **Comprobar si el núcleo instalado en tu ordenador contiene este módulo del kernel usando la orden kvm-ok. Alternativamente (o además), usar lscpu como se indica arriba.**
2. **Instalar un hipervisor para gestionar máquinas virtuales, que más adelante se podrá usar en pruebas y ejercicios.**

Utilizando _kvm-ok_ podemos comprobar si el kernel de mi dispositivo puede utilizar la aceleración por hardware. Efectivamente, se puede, como queda reflejado en la siguiente captura:

![kvm-ok](img/kvm-ok.png)

De la misma forma podemos comprobarlo con el comando

```bash
LC_ALL=C lscpu | grep Virtualization
```

que nos confirma la información que ya habíamos extraído al utilizar _kvm-ok_: el kvm está activo.

![LC_ALL=C lscpu | grep Virtualization](img/lscpu.png)

El hipervisor instalado no es software libre, pertenece a la Oracle: VirtualBox; es un hipervisor que hemos estado utilizando desde primero de carrera y que por eso es el que he elegido, ya que lo conozco bien y conozco algunos de los problemas que puede dar y cómo arreglarlos.

![Oracle VirtualBox](img/virtualbox.png)

## Ejercicio 5
**Darse de alta en servicios de nube usando ofertas gratuitas o cupones que pueda proporcionar el profesor.**

## Ejercicio 6
**Darse de alta en una web que permita hacer pruebas con alguno de los sistemas de gestión de nube anteriores.**