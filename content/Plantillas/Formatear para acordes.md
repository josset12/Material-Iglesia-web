<%*
let tp_text = tp.file.selection();

if (!tp_text) {
    tp_text = tp.file.content;
}

if (tp_text) {
    let lineas = tp_text.split("\n");
    let enMetadatos = false;
    let lineasLimpias = [];

    for (let i = 0; i < lineas.length; i++) {
        let linea = lineas[i];
        let lineaTrim = linea.trim();

        // 1. Detectar y OMITIR completamente la sección de Metadatos (Frontmatter)
        if (i === 0 && lineaTrim === "---") {
            enMetadatos = true;
            continue;
        }
        if (enMetadatos) {
            if (lineaTrim === "---") enMetadatos = false;
            continue;
        }

        // 2. Limpiar todos los asteriscos de la línea
        let lineaSinAsteriscos = linea.replace(/\*\*/g, "").replace(/\*/g, "");

        // 3. Acumular las líneas
        lineasLimpias.push(lineaSinAsteriscos);
    }

    // 4. Limpiar saltos de línea sobrantes al inicio y al final
    while (lineasLimpias.length > 0 && lineasLimpias[0].trim() === "") {
        lineasLimpias.shift();
    }
    while (lineasLimpias.length > 0 && lineasLimpias[lineasLimpias.length - 1].trim() === "") {
        lineasLimpias.pop();
    }

    // 5. Encerrar todo dentro del bloque de código para Chord Sheets
    let contenidoChordSheets = lineasLimpias.join("\n");
    let textoFinal = "```chords\n" + contenidoChordSheets + "\n```";

    const activeView = app.workspace.getActiveViewOfType(tp.obsidian.MarkdownView);
    if (activeView) {
        activeView.editor.setValue(textoFinal);
    }
} else {
    new Notice("No se encontró contenido.");
}
-%>
