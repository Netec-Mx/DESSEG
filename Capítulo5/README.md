# **Práctica de Seguridad en Aplicaciones Web: Uso de Postman y Burp Suite para Pruebas de Vulnerabilidades** 

## Objetivo de la práctica:

Al finalizar la práctica, serás capaz de:

- Utilizar Postman para crear cuentas, configurar ambientes de pruebas, y manipular variables para simular interacciones en un entorno web.
- Realizar acciones de prueba de seguridad en aplicaciones web, incluyendo la escalación de privilegios, eliminación de comentarios, y ataques de fuerza bruta con Burp Suite para identificar y explotar vulnerabilidades.

## Objetivo Visual 

![diagrama1](../images/cap5_0.png)

## Duración aproximada:
- 60 minutos.

## Instrucciones 

### Tarea 1. Configuracion
Paso 1. Dar doble clic al logo de `Docker` que se encuentra en la barra de tareas

![cap5](../images/cap5_1.png)

Paso 2. En la seccion de `Actions`, dar clic al boton que se indica para activar esos contenedores

![cap5](../images/cap5_2.png)

Paso 3. Verificar que todos los contenedores se encuentren ejecutandose

![cap5](../images/cap5_3.png)

Paso 4. Abrir Google Chrome y verificar el Frontend y el Backend en la seccion de favoritos

![cap5](../images/cap5_4.png)

Paso 5. Abrir `Postman` en la barra de tareas

![cap5](../images/cap5_5.png)

Paso 6. Seleccionar `Create Account`

![cap5](../images/cap5_6.png)

Paso 7. Registrase con un correo electronico

![cap5](../images/cap5_7.png)

Paso 8. Dar clic en `Import`

![cap5](../images/cap5_8.png)

Paso 9. Seleccionar `folders`

![cap5](../images/cap5_9.png)

Paso 10. Ir a la ruta `C:\Labs` y dar clic a `Upload`

![cap5](../images/cap5_10.png)

Paso 11. Dar clic a `Enviroments` y luego a `+`

![cap5](../images/cap5_11.png)

Paso 12. Luego colocar el nombre `CAPITAL` en la seccion que se muestra a continuacion, y colocar como nombre de Variable `APIURL`. En Initial value colocar `localhost:8000/api` y dar clic a `Save`

![cap5](../images/cap5_12.png)

Paso 13. Ir a Google Chrome e ingresar al frontend, para luego dar clic a `Sign up` para registrarse (no tienen que ser credenciales reales, se recomienda que sean faciles de usar)

![cap5](../images/cap5_13.png)

Paso 15. Volver a Postman y en la seccion de `Collections` activar el ambiente `Capital` que se creo anteriormente como se ve en la imagen

![cap5](../images/cap5_14.png)

### Tarea 2. Romper permisos de administacion

Paso 16. Desplegar la seccion `Auth` e ingresar a `Login`

![cap5](../images/cap5_15.png)

Paso 17. En la seccion de `Body`, colocar el correo electronico y la contraseña que se crearon anteriormente

![cap5](../images/cap5_16.png)

Paso 18. Dar clic en `Send` y luego se obtendra un valor de token en la salida, copiar dicho valor.

![cap5](../images/cap5_17.png)

Paso 19. Volver a la seccion `Enviroments` y crear una variable llamada `token`, cuyo `Initial value` se debera pegar el valor del token que se copio anteriomente 

![cap5](../images/cap5_18.png)

Paso 20. Ir a `Update User` e ingresar a la seccion `Body`

![cap5](../images/cap5_19.png)

Paso 21. Cambiar el valor a que ahora diga `"admin":"true"` y dar clic a `Send` para verificar que se cambio dicho valor 

![cap5](../images/cap5_20.png)

### Tarea 3. Eliminar comentarios

Paso 22. Ir al frontend y buscar la publicacion llamada `THIS IS MY AWESOME POST!`

![cap5](../images/cap5_21.png)

Paso 23. Al ingresar a esa publicacion se vera que ya se realizo un comentario previamente

![cap5](../images/cap5_22.png)

Paso 24. Abrir postman e ir a `Articles, Favorite, Comments`, ingresar a `All Articles` y dar clic a `Send`

![cap5](../images/cap5_23.png)

Paso 25. En los resultados, buscar la publicacion que se reviso anteriormente (linea 188) y copiar el valor del `slug`

![cap5](../images/cap5_24.png)

Paso 26. Ir al siguiente enlace para codificar la cadena en URL: `https://cyberchef.org/` y en el buscador colocar `URL` para seleccionar dando doble click a `URL Encode`

![cap5](../images/cap5_25.png)

Paso 27. En la seccion `Input` colocar el valor del `slug` que se coppio anteriomente, y copiar el valor de `Output` 

![cap5](../images/cap5_26.png)

