SELECT r.id, r.nombre FROM remero r
WHERE NOT EXISTS (SELECT * FROM alquiler a
WHERE r.id = a.id_remero);

SELECT e.nombre FROM editorial e 
WHERE NOT EXISTS (SELECT * FROM libro l
WHERE e.id_editorial = l.id_editorial);

SELECT COUNT(DISTINCT e.ciudad) AS cantidad_ciudades, e.nombre FROM editorial e
WHERE NOT EXISTS ( SELECT * FROM libro l
WHERE e.id_editorial = l.id_editorial)

SELECT m.ubicacion FROM mesa m 
WHERE NOT exists (SELECT * FROM pedido p INNER JOIN carta c ON p.id_carta = c.id
WHERE c.descripcion = "Medialuna" AND m.id = p.id_mesa);

SELECT m.ubicacion FROM mesa m 
WHERE  NOT EXISTS (SELECT * FROM carta c WHERE NOT EXISTS (SELECT * FROM pedido p
WHERE m.id = p.id_mesa AND p.id_carta = c.id)); 
