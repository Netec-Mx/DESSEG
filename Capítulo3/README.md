# Laboratorio: Pruebas de seguridad en aplicaciones: SAST y DAST con configuración de Burp Suite

## Objetivo de la práctica:

Al finalizar la práctica, serás capaz de:

- Comprender y aplicar técnicas de análisis estático de seguridad (SAST) utilizando _VisualCodeGrepper_.
- Instalar y configurar Burp Suite junto con el navegador para realizar pruebas de seguridad.
- Utilizar Burp Suite para realizar análisis dinámico de seguridad (DAST) en aplicaciones de prueba como Mutillidae, identificando vulnerabilidades en la aplicación de destino.

## Objetivo visual:

![diagrama1](../images/cap3_0.png)

## Duración aproximada:

- 60 minutos.

## Tabla de ayuda:

| Enlace |
| --- |
| [CaseLabs](./CASE Labs) |

## Instrucciones:

### Tarea 1. Realizar el Análisis Estático (SAST).

Paso 1. Descarga la herramienta que utilizarás. Para ello, abre el archivo `VCG-Setup.msi` ubicada en: `CASE Labs` > `Module 09: Static and Dynamic Application Security Testing` > `Lab 01: Performing Static Application Security Testing (SAST)`.

![cap3](../images/cap3_0_0.png)

<br><br>
![cap3](../images/cap3_0_1.png)

Paso 2. Da clic en `Next`.

![cap3](../images/cap3_1.png)
![cap3](../images/cap3_0_2.png)

Paso 3. Haz clic a `Next`.

![cap3](../images/cap3_3.png)

Paso 4. Da clic en `Close`.

![cap3](../images/cap3_4.png)

Paso 5. Abre la aplicación descargada dando doble clic al ícono.

![cap3](../images/cap3_5.png)

Paso 6. Dirígete a la ventana `Settings` y selecciona el lenguaje `Java`.

![cap3](../images/cap3_6.png)

Paso 7. Descarga el archivo con el que trabajarás, el cual tiene como nombre `SampleWebsite.zip`. Posteriormente, descomprímelo en una carpeta con una ruta de fácil acceso (un ejemplo podría ser en la carpeta de **descargas**).

![cap3](../images/cap3_0_3.png)

Paso 8. Selecciona `File` en la barra de menús, y luego haz clic en `New Target Directory`.

![cap3](../images/cap3_7.png)

Paso 9. Selecciona la carpeta descomprimida y da clic en `OK`.

![cap3](../images/cap3_8.png)

Paso 10. Selecciona `Scan`, el cual está ubicado en la barra de menús, y luego haz clic en `Full Scan`.

![cap3](../images/cap3_9.png)

Paso 11. De esta forma, se obtendrá toda la lista de vulnerabilidades en la pestaña `Results`. Una vez detectadas las vulnerabilidades, cierra la ventana de VCG.

![cap3](../images/cap3_10.png)

### Tarea 2. Análisis Dinámico ().

