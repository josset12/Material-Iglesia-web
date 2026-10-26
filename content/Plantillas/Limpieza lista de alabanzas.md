<%*
let tp_text = tp.file.selection();

if (!tp_text) {
    tp_text = tp.file.content;
}

if (tp_text) {
    let lineas = tp_text.split("\n");
    let enMetadatos = false;
    let bloques = [];
    let bloqueActual = [];

    for (let i = 0; i < lineas.length; i++) {
        let linea = lineas[i];
        let lineaTrim = linea.trim();

        // 1. Conservar Metadatos intactos (---)
        if (i === 0 && lineaTrim === "---") {
            enMetadatos = true;
            bloques.push({ tipo: "metadato", contenido: linea });
            continue;
        }
        if (enMetadatos) {
            bloques.push({ tipo: "metadato", contenido: linea });
            if (lineaTrim === "---") enMetadatos = false;
            continue;
        }

        // 2. Limpiar corchetes dobles [[Texto|Alias]] -> Texto
        let lineaLimpia = linea.replace(/\[\[([^\]\vert{}]+)(?:\Vert{}[^\]]+)?\]\]/g, "$1");

        // 3. IGNORAR divisores, emojis especiales o líneas que contengan #
        if (lineaLimpia.includes("━") || lineaLimpia.includes("▶️") || lineaLimpia.includes("🔹") || lineaLimpia.includes("#")) {
            if (bloqueActual.length > 0) {
                bloques.push({ tipo: "parrafo", contenido: bloqueActual.join("\n") });
                bloqueActual = [];
            }
            bloques.push({ tipo: "especial", contenido: lineaLimpia });
            continue;
        }

        // 4. Agrupar por párrafos (separados por líneas en blanco)
        if (lineaLimpia.trim() === "") {
            if (bloqueActual.length > 0) {
                bloques.push({ tipo: "parrafo", contenido: bloqueActual.join("\n") });
                bloqueActual = [];
            }
            bloques.push({ tipo: "espacio", contenido: "" });
        } else {
            bloqueActual.push(lineaLimpia);
        }
    }

    if (bloqueActual.length > 0) {
        bloques.push({ tipo: "parrafo", contenido: bloqueActual.join("\n") });
    }

    // 5. Armar el resultado aplicando los asteriscos al PÁRRAFO completo
    let textoFinal = bloques.map(b => {
        if (b.tipo !== "parrafo") return b.contenido;
        
        let contenidoParrafo = b.contenido.trim();
        
        // Si el párrafo ya empieza y termina con **, se deja intacto
        if (contenidoParrafo.startsWith("**") && contenidoParrafo.endsWith("**")) {
            return b.contenido;
        }
        
        // Si no, envuelve todo el bloque en un único par de **
        return `**${b.contenido}**`;
    }).join("\n");

    const activeView = app.workspace.getActiveViewOfType(tp.obsidian.MarkdownView);
    if (activeView) {
        activeView.editor.setValue(textoFinal);
    }
} else {
    new Notice("No se encontró contenido.");
}
-%>
