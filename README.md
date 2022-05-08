# proyecto-final-vision
proyecto final vision


# Detección de pelota en 2D y 3D
Esta parte fue bastane sencilla ya que practicamente todo el código fue reciclado de practicas anteriores, tanto para la parte 2D: las lineas de distancia en el suelo, la identificación de las pelotas mediante circulos de Hough, el filtro de color azul etc. 
como para la parte 3D: filtros de color azul para pointcloud, identificación de circulos mediante ramsac etc.

![Captura de pantalla de 2022-05-08 14-34-26](https://user-images.githubusercontent.com/78978326/167296343-6a935045-ff98-4ca8-87bc-404445b74379.png)

sin embargo, no todo podía ser reciclado (que no soy skone) y para proyectar los centros 3D en 2D hubo que ponerse manos a la obra
aún así fue bastante sencillo, basto con obtener las coordenadas 3d de los centros mediante el pointcloud y multiplicandolas por las matrices de proyección correectas obteníamos sus coordenadas 2D, que como se puede ver en la imagén son bastante parecidos a los centros obtenidos mediante los métodos 2D.

![Captura de pantalla de 2022-05-08 14-30-02](https://user-images.githubusercontent.com/78978326/167296212-c2661f81-222d-4309-a455-9acd185f51f6.png)

# Reconocimiento de mesa en 2D y obtención de objetos en 3D
En esta parte lo primero fue configurar yolo, lo cúal resulto muy fácil una vez comprendido el código de ejemplo que nos ha sido facilitado, simplemete tuve que sustituir la imagen de la que con la que se trabajaba y en vez de cargar una del sistema, utilizar la imagen obtenida de la camára del robot.

Con eso resuelto obtenemos el resultado que se ve a continuación:
![Captura de pantalla de 2022-05-08 14-55-43](https://user-images.githubusercontent.com/78978326/167297157-6ed308c8-d9c8-4c84-bf83-9db71a9b6ed3.png)

una vez acabado con yolo empezamos con lo bueno...

Filtrar los objetos encima de la mesa. mi idea para dar una solución a este problema se basaba en usar todo lo aprendido en la asignatura hasta ahora.
Lo primero fue separar la mesa de las demas cosas por lo que usar mediante un filtro de color hsv aplicado al pointcloud como hicimos con las pelotas era sin duda la mejor opción. Una vez tenemos la mesa filtrada vamos a localizar sus esquinas ya que todo lo que este encima de esta tendrá que estar si o si entre ellas, para ello recorremos el pointcloud y nos quedamos con la menor y mayor de las coordenadas x.
Pero esta mesa tambien tiene grosor el cúal no queremos tener en cuenta así que nuevamente recorremos el pointcloud y nos quedamos con con coordenada y más pequeña. De esta manera hemmos obtenido unas coordenadas -x +x y -y en las que estará todo lo que haya encima de la mesa, sin embargo no buscamos ninguna coordenda +y ya que un obejeto que este en la mesa podría tener cualquier altura y no podemos fijar un baremo superior a partir del cúal despreciar objectos.

Finalmente con estas coordenadas iremos de nuevo al pointcloud origanl y filtraremos todo lo que no esta dentro de estas coordenas y por otro ladon con un filtro de color hsv quitaremos la pared de fondo, obteniendo el resultado de la imagen en el que filtramos todos los objectos arriba de la mesa:
![Captura de pantalla de 2022-05-08 15-16-17](https://user-images.githubusercontent.com/78978326/167297991-b94644f2-245c-4bd8-a885-c89b70c2eed4.png)