Paso 12. Ingresa al siguiente [enlace](https://portswigger.net/burp/communitydownload) y seleccionar `Go straight to downloads`.

![cap3](../images/cap3_11.png)

Paso 13. Selecciona `Download`.

![cap3](../images/cap3_12.png)

Paso 14. Abre el archivo descargado.

![cap3](../images/cap3_13.png)

Paso 15. Selecciona `Yes, update the existing installation` y luego haz clic en `Next`.

![cap3](../images/cap3_14.png)

Paso 16. Selecciona `Finish`.

![cap3](../images/cap3_15.png)

Paso 17. Desde el menú de inicio, abre `Burp Suite`.

![cap3](../images/cap3_16.png)

Paso 18. Acepta los términos y condiciones.

![cap3](../images/cap3_17.png)

Paso 19. Selecciona `Next`.

![cap3](../images/cap3_18.png)

Paso 20. Selecciona `Start Burp`.

![cap3](../images/cap3_19.png)

Paso 21. Dirígete a la pestaña “Proxy” y selecciona `Open browser`.

![cap3](../images/cap3_20.png)

Paso 22. Una vez en el nuevo navegador abierto (tiene el logo de Google Chrome, pero ahora es azul), coloca la siguiente dirección de enlace: `127.0.0.1:8181/mutillidae`.

![cap3](../images/cap3_21.png)

### Tarea 3. Verificar referencias inseguras a objetos.

Paso 23. Para demostrar la detección de la vulnerabilidad de referencias directas a objetos inseguros, selecciona: `OWASP 2013` > `A4 - Referencias directas inseguras a objetos` > `Visor de archivos de texto`.

![cap3](../images/cap3_22.png)

Paso 24. Regresa a Burp Suite y activa la opción de intercepción, ubicada en la pestaña `Proxy`.

![cap3](../images/cap3_23.png)

Paso 25. Dirígete al navegador y selecciona `View File`.

![cap3](../images/cap3_24.png)

Paso 26. Burp Suite intercepta la solicitud que contiene un nombre de archivo de texto seleccionado.

![cap3](../images/cap3_25.png)

Paso 27. Para detectar si la aplicación tiene la vulnerabilidad de referencia de objeto indirecto, en Burp Suite, edita la referencia del archivo de texto existente intercambiándolo por `index.php` y haz clic en `Forward`.

![cap3](../images/cap3_26.png)

Paso 28. Regresa al navegador y verifica que la página es vulnerable a referencias de objetos indirectos, haciendo que este expuesto a los usuarios sin ningún otro control de acceso.

![cap3](../images/cap3_27.png)

### Tarea 4. Verificar la detección de vulnerabilidad de inyección SQL.

Paso 29. Apaga la intercepción en Burp Suite.

![cap3](../images/cap3_28.png)

Paso 30. Regresa al navegador y selecciona: `Owasp 2013` > `A1 - Inyeccion SQL` > `SQLi - Omision de autenticacion` > `Login`.

![cap3](../images/cap3_29.png)

Paso 31. En el nombre de usuario, coloca una comilla simple (`'`) y haz clic en `Login`.

![cap3](../images/cap3_30.png)

Paso 32. Esto activa una excepción que revela información sobre la estructura interna de la consulta de la base de datos utilizada en la aplicación.

![cap3](../images/cap3_31.png)
![cap3](../images/cap3_32.png)

Paso 33. Ahora, construye la consulta de inyección SQL de tal manera que la base de datos subyacente siempre se devuelva como verdadera después de la ejecución. Para ello, ingresa la siguiente declaración SQL (sin ningún espacio) en el nombre de usuario y haz clic al `Login`: `'or '1'='1'#`.

![cap3](../images/cap3_33.png)

### Tarea 5. Verificar ataques de fuerza bruta.

Paso 34. Para demostrar la detección de la vulnerabilidad de secuencias de comandos entre sitios, selecciona: `OWASP 2013` > `A2 Autenticación rota y gestión de sesiones` > `Omisión de autenticación` > `Mediante fuerza bruta` > `Login`.

![cap3](../images/cap3_34.png)

Paso 35. Selecciona `Logout.

![cap3](../images/cap3_35.png)

Paso 36. Activa la intercepción en Burp Suite.

![cap3](../images/cap3_36.png)

Paso 37. En el nombre de usuario, coloca: `Administrator` y en la contraseña: `password123` y da clic en **Login**. Esta contraseña es incorrecta y fue proporcionada intencionalmente para `Administrator` como nombre de usuario.

![cap3](../images/cap3_37.png)

Paso 38. En la respuesta intereceptada en Burp Suite, da clic derecho y selecciona `Send to Intruder`.

![cap3](../images/cap3_38.png)

Paso 39. Dirígete a la sección de `Intruder` y selecciona `Clear §`.

![cap3](../images/cap3_39.png)

Paso 40. Cambia el tipo de ataque por `Cluster Bomb`.

![cap3](../images/cap3_40.png)

Paso 41. Selecciona `Administrator` y da clic en `Add §`. Posteriormente, haz lo mismo con `password123`.

![cap3](../images/cap3_41.png)

Paso 42. Dirígete a la pestaña `Payloads` y selecciona que `Payload position` se encuentre en 1.

![cap3](../images/cap3_42.png)

Paso 43. En la sección de `Payload configuration`, escribe  los posibles nombres para el administrador y presiona `Enter` en el teclado; estos son `Admin` y `Administrator`. 

![cap3](../images/cap3_43.png)
![cap3](../images/cap3_44.png)

Paso 44. Cambia el `Payload position` para que se encuentre en 2 y en la sección de `Payload configuration`, escribe las posibles contraseñas: `test123`, `test@123` y `password123`. 

![cap3](../images/cap3_45.png)

Paso 45. Dirígete a la pestaña de `Settings` y la sección `Grep - Match`, da clic en `Clear` para limpiar la lista de campos existentes.

![cap3](../images/cap3_46.png)

Paso 46. Escribe `Incorrect` y haz clic en `Add`.

![cap3](../images/cap3_47.png)

Paso 47. Selecciona `Start Attack`.

![cap3](../images/cap3_48.png)

Paso 48. De todos los resultados mostrados, el único que no tiene una respuesta incorrecta resultan ser las credenciales. Esto infiere que ha forzado con éxito el nombre de usuario y la contraseña.

![cap3](../images/cap3_49.png)

Paso 49. Finalmente, apaga la intercepción en Burp Suite.

![cap3](../images/cap3_50.png)

Paso 50. Intenta iniciar sesión con el nombre de usuario identificado (`Administrator`) y la contraseña (`test@123`).

![cap3](../images/cap3_51.png)

### Resultado esperado:

#### Tarea 1.

![cap3](../images/cap3_10.png)

#### Tarea 3.

![cap3](../images/cap3_27.png)

#### Tarea 4.

![cap3](../images/cap3_33.png)

#### Tarea 5.

![cap3](../images/cap3_51.png)

---

#### Para regresar al índice general, da clic [aquí](./README.md).
