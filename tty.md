# Comandos necesarios para el tratamiento de la TTY

## Contentxo
Durante una fase de ataque, al lograr conseguir una reverse shell dado una IP víctima durante un pentesting, llega un momento en donde tenemos que conectarnos
hacia la máquina víctima para poder hurgar en los archivos internos o incluso lograr escalar sus privilegios. Es en ese momento cuando tenemos que hacer un
tratamiento a la tty

## ¿Que es un TTY?
tty es un comando de Unix (también en similares como GNU/Linux) que muestra (escribe a la salida estándar) el nombre de fichero de la terminal de la entrada estándar.
Recordemos que esto se ejecuta mediante una BASH (bourn again shell).

## ¿Por qué es Necesario Hacer un Tratamiento a la TTY?
Al momento de conectarnos hacia una máquina victima (de forma remota) existen ciertas complicaciones y restriciones a la hora de operar comandos de una bash.
Por ejemplo, si precionamos un [CTRL + C], esto le diche a la bash que corte toda la comunicación ya establecída, lo cual nos hace perder todo el trabajo que llevamos.
Entonces, hacer un tratamiento a la TTY nos ayudrará a evitar esos problemas y por ende, mejorar el rendimiento de nuestra bash.

## ¿Como se Logra?
Para hacer un correcto tratamiento de una TTY primero es necesarios ya estar conectados (ya haber logrado una reverse shell). Generalmente este paso se logra mediante
un lanzamiento de un servidor *netcat* especificando un puerto de escucha en nuestra bash.

El paso siguiente es seguir estas lineas de comandos y estaría listo.

### 1) Comprobar que tenemos la conexion establecida. Al lanzar el comando *whoami* debería devolvernos el nombre de la máquina.
```bash
whoami
```
### 2) Lanzar una bash interactíva (una pseudo consola)

```bash
script /dev/null -c bash
```

### 3) Enviar el proceso que se está ejecutando a segundo plano

```bash
[CTRL + Z]
```

### 4) Retomar el proceso anteriormente dejado en segundo plano (3)

```bash
stty raw -echo; fg
```

### 5) Reiniciar la configuración actual de la terminal (luego de este paso ya deberíamos poder operar la terminal externa de forma más cómoda.)

```bash
reset xterm
```

### 6) Exportamos una terminal Xterm

```bash
export TERM=xterm
```

### 7) Exportamos una bash

```bash
export SHELL=bash
```

### 8) Cambiar la resolución de nuestra bash interactiva. Nota: Para revisar el numero de rows y columns actuales ejecutar -> stty size.
```bash
stty rows 51 columns 189
```



