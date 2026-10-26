<%*
let currentSize = parseInt(getComputedStyle(document.body).getPropertyValue('--font-text-size')) || 16;
let newSize = Math.max(12, currentSize - 2); // No baja de 12px
document.body.style.setProperty('--font-text-size', newSize + 'px');
new Notice('Tamaño de fuente: ' + newSize + 'px');
-%>