>Mazmorra semi-procedural al estilo de [Spelunky](http://tinysubversions.com/spelunkyGen/)

Para lograr algo parecido he seguido este procedimiento llegado a mi por pura logica:

---

**Crear los segmentos usando el Tilemap**, actualmente los creo en un cuadrante de un tamaño especifico en el editor manualmente:

![[TilemapSegCreation.jpg]]

---

**Leer el segmento del Tilemap**:

![[ReadCellsFunc.jpg]]
Donde obtengo cada tile en el cuadrante pasando de _izquierda a derecha_ y de _arriba a abajo_, insertando todo en un **Array** doble; cada tile es guardado como un _vector_ con las coordenadas del autotile si existe un tile en esa posicion, si no siempre sera **-1**.

---

**Guardar el segmento en un archivo**, por ahora _JSON_ es el formato elegido:

![[SaveTilesFunc.jpg]]
En un nodo más arriba abro el archivo y guardo el array en un archivo json,
podria intentar guardar varios arrays para tener varios segmentos diferentes en un solo archivo, pero todavia no tengo claro como manejar archivos abiertos.
La informacion guardada se parece a algo como lo siguiente:
```gdscript
[[-1,-1,-1,-1,-1,"(0, 4)","(1, 3)","(1, 3)","(2, 3)",-1,-1,-1,-1,-1,-1,-1],
[-1,-1,-1,-1,"(0, 4)","(3, 7)",-1,-1,-1,"(0, 3)","(3, 4)",-1,-1,-1,-1,-1]]
```
	Dando como resultado Array[y][x], notese que los vectores se guardan como Strings ya que JSON no soporta vectores.

---

**Cargar un segmento desde un archivo**, una simple funcion para decirle al tilemap que cargue el segmento extraido:

![[LoadTilesFunc.jpg]]

---

**Mostrar el segmento extraido**, junto con una forma muy inoptimizada de convertir un _String_ en un _Vector_:

![[WriteCellsFunc.jpg]]
Convertir el string a vector es necesario porque se guarda en formato _JSON_.
