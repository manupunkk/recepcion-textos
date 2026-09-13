# Acividad 7

## Diagnostico
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

## Estado Compartido 
Problema encontrado: la función useRecepcionStore() retornaba un objeto vacío en lugar de exponer el state, por lo que ningún componente podía acceder a los datos. Además, el campo id_reception estaba mal escrito (no coincidía con id_recepcion usado en otros componentes) y cantidad se guardaba como texto en vez de número.
Corrección: se retornó { state } desde el store, se corrigió el nombre del campo a id_recepcion y se cambió cantidad a tipo numérico.
Por qué debe ser compartido: porque varios componentes (Libros, Recepciones, ItemsRecepcion) necesitan leer y modificar la misma información (por ejemplo, la lista de proveedores se usa tanto en Recepciones como potencialmente en Proveedores), y sin un estado central cada uno tendría su propia copia desincronizada.
