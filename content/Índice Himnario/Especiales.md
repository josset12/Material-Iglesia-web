
```dataview
TABLE WITHOUT ID file.link AS "Himnos", Tono AS "Tono"
FROM "Himnario"
WHERE Categoria = "Especial"
SORT number(split(file.name, " ")[0]) ASC
```