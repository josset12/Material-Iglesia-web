<%*
// Obtiene el tamaño de fuente actual del elemento raíz de Obsidian
let currentSize = parseInt(getComputedStyle(document.body).getPropertyValue('--font-text-size')) || 16;
// Le suma 2 píxeles
let newSize = currentSize + 2;
// Aplica el nuevo tamaño
document.body.style.setProperty('--font-text-size', newSize + 'px');
new Notice('Tamaño de fuente: ' + newSize + 'px');
-%>