```dataviewjs
// 1. Obtener todas las notas de la bóveda que coincidan con la Categoria deseada
let pages = dv.pages('').where(p => p.Categoria == "Alab. 3 Tiempos Normal");

// 2. Función para extraer la letra inicial real limpiando números y signos
function getCleanLetter(filename) {
    let cleanName = filename.replace(/^[\d¡¿\s]+/, '').trim();
    if (!cleanName) return "#";
    
    let firstChar = cleanName.charAt(0).toUpperCase();
    firstChar = firstChar.normalize("NFD").replace(/[\u0300-\u036f]/g, "");
    return /[A-Z]/.test(firstChar) ? firstChar : "#";
}

// 3. Función para limpiar el título al ordenar alfabéticamente
function getCleanTitle(filename) {
    return filename.replace(/^[\d¡¿\s]+/, '').trim();
}

// 4. Agrupar las páginas filtradas por su letra inicial
let grouped = pages.groupBy(p => getCleanLetter(p.file.name));

// 5. Ordenar los grupos alfabéticamente (- A -, - B -, - C -)
grouped.sort(g => g.key, 'asc');

// 6. Generar arreglo único de filas para la tabla
let allRows = [];

for (let i = 0; i < grouped.length; i++) {
    let group = grouped[i];
    
    // Insertar línea divisora blanca si no es la primera sección
    if (i > 0) {
        allRows.push(["<hr style='border: 1px solid var(--table-line-color, #ffffff); margin: 15px 0 5px 0;'>", ""]);
    }
    
    // Encabezado de la letra (– A –, – B –) sin viñeta
    allRows.push([`**– ${group.key} –**`, ""]);
    
    // Ordenar canciones ALFABÉTICAMENTE por título limpio dentro del grupo
    let sortedRows = group.rows.sort(p => getCleanTitle(p.file.name), 'asc');
    
    for (let p of sortedRows) {
        let cleanTono = (p.Tono && String(p.Tono).trim() !== "") ? String(p.Tono).trim() : "–";
        allRows.push([p.file.link, cleanTono]);
    }
}

// 7. Renderizar la tabla unificada sin encabezados molesto
dv.table(["", ""], allRows);
```