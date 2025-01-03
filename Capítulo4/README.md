# Laboratorio: Seguridad en aplicaciones móviles: Exploración de vulnerabilidades en Android con BlueStacks y técnicas de penetración

## Objetivo de la práctica:

Al finalizar la práctica, serás capaz de:

- Instalar y configurar BlueStacks en un entorno de laboratorio para ejecutar y analizar aplicaciones móviles.
- Identificar y analizar vulnerabilidades de seguridad en la aplicación DIVA, como registros inseguros, hardcoding de credenciales, y fallos en la validación de entradas.
- Utilizar herramientas de análisis como ADB, `dex2jar` y `jd-gui` para extraer y examinar datos internos que puedan exponer información sensible o accesos no autorizados.

## Objetivo visual:

![diagrama1](../images/cap4_0.png)

## Duración aproximada:

- 60 minutos.

## Instrucciones:

### Tarea 1. Instalación.

Paso 1. Ejecuta el archivo `BlueStacksInstaller_5.21.111.1002_native_dc6b14c4d9f7b1785bcc5c837e88652a_MzsxNSwwOzUsMTsxNSw0OzE1.exe`, el cual se encuentra en la carpeta de archivos del laboratorio 4.

Paso 2. Haz clic en `Install now`, botón que se muestra a continuación:

![cap4](../images/cap_0_1.png)

Paso 3. Después, haz clic `I agree`, el cual es el botón que se muestra a continuación:

![cap4](../images/cap_0_2.png)

Paso 4. Posterior a completar la instalación, espera a que se inicie BlueStacks, tal como puedes observar en la siguiente imagen:

![cap4](../images/cap_0_3.png)

Paso 5. En el panel derecho, dirígete al ícono del `Administrador de instancias múltiples`.

![cap4](../images/cap_0_4.png)

Paso 6. Selecciona `Stop` en el reproductor de la aplicación BluStacks y haz clic en `Close`.

![cap4](../images/cap_0_5.png)

Paso 7. Da clic en `Instance` y, posteriormente, en `Fresh instance`.

![cap4](../images/cap_0_6.png)
![cap4](../images/cap_0_7.png)

Paso 8. Elige la versión de Android seleccionando la `Nougat 32-bit` y da clic en `Next`.

![cap4](../images/cap_0_8.png)

Paso 9. En `CPU cores` selecciona `Low(1 Core)` y en asignación de memoria, `Standard (2 GB)`. Finalmente, haz clic en `Download`.

![cap4](../images/cap_0_9.png)

Paso 10. Después de completar la descarga, selecciona `Start` en la instancia creada (la que usa `Nougat 32-bit`).

![cap4](../images/cap_0_10.png)

Paso 11. Elimina la instancia creada por defecto. Para ello, selecciona el ícono de eliminar y, cuando aparezca la confirmación, haz clic en `Delete`.

![cap4](../images/cap_0_11.png)

Paso 12. En el panel derecho, haz clic en el ícono de **Configuración**. Luego, selecciona `Phone` y elige la opción `Choose a predefined profile`. A continuación, selecciona `Samsung Galaxy S10` y haz clic en `Save changes`. Finalmente, ve a la sección `Advanced`, habilita la opción `Android Debug Bridge (ADB)` y guarda los cambios haciendo clic en `Save changes`.

![cap4](../images/cap_0_12.png)
![cap4](../images/cap_0_13.png)
![cap4](../images/cap_0_14.png)

Paso 13. Accede a la carpeta `C:\ProgramData\BlueStacks_nxt` y abre el archivo `buestacks.conf` con un editor de texto. Para hacerlo, haz clic derecho sobre ese archivo y selecciona la opción `Edit with Notepad ++`. Una vez dentro, localiza la línea 102: `bst.instance.Nougat32.enable_root_access=”0”`. Cambia el valor de `0` a `1`. Finalemnte, guarda los cambios.

![cap4](../images/cap_0_15.png)
![cap4](../images/cap_0_16.png)

Paso 14. Reinicia tu computadora para que los cambios se actualicen.

![cap4](../images/cap_0_17.png)

Paso 15. Abre `BlueStacks Multi-Instance Manager`.

![cap4](../images/cap_0_18.png)

Paso 16. Da clic en `Start`.

![cap4](../images/cap_0_19.png)

Paso 17. Abre la carpeta `Lab 04 - Mobile Security` y extrae el archivo de la aplicación que se utilizará. Para hacerlo, haz clic derecho sobre `diva-beta.tar.gz` y selecciona la opción `Extract files`.

![cap4](../images/cap_0_20.png)

Paso 18. Haz doble clic en la aplicación `diva-beta.apk` para abrirla.

![cap4](../images/cap_0_21.png)

Paso 19. Toca o haz clic en el ícono de la aplicación **DIVA** para iniciarla.

![cap4](../images/cap4_20.png)
![cap4](../images/cap_0_22.png)

### Tarea 2. `INSECURE LOGGING`.

Paso 20. Abre una terminal y escribe el siguiente comando:

```
adb root
```

![cap4](../images/cap_0_23.png)

Paso 21. Escribe el comando siguiente en la terminal:
```
adb devices
```

Verifica que el resultado correspondiente a `emulator-5554` sea `device`.

![cap4](../images/cap_0_24.png)

Paso 22. En la terminal, escribe el siguiente comando:

```
adb shell
``` 

Luego, ingresa el comando:

```
su
```

![cap4](../images/cap_0_25.png)

Paso 23. En la aplicación DIVA, navega a la sección `INSECURE LOGGING`.

![cap4](../images/cap_0_26.png)

Paso 24. Antes de ingresar un número de tarjeta de crédito ficticio, escribe el comando `logcat` en el símbolo del sistema.

![cap4](../images/cap_0_27.png)

