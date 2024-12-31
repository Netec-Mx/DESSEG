# Preventing Applications from SQL Injection Attack

## Objetivo de la práctica:

Identificar y mitigar vulnerabilidades de inyección SQL mediante la implementación de consultas SQL parametrizadas, garantizando que los datos de entrada no comprometan el mecanismo de autenticación de la aplicación.

## Duración aproximada:
- 5 minutos.

## Instrucciones 

Paso 1. Inicia sesión con credenciales de usuario válidas:

    Nombre de usuario: test
    Contraseña: test1

Paso 2. Haz clic en `LOGOUT` desde el menú.

Paso 3. Intenta iniciar sesión utilizando los siguientes datos de entrada de inyección SQL:

    Nombre de usuario: ' or '1'='1
    Contraseña: ' or '1'='1

Resultado:
- Esto indica que la aplicación es vulnerable a ataques de inyección SQL.
- La vulnerabilidad se debe al uso de consultas SQL no parametrizadas.

**Confirmación de la vulnerabilidad a inyección SQL:**

- Ve a la pestaña `LoginController.jsp`, líneas n.º 21-22.

- Encontrarás el uso de una consulta SQL no parametrizada.

![imagen resultado](../ImagesLabs/img15.png)

Paso 4. Para prevenir la inyección SQL, ve a la pestaña `LoginController.jsp`, líneas n.º 21-23, y reemplaza la consulta SQL no parametrizada con la siguiente consulta SQL parametrizada:

    PreparedStatement ps = con.prepareStatement(
        "select * from ecempinfo where uname=? and pwd=?");
    ps.setString(1, uname);
    ps.setString(2, pwd);
    ResultSet rs = ps.executeQuery();

![imagen resultado](../images/img16.png)

Paso 5. Haz clic en el botón `Save` en la parte superior del editor para guardar los cambios.

Paso 6. Intenta iniciar sesión nuevamente utilizando los datos de entrada de inyección SQL indicados en el paso 3.

Resultado: 
- Esta vez, la aplicación no permitirá al usuario eludir el mecanismo de autenticación.
- Esto demuestra que el uso de consultas SQL parametrizadas puede prevenir ataques de inyección SQL en la aplicación.

Paso 7. Haz clic en el botón `Reset` para restaurar el laboratorio al estado anterior y haz clic en `OK` en el mensaje emergente que indica `¡Restablecimiento exitoso!`.
