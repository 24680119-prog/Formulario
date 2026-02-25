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

## Campos 
En esta sección del código se crean todos los campos que forman el formulario de registro. Se utilizan diferentes componentes de Flet como TextField, Dropdown y RadioGroup para permitir al usuario ingresar o seleccionar información. Además, se implementa validación en tiempo real mediante el evento on_change, el cual llama a la función validar_campo() cada vez que el usuario escribe. Esto permite verificar que los datos cumplan con el formato correcto antes de enviarlos.

**Campos de texto (TextField)**

Los siguientes elementos son objetos TextField, que permiten al usuario escribir información.

Cada campo tiene:
-label → Es el texto que aparece como nombre del campo.

-on_change → Evento que se ejecuta cada vez que el usuario escribe algo.

-lambda e: → Función anónima que llama a validar_campo() para validar el contenido en tiempo real.

**Ejemplo de codigo**
```python
  txt_nombre = ft.TextField(label="Nombre *", on_change=lambda e: validar_campo(txt_nombre, "texto"))
```
Se crea un campo de texto para el nombre.
-El asterisco (*) indica que es obligatorio.

-Cada vez que el usuario escribe, se valida que solo contenga letras.

**Numero de control**
```python
   txt_control = ft.TextField(label="Número de control *", on_change=lambda e: validar_campo(txt_control, "numeros"))
```
-Solo permite números.
-Se valida automáticamente mientras el usuario escribe.

**Email**
```python
  txt_email = ft.TextField(label="Email *", on_change=lambda e: validar_campo(txt_email, "correo"))
```
-Se valida que tenga formato correcto de correo electronico.

**Telefono**
```python
    txt_telefono = ft.TextField(label="Número telefónico *", on_change=lambda e: validar_campo(txt_telefono, "numeros", 10))
```
-Solo acepta numeros y deben ser exactamente 10 numeros.

**Codigo postal**
```python
  txt_cp = ft.TextField(label="Código postal *", on_change=lambda e: validar_campo(txt_cp, "numeros", 5))
```
-Solo acepta numeros y deben ser 5.

## Campos desplegables 
Es un elemento gráfico que muestra una lista de opciones para que el usuario seleccione una sola. Se utiliza para controlar el tipo de datos ingresados y mejorar la organización del formulario.

**Carrera**

```python
    dd_carrera = ft.Dropdown(
        label="Carrera *",
        options=[
            ft.dropdown.Option("Ingeniería en Sistemas"),
            ft.dropdown.Option("Ingeniería Civil"),
            ft.dropdown.Option("Ingeniería Industrial"),
        ]
    )

```
Pwermite elegir una carrera y solo se puede seleccionar una opcion.

**Semestre**

```python
    dd_semestre = ft.Dropdown(
        label="Semestre *",
        options=[ft.dropdown.Option(str(i)) for i in range(1, 7)]
    )
```
Aquí se está usando algo llamado comprensión de lista (list comprehension).


**range(1, 7)**

Genera números desde el 1 hasta el 6.

En Python el 7 no se incluye, por eso genera:
1, 2, 3, 4, 5, 6

**for i in range(1, 7)**

Esto significa:
“Para cada número generado, guárdalo en la variable i”.

**str(i)**

Convierte el número en texto, esto es necesario porque las opciones del Dropdown deben ser texto.

Por lo tanto el programa automáticamente crea estas opciones en lugar de escribirlas manualmente una por una.

-“1”

-“2”

-“3”

-“4”

-“5”

-“6”

**Campo ciudad**
Este campo permite que el usuario seleccione la ciudad donde vive.
```python
    dd_ciudad = ft.Dropdown(
        label="Ciudad donde vive *",
        options=[
            ft.dropdown.Option("Ciudad de México"),
            ft.dropdown.Option("Guadalajara"),
            ft.dropdown.Option("Monterrey"),
            ft.dropdown.Option("Otras")
        ]
    )


```

## Botones de seleccion
En esta formulario se utilizan lbotones de seleccion tipo radio, agrupados dentro de RadioGroup, lo cual permiten al usuario seleccionar una sola opcion entre varias disponibles cuando el usuario selecciona una opcion , automaticamente se deselecciona la otra, es decir, solo se puede elegir una opcion a la vez.

```python
    radio_genero = ft.RadioGroup(
        content=ft.Column([
            ft.Radio(label="Masculino", value="Masculino"),
            ft.Radio(label="Femenino", value="Femenino"),
        ])
    )
```
Permite elegir solo una opcion del genero masculino o femenino

**Tipo de sangre**
Este bloque crea un campo desplegable (Dropdown) que permite al usuario seleccionar su tipo de sangre, el usuario no puede escribir manualmente el tipo de sangre, solo puede elegir una opción de la lista.
```python
    dd_tipo_sangre = ft.Dropdown(
        label="Tipo de sangre *",
        options=[
            ft.dropdown.Option("A+"), ft.dropdown.Option("A-"),
            ft.dropdown.Option("B+"), ft.dropdown.Option("B-"),
            ft.dropdown.Option("O+"), ft.dropdown.Option("O-"),
            ft.dropdown.Option("AB+"), ft.dropdown.Option("AB-")
        ]
    )
```

## Campos adicionales
La validación en los campos adicionales se realiza mediante la función validar_campo(), la cual verifica que cada dato cumpla con el formato correspondiente (solo letras, solo números o cantidad exacta de dígitos). Además, cambia el color del campo para indicar visualmente si la información es correcta o incorrecta.
**Eejemplo codigo**
```python
  txt_alergias = ft.TextField(label="Alergias o padecimientos", on_change=lambda e: validar_campo(txt_alergias, "alergias"))
```
Solo se valida si el usuario escribe algo.
Permite:
-Letras

-Espacios

-Comas
Evitando que el usuario escriba caracteres incorrectos.

```python
    txt_contacto_emergencia = ft.TextField(label="Nombre de contacto de emergencia *", on_change=lambda e: validar_campo(txt_contacto_emergencia, "texto"))
    txt_telefono_emergencia = ft.TextField(label="Teléfono de contacto de emergencia *", on_change=lambda e: validar_campo(txt_telefono_emergencia, "numeros", 10))
    txt_seguridad_social = ft.TextField(label="Número de Seguridad Social (11 dígitos) *", on_change=lambda e: validar_campo(txt_seguridad_social, "numeros", 11))
```

