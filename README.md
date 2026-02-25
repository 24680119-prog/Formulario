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
Este bloque de código define la función principal del programa (main), que es donde se configura la ventana de la aplicación en Flet. Dentro de esta función se establecen las propiedades básicas de la interfaz gráfica: el título que aparece en la ventana, el color de fondo, el espacio interno (padding) y el modo de tema claro.
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

**page.title** = “Formulario Completo - Registro Estudiantes”

Esta línea establece el título de la ventana.

El texto que está entre comillas será el nombre que aparece en la parte superior de la aplicación.


En este caso, el título de la interfaz será:
Formulario Completo - Registro Estudiantes

** page.bgcolor** = “#FDFBE3”

Aquí se define el color de fondo de toda la ventana.

-bgcolor significa background color (color de fondo).

-"#FDFBE3" es un color en formato hexadecimal.

Este código hexadecimal representa un tono claro (similar a beige o crema suave), lo cual hace que la interfaz sea visualmente agradable.


**page.padding = 20**

El padding es el espacio interno entre el borde de la ventana y los elementos que se colocan dentro.

En este caso, se deja un espacio de 20 píxeles alrededor del contenido, para que los elementos no estén pegados al borde.

Esto mejora la presentación visual del formulario.

**page.theme_mode = ft.ThemeMode.LIGHT**

Aquí se define el modo de tema de la aplicación.

Flet permite dos modos principales:
-LIGHT (modo claro)

-DARK (modo oscuro)
En este caso, se selecciona el modo claro (LIGHT), lo que significa que la interfaz tendrá colores claros por defecto.

## Seccion de registros 

Este bloque de código crea la sección donde se mostrarán los registros almacenados. Se define una columna con desplazamiento automático para guardar los datos ingresados y un título en negrita que identifica la sección.


```python
    datos_guardados = ft.Column(
        spacing=10,
        scroll=ft.ScrollMode.AUTO
    )

    titulo_registros = ft.Text(
        "Registros Guardados",
        size=18,
        weight=ft.FontWeight.BOLD
    )
```
**datos_guardados = ft.Column(…)**

Aquí se crea un contenedor vertical usando ft.Column.

Una Column en Flet organiza los elementos uno debajo de otro, de forma vertical.

Se le asignan dos propiedades importantes:
-spacing=10 : Define el espacio (en píxeles) entre cada elemento que se agregue dentro de la columna, esto evita que los registros aparezcan pegados.

scroll=ft.ScrollMode.AUTO: Activa el desplazamiento automático (scroll). 
Esto significa que si se guardan muchos registros y ya no caben en pantalla, aparecerá una barra de desplazamiento para poder verlos todos.

Esta variable (datos_guardados) será donde se irán agregando dinámicamente los registros después de presionar el botón “Enviar”.


**titulo_registros = ft.Text(…)**

Aquí se crea un texto que funcionará como título para la sección de registros.

Sus propiedades son:
-"Registros Guardados" → Es el texto que se mostrará en pantalla.

-size=18 → Define el tamaño de la letra.

-weight=ft.FontWeight.BOLD → Hace que el texto esté en negrita.

Este título se colocará encima de la columna donde se muestran los registros.


## Funcion validacion de campos

Esta funcion  se encarga de validar los datos ingresados por el usuario segun su tipo texto, numeros, correo o alergias. Se utiliza expresiones regulares para comporbar formatos especificos y cambia el color del borde del campo para indicar visualmente si el dato es correcto o incorrecto.
```python
    def validar_campo(campo, tipo="texto", longitud=None):
        valor = campo.value.strip()
        valido = True

```
**def validar_campo(campo, tipo=“texto”, longitud=None)**: Aquí se define una función llamada validar_campo.

Esta función sirve para verificar si la información que el usuario escribe en un campo es correcta.

Recibe tres parámetros:
-campo → Es el TextField que se va a validar.

-tipo="texto" → Indica qué tipo de validación se aplicará (por defecto es texto).

-longitud=None → Se usa cuando se necesita validar una cantidad específica de dígitos (por ejemplo, 10 números).

 **valor = campo.value.strip()**
-campo.value obtiene el texto que el usuario escribió.

-.strip() elimina espacios en blanco al inicio y al final.

Esto evita errores si el usuario deja espacios innecesarios.

- valido = True

Se crea una variable llamada valido y se inicializa en True.

Se asume que el dato es correcto hasta que se demuestre lo contrario.

## Validacion segun el tipo
```python
        if tipo == "texto":
            if not valor or not re.match(r"^[A-Za-zÁÉÍÓÚáéíóúÑñ ]+$", valor):
                valido = False
```
Verifica que el campo no esté vacío.
-Usa una expresión regular (re.match) para permitir solo letras y espacios.

-Si contiene números o símbolos, será inválido.

-Si no cumple las condiciones, valido pasa a ser False.


## Validacion de numeros 
```python
        elif tipo == "numeros":
            if not valor.isdigit() or (longitud and len(valor) != longitud):
                valido = False
```
valor.isdigit() verifica que solo haya números.
-Si se especifica una longitud, también verifica que tenga exactamente esa cantidad de dígitos.

Por ejemplo:
-Teléfono → 10 dígitos

-Código postal → 5 dígitos

-NSS → 11 dígitos

## Validacion de correo electronico 
```python
        elif tipo == "correo":
            if not re.match(r"^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$", valor):
                valido = False
```
Aquí se usa una expresión regular para verificar que el correo tenga formato correcto:

Debe contener:
-Texto antes del @

-Un dominio después del @

-Una extensión como .com, .mx, etc.

Si no cumple el formato, se marca como inválido.

## Validacion de alergias
```python
        elif tipo == "alergias":
            if valor and not re.match(r"^[A-Za-zÁÉÍÓÚáéíóúÑñ ,]*$", valor):
                valido = False
```
Este campo es opcional.
-Solo se valida si el usuario escribió algo.

-Permite letras, espacios y comas.

-No permite números ni símbolos especiales.

## Campo visual segun validacion

```python
        campo.border_color = ft.Colors.GREEN if valido else ft.Colors.RED
        campo.update()
        return valido
```
**campo.border_color**

Aquí se cambia el color del borde del campo:
-Verde → si es válido.

-Rojo → si es inválido.

Se usa una expresión condicional:
verde si valido es True, rojo si es False.


**campo.update()**

Actualiza visualmente el campo para que el cambio de color se refleje en pantalla.


**return valido**

La función devuelve True si el campo es válido o False si no lo es.
Esto permite que otras partes del programa (como el botón Enviar) sepan si pueden continuar o no.

