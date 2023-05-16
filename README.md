//remeros que no hayan alquilado botes 
SELECT r.id, r.nombre FROM remero r
WHERE NOT EXISTS (SELECT * FROM alquiler a
WHERE r.id = a.id_remero);

//nombre de editoriales que no tengan libros publicados
SELECT e.nombre FROM editorial e 
WHERE NOT EXISTS (SELECT * FROM libro l
WHERE e.id_editorial = l.id_editorial);

//cantidad de distintas ciudades en las que no se hayan editado libros
SELECT COUNT(DISTINCT e.ciudad) AS cantidad_ciudades, e.nombre FROM editorial e
WHERE NOT EXISTS ( SELECT * FROM libro l
WHERE e.id_editorial = l.id_editorial)

//Ubicacion de mesas que no hayan pedido medialunas
SELECT m.ubicacion FROM mesa m 
WHERE NOT exists (SELECT * FROM pedido p INNER JOIN carta c ON p.id_carta = c.id
WHERE c.descripcion = "Medialuna" AND m.id = p.id_mesa);

//Ubicacion de mesas que hayan pedido todos los elementos de la carta
SELECT m.ubicacion FROM mesa m 
WHERE  NOT EXISTS (SELECT * FROM carta c WHERE NOT EXISTS (SELECT * FROM pedido p
WHERE m.id = p.id_mesa AND p.id_carta = c.id)); 

//nombre de remeros que no hayan alquilado botes azules
SELECT r.nombre FROM remero r WHERE r.id NOT IN (SELECT a.id_remero FROM alquiler a
INNER JOIN bote b ON a.id_bote = b.id WHERE b.color = "Azul") 
