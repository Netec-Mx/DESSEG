# Preventing URL Manipulation Attacks by Securing Querystring with Encryption

## Objetivo de la práctica:

Identificar y mitigar la exposición de datos sensibles en la URL al cifrar las cadenas de consulta mediante funciones criptográficas, mejorando la seguridad de los datos frente a ataques como Man-in-the-Middle y fijación de sesión.

## Duración aproximada:

- 15 minutos.

## Instrucciones 

Paso 1. Inicia sesión utilizando las siguientes credenciales válidas:

    Nombre de usuario: test
    Contraseña: test1

Paso 2. Haz clic en el menú `SHOP`. Verás una lista de productos.

Paso 3. Para agregar el producto `macbook2018series` al carrito, haz clic en el botón Add to cart debajo de la imagen del producto `macbook2018series`.

- Resultado: Serás redirigido a la página de Checkout. Los detalles del producto seleccionado se envían en la cadena de consulta (querystring) como texto sin cifrar.
- Esto implica que la aplicación está exponiendo datos sensibles a través de la URL.

![imagen resultado](../images/img13.png)


**Confirmación del uso de cadenas de consulta para enviar datos sensibles:**

- Ve a la línea n.º 88 en `Shop.jsp`.

- Verás que los datos del producto se envían sin cifrar a través de la cadena de consulta.

**Recomendación:**

Las cadenas de consulta basadas en parámetros deben cifrarse utilizando funciones criptográficas, ya que pueden manipularse fácilmente.

Paso 4. Para cifrar la cadena de consulta, ve a la línea n.º 22 en `Shop.jsp` y añade el siguiente código:

    byte[] a1 = Product.getBytes();
    byte[] a2 = Base64.encodeBase64(a1);
    byte[] a3 = Price.getBytes();
    byte[] a4 = Base64.encodeBase64(a3);
    String s1 = new String(a2);
    String s2 = new String(a4);
    Product = s1;
    Price = s2;

Paso 5. Ahora, ve a la pestaña `checkout.jsp`, línea n.º 28, y añade el siguiente código:

    <%
    String Pro = null;
    String Pri = null;
    if (Product != null && Price != null) {
        byte[] a5 = Product.getBytes();
        byte[] a6 = Base64.decodeBase64(a5);
        byte[] a7 = Price.getBytes();
        byte[] a8 = Base64.decodeBase64(a7);
        Pro = new String(a6);
        Pri = new String(a8);
        Product = Pro;
        Price = Pri;
    } else {
        response.sendRedirect("Login.jsp");
    }
    %>

Paso 6. Haz clic en el botón `Save` en la parte superior del editor para guardar los cambios.

Paso 7. Inicia sesión nuevamente como se indica en el `Paso 1` y agrega el producto `macbook2018series` al carrito siguiendo los pasos 2 y 3.

Resultado: 
- Esta vez verás que la URL está cifrada y, por lo tanto, está protegida contra ataques como Man-in-the-Middle y fijación de sesión (session fixation).

![imagen resultado](../images/img14.png)

Paso 8. Haz clic en el botón `Reset` para restaurar el laboratorio al estado anterior y haz clic en `OK` en el mensaje emergente que indica `¡Restablecimiento exitoso!`.

Paso 9. Haz clic en el botón `HOME` para regresar a la página principal.
