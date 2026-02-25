## Importacion de librerias 
```python
import flet as ft
import re
```
Estas dos líneas sirven para importar las librerías que el programa necesita para funcionar.

**import flet as ft**
Esta línea importa la librería Flet, que es la que permite crear interfaces gráficas (formularios, botones, campos de texto, etc.).

Se usa as ft para asignarle un alias más corto.
Esto significa que en lugar de escribir flet.TextField, se puede escribir ft.TextField, lo cual hace el código más limpio y fácil de leer.

**import re**
Esta línea importa la librería re, que significa regular expressions (expresiones regulares).

Las expresiones regulares se usan para validar textos, por ejemplo:

-Verificar que un nombre solo tenga letras.
  
-Comprobar que un correo tenga el formato correcto.

-Validar que un número tenga cierta cantidad de dígitos.

##  Funcion principal main 
```python
def main(page: ft.Page):
    page.title = "Formulario Completo - Registro Estudiantes"
    page.bgcolor = "#FDFBE3"
    page.padding = 20
    page.theme_mode = ft.ThemeMode.LIGHT
```
def main(page: ft.Page):

Aquí se define la función principal del programa llamada main.
	•	def es la palabra reservada que se usa para crear funciones en Python.
	•	main es el nombre de la función.
	•	page: ft.Page indica que el parámetro page es un objeto del tipo Page de la librería Flet.

En Flet, page representa la ventana principal de la aplicación.
Todo lo que se agregue a page será lo que el usuario verá en pantalla.

⸻

🔹 page.title = “Formulario Completo - Registro Estudiantes”

Esta línea establece el título de la ventana.

El texto que está entre comillas será el nombre que aparece en la parte superior de la aplicación.

En este caso, el título de la interfaz será:
Formulario Completo - Registro Estudiantes

⸻

🔹 page.bgcolor = “#FDFBE3”

Aquí se define el color de fondo de toda la ventana.
	•	bgcolor significa background color (color de fondo).
	•	"#FDFBE3" es un color en formato hexadecimal.

Este código hexadecimal representa un tono claro (similar a beige o crema suave), lo cual hace que la interfaz sea visualmente agradable.

⸻

🔹 page.padding = 20

El padding es el espacio interno entre el borde de la ventana y los elementos que se colocan dentro.

En este caso, se deja un espacio de 20 píxeles alrededor del contenido, para que los elementos no estén pegados al borde.

Esto mejora la presentación visual del formulario.

⸻

🔹 page.theme_mode = ft.ThemeMode.LIGHT

Aquí se define el modo de tema de la aplicación.

Flet permite dos modos principales:
	•	LIGHT (modo claro)
	•	DARK (modo oscuro)

En este caso, se selecciona el modo claro (LIGHT), lo que significa que la interfaz tendrá colores claros por defecto.
##
