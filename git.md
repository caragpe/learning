# Git

Asegurate de tener Git instalado en tu sistema. Puedes descargarlo desde el sitio web oficial de Git ([https://git-scm.com](https://git-scm.com)).

## Configuracion Inicial

1. Abre la línea de comandos o terminal.
2. Configura tu nombre de usuario global para Git utilizando el siguiente comando:

```shell
git config --global user.name "Tu nombre"
```

3. Configura tu dirección de correo electrónico global para Git utilizando el siguiente comando:

```shell
git config --global user.email "tu@email.com"
```

## Creacion de repositiorio

1. Crea una nueva carpeta para tu repositorio.
2. Navega hasta la carpeta del repositorio utilizando el comando `cd`.
3. Inicializa un nuevo repositorio Git en la carpeta utilizando el siguiente comando:

```shell
git init
```

## Agrega cambios

1. Crea un archivo de ejemplo en la carpeta del repositorio. Por ejemplo, puedes usar `touch archivo.txt` para crear un archivo de texto vacío.
2. Añade el archivo a la zona de preparación utilizando el siguiente comando:

```shell
git add archivo.txt
```

3. Confirma los cambios realizados utilizando el siguiente comando:

```shell
git commit -m "Mensaje descriptivo del commit"
```

## Ramas y fusiones

1. Crea una nueva rama utilizando el siguiente comando:

```shell
git branch nueva-rama
```

2. Cambia a la nueva rama utilizando el siguiente comando:

```shell
git checkout nueva-rama
```

Tambien puedes crear y cambiar a la nueva rama con:

```shell
git checkout -b nueva-rama
```

3. Realiza algunos cambios en archivos y confírmalos como hicimos anteriormente.
4. Cambia de nuevo a la rama principal (rama predeterminada) utilizando el comando:

```shell
git checkout main
```

5. Fusiona la rama nueva-rama con la rama principal utilizando el siguiente comando:

```shell
git merge nueva-rama
```

## Sincronizacion con un repositorio remoto

1. Crea un repositorio en un servicio de alojamiento remoto como GitHub o GitLab.
2. Copia la URL del repositorio remoto.
3. Asocia el repositorio remoto con tu repositorio local utilizando el siguiente comando:

```shell
git remote add origin URL_DEL_REPOSITORIO
```

4. Sube tus cambios locales al repositorio remoto utilizando el siguiente comando:

```shell
git push -u origin main
```

## Git stash

Git stash es una herramienta útil en Git que te permite guardar temporalmente los cambios en una rama sin tener que realizar un commit. Es especialmente útil cuando necesitas cambiar de contexto rápidamente y guardar tu trabajo en progreso sin afectar el estado actual de tu rama. A continuación, te mostraré cómo usar git stash y algunos casos de uso comunes:

### Caso de Uso 1: Guardar los cambios antes de cambiar de rama

Imagina que estás trabajando en una rama y tienes cambios sin confirmar. Sin embargo, necesitas cambiar rápidamente a otra rama para solucionar un problema urgente. En lugar de hacer un commit de los cambios a medias, puedes usar git stash para guardar temporalmente esos cambios.

1. Asegúrate de que tienes cambios sin confirmar en tu rama actual.
2. Ejecuta el siguiente comando para guardar los cambios en un stash:

    ```shell
    # descripción opcional para identificar el stash 
    git stash save "Descripción del stash"
    ```

3. Cambia a la otra rama utilizando `git checkout` para solucionar el problema urgente.
4. Una vez que hayas terminado en la otra rama, puedes volver a tu rama original y aplicar los cambios guardados mediante el siguiente comando:

    ```shell
    # Esto aplicará el último stash guardado a tu rama.
    git stash apply
    ```

### Caso de Uso 2: Guardar los cambios antes de actualizar la rama

Imaginemos que estás trabajando en una rama y necesitas actualizarla con los últimos cambios de la rama principal (o cualquier otra rama). Sin embargo, tienes cambios sin confirmar en tu rama y no quieres perderlos. En este caso, puedes utilizar git stash antes de la actualización.

1. Asegúrate de tener cambios sin confirmar en tu rama actual.
2. Guarda los cambios en un stash utilizando:

    ```shell
    git stash save "Cambios antes de la actualización"
    ```

3. Actualiza tu rama con los últimos cambios de la rama objetivo utilizando `git pull`, `git merge` u otro comando apropiado.
4. Una vez que hayas actualizado tu rama, puedes aplicar los cambios guardados utilizando `git stash apply`.

## Mergeando cambios

`git merge` y `git squash` son dos comandos diferentes en Git que se utilizan para combinar cambios de ramas diferentes, pero tienen resultados y casos de uso distintos. Aquí tienes una explicación de cada uno junto con ejemplos y una comparativa de casos de uso:

### Git Merge

Se utiliza para fusionar cambios de una rama a otra, creando un nuevo commit que representa la combinación de ambos historiales.

Ejemplo: Supongamos que tienes dos ramas: `rama1` y `rama2`, y quieres fusionar los cambios de `rama2` en `rama1`.

1. Cambia a la rama objetivo:

    ```shell
    git checkout rama1
    ```

2. Fusiona los cambios de la otra rama utilizando `git merge`:

    ```shell
    # nuevo commit que contiene los cambios de ambas ramas
    git merge rama2
    ```

**Casos de uso:**

* `git merge` es útil cuando deseas combinar todos los cambios de una rama en otra de forma transparente. Es adecuado para mantener un historial de commits completo y conservar la trazabilidad de los cambios realizados en ambas ramas.
* Es comúnmente utilizado en flujos de trabajo de colaboración, donde varios desarrolladores trabajan en diferentes ramas y se fusionan para combinar el trabajo realizado.

### Git Squash

Permite combinar varios commits en uno solo, lo que resulta en un historial de commits más limpio y fácil de leer. Los commits anteriores se "aplastan" en un solo commit.

Ejemplo: Supongamos que tienes tres commits en tu rama actual que deseas combinar en uno solo.

1. Utiliza el comando `git log` para identificar los hashes de los commits que deseas combinar.
2. Ejecuta el siguiente comando para combinar los commits en un solo commit:

    ```shell
    # esto abre un editor donde podrás elegir qué commits mantener
    # y cómo combinarlos. Cambia "pick" por "squash" o "s" en los 
    # commits que deseas aplastar.
    git rebase -i HEAD~3
    ```

3. Guarda y cierra el editor de texto.
4. Se abrirá otro editor de texto donde puedes editar el mensaje del commit resultante.
5. Guarda y cierra el editor de texto.

**Casos de uso:**

* `git squash` es útil cuando deseas combinar varios commits relacionados en uno solo para tener un historial más limpio y conciso.
* Es útil antes de enviar una solicitud de extracción (pull request) o antes de fusionar cambios en una rama principal, ya que ayuda a mantener un historial más claro y fácil de revisar.

En resumen, `git merge` se utiliza para fusionar cambios de una rama a otra, creando nuevos commits, mientras que `git squash` se utiliza para combinar varios commits en uno solo, creando un historial más limpio y conciso. La elección entre ellos depende de tus necesidades y preferencias específicas en cuanto a la estructura del historial de commits.

### Conflictos

Cuando realizas un `git merge` y hay conflictos, Git pausa el proceso de fusión y te solicita que resuelvas los conflictos manualmente

1. Realiza un `git merge` que genere conflictos. Por ejemplo, supongamos que estás en la rama `rama1` y quieres fusionar la rama `rama2`:

    ```sql
    git checkout rama1
    git merge rama2
    ```

    Si hay conflictos, Git te mostrará un mensaje indicando los archivos con conflictos.

2. Abre el archivo en conflicto con un editor de texto y busca las secciones marcadas como conflictos. Verás algo similar a esto:

    ```markdown
    <<<<<<< HEAD
    // Código en la rama actual (rama1)
    =======
    // Código en la rama que estás fusionando (rama2)
    >>>>>>> rama2
    ```

3. Edita el archivo en conflicto y selecciona qué cambios quieres mantener. Puedes optar por quedarte con los cambios de `rama1` (rama actual) o con los cambios de `rama2` (rama que estás fusionando).

    ```shell
    Por ejemplo, si deseas mantener los cambios de `rama1`, elimina las líneas marcadas como `<<<<<<< HEAD` y `=======` para que solo quede el código de `rama1`.

    Si prefieres mantener los cambios de `rama2`, elimina las líneas marcadas como `<<<<<<< HEAD` y `>>>>>>> rama2`, dejando solo el código de `rama2`.
    ```

4. Guarda el archivo modificado.

5. Una vez que hayas resuelto los conflictos en todos los archivos en conflicto, utiliza el comando `git add` para marcar los archivos como resueltos:

    ```csharp
    git add archivo1.txt archivo2.js
    ```

6. Continúa con el proceso de fusión ejecutando `git merge --continue`:

    ```kotlin
    git merge --continue
    ```

Git finalizará el proceso de fusión y creará un nuevo commit que refleje la resolución de conflictos.

Recuerda que también puedes utilizar herramientas externas de línea de comandos, como `git mergetool`, que te ayudan a resolver conflictos proporcionando una interfaz gráfica o herramientas de comparación visual para seleccionar los cambios que deseas mantener.

Es importante destacar que es fundamental revisar cuidadosamente los cambios y asegurarte de que la resolución de conflictos sea correcta antes de continuar con el proceso de fusión.

### Seleccionar cambios locales o remotos

Puedes especificar si deseas quedarte con tus cambios locales o con los cambios de la rama destino directamente desde la línea de comandos al resolver conflictos en Git. Puedes utilizar los siguientes comandos:

* `git checkout --ours <archivo>`: Este comando te permite quedarte con los cambios locales, es decir, los cambios en tu rama actual.

* `git checkout --theirs <archivo>`: Este comando te permite quedarte con los cambios de la rama destino, es decir, los cambios en la rama que estás fusionando.

**Ejemplo**

1. Ejecuta un `git merge` que genere conflictos, como se mencionó anteriormente.

2. Abre el archivo en conflicto y encuentra las secciones marcadas como conflictos.

3. Para quedarte con tus cambios locales (rama actual), utiliza el siguiente comando:

    ```shell
    git checkout --ours archivo.txt
    ```

4. Si prefieres quedarte con los cambios de la rama destino (rama que estás fusionando), utiliza el siguiente comando:

    ```shell
    git checkout --theirs archivo.txt
    ```

5. Repite los pasos 3 y 4 para cada archivo en conflicto que desees resolver.

6. Una vez que hayas resuelto todos los conflictos, marca los archivos como resueltos utilizando `git add`:

    ```shell
    git add archivo.txt
    ```

7. Continúa con el proceso de fusión ejecutando `git merge --continue`:

    ```shell
    git merge --continue
    ```

Ten en cuenta que `--ours` y `--theirs` se refieren a la perspectiva desde la cual estás resolviendo el conflicto. Si estás en la rama actual, `--ours` se refiere a tus cambios locales, y si estás fusionando otra rama, `--theirs` se refiere a los cambios de la rama que estás fusionando.

## Comparando ramas

Puedes utilizar los comandos `git diff` y `git difftool` para comparar diferencias entre ramas y archivos específicos en Git.

### Comparar diferencias entre dos ramas

Puedes utilizar `git diff` para ver las diferencias entre dos ramas. Aquí tienes un ejemplo:

```shell
git diff rama1 rama2
```

Este comando muestra las diferencias entre `rama1` y `rama2`. Verás una lista de cambios que incluye adiciones, eliminaciones y modificaciones de archivos.

### Comparar diferencias entre dos archivos

Puedes utilizar `git diff` para ver las diferencias entre dos archivos específicos. Aquí tienes un ejemplo:

```shell
git diff archivo1.txt archivo2.txt
```

Este comando muestra las diferencias entre `archivo1.txt` y `archivo2.txt`. Verás las líneas modificadas, añadidas o eliminadas en cada archivo.

## Comandos git importantes

1. `git status`: Muestra el estado actual del repositorio, incluyendo los archivos modificados, los archivos añadidos o eliminados, y la rama actual.

2. `git add`: Agrega archivos al área de preparación (staging area) para ser incluidos en el próximo commit. Puedes utilizar `git add .` para agregar todos los archivos modificados.

3. `git commit`: Crea un nuevo commit con los cambios en el área de preparación. Puedes utilizar `git commit -m "mensaje"` para hacer un commit con un mensaje descriptivo.

4. `git push`: Envía los commits locales a un repositorio remoto. Por ejemplo, `git push origin rama` envía los commits de la rama actual al repositorio remoto llamado "origin".

5. `git pull`: Obtiene los cambios más recientes del repositorio remoto y los fusiona con la rama actual. Es equivalente a ejecutar `git fetch` seguido de `git merge`.

6. `git clone`: Crea una copia local de un repositorio remoto. Por ejemplo, `git clone url_repositorio` crea una copia del repositorio en la URL especificada.

7. `git branch`: Muestra una lista de ramas en el repositorio. Puedes utilizar `git branch -a` para mostrar todas las ramas, incluyendo las ramas remotas.

8. `git checkout`: Cambia a una rama o estado específico del repositorio. Por ejemplo, `git checkout rama` cambia a la rama especificada.

9. `git merge`: Fusiona los cambios de una rama en otra rama. Lo hemos discutido anteriormente en más detalle.

10. `git stash`: Guarda temporalmente los cambios no comprometidos en una pila de almacenamiento temporal (stash). Puedes utilizar `git stash push` para almacenar los cambios y `git stash pop` para restaurar los cambios desde el stash.

## Ejemplos git branch

1. Ejemplo de `git branch`:

    * Para ver una lista de ramas en el repositorio:

        ```shell
        git branch
        ```

        Esto mostrará todas las ramas locales y resaltará la rama actual con un asterisco (\*).

    * Para crear una nueva rama:

        ```shell
        git branch nueva-rama
        ```

        Esto creará una nueva rama llamada "nueva-rama" basada en la rama actual. Sin embargo, aún estarás en la rama actual después de crearla.

    * Para eliminar una rama:

        ```shell
        git branch -d rama-a-eliminar
        ```

        Esto eliminará la rama especificada. Asegúrate de no tener cambios sin fusionar en la rama antes de eliminarla.

2. Ejemplo de `git checkout`:

    * Para cambiar a una rama existente:

        ```shell
        git checkout nombre-de-rama
        ```

        Esto te cambiará a la rama especificada y actualizará tu directorio de trabajo con los archivos de esa rama.

    * Para crear y cambiar a una nueva rama al mismo tiempo:

        ```shell
        git checkout -b nueva-rama
        ```

        Esto creará una nueva rama llamada "nueva-rama" basada en la rama actual y te cambiará a ella.

    * Para cambiar a una revisión específica (commit, tag, o identificador):

        ```shell
        git checkout nombre-revision
        ```

        Esto te cambiará a la revisión especificada, permitiéndote revisar versiones anteriores de tu código.

    * Para deshacer cambios no confirmados en un archivo:

        ```shell
        git checkout -- nombre-archivo
        ```

        Esto descartará los cambios no confirmados y restaurará el archivo a su estado anterior.

## Usos avanzados

Tanto `git branch` como `git checkout` tienen algunos usos más avanzados que pueden ser útiles en determinadas situaciones. A continuación, te presento algunos de estos usos más avanzados:

1. `git branch`:

    * Crear una rama a partir de un commit específico:

        ```shell
        git branch nueva-rama commit
        ```

        Esto creará una nueva rama llamada "nueva-rama" a partir del commit especificado. Puedes proporcionar el identificador del commit o su referencia (por ejemplo, `HEAD~3` para el tercer commit anterior).

    * Mostrar los commits asociados con cada rama:

        ```shell
        git branch --verbose
        ```

        Esto muestra una lista de todas las ramas con el último commit asociado a cada una de ellas. Es útil para tener una vista general de los commits en el repositorio.

    * Renombrar una rama:

        ```shell
        git branch -m nombre-viejo nombre-nuevo
        ```

        Esto renombra la rama especificada de "nombre-viejo" a "nombre-nuevo".

2. `git checkout`:

    * Crear y cambiar a una nueva rama remota:

        ```shell
        git checkout --track origin/nueva-rama
        ```

        Esto crea una nueva rama local basada en la rama remota "nueva-rama" y cambia a ella.

    * Cambiar a un commit específico en modo "detached HEAD":

        ```shell
        git checkout commit
        ```

        Esto cambia a la revisión especificada (commit, tag o identificador) en modo "detached HEAD", lo que significa que no estarás en una rama y no podrás hacer nuevos commits hasta que cambies a una rama.

    * Descartar cambios no confirmados en todos los archivos:

        ```shell
        git checkout .
        ```

        Esto descarta los cambios no confirmados en todos los archivos del repositorio.

## Git log y git reflog

1. `git log`:

    El comando `git log` se utiliza para ver el historial de commits en el repositorio. Aquí tienes algunos casos de uso avanzados:

    * Mostrar el historial de commits:

        ```shell
        git log
        ```

        Esto muestra una lista de commits ordenados cronológicamente, desde el más reciente hasta el más antiguo. Verás información como el autor del commit, la fecha, el mensaje de commit y el identificador único (hash) del commit.

    * Ver cambios en cada commit:

        ```shell
        git log -p
        ```

        Esto muestra el historial de commits junto con los cambios realizados en cada uno. Puedes ver las adiciones, eliminaciones y modificaciones de archivos en cada commit.

    * Filtrar el historial de commits por autor:

        ```shell
        git log --author="nombre_autor"
        ```

        Esto muestra solo los commits realizados por el autor especificado.

    * Limitar la salida del historial de commits:

        ```shell
        git log --since="fecha_inicio" --until="fecha_fin"
        ```

        Esto muestra los commits realizados dentro del rango de fechas especificado. Puedes utilizar diferentes formatos de fecha, como "YYYY-MM-DD" o "1 week ago".

2. `git reflog`:

    El comando `git reflog` muestra el registro de referencias en Git, lo cual incluye los movimientos del puntero HEAD y las ramas. Aquí tienes algunos casos de uso avanzados:

    * Mostrar el registro de referencias:

        ```shell
        git reflog
        ```

        Esto muestra una lista de los movimientos del puntero HEAD y las ramas, junto con los identificadores únicos (hash) de los commits asociados.

    * Ver cambios en el registro de referencias:

        ```shell
        git reflog -p
        ```

        Esto muestra el registro de referencias junto con los cambios en cada movimiento. Puedes ver las adiciones, eliminaciones y modificaciones de archivos asociadas con cada movimiento.

    * Restaurar un commit anterior:

        ```shell
        git reflog
        git checkout HEAD@{n}
        ```

        Utiliza `git reflog` para encontrar el identificador único (hash) del commit anterior que deseas restaurar y luego usa `git checkout` para cambiar al commit especificado.

    * Recuperar una rama eliminada:

        ```shell
        git reflog
        git checkout -b nueva-rama nombre_commit
        ```

        Utiliza `git reflog` para encontrar el identificador único (hash) del commit asociado con la rama eliminada y luego crea una nueva rama basada en ese commit utilizando `git checkout -b`.
