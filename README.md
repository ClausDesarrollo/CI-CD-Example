# CI-CD-Example
Ejemplo de implementación de pruebas automáticas 

Este ejemplo esta pensado para ejemplificar como automatizar los prosesos de integracion y entrega en platafomas como :

- GitHub
- GitLab
- Azure DevOps (anteriormente conocido como Visual Studio Team Services):  

CI/CD es una práctica de desarrollo de software que se refiere a la integración continua (CI) y la entrega continua (CD). Estas prácticas están diseñadas para mejorar la eficiencia y calidad del desarrollo de software, permitiendo a los equipos desarrollar, probar y entregar código de manera más rápida y confiable.

Integración Continua (CI):

Es un proceso en el que los desarrolladores combinan su código en un repositorio central varias veces al día. 
Cada vez que se realiza una integración, se ejecutan pruebas automáticas para verificar si el nuevo código introdujo errores o rompió alguna funcionalidad existente. 
La idea es detectar y corregir problemas de integración tan pronto como sea posible, lo que ayuda a reducir el riesgo de conflictos entre el trabajo de diferentes desarrolladores y garantiza que el código base siempre esté en un estado funcional.

puedes configurar fácilmente la integración continua (CI) para ejecutar pruebas automáticas cada vez que se realiza un cambio en el código. Esto se hace mediante el uso de un archivo llamado .gitlab-ci.yml, que se coloca en la raíz del repositorio y que contiene las instrucciones para la configuración de la CI.

1 - Crea un archivo de flujo de trabajo: En tu repositorio, crea un archivo YAML para definir tu flujo de trabajo en este caso nos apegaremos a GitHub Actions para automatizar la creacion de este producto. 

2 - Este archivo debe colocarse en la ruta .github/workflows en tu repositorio. Puedes nombrar el archivo como desees, por ejemplo, test.yml.
3 - Define el flujo de trabajo con el archivo YAML, define el flujo de trabajo especificando los eventos que desencadenarán la ejecución de las pruebas. 
Por lo general, querrás que las pruebas se ejecuten cuando se realizan cambios en el código (por ejemplo, cuando se envían solicitudes de extracción o se realizan commits en la rama principal).

ejemplo de documento YAML ejemplo.yml
name: CI

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
----------------------------------------------------------

4 - Configura los trabajos y las acciones: Dentro del bloque de flujo de trabajo, puedes configurar los trabajos y las acciones que deseas ejecutar. 
Puedes utilizar acciones predefinidas proporcionadas por GitHub o crear tus propias acciones personalizadas. 
Por ejemplo, puedes usar acciones para clonar el repositorio, instalar dependencias y ejecutar las pruebas.

------------------ ejemplo documento YAML .yml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'
      - name: Install dependencies
        run: npm install
      - name: Run tests
        run: npm test
----------------------------------------------  

5 - Agrega y compromete el archivo YAML: Una vez que hayas configurado tu archivo de flujo de trabajo, agrégalo y "compromételo" en tu repositorio de GitHub.

6 - Observa los resultados en GitHub: GitHub Actions ejecutará automáticamente el flujo de trabajo configurado cada vez que se cumplan los eventos especificados. 
Puedes ver los resultados de las pruebas en la pestaña "Actions" de tu repositorio en GitHub, donde podrás ver el estado de los trabajos y cualquier resultado de las pruebas que se hayan ejecutado. en Gitlab podemos configurar esto igual mente comprometiendo los cambios y se pueden ver los cambios en la interface de usuario



EJEMPLO PRACTICO PARA ESTE PROYECTO 
Vamos a ejecutar pruebas unitarias de JavaScript utilizando una herramienta como Jest. 
Aquí tienes un ejemplo del archivo .github/workflows/test.yml:
--------------------------------------
name: CI

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test
-----------------------------------------

En este archivo YAML:

Se define un flujo de trabajo llamado "CI".
Se especifican los eventos que desencadenarán la ejecución del flujo de trabajo, en este caso, push a la rama main y pull requests a la rama main.
Se define un trabajo llamado "test" que se ejecutará en un entorno Ubuntu.

En los pasos del trabajo:
Se realiza la clonación del repositorio.
Se configura el entorno Node.js.
Se instalan las dependencias del proyecto (en este caso, asumimos que usas npm).
Finalmente, se ejecutan las pruebas utilizando el comando npm test.

Este archivo YAML debería colocarse en la carpeta .github/workflows dentro de tu repositorio GitHub CI-CD-Example. 
Después de agregar y comprometer este archivo en tu repositorio, GitHub Actions ejecutará automáticamente este flujo de trabajo cada vez que se realicen cambios en la rama main o se abra una solicitud de extracción hacia main, ejecutando así las pruebas definidas en tu proyecto.

Asegúrate de que tus pruebas estén configuradas correctamente para que puedan ejecutarse con éxito en este flujo de trabajo.





