# Analisi de código con dos entornos python

Este manual nos ayudará a construir un espacio para poder revisar código python con pylint, concretamente utilizamos una librería especial llamada
pylint_runner que nos permite hacer un análisis recursivo de todos los ficheros dentro de un paquete.

*Al trabajar con dos entornos y en especial el de Python 2.7 es la única que he encontrado con esta característica recursiva.*

## Requisitos previos

[Instalar pyenv](https://gist.github.com/macagua/2a5d7b8c23ba28db9a4d43ff4fd452ba#instalar-pyenv)

Instalar virtualenv y pip

```
pip3.8 install virtualenv==20.19.0
pip3.8 install -U pip
```

### Instalar versiones de Python necesarias con pyenv

Comprobamos las versiones actuales que tenemos

```pyenv versions```

Necesitamos Python 2.7.18 y 3.11.2

Buscamos las versiones para Python 3.11 y python 2.7 si no las tenemos instaladas

```
pyenv install -l | egrep '^\s*3.11.'
pyenv install -l | egrep '^\s*2\.7\.'
```

Instalamos aquellas que no tengamos

```
pyenv install 3.11.2
pyenv install 2.7.18
```

### Crear entornos virtuales

```
virtualenv --python ~/.pyenv/versions/3.11.2/bin/python3.11 venv3
virtualenv --python ~/.pyenv/versions/2.7.18/bin/python venv2
```

### Instalar pylint_runner para cada entorno

Activamos el entorno 2.7

```
source ./venv2/bin/activate
pip install pylint-runner==0.5.4
deactivate
```

Activamos el entorno 3.11

```
source ./venv3/bin/activate
pip install pylint-runner==0.6.0
deactivate
```

## Uso de la librería

### Para analizar paquete de python 2.7

Activamos el entorno 2.7

```source ./venv2/bin/activate```

Analizamos el paquete con código python 2

Nos desplazamos a la raíz del paquete a analizar ubicado en la carpeta plone4

```cd plone4/nombre_de_producto```

Ejecutamos el comando de pylint_runner

```pylint_runner --rcfile=../.pylintrc```

Esto nos dará un resultado de calidad de código

Finalmente desactivamos entorno

```deactivate```

### Para analizar paquete de python 3

Activamos el entorno 3

```source ./venv3/bin/activate```

Analizamos el paquete con código python 3

Nos desplazamos a la raíz del paquete a analizar ubicado en la carpeta plone6

```cd plone6/nombre_de_producto```

Ejecutamos el comando de pylint_runner

```pylint_runner --rcfile=../.pylintrc```

Esto nos dará un resultado de calidad de código.
También nos dará un listado de los diferentes archivos con las mejoras a abordar.

Finalmente desactivamos entorno

```deactivate```