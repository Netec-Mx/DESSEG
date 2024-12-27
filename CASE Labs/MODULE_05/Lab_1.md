# Preventing Applications from Unauthorized Access Atacks 

## Objetivo de la práctica:

Identificar y solucionar una vulnerabilidad de omisión de autorización en la aplicación mediante la implementación de verificaciones de acceso a nivel de funciones, garantizando que solo usuarios con privilegios administrativos puedan acceder a la consola de administración.

## Duración aproximada:

- 10 minutos.

## Instrucciones 

Paso 1. Iniciar sesión con las siguientes credenciales de usuario que son válidas:

    Nombre de usuario: admin

    Contraseña: admin123


Paso 2. Hacer clic en el menú `CHECKOUT`, y será redirigido a la página de **Carrito de Compras**. Luego haz clic en el menú `PRODUCTINFO`.

- Resultado: Serás redirigido a la página de bienvenida del administador (`Welcome Admin`) que solo es accesible para el administador con privilegios administrativos.

Paso 3. Haz clic en el menú `Logout`.


Paso 4. Inicia sesión nuevamente con las siguientes credenciales:

    Nombre de usuario: user
    Contraseña: user123

Paso 5. Haz clic en el menú `CHECKOUT`.
Serás redirigido a la página de `Carrito de Compras`. Luego haz clic en el menú PRODUCTINFO.

- Resultado: Aún podrás acceder a la página de administrador sin tener privilegios administrativos.

- La aplicación no verifica el acceso a nivel de funciones al redirigir a la página de la consola de administración. Esto permite que la página se cargue directamente, dejando la aplicación vulnerable a un ataque de omisión de autorización.

**Confirmación del uso de acceso incorrecto a nivel de funciones:**

Ve a la pestaña ProdInfo.jsp, línea n.º 85.
Para prevenir el ataque de omisión de autorización, implementa una verificación de acceso a nivel de funciones adecuada. Ve a la línea n.º 87 en ProdInfo.jsp 

![imagen resultado](../images/img1.png)


E inserta las siguientes líneas de código:

`if(!(session.getAttribute("useracc").toString()).equals("admin"))
{
    session.invalidate();
    response.sendRedirect("Login.jsp");
}`

![imagen resultado](../images/img2.png)

Paso 6. Haz clic en el botón **Save** en la parte superior del editor para guardar los cambios.

![imagen resultado](../images/img3.png)

Paso 7. Repite los pasos 4 y 5.

- Resultado: Esta vez, la aplicación no permitirá que el usuario omita el mecanismo de autenticación y no podrás acceder a la página `PRODUCTINFO`.
- Esto demuestra que implementar una verificación adecuada de acceso a nivel de funciones puede prevenir la omisión de autenticación en la aplicación.

Paso 8. Haz clic en el botón Reset para restaurar el laboratorio al estado anterior y haz clic en el botón `OK` del mensaje emergente `¡Restablecimiento exitoso!`.

Paso 9. Haz clic en el botón `HOME` para volver a la página principal.


