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

## Gestión de Libros
Error de validación: la condición length < 10 && length < 13 nunca aplicaba correctamente la regla de negocio (ISBN de 10 o 13 caracteres); con && la condición era casi imposible de activar bien.
Corrección: se cambió a len !== 10 && len !== 13, que rechaza cualquier ISBN que no tenga exactamente 10 o 13 caracteres.
Problema con el año: el formulario guardaba el dato como anio_publicacion, pero el resto del sistema (estado inicial y listado) usaba anio, generando inconsistencia. Se unificó todo al nombre anio.

## Gestión de Recepciones 
Error encontrado: en la función guardar(), faltaba un return después del alert('Seleccione proveedor'). Como resultado, aunque se mostraba la alerta, el código seguía ejecutándose y la recepción se registraba igual sin proveedor.
Corrección: se agregó return justo después del alert, cortando la ejecución cuando no hay proveedor seleccionado.

## Detalle de recepción
Problema con el identificador de la recepción: el estado inicial (useRecepcionStore.js) guardaba el campo como id_reception (mal escrito), mientras que el resto del proyecto usaba id_recepcion. Esto, sumado a que el filtro en ItemsRecepcion.vue comparaba it.id_reception en vez de it.id_recepcion, hacía que nunca se encontraran coincidencias.
Cómo se solucionó el filtrado: se unificó el nombre del campo a id_recepcion tanto en el estado inicial como en el filtro (computed), quedando it.id_recepcion === props.idRecepcion.
Cómo se logró agregar un ítem correctamente: la función agregar() hace state.items.push({...}) incluyendo id_recepcion: props.idRecepcion, y la cantidad se convierte explícitamente con Number() para asegurar que sea un valor numérico y no texto.