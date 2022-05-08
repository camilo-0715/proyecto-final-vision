# proyecto-final-vision
proyecto final vision


# Detección de pelota en 2D y 3D
Esta parte fue bastane sencilla ya que practicamente todo el código fue reciclado de practicas anteriores, tanto para la parte 2D: las lineas de distancia en el suelo, la identificación de las pelotas mediante circulos de Hough, el filtro de color azul etc. 
como para la parte 3D: filtros de color azul para pointcloud, identificación de circulos mediante ramsac etc.

sin embargo, no todo podía ser reciclado (que no soy skone) y para proyectar los centros 3D en 2D hubo que ponerse manos a la obra
aún así fue bastante sencillo, basto con obtener las coordenadas 3d de los centros mediante el pointcloud y multiplicandolas por las matrices de proyección correectas obteníamos sus coordenadas 2D, que como se puede ver en la imagén son bastante parecidos a los centros obtenidos mediante los métodos 2D.

