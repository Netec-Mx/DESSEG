# **Práctica de Seguridad en Aplicaciones Móviles: Exploración de Vulnerabilidades en Android con BlueStacks y Técnicas de Penetración**

## Objetivo de la práctica:

Al finalizar la práctica, serás capaz de:

- Instalar y configurar BlueStacks en un entorno de laboratorio para ejecutar y analizar aplicaciones móviles.
- Identificar y analizar vulnerabilidades de seguridad en la aplicación DIVA, como registros inseguros, hardcoding de credenciales, y fallos en la validación de entradas.
- Utilizar herramientas de análisis como ADB, `dex2jar` y `jd-gui` para extraer y examinar datos internos que puedan exponer información sensible o accesos no autorizados.

## Objetivo Visual 

![diagrama1](../images/cap4_0.png)

## Duración aproximada:
- 60 minutos.

## Instrucciones 

### Tarea 1. Instalacion

Paso 1. Ejecutar el archivo `BlueStacksInstaller_5.21.111.1002_native_dc6b14c4d9f7b1785bcc5c837e88652a_MzsxNSwwOzUsMTsxNSw0OzE1.exe` que se encuentra en la carpeta de archivos del laboratorio 4.

Paso 2. Hacer clic `Install now` botón que se muestra a continuación

![cap4](../images/cap_0_1.png)

Paso 3. Luego haga clic `I agree` botón que se muestra  a continuación

![cap4](../images/cap_0_2.png)


Paso 4. Después de completar la instalación, espere a que se inicie BlueStacks como se muestra a continuación

![cap4](../images/cap_0_3.png)


Paso 5. En el panel derecho, vaya al icono del `Administrador de instancias múltiples`

![cap4](../images/cap_0_4.png)

Paso 6. Seleccionar `Stop` en el reproductor de la aplicación BluStacks, haga clic en `Close`

![cap4](../images/cap_0_5.png)


Paso 7.  Dar clic en `Instance` y luego en `Fresh instance`

![cap4](../images/cap_0_6.png)
![cap4](../images/cap_0_7.png)

Paso 8. EnElija la versión de Android seleccionando la `Nougat 32-bit` y de clic en `Next`.

![cap4](../images/cap_0_8.png)

Paso 9. en `CPU cores` seleccione `Low(1 Core)`, y en  asignación de memoria seleccione `Standard (2 GB)`, y haga clic en `Download`.

![cap4](../images/cap_0_9.png)

Paso 10. Después de completar la descarga seleccione `Start` en la instancia creada (la que usa `Nougat 32-bit`).

![cap4](../images/cap_0_10.png)

Paso 11. Borrar la instancia creada por defecto seleccionando el icono de eliminar, y cuando salga una confirmación, haga clic `Delete`.

![cap4](../images/cap_0_11.png)

Paso 12. En el panel derecho, dar clic en el simbolo de Configuracion, luego haga clic en `Phone`, y en `Choose a predefined profile`, seleccione `Samsung Galaxy S10`, y de clic en `Save changes`, para finalmente ir a `Advanced` y habilitar `Android Debug Bridge (ADB)`, y seleccione `Save changes`.

![cap4](../images/cap_0_12.png)
![cap4](../images/cap_0_13.png)
![cap4](../images/cap_0_14.png)

Paso 13. Vaya a la carpeta `C:\ProgramData\BlueStacks_nxt` y abra el archivo `buestacks.conf` con un editor de texto dando clic derecho sobre ese archivo y luego a `Edit with Notepad ++`. Una vez dentro, busque la línea 102 `bst.instance.Nougat32.enable_root_access=”0”` y cambie el valor de `0` a `1`, y guarde los cambios.

![cap4](../images/cap_0_15.png)
![cap4](../images/cap_0_16.png)

Paso 15. Para que los cambios se actualicen, reinicie su computadora

![cap4](../images/cap_0_17.png)

Paso 16. Abra `BlueStacks Multi-Instance Manager`

![cap4](../images/cap_0_18.png)

Paso 17. Dar clic en `Start`

![cap4](../images/cap_0_19.png)

Paso 18. Abra la carpeta `Lab 04 - Mobile Security` y exrtaiga el arhivo de la aplicacion a usar dando clic derecho sobre `diva-beta.tar.gz` y luego a `Extract files`. 

![cap4](../images/cap_0_20.png)

Paso 19. Y de doble clic a la aplicacion `diva-beta.apk` 

![cap4](../images/cap_0_21.png)

Paso 20. Toque (haga clic) en el ícono de la aplicación DIVA para iniciar la aplicación.

![cap4](../images/cap4_20.png)
![cap4](../images/cap_0_22.png)

### Tarea 2. INSECURE LOGGING

Paso 21. Abrir una terminal y escribir el comando `adb root`

![cap4](../images/cap_0_23.png)

Paso 22. Escribir el comando `adb devices` y verificar que para `emulator-5554` el resultado sea `device`

![cap4](../images/cap_0_24.png)

Paso 23. Escribir el comando `adb shell` y luego `su`

![cap4](../images/cap_0_25.png)

Paso 24. Dentro de DIVA, ingresar a `INSECURE LOGGING`

![cap4](../images/cap_0_26.png)

Paso 25. Antes de colocar un numero de tarjeta de crédito ficticio, escribir `logcat` en el símbolo del sistema

