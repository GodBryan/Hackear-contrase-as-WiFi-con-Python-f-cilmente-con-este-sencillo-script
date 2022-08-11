# Hackear-contrase-as-WiFi-con-Python-f-cilmente-con-este-sencillo-script

![Sin-título-3](https://user-images.githubusercontent.com/90482037/184072826-12ab5465-ca9f-4e2d-b316-fdd2833638ce.png)

Este script busca en Windows contraseñas wifi con python ya conocidas y las muestra junto al nombre de la red.  Esto es útil para las ocasiones en que olvida su contraseña de WiFi.
Anteriormente hablas de algunos comandos de windows "netsh wlan", he incluso desarrollamos un script con bat, y con powershell hoy veremos como hacer un script simple y sencillo con python .

'Bienvenido al buscador de claves wifi básicamente sirve para tener un respaldo de las claves wifi de tu maquina, por si quieres formatear, o algo parecido XD ya que las claves te las muestra cifradas. también puedes usar ingenieria social para obtener las claves de las pc de tus compañeros , amigos etc.'.  Si te da algun error, ejecuta como administrador ,

Obtenga contraseñas
Si escribe netsh wlan show profiles cmd, se le mostrarán los perfiles para las conexiones wifi que su computadora ha almacenado.

Si a continuación, escribir netsh wlan show profile {Profile Name} key=clear, la salida proporcionada contendrá la clave de red que es la contraseña de WiFi.
 ╔═══════ ≪ °❈° ≫ ═══════╗ 
 ![Screenshot_1](https://user-images.githubusercontent.com/90482037/184072887-eb6d7686-eecb-4c62-84e8-143e28c82571.png)
  ╚═══════ ≪ °❈° ≫ ═══════╝
Requisitos
Windows 7/10
Instalar python 2.7
Instalar py2exe-0.6.9.win32-py2.7.exe
EDI Editor de texto (notepad++)
Código Completo 
✄ ------------------------------------------------ 
#!/usr/bin/python
# -*- coding: utf-8 -*-
#Primero subproceso de importación, este es el módulo que utilizaremos
# para interactuar con el cmd.
import subprocess
#El módulo del sistema operativo en Python proporciona funciones para 
#interactuar con el sistema operativo.
import os
import errno
import glob
import shutil
#----------------Baner---------------------------
print (".     __      __  _   ___   _             ")
print (".     \ \    / / | | | __| | |        ")
print (".      \ \/\/ /  |_| | _|  |_|        ")
print (".       \_/\_/   (_) |_|   (_)            ")
print (".    Autor: Luishino Pericena Choque        ")
print (".    https://lpericena.blogspot.com/      ")
#Creamos una carpeta/folder donde se guardara las claves de wifi
try:
os.mkdir('./wifi')
except OSError as error:
if error.errno != errno.EEXIST:
raise
#Muestra todas las redes wifi que la pc fue conectada
show = subprocess.check_output(['netsh', 'wlan', 'show', 'profile'])
print show
networks = subprocess.check_output(['netsh', 'wlan', 'show', 'networks'])
print networks
#exporta las claves de wifi en archivos .xml
a = subprocess.check_output(['netsh', 'wlan', 'export', 'profile','key=clear']).
decode('utf-8').split('\n')
#Mover archivos .xml a la carpeta wifi
source_dir = './' #Inicio de la carpeta 
dst = './wifi' #Nueva carpeta destinatario 
files = glob.iglob(os.path.join(source_dir, "*.xml"))
#englobar los archivos a mover
for file in files:
if os.path.isfile(file):
shutil.move(file, dst) #Mover todos los archivos a una nueva carpeta

✄ ------------------------------------------------ 

A continuación, obtenga el resultado para el comando "netsh wlan show profiles" usando subprocess.check_output (). Luego decodifique la salida con utf-8 y divida la cadena por un carácter de nueva línea para obtener cada línea en una cadena separada.
 ╔═══════ ≪ °❈° ≫ ═══════╗ 
 ![Screenshot_7](https://user-images.githubusercontent.com/90482037/184072953-426d46be-9d26-4d17-98db-56a1c047bd19.png)
╚═══════ ≪ °❈° ≫ ═══════╝
Ahora que la variable a contiene los nombres de perfil WiFi, podemos obtener el resultado para el comando "netsh wlan show profile {Profile Name} key = clear" usando subprocess.check_output () nuevamente para un perfil particular mientras recorremos todos los perfiles.
Observamos que se nos importara las claves de wifi en archivos .xml 

 ╔═══════ ≪ °❈° ≫ ═══════╗ 
 ![Screenshot_2](https://user-images.githubusercontent.com/90482037/184073001-d8993522-c179-4dfe-8cb7-4e5bf914da60.png)
 ╚═══════ ≪ °❈° ≫ ═══════╝
Compilar el archivo py
Desargamos el programa py2exe-0.6.9.win32-py2.7.exe y instalamos en windows 7/10

https://sourceforge.net/projects/py2exe/files/py2exe/0.6.9/
https://es.osdn.net/projects/sfnet_py2exe/downloads/py2exe/0.6.9/py2exe-0.6.9.win32-py2.7.exe/

Copiamos el código setup.py https://github.com/Pericena/Scriptpy/blob/master/setup.py
Vamos cambiando de acorde a nuestro script.
✄ ------------------------------------------------ 
# -*- coding: utf-8 -*-
#powershell python setup.py py2exe
import sys
from distutils.core import setup
kwargs = {}
if 'py2exe' in sys.argv:
import py2exe
kwargs = {
'console' : [{
'script'         : 'WiFi.py',
'description'    : 'Descripcion del programa.',
'icon_resources' : [(90, 'icon.ico')]
}],
'zipfile' : None,
'options' : { 'py2exe' : {
'dll_excludes'   : ['w9xpopen.exe'],
'bundle_files'   : 1,
'compressed'     : True,
'optimize'       : 2
}},
}
setup(
name='WiFi',
author='Luishiño',
author_email='lpericena@gmail.com',
**kwargs)
✄ ------------------------------------------------ 
 ╔═══════ ≪ °❈° ≫ ═══════╗ 
![Screenshot_3](https://user-images.githubusercontent.com/90482037/184073083-5e1d2bef-b22b-42c5-97dd-8cbc6cfbdba4.png)
╚═══════ ≪ °❈° ≫ ═══════╝
Listo para ser ejecutado desde cualquier ordenador con sistema operativo windows 7/10 
  ╔═══════ ≪ °❈° ≫ ═══════╗ 
  ![Screenshot_4](https://user-images.githubusercontent.com/90482037/184073114-16e944c0-3753-4750-82d3-497f5dce0c64.png)
╚═══════ ≪ °❈° ≫ ═══════╝
Archivo xml
Una vez ejecutado nuestro programa ,las claves de wifi se  guardan en un archivo xml como podemos observar en la imagen 
  ╔═══════ ≪ °❈° ≫ ═══════╗
  ![Screenshot_6](https://user-images.githubusercontent.com/90482037/184073157-15fff028-c8ab-4123-a397-cfa3a0e4ca36.png)
╚═══════ ≪ °❈° ≫ ═══════╝

Descargar
https://github.com/Pericena/Scriptpy/blob/master/WiFi.py

Windows
git clone https://github.com/Pericena/Scriptpy/blob/master/WiFi.py
python WiFi.py
Linux
git clone https://github.com/Pericena/Scriptpy/blob/master/WiFi.py
python2 WiFi.py
Cursos de mega gratis
_____________________________________________________
Aprende Programación en C desde cero
https://mega.nz/#F!DKoQVSBB!OO4BAwVSKdZolONv6rD3ow
_____________________________________________________
1,024 GB De Cursos Completos
https://mega.nz/#F!jgkzASwB
Clave
u7ByJExNs5fK58FIABKLLw
https://mega.nz/#F!jgkzASwB!u7ByJExNs5fK58FIABKLLw


