
```dataview
TABLE WITHOUT ID file.link AS "Últimas agregadas", file.cday AS "Fecha"
FROM ""
SORT file.cday DESC
LIMIT 15
```

```dataview
TABLE WITHOUT ID file.link AS "Modificadas recientemente", file.mday AS "Fecha"
FROM ""
SORT file.mday DESC
LIMIT 10
```