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

        // 1. Conservar Metadatos intactos
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

        // 2. IGNORAR carácter divisor ━ (Se queda intacto y sin asteriscos)
        if (linea.includes("━")) {
            if (bloqueActual.length > 0) {
                bloques.push({ tipo: "estrofa", contenido: bloqueActual.join("\n") });
                bloqueActual = [];
            }
            bloques.push({ tipo: "especial", contenido: lineaTrim });
            continue;
        }

        // 3. Detectar línea de TONO
        if (lineaTrim.toUpperCase().startsWith("TONO")) {
            if (bloqueActual.length > 0) {
                bloques.push({ tipo: "estrofa", contenido: bloqueActual.join("\n") });
                bloqueActual = [];
            }
            bloques.push({ tipo: "tono", contenido: lineaTrim.toUpperCase() });
            continue;
        }

        // 4. Separar por líneas en blanco y limpiar espacios extras
        if (lineaTrim === "") {
            if (bloqueActual.length > 0) {
                bloques.push({ tipo: "estrofa", contenido: bloqueActual.join("\n") });
                bloqueActual = [];
            }
            // Agrega solo un espacio si el último bloque no era ya un espacio o metadato inicial
            let ultimoBloque = bloques[bloques.length - 1];
            if (ultimoBloque && ultimoBloque.tipo !== "espacio" && ultimoBloque.tipo !== "metadato") {
                bloques.push({ tipo: "espacio", contenido: "" });
            }
        } else {
            bloqueActual.push(lineaTrim.toUpperCase());
        }
    }
    
    if (bloqueActual.length > 0) {
        bloques.push({ tipo: "estrofa", contenido: bloqueActual.join("\n") });
    }

    // Limpiar espacios en blanco remanentes al final de la nota
    while (bloques.length > 0 && bloques[bloques.length - 1].tipo === "espacio") {
        bloques.pop();
    }

    // Armar el resultado aplicando los asteriscos solo a las estrofas
    let textoFinal = bloques.map(b => {
        if (b.tipo !== "estrofa") return b.contenido;
        let estrofa = b.contenido;
        if (estrofa.startsWith("**")) {
            return estrofa.endsWith("**") ? estrofa : `${estrofa}**`;
        }
        return `**${estrofa}**`;
    }).join("\n");

    const activeView = app.workspace.getActiveViewOfType(tp.obsidian.MarkdownView);
    if (activeView) {
        activeView.editor.setValue(textoFinal);
    }
} else {
    new Notice("No se encontró contenido.");
}
-%>