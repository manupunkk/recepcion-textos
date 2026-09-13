# Acividad 7

## Parte 1 Diagnostico
1-Problema detectado: Servidor no arrancaba
Archivo: main.js
Causa: Import a ./styles.css cuando el archivo real es style.css

2-Problema detectado: Error de compilación (regex sin cerrar)
Archivo: Recepciones.vue
Causa: Carácter / suelto dentro de guardar()

3-Problema detectado: Error de compilación (falta punto y coma)
Archivo: ItemsRecepcion.vue	
Causa: Falta state.items.push({ al inicio de agregar()

4-Problema detectado: Error de compilación (SFC vacío)
Archivo: Proveedores.vue
Causa: Archivo completamente vacío, sin <template> ni <script>

5-Problema detectado: 	Listas vacías / formularios sin efecto
Archivo: useRecepcionStore.js
Causa: useRecepcionStore() retorna {} en vez de { state }
