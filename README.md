### 1. **`main`**

- **Recibe:**  
  - No recibe parámetros explícitos.
  
- **Devuelve:**  
  - No devuelve un valor, ya que la función `main` es la entrada principal del programa. Solo llama a `menuAcciones()`, que maneja la interacción del usuario y ejecuta las funcionalidades del sistema.

---

### 2. **`menuAcciones`**

- **Recibe:**  
  - No recibe parámetros explícitos.

- **Devuelve:**  
  - No devuelve nada directamente. La función controla el flujo del programa, mostrando un menú en la consola y ejecutando las acciones correspondientes según la opción seleccionada por el usuario.

  - Esta función contiene un ciclo `do-while` que mantiene el menú activo hasta que el usuario selecciona la opción para salir (opción 5).

  - Interactúa con el usuario pidiendo que ingrese una opción (número) y luego ejecuta el bloque correspondiente según la selección.

- **Comportamiento adicional:**  
  - Cuando el usuario elige "1. Agregar Estudiante", se llama a `agregarEstudiante()`.
  - Si elige "2. Mostrar Todos Los Estudiantes", se llama a `mostrarEstudiantes()`.
  - Si selecciona "3. Actualizar Estudiante", se llama a `actualizarEstudiante()`.
  - Si selecciona "4. Eliminar Estudiante", se llama a `eliminarEstudiante()`.

---

### 3. **`idExistente(int id)`**

- **Recibe:**  
  - **`id`** (tipo `int`): Este es el identificador del estudiante que se busca en el archivo `estudiantes.txt`.

- **Devuelve:**  
  - **`true`** si el ID ya existe en el archivo, es decir, si ya hay un estudiante registrado con ese ID.
  - **`false`** si el ID no existe en el archivo, es decir, si no hay un estudiante con ese ID.

- **Comportamiento adicional:**  
  - La función abre el archivo `estudiantes.txt` en modo lectura (`ifstream`) y verifica si algún estudiante en el archivo tiene el mismo ID que el que se le pasa como argumento.  
  - Si se encuentra una coincidencia, cierra el archivo y devuelve `true`. Si no se encuentra ninguna coincidencia, devuelve `false`.

- **Interacción con el archivo:**  
  - La función lee el archivo línea por línea, descomponiendo cada línea en un `id`, `nombre`, y `nota`. Si encuentra un estudiante con el mismo ID, devuelve `true`.

---

### 4. **`agregarEstudiante(estudiante e)`**

- **Recibe:**  
  - **`e`** (tipo `estudiante`): Esta es una estructura que contiene los datos del estudiante (ID, nombre y nota) a agregar al archivo.  
    - `e.id` (tipo `int`): El ID del estudiante.
    - `e.nombre` (tipo `string`): El nombre del estudiante.
    - `e.nota` (tipo `int`): La nota del estudiante.

- **Devuelve:**  
  - **Nada** (la función no tiene un valor de retorno explícito, pero realiza acciones como agregar un estudiante al archivo).

- **Comportamiento adicional:**  
  - Solicita al usuario ingresar un ID, un nombre y una nota para el estudiante.
  - Verifica que el ID sea válido (no negativo) y que no exista un estudiante con ese ID (usando la función `idExistente()`).
  - Si el ID es válido y no existe previamente, agrega los datos del estudiante al archivo `estudiantes.txt` en el formato "ID Nombre Nota" y muestra un mensaje de confirmación.
  
- **Interacción con el archivo:**  
  - La función abre el archivo `estudiantes.txt` en modo append (`ios::app`), lo que significa que agrega la nueva entrada al final del archivo sin sobrescribir los datos existentes.

---

### 5. **`mostrarEstudiantes()`**

- **Recibe:**  
  - No recibe parámetros.

- **Devuelve:**  
  - **Nada** (la función no devuelve un valor, pero muestra la lista de estudiantes en la consola).

