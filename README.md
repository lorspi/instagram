Feed de instagram
=========
Feed de instagram basado en jQuery para diferentes criterios de búsqueda.

![](https://raw.githubusercontent.com/lorspi/instagram/master/Captura.png)

Modo de uso
----

Contenedor HTML:

    <div class="feed"></div>

jQuery:

    <script src="http://code.jquery.com/jquery-latest.min.js"></script>
    
Código:

- Datos

```
var client_id = '[CLIENT_ID]'
// Se genera en el respectivo cliente creado en http://instagram.com/developer/clients/manage/
    
var access_token = '[ACCESS_TOKEN]'
var user_id = '[USER_ID]'
// Se pueden generar en http://www.pinceladasdaweb.com.br/instagram/access-token/
    
var count = 30 //Cantidad de entradas a mostrar
var tag = '[HASHTAGG]'
```

- URL Api
    
```
//Por hashtag
var apiUrl = "https://api.instagram.com/v1/tags/" + tag +"/media/recent/?client_id=" + client_id + "&callback=?&count=" + count  

//Feed de usuario
var apiUrl = "https://api.instagram.com/v1/users/" + user_id + "/media/recent/?access_token=" + access_token + "&callback=?&count=" + count 

//Mis likes
var apiUrl = "https://api.instagram.com/v1/users/self/media/liked?access_token="  + access_token + "&callback=?&count=" + count 

//Feed de los que sigo
var apiUrl = "https://api.instagram.com/v1/users/self/feed?access_token="  + access_token + "&callback=?&count=" + count 
```
- Funciones y estructura

Esto se ejecuta si la llamada ajax tiene éxito. El "instagramData" que pasa a esta función son los datos devueltos por la url

```
function success (instagramData) {

// Aquí va el código del siguiente bloque.

});
 }

 $.ajax({
   type: "GET",
   url: apiUrl,
   dataType: "json",
   success: success
 });
});

```

Si instagramData.meta.code es igual a 200, quiere decir que instagram no arrojó ningun error. En caso de que sí lo haya arrojado, pondremos el mensaje de error correspondiente en el div asignado.

```
   if (instagramData.meta.code != 200) {
     $('.feed').html('<h1>Error: </h1><p>' + instagramData.meta.error_message + '</p>');
     return
   }
```

- instagramData son los datos devueltos por el json.
- index es el numero de la repetitiva que se incrementa con cada gram.
- gram es el contenido de cada uno de los post devueltos por la repetitiva.

```

   $.each(instagramData.data, function(index, gram) {

```

Le decimos que al elemento de clase .feed le escribamos el contenido retornado por la url según la estructura que armemos.

```
     $('.feed').append('<div">' +                                 
        '<a href="' + gram.link + '" target="_blank"><img class="imagen" src="' + gram.images.low_resolution.url + '"/></a>' +
        '</div>')
```


###Opciones

- Estas son las variables que se pueden usar:

    ```
    gram.type = Tipo de publicación: image, video
    gram.user.username = Nombre de usuario.
    gram.user.full_name = Nombre completo del usuario.
    gram.user.profile_picture = Foto del usuario.
    gram.link = Url de la foto en la web de instagram.
    gram.tags = Hashtags de la foto.
    gram.caption.text = Descripcion de la foto.
    gram.filter = Filtro que se usó.
    
    gram.images.low_resolution.url = Foto en baja resolución.
    gram.images.standard_resolution.url = Foto en resolución estandar.
    gram.images.thumbnail.url = Foto en miniatura.
        .height = Altura de la foto.
        .width = Ancho de la foto.
    ```
    
- Condición para el tipo de contenido:

    ```
    if (gram.type == 'image') {
       /*
       - 'image' muestra solo imágenes
       - 'video' muestra solo videos
       */
      }
    ```



    

Autor
----
Juan Pablo Pérez<br>
[juan.perez@lorspi.com][1]<br>
[lorspi.com][2]

  [1]: mailto://juan.perez@lorspi.com
  [2]: http://lorspi.com
