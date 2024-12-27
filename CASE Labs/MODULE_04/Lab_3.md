# Examining the Importance of Whitelist-based Input Validation

## Objetivo de la práctica:

Identificar las limitaciones de la validación basada en listas negras y mitigar vulnerabilidades de inyección SQL implementando un enfoque de validación basado en listas blancas, asegurando que solo se permitan entradas seguras y predefinidas.

## Duración aproximada:
- 5 minutos.

## Instrucciones 

Paso 1. Inicia sesión con las siguientes credenciales válidas:

    Nombre de usuario: test
    Contraseña: test1

Paso 2. Haz clic en el menú `LOGOUT`.

Paso 3. Intenta iniciar sesión utilizando los siguientes datos de entrada de inyección SQL:

    Nombre de usuario: ' or '1'='1
    Contraseña: test1

Resultado:
- Esto indica que, antes de procesar, la entrada del usuario no se valida correctamente.

**Confirmación del mecanismo de validación:**

Ve a la pestaña `LoginController.jsp`, líneas n.º 81-90.

Verás que la entrada se valida utilizando un enfoque de lista negra (Blacklisting Validation Approach), verificando contra ciertos caracteres "maliciosos".

**Problema con el enfoque de lista negra:**

- El problema del enfoque de lista negra es que verifica la entrada solo contra un conjunto limitado de caracteres no permitidos.
- Si un atacante usa una entrada "maliciosa" que no está en la lista negra, puede eludir fácilmente la validación.
- Por lo tanto, es una mala práctica implementar validación basada en listas negras.

Paso 4. Para implementar una validación basada en listas blancas (Whitelist-based Input Validation), ve a la pestaña `LoginController.jsp` y reemplaza el código de la función validateUserName() en las líneas n.º 81-89 con el siguiente código:

    Pattern p = Pattern.compile("^[a-zA-Z0-9_@.-]*$");
    Matcher m = p.matcher(uname);
    boolean result = m.matches();
    return result;

Paso 5. Haz clic en el botón `Save` en la parte superior del editor para guardar los cambios.

Paso 6. Intenta iniciar sesión nuevamente utilizando los datos de entrada de inyección SQL indicados en el paso 3.

Resultado:
- Esta vez, la aplicación validará correctamente la entrada del usuario, permitiendo solo los caracteres definidos.

Paso 7. Haz clic en el botón `Reset` para restaurar el laboratorio al estado anterior y haz clic en `OK` en el mensaje emergente que indica `¡Restablecimiento exitoso!`.