Paso 28. Volver a Postman y en la seccion de `Enviroments` crear una nueva variable llamada `slug`, la cual debera tener como `Initial value` el valor codificado que se copio anteriormente.

![cap5](../images/cap5_27.png)

Paso 29. Ahora abrir `All Comments for Article` y dar click a `Send`, alli vera el valor del `id` del comentario del cual se copio su `slug`

![cap5](../images/cap5_28.png)

Paso 30. Ir a la seccion `Delete Comment for Article` y se vera que se puede colocar un valor de id de algun comentario

![cap5](../images/cap5_29.png)

Paso 31. Cambiar dicho valor por el del `id` que se obtuvo anteriormente, que es `1`, dar clic a send y con ello se habra eliminado el comentario

![cap5](../images/cap5_30.png)

Paso 32. Recargar la pagina del frontend donde se encontraba la publicacion, y se vera que el comentario fue eliminado

![cap5](../images/cap5_31.png)

### Tarea 4. Ataque de fuerza bruta

Paso 33. Volver a la pagina principal y buscar la publicacion denominada `My favourites pokemon!`

![cap5](../images/cap5_32.png)

Paso 34. Ahi se vera una lista de gustos personales de un ususario, que son un indicador usado por los atacantes para probar posibles contraseñas

![cap5](../images/cap5_33.png)

Paso 35. Guardar todo ese texto en un bloc de notas colocando uno debajo de otro

    flygon
    luxray
    garchomp
    gyarados
    absol
    ninetales
    torterra
    komala
    lurantis
    charizard
    gengar
    arcanine
    bulbasaur
    dragonite
    Blaziken
    snorlax
    Mudkip
    Jigglypuff
    ninetals
    squirtle

![cap5](../images/cap5_34.png)

Paso 36. Volver a abrir Burp Suite, y una vez abierto dar clic a `Next` y luego a `Start Burp`

![cap5](../images/cap5_36.png)

Paso 37. Ir a `Proxy` y dar clic a `Proxy settings`

![cap5](../images/cap5_37.png)

Paso 38. En la seccion `Proxy listeners`, seleccionar el puerto por defecto y dar clic a `Edit`

![cap5](../images/cap5_38.png)

Paso 39. Cambiar `Bind to port` a `8081`, y en `Specific address` desplegar su barra de opciones para seleccionar la `127.0.0.1` y luego presionar `OK`

![cap5](../images/cap5_39.png)

Paso 40. Dar clic en el recuadro debajo de `Running` para que el puerto se active y cerrar la configuracion 

![cap5](../images/cap5_40.png)

Paso 41. Ir a Postman y dar clic al icono de configuracion para luego dar clic a `Settings`

![cap5](../images/cap5_41.png)

Paso 42. Ir a la seccion `Proxy` para activar la opcion `Use custom proxy configuration` colocando los valores en `Proxy server` en `127.0.0.1` y `8081` para que la intercepcion de Burp Suite este conectada a las llamdas que se haran en Postman.

![cap5](../images/cap5_42.png)

Paso 43. Volver a Burp Suite y en la seccion de `Proxy` activar la intercepcion

![cap5](../images/cap5_43.png)

Paso 44. En Postman, ir a `Auth` y seleccionar `Login`, al dar clic en `Send`, dichos valores seran interceptados

![cap5](../images/cap5_44.png)

Paso 45. Enviar dicha `Request` interceptada al intruder dando clic derecho sobre ella y luego a `Send to Intruder`

![cap5](../images/cap5_45.png)

Paso 46. Ir al `Intruder` y seleccionar la contraseña (en este caso `123`, pero seleccionar la que usted creo) y dar clic en `Add §` 

![cap5](../images/cap5_46.png)

Paso 47. Modificar el valor del `email` al del ususario al que se le realizara el ataque: `Pikachu@checkmarx.com`

![cap5](../images/cap5_47.png)

Paso 48. Ir a Payloads y dar clic a `Load...`

![cap5](../images/cap5_48.png)

Paso 49. Seleccionar el archivo de texto donde se encuentran todas las posibles contraseñas que se copiaron de la publicacion del usuario y dar clic a `Open`

![cap5](../images/cap5_49.png)

Paso 50. Una vez se encuentren cargados, dar clic a `Start attack`

![cap5](../images/cap5_50.png)

Paso 51. Se vera que hay un valor de `Status code` distinto a los demas (`200`) 

![cap5](../images/cap5_51.png)

Paso 52. Al revisarlo, se encontrara con las credenciales de dicho ususario aprovechando esa brecha de seguridad al exponer sus posibles contraseñas en un foro publico

![cap5](../images/cap5_52.png)

### Resultado esperado

#### Tarea 2.

![cap5](../images/cap5_20.png)

#### Tarea 3.

![cap5](../images/cap5_31.png)

#### Tarea 4.

![cap5](../images/cap5_52.png)
