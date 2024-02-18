# EJERCICIO KTOR - HOBBYTE

---
## MANUAL DE USO

---
- Para lanzar el servidor correctamente primero se debe modificar el archivo ``Parametros`` que se encuentra en ``/src/main/kotlin/utils/Parametros`` en ``val ip = "192.168.XXX.XXX"`` y poner la ``ip`` de nuestro ordenador.
- Finalmente en ``Application.kt`` podremos lanzar el servidor.

## Rutas Usuarios

---

#### Registrarse

- URL : ``http://192.168.1.150:8080/registrar``
- Método : ``POST``
- Datos Requeridos : 
    - ``nombre`` : Nombre del usuario (string)
    - ``correo`` : Correo del usuario (string)
    - ``contrasena`` : Contraseña del usuario (string)

##### Ejemplo de solicitud para registrar usuario
```json
{
  "nombre": "Usuario",
  "email": "usuario@correo.com",
  "password": "admin123"
}
```
--- 
#### Iniciar sesión

- URL: `http://192.168.1.150:8080/login`
- Método: `POST`
- Datos requeridos:
    - `email`: Email del usuario registradi (string)
    - `password`: Contraseña del usuario registrado (string)
- Datos de respuesta:
    - `token`: Token de autenticación (string)
> El token de autenticación es necesario para realizar cualquier solicitud a la API.

##### Ejemplo de solicitud para iniciar sesión
```json
{
  "email" : "usuario@correo.com",
  "password": "admin123"
}
```
---

#### Ver usuarios

- URL: `http://192.168.1.150:8080/usuarios`
- Método: `GET`
- Datos requeridos:
    - `token`: Token de autenticación (string)
> El token de autenticación recibido en el login se colocará en ``Auth`` > ``Bearer`` (Thunder Client)
---

#### Ver usuario por email

- URL: `http://192.168.1.150:8080/usuarios/:email`
- Método: `GET`
- Datos requeridos:
    - `token`: Token de autenticación (string)
    - `email`: Email del usuario (string)
---

#### Modificar usuario

- URL: `http://192.168.1.150:8080/usuarios/:email`
- Método: `PUT`
- Datos requeridos:
    - `token`: Token de autenticación (string)
    - `email`: Email del usuario (string)
    - `nombre`: Nombre del usuario (string)
    - `password`: Contraseña del usuario (string)

##### Ejemplo de solicitud para modificar usuario
```json
{
  "nombre": "Usuario",
  "email": "prueba@correo.com",
  "password": "admin123"
}
```
---

#### Eliminar usuario

- URL: `http://192.168.1.150:8080/usuarios/:email`
- Método: `DELETE`
- Datos requeridos:
    - `token`: Token de autenticación (string)
    - `email`: Email del usuario (string)
---

## Rutas Juego Hobbyte

---

#### Iniciar partida (normal)

- URL: `http://192.168.1.150:8080/iniciar/:idUsuario`
- Método: `POST`
- Datos requeridos:
    - `token`: Token de autenticación (string)
    - `idUsuario`: Id del usuario que quiere jugar (int)

---

#### Iniciar partida (personalizada)

- URL: `http://192.168.1.150:8080/iniciar/:idUsuario/:numeroCasillas`
- Método: `POST`
- Datos requeridos:
    - `token`: Token de autenticación (string)
    - `idUsuario`: Id del usuario que quiere jugar (int)
    - `numeroCasillas`: Número de casillas que tendrá el tablero (int)

---

#### Ver tablero

- URL: `http://192.168.1.150:8080/tablero/:idPartida`
- Método: `GET`
- Datos requeridos:
    - `token`: Token de autenticación (string)
    - `idPartida`: Id de la partida para ver su tablero (int)

--- 
#### Destapar Casilla

- URL: `http://192.168.1.150:8080/destapar/:idUsuario/:idCasilla`
- Método: `POST`
- Datos requeridos:
    - `token`: Token de autenticación (string)
    - `idUsuario`: Id del usuario al que pertenece la partida y la casilla (int)
    - `idCasilla`: Id de la casilla que se quiere destapar (int)

> El usuario al que le pertenece la partida será el unico que pueda destapar sus casillas
--- 
#### Estado de la partida

- URL: `http://192.168.1.150:8080/partida/estado/:idPartida`
- Método: `GET`
- Datos requeridos:
    - `token`: Token de autenticación (string)
    - `idPartida`: Id de la partida para ver su estado (int)
--- 

#### Estado de la casilla

- URL: `http://192.168.1.150:8080/casilla/estado/:idCasilla/:idPartida`
- Método: `GET`
- Datos requeridos:
    - `token`: Token de autenticación (string)
    - `idCasilla`: Id de la casilla de la partida (int)
    - `idPartida`: Id de la partida (int)
---
## Rutas para comprobar el funcionamiento del juego

---

#### Actualizar partida

- URL: `http://192.168.1.150:8080/partida/actualizar/:idPartida/:casillaSuperada`
- Método: `POST`
- Datos requeridos:
    - `token`: Token de autenticación (string)
    - `idPartida`: Id de la partida (int)
    - `casillaSuperada`: si se ha superado o no la casilla (boolean)

---

#### Comprobar la existencia de partidas pendientes

- URL: `http://192.168.1.150:8080/partida/pendiente/:idUsuario`
- Método: `GET`
- Datos requeridos:
    - `token`: Token de autenticación (string)
    - `idUsuario`: Id del usuario (int)

---

#### Comprobar victoria de la partida

- URL: `http://192.168.1.150:8080/partida/gana/:idPartida`
- Método: `GET`
- Datos requeridos:
    - `token`: Token de autenticación (string)
    - `idPartida`: Id de la partida (int)

---

#### Comprobar si hay heroes suficientes en la partida (max 3, min 1)

- URL: `http://192.168.1.150:8080/partida/heroes/:idPartida`
- Método: `GET`
- Datos requeridos:
    - `token`: Token de autenticación (string)
    - `idPartida`: Id de la partida (int)

---

#### Crear los heroes de la partida (se utiliza para la función de iniciar partida)

- URL: `http://192.168.1.150:8080/partida/crearHeroes/:idPartida`
- Método: `POST`
- Datos requeridos:
    - `token`: Token de autenticación (string)
    - `idPartida`: Id de la partida (int)

---

#### Comprobar si ya existen los heroes en la partida (se utiliza para la función de crear heroes)

- URL: `http://192.168.1.150:8080/partida/heroesCreados/:idPartida`
- Método: `GET`
- Datos requeridos:
    - `token`: Token de autenticación (string)
    - `idPartida`: Id de la partida (int)

---

#### Mostrar Heroe por su tipo

- URL: `http://192.168.1.150:8080/heroes/:tipo_prueba`
- Método: `GET`
- Datos requeridos:
    - `token`: Token de autenticación (string)
    - `tipo_prueba`: Tipo de prueba que realiza el heroe (string)

---

#### Mostar Heroe de la partida por su tipo

- URL: `http://192.168.1.150:8080/partida/sacarHeroe/:idPartida/:tipo_prueba`
- Método: `GET`
- Datos requeridos:
    - `token`: Token de autenticación (string)
    - `idPartida`: Id de la partida (int)
    - `tipo_prueba`: Tipo de prueba que realiza el heroe  (string)
---






