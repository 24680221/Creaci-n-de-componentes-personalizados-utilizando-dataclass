# Creacion-de-componentes-personalizados-utilizando-dataclass

El siguiente código se enfoca en el desarrollo de componentes gráficos personalizados utilizando la librería Flet, integrando además el uso de estructuras de datos mediante @dataclass para organizar la información. Su propósito es mostrar cómo separar los datos (usuarios) de la presentación visual (tarjetas de perfil), aplicando principios de programación orientada a objetos para crear interfaces más organizadas, reutilizables y fáciles de mantener. Este enfoque se relaciona principalmente con el tema 2.3: Creación de componentes definidos por el usuario.

Importación de librerías
-

Se utilizan dos librerías:

- Flet → para crear la interfaz gráfica.
- dataclasses → para definir estructuras de datos de forma sencilla.
```
import flet as ft
from dataclasses import dataclass
```

Definición de la clase Usuario (estructura de datos)
-

Aquí se define una clase de datos usando @dataclass.

Sirve para:

- Agrupar información del usuario
- Evitar código repetitivo (como constructores manuales)
- Cada objeto Usuario representa un modelo de datos.
```
@dataclass
class Usuario:
    nombre: str
    rol: str
    color_border: ft.ColorValue = ft.Colors.BLUE
```

Creación del componente personalizado tarjetaperfil
-

Se crea un componente visual personalizado que representa una tarjeta de usuario.

- Hereda de Container.
```
class tarjetaperfil(ft.Container):
```

Constructor del componente
-

Ahora el componente recibe un objeto completo en lugar de datos separados.
```
    def __init__(self, usuario: Usuario):
        super().__init__()
        self.usuario = usuario
```

Contenido del componente
-

Aqui se construye la interfaz:

- Nombre en negrita
- Rol en cursiva
- Organización vertical
```
self.content = ft.Column(
      controls=[
         ft.Text(usuario.nombre, size=20, weight=ft.FontWeight.BOLD),
          ft.Text(usuario.rol, italic=True),
            ],
            tight=True,
        )
```

Estilos del componente
-

Se personaliza la apariencia:

- Color dinámico del borde
- Fondo blanco
- Diseño uniforme
- Se asigna un evento al hacer clic.
```
        self.border = ft.border.all(2, usuario.color_border)
        self.padding = 10
        self.border_radius = 10
        self.width = 200
        self.bgcolor = ft.Colors.WHITE
        self.on_click = self.saludar
```

Método del evento
-

Se muestra en consola el nombre del usuario y Usa los datos del objeto Usuario
```
    def saludar(self, e):
        print(f"Interactuando con el componente de {self.usuario.nombre}")
```

Clase principal appusuarios
-

Se utiliza una clase para organizar toda la aplicación.
```
class appusuarios:
   def __init__(self,page: ft.Page):
     self.page = page
        self.configurar_pagina()
        self.construir_ui()
```

Configuración de la página
-

Se define el titulo y la alineacion
```
    def configurar_pagina(self):
        self.page.title = "unidad 2: componentes definidos por el usuario"
        self.page.horizontal_alignment = ft.CrossAxisAlignment.CENTER 
```

Construcción de la interfaz
-

Aquí ocurre lo más importante:
``` def construir_ui(self): ```

- Creación de objetos Usuario
donde se crean los componentes y se separa la logica de datos de la interfaz grafica.
```
        u1 = Usuario("Ana Garcia", "Desarrolladora senior", ft.Colors.GREEN)
        u2 = Usuario("Carlos Ruiz", "Arquitecto de software")
```

- Creación de componentes visuales
Aqui se usan los datos para construir la UI
```
        tarjeta1 = tarjetaperfil(u1)
        tarjeta2 = tarjetaperfil(u2)
```

- Mostrar en pantalla
Se agrega el titulo y se organizan tarjetas en fila.
```
        self.page.add(
            ft.Text("lista de usuarios", size=30, weight="bold"),
            ft.Row([
                tarjeta1,
                tarjeta2,
            ], alignment=ft.MainAxisAlignment.CENTER),
        )
```
Función principal
-
Inicializa la aplicación.
```
def main(page: ft.Page):
    appusuarios(page)
```

Ejecución
-

Ejecuta el programa.
```
ft.run(main)
```

A continuacion se muestra el codigo:

```
import flet as ft
from dataclasses import dataclass

@dataclass
class Usuario:
    nombre: str
    rol: str
    # use ColorValue type since flet doesn't expose `ft.Color` directly
    color_border: ft.ColorValue = ft.Colors.BLUE


class tarjetaperfil(ft.Container):
    def __init__(self, usuario: Usuario):
        super().__init__()
        self.usuario = usuario

        self.content = ft.Column(
            controls=[
                ft.Text(usuario.nombre, size=20, weight=ft.FontWeight.BOLD),
                ft.Text(usuario.rol, italic=True),
            ],
            tight=True,
        )
        self.border = ft.border.all(2, usuario.color_border)
        self.padding = 10
        self.border_radius = 10
        self.width = 200
        self.bgcolor = ft.Colors.WHITE

        self.on_click = self.saludar

    def saludar(self, e):
        print(f"Interactuando con el componente de {self.usuario.nombre}")

class appusuarios:

    def __init__(self,page: ft.Page):
        self.page = page
        self.configurar_pagina()
        self.construir_ui()
    
    def configurar_pagina(self):
        self.page.title = "unidad 2: componentes definidos por el usuario"
        self.page.horizontal_alignment = ft.CrossAxisAlignment.CENTER
        
    def construir_ui(self):
        # crear instancias de Usuario primero
        u1 = Usuario("Ana Garcia", "Desarrolladora senior", ft.Colors.GREEN)
        u2 = Usuario("Carlos Ruiz", "Arquitecto de software")

        tarjeta1 = tarjetaperfil(u1)
        tarjeta2 = tarjetaperfil(u2)

        self.page.add(
            ft.Text("lista de usuarios", size=30, weight="bold"),
            ft.Row([
                tarjeta1,
                tarjeta2,
            ], alignment=ft.MainAxisAlignment.CENTER),
        )
def main(page: ft.Page):
    appusuarios(page)

ft.run(main)
```

Acontinuacion se muestra la ejecucion:

<img width="956" height="468" alt="image" src="https://github.com/user-attachments/assets/289ed9b7-6e4f-4200-9abc-4f579ada5381" />

la accion de clic se muestra en la consola:

<img width="556" height="153" alt="image" src="https://github.com/user-attachments/assets/cdc46dd2-8567-469e-ab73-e0d48fc80524" />