- **Comportamiento adicional:**  
  - Abre el archivo `estudiantes.txt` y lee cada línea.
  - Muestra cada línea completa en la consola, lo que equivale a mostrar todos los estudiantes registrados.
  - Si no hay estudiantes en el archivo o hay algún error al abrir el archivo, muestra un mensaje de error.

- **Interacción con el archivo:**  
  - La función lee el archivo línea por línea, sin modificarlo. Utiliza `getline()` para leer cada línea del archivo y la muestra en la consola.

---

### 6. **`actualizarEstudiante()`**

- **Recibe:**  
  - No recibe parámetros explícitos, pero usa una variable interna para almacenar el ID del estudiante a actualizar.
  
- **Devuelve:**  
  - **Nada** (la función no tiene valor de retorno explícito, pero realiza la actualización de un estudiante en el archivo).

- **Comportamiento adicional:**  
  - Solicita al usuario que ingrese el ID del estudiante a actualizar.
  - Si el ID existe (verificado por `idExistente()`), pide al usuario ingresar el nuevo nombre y nueva nota.
  - Reemplaza los datos del estudiante en el archivo `estudiantes.txt` por los nuevos valores utilizando un archivo temporal.

- **Interacción con los archivos:**  
  - La función abre el archivo original en modo lectura y un archivo temporal en modo escritura.
  - Lee el archivo original línea por línea, y si encuentra el ID correspondiente, reemplaza los datos con los nuevos valores.
  - Al finalizar, elimina el archivo original y renombra el archivo temporal para que sustituya al original.

---

### 7. **`eliminarEstudiante()`**

- **Recibe:**  
  - No recibe parámetros explícitos, pero usa una variable interna para almacenar el ID del estudiante a eliminar.

- **Devuelve:**  
  - **Nada** (la función no devuelve valor, pero elimina un estudiante del archivo).

- **Comportamiento adicional:**  
  - Solicita al usuario que ingrese el ID del estudiante a eliminar.
  - Si el ID existe en el archivo, elimina el registro del estudiante correspondiente y mantiene el resto de los datos.
  - Si el ID no existe, muestra un mensaje informando que el estudiante no fue encontrado.

- **Interacción con los archivos:**  
  - La función abre el archivo original en modo lectura y un archivo temporal en modo escritura.
  - Copia todas las líneas del archivo original al archivo temporal, excepto aquellas correspondientes al ID que se quiere eliminar.
  - Si el ID es encontrado, se omite esa línea del archivo temporal.
  - Al finalizar, elimina el archivo original y renombra el archivo temporal para que sustituya al original.

---

### Resumen Completo de Recepciones y Devoluciones

| **Función**               | **Parámetros Recibidos**                                     | **Valor de Retorno**                   | **Descripción**                                                                 |
|---------------------------|--------------------------------------------------------------|----------------------------------------|---------------------------------------------------------------------------------|
| `main`                    | Ninguno                                                      | Ninguno                                | Llama a `menuAcciones` para iniciar el proceso de interacción con el usuario.  |
| `menuAcciones`            | Ninguno                                                      | Ninguno                                | Muestra el menú interactivo y ejecuta la acción seleccionada por el usuario.    |
| `idExistente(int id)`     | `id` (int)                                                   | `true` si el ID existe, `false` si no  | Verifica si un ID de estudiante existe en el archivo `estudiantes.txt`.         |
| `agregarEstudiante(estudiante e)` | `e` (estructura de tipo `estudiante` que contiene `id`, `nombre`, `nota`) | Ninguno                                | Agrega un estudiante al archivo si el ID no existe y es válido.                |
| `mostrarEstudiantes`      | Ninguno                                                      | Ninguno                                | Muestra todos los estudiantes guardados en `estudiantes.txt`.                  |
| `actualizarEstudiante`    | Ninguno (pero usa un ID proporcionado por el usuario)        | Ninguno                                | Actualiza los datos de un estudiante en el archivo `estudiantes.txt`.           |
| `eliminarEstudiante`      | Ninguno (pero usa un ID proporcionado por el usuario)        | Ninguno                                | Elimina a un estudiante del archivo `estudiantes.txt`.                          |

---
