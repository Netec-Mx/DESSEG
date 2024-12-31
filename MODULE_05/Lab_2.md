# Preventing Application from Authorization Bypass Attacks

## Objetivo de la práctica:

Demostrar el riesgo de exponer datos sensibles en la URL mediante cadenas de consulta. Además de implementar variables de sesión para proteger información confidencial como nombres de usuario y contraseñas y verificar que las credenciales del usuario no se transfieran a través de la URL tras la implementación de las medidas de seguridad.

## Duración aproximada:

- 10 minutos.

## Instrucciones 

Paso 1. Inicia sesión con credenciales de usuario válidas.

    Nombre de usuario: user
    Contraseña: pass

Paso 2. Haz clic derecho en el botón `CONTINUE LOGIN` y selecciona `Copiar dirección del enlace`.

Paso 3. Haz clic en el botón `CONTINUE LOGIN`.

- Resultado: Has iniciado sesión como USER.

Paso 4. Haz clic en el botón `Logout`.

Paso 5. Abre **Firefox**, pega la dirección del enlace del botón CONTINUE LOGIN copiada en el paso 2 y presiona Enter.

- Resultado: Has iniciado sesión como `USER`.
- La aplicación utiliza la cadena de consulta (querystring) para transferir el nombre de usuario y la contraseña. Estas cadenas de consulta se añaden a la URL, lo que permite copiarlas fácilmente.

**Confirmación del uso de la cadena de consulta para transferir datos sensibles:**

Ve a la pestaña `CheckLogin.jsp`, línea n.º 50.

![imagen resultado](../images/img4.png)
![imagen resultado](../images/img5.png)

Notarás que el nombre de usuario y la contraseña se añaden a la URL como una cadena de consulta (querystring).

**Prevención del uso de cadenas de consulta para datos sensibles:**

Para evitar que la URL contenga datos sensibles como nombre de usuario y contraseña, utiliza variables de sesión para almacenar esta información.

Ve a la línea n.º 49 en CheckLogin.jsp e inserta el siguiente código:

    session.setAttribute("pwd", pwd);
    session.setAttribute("user", user);

![imagen resultado](../images/img6.png)

Paso 6. Ahora, ve a la pestaña Home.jsp y reemplaza las líneas n.º 32-43

![imagen resultado](../images/img6_2.png)

Con el siguiente código:

    if((session.getAttribute("user")!=null)&& (session.getAttribute("pwd")!=null))
    {
        userName=session.getAttribute("user").toString();
        userpass=session.getAttribute("pwd").toString();
        session.setAttribute("username", userName); 
    }
    else{
        response.sendRedirect("Login.jsp");
    }

![imagen resultado](../images/img7.png)

Paso 7. Haz clic en el botón `Save` en la parte superior del editor para guardar los cambios.

Paso 8. Repite los pasos del 1 al 5.

- Resultado: Esta vez no serás redirigido a la página principal (Home) porque las credenciales del usuario no se envían junto con la URL como una cadena de consulta (querystring).

Paso 9. Haz clic en el botón `Reset` para restaurar el laboratorio al estado anterior y haz clic en OK en el mensaje emergente que indica `¡Restablecimiento exitoso!`.