Paso 25. A continuación, ingresa los números de una tarjeta de crédito ficticia en la aplicación.

![cap4](../images/cap_0_28.png)

Paso 26. Lo que es capturado por los registros del comando, haciendo que esta sea expuesta.

![cap4](../images/cap_0_29.png)

### Tarea 3. `HARDCODING ISSUES - PART 1`.

Paso 27. Regresa al menú principal de **DIVA** e ingresa a la sección `HARDCODING ISSUES - PART 1`.

![cap4](../images/cap_0_30.png)

Paso 28. A continuación, ve al archivo de la aplicación **diva-beta.apk**, haz clic derecho sobre él y selecciona la opción `Rename`. Cambia la extensión del archivo de `.apk` a `.rar`.

![cap4](../images/cap_0_31.png)

Paso 29. Acepta los cambios realizados. 

![cap4](../images/cap_0_32.png)

Paso 30. Extrae los archivos.

![cap4](../images/cap_0_33.png)

Paso 31. Accede a la carpeta extraída y corta el archivo `classes.dex`.

![cap4](../images/cap_0_34.png)

Paso 32. Regresa a la carpeta `Lab 04 - Mobile Security`, extrae el archivo `dex2jar-2.0.zip` y accede a la carpeta extraída.

![cap4](../images/cap_0_35.png)

Paso 33. Dentro de la carpeta extraída de `dex2jar-2.0`, pega el archivo `classes.dex` que cortaste anteriormente.

![cap4](../images//cap_0_36.png)

Paso 34. Abre una nueva terminal e ingresa a la ruta donde pegaste el archivo classes.dex utilizando el comando cd seguido de la ruta. Por ejemplo, ingresa:

```
cd C:\Users\Netec\Desktop\Lab 04 - Mobile Security\dex2jar-2.0
```

![cap4](../images/cap_0_37.png)

Paso 35. Ejecuta el siguiente comando:

```
d2j-dex2jar classes.dex
```

![cap4](../images/cap_0_38.png)

Paso 36. Ahora podrás ver el archivo `classes-dex2jar.jar`.

![cap4](../images/cap_0_39.png)

Paso 37. Abre `jd-gui`.

![cap4](../images/cap_0_40.png)

Paso 38. Abre el archivo que se convirtió anteriormente dentro de la GUI.

![cap4](../images/cap_0_41.png)
![cap4](../images/cap_0_42.png)

Paso 39. Abre `jakhar.aseem.diva`.

![cap4](../images/cap_0_43.png)

Paso 40. Selecciona `HardcodeActivity.class`. Ahí podrás encontrar la clave `vendorsecretkey` y el mensaje "Access granted! See you on the other side :)".

![cap4](../images/cap_0_44.png)

Paso 41. Escribe la contraseña obtenida en DIVA.

![cap4](../images/cap_0_45.png)

### Tarea 4. `INPUT VALIDATION ISSUES – PART 1`.

Paso 42. Regresa a **DIVA** y abre la sección `INPUT VALIDATION ISSUES – PART 1`.

![cap4](../images/cap_0_46.png)

Paso 43. Ingresa el comando de ataque:

```
' OR '1' == '1
```

![cap4](../images/cap_0_47.png)

### Tarea 4. `INPUT VALIDATION ISSUES – PART 2`.

Paso 44. Abre la sección `INPUT VALIDATION ISSUES – PART 2`.

![cap4](../images/cap_0_48.png)

Paso 45. Verifica que puedas acceder a conexiones ingresando `https://www.google.com`.

![cap4](../images/cap_0_49.png)

Paso 46. Una vez verificado el acceso, es posible obtener el contenido del archivo de configuración llamado hosts, el cual se encuentra en el directorio /etc en sistemas operativos tipo Unix/Linux. Para ello, coloca la ruta `file:////etc/hosts` y haz clic en `VIEW`.

![cap4](../images/cap_0_50.png)

### Tarea 5. `ACCESS CONTROL ISSUSES - PART 1`.

Paso 47. En **DIVA**, ingresa a la sección `ACCESS CONTROL ISSUES – PART 1`.

![cap4](../images/cap_0_51.png)

Paso 48. Abre una nueva terminal y escribe el siguiente comando:
```
adb root
```

![cap4](../images/cap_0_23.png)

Paso 49. Escribe el comando 

```
adb devices
```

Verifica que el resultado correspondiente a `emulator-5554` sea `device`.

![cap4](../images/cap_0_24.png)

Paso 50. Escribe el siguiente comando:

```
adb shell
``` 

Luego, ingresa el siguiente comando:

```
su
```

![cap4](../images/cap_0_25.png)

Paso 51. Ejecuta el siguiente comando en el símbolo del sistema:

```
logcat
```

![cap4](../images/cap_0_27.png)

Paso 52. En **DIVA**, haz clic en `VIEW API CREDENTIALS`.

![cap4](../images/cap_0_52.png)

Paso 53. Verás la credencial de la API tanto en la aplicación (proceso legal) como en la consola de comandos, donde aparecerá el nombre de la actividad.

![cap4](../images/cap_0_54.png)
![cap4](../images/cap_0_53.png)

Paso 54. Finalmente, abre una nueva terminal y ejecuta el siguiente comando para ver la información:

```
adb shell am start -n jakhar.aseem.diva/.APICredsActivity
```

![cap4](../images/cap_0_55.png)

## Resultado esperado:

#### Tarea 2.

![cap4](../images/cap_0_29.png)

#### Tarea 3.

![cap4](../images/cap_0_45.png)

#### Tarea 4.

![cap4](../images/cap_0_47.png)

#### Tarea 5.

![cap4](../images/cap_0_55.png) 

---

#### Para regresar al índice general, da clic [aquí](./README.md).