![cap4](../images/cap_0_27.png)

Paso 26. A continuacion escriba numeros de una tarjeta de credito ficticia

![cap4](../images/cap_0_28.png)

Paso 27. Lo que es capturado por los registros del comando, haciendo que esta sea expuesta

![cap4](../images/cap_0_29.png)

### Tarea 3. HARDCODING ISSUES - PART 1

Paso 28. Ahora volver al menu principal de DIVA e ingresar a `HARDCODING ISSUES - PART 1`

![cap4](../images/cap_0_30.png)

Paso 29. A continuacion, ir al archivo de la aplicacion `diva-beta.apk`, dar click derecho y luego `Rename` para cambiar esa extension `apk` a `rar`

![cap4](../images/cap_0_31.png)

Paso 30. Aceptar los cambios

![cap4](../images/cap_0_32.png)

Paso 31. Extraer los archivos

![cap4](../images/cap_0_33.png)

Paso 32. Ingresar a la carpeta extraida y cortar el archivo `classes.dex`

![cap4](../images/cap_0_34.png)

Paso 33. Volver a la carpeta `Lab 04 - Mobile Security` y extraer el archivo `dex2jar-2.0.zip` e ingresar a la carpeta extraida

![cap4](../images/cap_0_35.png)

Paso 34. Dentro de esa carpeta es donde se pegara el archivo `classes.dex`

![cap4](../images//cap_0_36.png)

Paso 35. Abrir una nueva terminal e ingresar a la ruta usando el comando `cd` seguido de la ruta donde se pego el archivo; por ejemplo `cd C:\Users\Netec\Desktop\Lab 04 - Mobile Security\dex2jar-2.0`

![cap4](../images/cap_0_37.png)

Paso 36. Ejecutar el comando `d2j-dex2jar classes.dex`

![cap4](../images/cap_0_38.png)

Paso 37. Ahora vera el archivo `classes-dex2jar.jar`

![cap4](../images/cap_0_39.png)

Paso 38.Abrir `jd-gui`

![cap4](../images/cap_0_40.png)

Paso 39. Abrir el archivo que se convirtió anteriormente dentro de la GUI

![cap4](../images/cap_0_41.png)
![cap4](../images/cap_0_42.png)

Paso 40. Abrir `jakhar.aseem.diva`

![cap4](../images/cap_0_43.png)

Paso 41. Seleccionar `HardcodeActivity.class` y ahi encontrara `vendorsecretkey` y el memsaje `"Access granted! See you von the other side :)"`

![cap4](../images/cap_0_44.png)

Paso 42. Escribir esa contrasena robada en DIVA

![cap4](../images/cap_0_45.png)

### Tarea 4. INPUT VALIDATION ISSUES – PART 1

Paso 43. Volver a DIVA y abrir el `INPUT VALIDATION ISSUES – PART 1`

![cap4](../images/cap_0_46.png)

Paso 44. Colocar el comando de ataque `' OR '1' == '1`

![cap4](../images/cap_0_47.png)

### Tarea 4. INPUT VALIDATION ISSUES – PART 2

Paso 45. Abrir el `INPUT VALIDATION ISSUES – PART 2`

![cap4](../images/cap_0_48.png)

Paso 46. Verificar que se puede acceder a conexiones colocando `https://www.google.com`

![cap4](../images/cap_0_49.png)

Paso 47. Con ello verificado, es posible obtener el contenido del archivo de configuración llamado hosts, que se encuentra en el directorio /etc en sistemas operativos tipo Unix/Linux colocando la ruta `file:////etc/hosts` y dando clic a `VIEW`.

![cap4](../images/cap_0_50.png)

### Tarea 5. ACCESS CONTROL ISSUSES - PART 1

Paso 48. En DIVA ingresar a `ACCESS CONTROL ISSUSES - PART 1`

![cap4](../images/cap_0_51.png)

Paso 49. Abrir una nueva terminal y escribir el comando `adb root`

![cap4](../images/cap_0_23.png)

Paso 50. Escribir el comando `adb devices` y verificar que para `emulator-5554` el resultado sea `device`

![cap4](../images/cap_0_24.png)

Paso 51. Escribir el comando `adb shell` y luego `su`

![cap4](../images/cap_0_25.png)


Paso 52. Ejecutra el comando `logcat` en el símbolo del sistema

![cap4](../images/cap_0_27.png)

Paso 50. En DIVA dar clic `VIEW API CREDENTIALS`

![cap4](../images/cap_0_52.png)

Paso 51. Y se vera la credencial de la API tanto en la aplicacion (proceso legal), y en la consola de comandos el nombre de la actividad.

![cap4](../images/cap_0_54.png)
![cap4](../images/cap_0_53.png)

Paso 52. Y finalmente para ver la informacion, abrir una nueva terminal y ejecutar `adb shell am start -n jakhar.aseem.diva/.APICredsActivity`

![cap4](../images/cap_0_55.png)

### Resultado esperado

#### Tarea 2.

![cap4](../images/cap_0_29.png)

#### Tarea 3.

![cap4](../images/cap_0_45.png)


#### Tarea 4.

![cap4](../images/cap_0_47.png)

#### Tarea 5.

![cap4](../images/cap_0_55.png) 
