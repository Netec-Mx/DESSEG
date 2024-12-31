# Preventing Applications fronm Session Attacks by Avoding Overly Long Sessions

## Objetivo de la práctica:

Proteger las sesiones de usuario configurando un intervalo de expiración más corto para las cookies de sesión, reduciendo el tiempo en que un atacante podría robar una sesión activa mediante el secuestro de sesión (session hijacking).

## Duración aproximada:
- 20 minutos.

## Instrucciones 

### **Paso 1:**  
Inicia sesión utilizando las siguientes credenciales:  
- **Usuario:** user  
- **Contraseña:** pass  

**Resultado: Estarás autenticado como usuario.**

---

### **Paso 2:**  
Abre **Firefox** e ingresa la URL:  
`http://localhost:8080/Mod7Lab2/userfiles/index.jsp`  

Serás redirigido a la página de inicio de sesión.  

---

### **Paso 3:**  
1. Ve al navegador **Chrome**.  
2. Haz clic en el ícono **EditThisCookie**.  

![imagen resultado](../images/mod7-lab2-1.png)

3. Busca la cookie con el nombre **JSESSIONID** y copia su valor en un archivo de **Notepad**.  

![imagen resultado](../images/mod7-lab2-2.png)

---

### **Paso 4:**  
1. Ve al navegador **Firefox**.  
2. Haz clic derecho en el navegador y selecciona **Inspect Element**.  

![imagen resultado](../images/mod7-lab2-3.png)

---

### **Paso 5:**  
1. Ve a la pestaña **Storage**.  
2. Ve a `Cookies` y selecciona `http://localhost:8080` en la sección de cookies.  

![imagen resultado](../images/mod7-lab2-4.png)

---

### **Paso 6:**  

Para editar la cookie, dar doble click en el valor actual, para luego pegar el valor de la cookie copiada anteriormente.  
- **Dominio:** localhost  

![imagen resultado](../images/mod7-lab2-5.png)

---

### **Paso 7:**  
Abrea una nueva pestaña en Firefok y accede a la URL `http://localhost:8080/Mod7Lab2/userfiles/index.jsp`.  
- **Resultado:** Podrás copiar la sesión activa de Chrome y acceder a la página de inicio como usuario autenticado.  

![imagen resultado](../images/mod7-lab2-6.png)

- **Problema:** El **MaxAge** de la cookie está configurado con un valor muy alto, lo que permite a los atacantes suficiente tiempo para copiar sesiones válidas.  
- Para confirmar esta vulnerabilidad:  
   - Ve al archivo **LoginController.jsp**, línea n.º **20**.  
   - Observa que el valor de `setMaxAge` está configurado en `(60 * 60 * 2)` minutos.  
   - **Recomendación:** Configura un intervalo de tiempo menor para las cookies de sesión, lo que reduce el tiempo que los atacantes tienen para robarlas.  

---

### **Nota:**  
Si no puedes realizar el secuestro de la sesión de Chrome en el **Paso 7**, realiza lo siguiente:  
1. Cierra sesión en **Chrome** después de copiar la cookie **JSESSIONID**.  
2. Inicia sesión nuevamente antes de ejecutar los **Pasos 4, 5 y 6**.  

---

### **Paso 8:**  
Para establecer un intervalo más corto para las cookies de sesión:  
1. Ve al archivo **LoginController.jsp**.  
2. Reemplaza el código en la línea n.º **20** con lo siguiente:  
```java
session.setMaxInactiveInterval(60*1);
```  

---

### **Paso 9:**  
Haz clic en el botón **Save** en la parte superior del editor para guardar los cambios.  

---

### **Paso 10:**  
Repite los pasos del **1 al 7** para intentar copiar la sesión de un navegador a otro.  
- **Resultado:** Esta vez no podrás copiar la sesión, ya que la sesión expirará automáticamente después de 1 minuto.  

Esto demuestra que configurar un intervalo de tiempo mínimo para las cookies de sesión protege la sesión de ser secuestrada.  

---

### **Paso 11:**  
Haz clic en el botón **Reset** para restaurar el laboratorio al estado anterior.  
Selecciona **OK** en el mensaje emergente que indica:  
**"Reset Successful!"**  

---

### **Paso 12:**  
Haz clic en el botón **HOME** para volver a la página principal.  