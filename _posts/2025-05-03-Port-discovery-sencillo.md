---
title: Port Discovery pwntools 
published: true
---
En este artículo nos adentraremos en crear nuestro propio portDiscovery en Python usando **PwnTools**, pero antes de empezar debemos de saber que es PwnTools.
`PwnTools` es una librería de Python diseñada para el desarrollo de exploits y tareas de hacking ético, orientada a la automatización de ataques binarios, manipulación de procesos, comunicación con sockets, análisis de memoria, y tareas relacionadas con binary exploitation y reverse engineering.
Una vez entendido esto, pasaremos a el portDiscovery.

#### Paso 1: Instalar la librería.
Bueno, esto es tan sencillo como ejecutar el siguiente comando que instala PwnTools.
```bash
pip3 install pwntools
```
Una vez hecho eso, podrás verificar la instalación con el siguiente script:
```python
#!/usr/bin/python3.13
from pwn import *
print(cyclic(32))
```
Lo cual debería de imprimir una cadena de 32 caracteres.


#### Paso 2: Crear el archivo donde se alojará el script.
Esto es tan sencillo como usar el comando `touch` y el nombre que le quisieras poner al archivo. He aquí un ejemplo:
```bash
touch portDiscovery.py
```

#### Paso 3: Editar el archivo y agregar la librería pwn.
Para esto tendremos que usar un editor de texto o un IDE para editar el archivo portDiscovery.py, en mi caso uso neovim por lo cual para editar el archivo tendré que usar el siguiente comando:
```bash
nvim portDiscovery.py
```

Ya que estemos editando el archivo, llamaremos a la librería pwntools de la siguiente manera:
```python
#!/usr/bin/python3.13
from pwn import *
```
Esto lo hicimos anteriormente para verificar que se instaló correctamente pero ahora no imprimiremos nada.

#### Paso 4: Definir la variable objetivo.
Para esto tendremos que definir la variable con el nombre que tu desees, en mi caso usaré IP para el nombre de la variable.
```python
#!/usr/bin/python3.13
from pwn import *

ip = input("Target IP:")
```
Esto nos servirá para tener la IP objetivo para el escaneo de puertos.

#### Paso 5: Definir el rango de puertos a explorar y el resultado si el puerto está abierto.
Esto también es muy sencillo de hacer, usaremos `for <variable> in range` para poner el rango de puertos a explorar. en mi caso usaré "ports" para la variable.
```python
#!/usr/bin/python3.13
from pwn import *

ip = input("Target IP:")

for port in range(65535):
```
Una vez hecho esto, podemos definir que hacer si un puerto se encuentra abierto con lo siguiente.
```python
#!/usr/bin/python3.13
from pwn import *

ip = input("Target IP:")

for port in range(65535):
    try:
        remote(ip, port)
        print(f"The port {port} is open")
```

#### Paso 6: Definir que hacer en caso que el puerto esté cerrado.
Para esto necesitamos usar `except:` para definir que hacer en caso de que el puerto esté cerrado, de esta manera:
```python
#!/usr/bin/python3.13
from pwn import *

ip = input("Target IP:")

for port in range(65535):
    try:
        remote(ip, port)
        print(f"The port {port} is open")
    except:
         print(f"Failed connection at port {port}")
```

Y enhorabuena, has hecho tu propio portDiscovery en python usando pwntools. ¡Felicidades!

