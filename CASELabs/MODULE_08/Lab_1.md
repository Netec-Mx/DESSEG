# Preventing Applications from Deniel-Of-Service (DOS) Attacks

## Objetivo de la práctica:

Prevenir un posible **ataque de Denegación de Servicio (DoS)** causado por una recursión infinita, implementando un control adecuado sobre la entrada del usuario y el uso de un bloque **try-catch** para manejar excepciones y evitar un **StackOverflowError**.

## Duración aproximada:
- 15 minutos.

## Instrucciones 

**Paso 1:**  
Haz clic en el menú **Blog**.  

**Paso 2:**  
Para imprimir el artículo, desplázate hacia abajo, ingresa el valor **1** en el cuadro de texto **"Enter No. of copies to Print"** y haz clic en el botón **"print"**.  
- **Resultado:** Verás el mensaje: **"Document successfully Printed Back..!"**  

**Paso 3:**  
Haz clic en **Back**.  

**Paso 4:**  
Haz clic nuevamente en el menú **Blog**. Esta vez, ingresa un valor inválido, como **-1**, en el cuadro de texto **"Enter No. of copies to Print"** y haz clic en el botón **"print"**.  
- **Resultado:** Verás un error de **StackOverFlowError**. Esto ocurre debido a una recursión infinita, lo que puede dar lugar a un ataque de Denegación de Servicio (DoS).  

![imagen resultado](.../CASELabs/Images/mod8-lab1-1.png)

**Confirmación de la vulnerabilidad de recursión infinita:**  
Ve a la pestaña **Print.jsp**, línea n.º **13**. Allí notarás que:  
1. El parámetro de entrada no se valida adecuadamente antes de procesar el bucle **for**.  
2. El bucle **for** no se ejecuta dentro de un bloque **try-catch**.  

Un bloque **try-catch** puede capturar cualquier excepción mientras se ejecuta el bucle **for** y evitar así la recursión infinita que podría provocar un ataque de DoS.  

**Paso 5:**  
Para evitar un ataque DoS, implementa un bloque **try-catch** antes de ejecutar el bucle.  
1. Ve a la pestaña **Print.jsp**.  
2. Reemplaza el código de las líneas n.º **11 a 16** por el siguiente:  
```jsp
<%
String p = request.getParameter("print");
try {
    int pageno = Integer.parseInt(p);
    if (pageno < 0) {
        out.println("<center><div style='color:red;text-align:center;font-size:larger;'>Please Enter valid Number <a href='index.jsp'>Back..!</a></div></center>");
    } else {
        out.println("<center><div style='color:green;text-align:center;font-size:larger;'>Document successfully Printed!! <a href='index.jsp'> Back..! </a></div></center>");
    }
} catch (Throwable th) {
    out.println("<center><div style='color:red;text-align:center;font-size:larger;'>Please Enter valid Number <a href='index.jsp'> Back..! </a></div></center>");
}
%>
```  
![imagen resultado](./images/mod8-lab1-2.png)

**Paso 6:**  
Haz clic en el botón **Save** en la parte superior del editor para guardar los cambios.  

**Paso 7:**  
Repite los pasos 1 y 4.  
- **Resultado:** Esta vez verás el mensaje: **"Please Enter valid Number Back..!"**  

![imagen resultado](./images/mod8-lab1-3.png)

**Paso 8:**  
Haz clic en el botón **Reset** para restaurar el laboratorio al estado anterior y selecciona **OK** en el mensaje emergente que indica **"Reset Successful!"**.  

**Paso 9:**  
Haz clic en el botón **HOME** para volver a la página principal.  
