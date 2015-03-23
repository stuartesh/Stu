#### Remover espacios en blanco: > y <
Dan más control sobre los espacios en blanco cerca de las etiquetas. > eleminará todos los espacios en blanco que están cerca de la etiqueta, mientras < removerá todos los espacios que estan inmediatamente de la etiqueta. Se pueden tomar como elementos que comen espacios en blanco: > se enfrenta fuera de la etiqueta y se come el espacio en blanco en el exterior, y < se pone frente a la etiqueta y se come los espacios en blanco en el interior. Se colocan al final de una definición de etiqueta, después de la clase, id y declaraciones del atributo pero antes de / o =. Por ejemplo:\

    ```
    %blockquote<
    %div
    Foo!
    ```
es compilado como:
    ```
    <blockquote>
    <div>Foo!</div>
    </blockquote>
    ```
Y esto:
    ```
    %img
    %img>
    %img
    ```
es compilado como:
    ```
    <img/><img/><img/>
    ```
Y esto:
    ```
    %p<= "Foo\nBar"
    ```
es compilado como:
    ```
    <p>FooBar</p>
    ```
Y finalmente:
    ```
    %img
    %pre><
    foo
    bar
    %img
    ```
es compilado como:
    ```
    <img /><pre>foobar</pre><img />
    ```

#### Doctype: !!!
Al describir los documentos HTML con Haml, puede tener un tipo de documento XML o prologo generado automáticamente por incluir los caracteres !!!. Por ejemplo:
    ```
    !!! XML
    !!!
    %html
    %head
    %title Myspace
    %body
    %h1 I am the international space station
    %p Sign my guestbook
    ```
se compila como:
    ```
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    <html>
    <head>
    <title>Myspace</title>
    </head>
    <body>
    <h1>I am the international space station</h1>
    <p>Sign my guestbook</p>
    </body>
    </html>
    ```
Cuando la opción de :format se establece en :html5, !!! es siempre <!DOCTYPE html>. Si no estás usando el conjunto de su documento de caracteres UTF-8, puede especificar qué codificación debe aparecer en el prólogo XML de una manera similar. Por ejemplo:

    !!! XML iso-8859-1

#### HTML Comments: /
El carácter de barra inclinada, cuando se coloca al principio de la línea, envuelve todo el texto en un comentario de HTML. Por ejemplo:
    ```
    %peanutbutterjelly
    / This is the peanutbutterjelly element
    I like sandwiches!
    ```
se compila como:
    ```
    <peanutbutterjelly>
    <!-- This is the peanutbutterjelly element -->
    I like sandwiches!
    </peanutbutterjelly>
    ```
La barra inclinada también pueden envolver con sangría secciones de código. Por ejemplo:
/
    ```
    /
    %p This doesn't render...
    %div
    %h1 Because it's commented out!
    ```
se compila como:
    ```
    <!--
    <p>This doesn't render...</p>
    <div>
    <h1>Because it's commented out!</h1>
    </div>
    -->
    ```

#### Haml Comments: -#
El guión seguido inmediatamente por el signo de número, significa un comentario silencioso. Cualquier texto que sigue a esto no es tomado en el documento resultante en absoluto. Por ejemplo:
    ```
    %p foo
    -# This is a comment
    %p bar
    is compiled to:
    <p>foo</p>
    <p>bar</p>
    ```
También puede unir texto debajo de una observación silenciosa. Por ejemplo:
    ```
    %p foo
    -#
    This won't be displayed
    Nor will this
    Nor will this.
    %p bar
    is compiled to:
    <p>foo</p>
    <p>bar</p>
    ```

### Filtros
Los dos puntos indican un filtro. Esto permite pasar un bloque de texto con sangría como entrada a otro programa de filtrado y añadir el resultado a la salida de Haml. La sintaxis es simplemente con dos puntos seguidos por el nombre del filtro. Por ejemplo:
    ```
    %p
    :markdown
    # Greetings
    Hello, *World*
    ```
Se compila como:
    ```
    <p>
    <h1>Greetings</h1>
    <p>Hello, <em>World</em></p>
    </p>
    ```
Los filtros podrían tener código de Ruby incorporado con #{}. Por ejemplo:
    ```
    - flavor = "raspberry"
    #content
    :textile
    I *really* prefer _#{flavor}_ jam.
    ```
se compila como:
    ```
    <div id='content'>
    <p>I <strong>really</strong> prefer <em>raspberry</em> jam.</p>
    </div>
    ```

#### Estos son algunos de los filtros de Haml:

##### :cdata
rodea el texto filtrado con etiquetas CDATA.

##### :coffee
compila el texto filtrado a Javascript usando Cofeescript. También puede hacer referencia a este filtro como  :coffeescript. Este filtro se implementa con Tilt.

##### : css
rodea el texto con un filtro de <style> y opcionalmente con etiquetas CDATA . Se usa mucho para las líneas de CSS.

##### :javascript
rodea el texto con un filtro de <script> y opcionalmente con etiquetas CDATA . Se usa mucho para las líneas de JS.

##### :less
Analiza el texto filtrado con menos para producir la salida CSS. Este filtro se implementa con Tilt.

### Métodos Auxiliares
A veces es necesario manipular los espacios en una forma más precisa de lo que los métodos de eliminación de  espacios en blanco nos permiten.
Hay algunos métodos auxiliares que son útiles cuando se trata de contenido en línea. Todos estos métodos tienen un bloque Haml a modificar.

#### surround
Rodea un bloque Haml con texto. Espera 1 ó 2 argumentos de cadena usados para rodear el bloque Haml. Si no se proporciona un segundo argumento, el primer argumento es utilizado como el segundo.
    ```
    = surround "(", ")" do
    = link_to "learn more", "#"
    ```

#### precede
Antepone un bloque Haml con texto. Espera 1 argumento.
    ```
    = precede "*" do
    %span Required
    ```

#### succeed
Anexa un bloque Haml con texto. Espera 1 argumento.

Comienza por:
    ```
    = succeed "," do
    = link_to "filling out your profile", "#"
    = succeed "," do
    = link_to "adding a bio", "#"
    and
    = succeed "." do
    = link_to "inviting friends", "#"
    ```

>ESTO ES UN ELANCE QUE PUEDE AYUDAR A OBTENER MÁS INFORMACIÓN SOBRE HAML.
[http://haml.info/docs/yardoc/](http://haml.info/docs/yardoc/)

##### Bibliografia:
[http://haml.info](http://haml.info)
[http://haml.info/docs.html](http://haml.info/docs.html)
[http://haml.info/docs/yardoc/file.REFERENCE.html](http://haml.info/docs/yardoc/file.REFERENCE.html)