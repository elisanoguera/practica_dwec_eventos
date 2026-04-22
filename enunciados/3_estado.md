# Gestión del estado

El objetivo de esta práctica es centralizar la gestión del estado en nuestro proyecto `VueJS` haciendo uso de la librería `Pinia`.

## Repositorio de la práctica

El **repositorio base** de la práctica está disponible en: https://github.com/elisanoguera/practica_dwec_eventos.git

Se supone que ya está configurado el **repositorio personal** y el **remoto secundario** (`profesora`). Si no es así, revisa las instrucciones de las prácticas anteriores. En el apartado de **Preparación** se indica cómo proceder.

## Requisitos de software

Para trabajar con `VueJS` (en desarrollo), es imprescindible tener instalado `Node.js`, que incluye `npm` (`Node Package Manager`).

Requisitos: 
- `Node.js v18` o superior (recomendado: `v20.x`)
- `npm v9` o superior
- Un entorno de desarrollo (recomendado `Visual Studio Code`).

Comprobación (ejecutar en terminal):

```sh
node -v
npm -v
```

## Preparación
1. Instalar los requisitos de software indicados
2. Abrir un terminal
3. Situarse en la carpeta del repositorio personal de la práctica
4. **Añadir el remoto secundario** a tu repositorio personal. Para ello hay que ejecutar el comando:
   ```sh
     git remote add profesora https://github.com/elisanoguera/practica_dwec_eventos.git
   ```
5. **Incorporar a tu repositorio personal los cambios** realizados por la profesora correspondientes a los archivos de esta práctica. Para ello hay que ejecutar:
   ```sh
     git pull profesora main
   ```
6. Este comando **descarga** los cambios que ha realizado la **profesora** en el **repositorio base** y los **integra** en tu repositorio personal. Tras realizar este paso, seguramente *git* **abra el editor configurado por defecto** para que introduzcas un **mensaje para crear un nuevo commit** que integre tus cambios y los cambios de la profesora. Debes introducir el texto y guardar los cambios.
7. En principio no deben producirse **conflictos**. En caso de que se produzcan (por ejemplo, porque has editado el fichero `.gitignore` y yo también porque lo exigía la práctica), **resuélvelos y notifícamelo a través de un Issue**.
8. Ejecuta el comando `git push` para subir los cambios a tu repositorio personal (el remoto principal) en *GitHub* y que queden guardados ahí también.
9. Ejecutar el comando `npm install`. Este comando instalará todas las librerías de *Node* necesarias para ejecutar la aplicación. Dichas librerías se guardarán en una carpeta con nombre `node_modules` dentro del repositorio. Nótese que dicha carpeta está excluida del repositorio en el archivo `.gitignore`.

## Integrar Pinia en nuestro proyecto

Para integrar `Pinia` un nuestro proyecto `VueJS` seguiremos los siguientes pasos:

1. Nos situamos en la carpeta del proyecto:

```sh
cd nombre-proyecto-vue
```

2. Instalamos `Pinia` y sus dependencias usando `npm`:

```sh
npm install pinia
```
   
3. Abrimos el archivo `src/main.js` e importamos la librería `Pinia`:

```sh
import { createPinia } from 'pinia';
```

4. Por último, dentro del archivo `src/main.js`, crearemos una instancia de `Pinia` y la pasaremos a la aplicación como si fuese un *plugin*. El código quedaría así:

```js
const pinia = createPinia();
const app = createApp(App);

app.use(pinia);
app.mount('#app');
```

## Tareas a realizar

### Lectura

Lee atentamente los siguientes artículos y sus correspondientes subsecciones en caso de que las tengan:

- [Documentación oficial de Pinia](https://pinia.vuejs.org/core-concepts/)
- [Tutorial de Pinia](https://cipfpbatoi.github.io/materials/daw/dwc/02-vue-composition-api/pinia.html)

### Ficheros de la aplicación

En esta práctica introduciremos un almacén o `store` de `Pinia` dentro de nuestro proyecto `VueJS`, que nos permitirá acceder desde cualquier componente a la variable `eventos`.

A continuación, se explica qué modificaciones debemos realizar en nuestro proyecto.

#### Almacen (`Store`) `eventosStore`

Crea el fichero `eventosStore.vue` (estará ubicado en la carpeta `src/stores`) con la siguiente información:

- Librerías
    - Importa `defineStore` de `Pinia` y `reactive` de `vue`:
        ```html
          import { defineStore } from 'pinia'
          import { reactive } from 'vue'
        ```
- Variables de datos    
    - `useEventosStore` - Define una *store* llamada `useEventosStore` con el método `defineStore`. Dentro de `useEventosStore`, copia la variable `eventos` que definimos en el componente `App`. Borra la variable `eventos` de `App`. A partir de ahora, tendremos esta variable disponible en nuestra `store`.

#### Componente principal `App`

Modifica el fichero `App.vue` con la siguiente información:

- Librerías
     - Importa `useEventosStore` desde nuestro almacen `eventosStore`:
        ```js
          import { useEventosStore }  from './stores/eventosStore' 
        ```
- Variables de datos    
  - `useEventos` - Almacenará una instancia de `useEventosStore`. Se realiza invocando a la función que hemos exportado al definir el almacén `useEventosStore()`. 
  - `eventos` - La variable `eventos` almacenará la variable `eventos` que hemos definido en `useEventos`.

      ```js
        eventos = useEventos.eventos;
      ```

#### Componente `MostrarEventos`

- Librerías
     - Importa `useEventosStore` desde nuestro almacen `eventosStore`:

        ```js
          import { useEventosStore }  from '../stores/eventosStore' 
        ```

- Parámetros (*props*):
  - `eventos` - Eliminaremos esta *prop*. A partir de ahora, accederemos a la variable `eventos` de nuestra `store`.

- Variables de datos
  - `useEventos` - Almacenará una instancia de `useEventosStore`. Se realiza invocando a la función que hemos exportado al definir el almacén `useEventosStore()`. 
  - `eventos` - La variable `eventos` almacenará la variable `eventos` que hemos definido en `useEventos`.
  
      ```js
        eventos = useEventos.eventos;
      ```

## Formato de la entrega
- Cada persona trabajará en su **repositorio personal** que habrá creado tras realizar el *fork* del repositorio base.
- Todos los archivos de la práctica se guardarán en el repositorio y se subirán a *GitHub* periódicamente. Es conveniente ir subiendo los cambios aunque no sean definitivos. **No se admitirán entregas de tareas que tengan un solo commit**.
- **Como mínimo** se debe realizar **un commit** por **cada elemento de la lista de tareas** a realizar (si es que estas exigen crear código, claro está).
- Para cualquier tipo de **duda o consulta** se pueden abrir `Issues` haciendo referencia a la profesora mediante el texto `@elisanoguera` dentro del texto del `Issue`. Los `issues` deben crearse en **tu repositorio**: si no se muestra la pestaña de `Issues` puedes activarla en los `Settings` de tu repositorio.
- Una vez **finalizada** la tarea se debe realizar una `Pull Request` al repositorio base indicando tu **nombre y apellidos** en el mensaje.
