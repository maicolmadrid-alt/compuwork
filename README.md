# Documentación Técnica del Proyecto

> **Nota del autor**: La documentación técnica fue realizada inicialmente por mi persona quien desarrolló toda la estructura y explicación de la lógica implementada.  
> Posteriormente, se utilizó **ChatGPT (OpenAI)** únicamente para dar formato y presentarla de manera más conceptual y clara.

---

## 1. Creación de la clase base Empleado
**Objetivo:** representar de manera genérica a cualquier empleado de la empresa.  

**Atributos definidos:**
- `id` (único por empleado)  
- `nombre` (nombre completo del empleado)  
- `departamento` (inicialmente `"Sin asignar"`)  

**Métodos implementados:**
- Getters y setters para manipular los atributos.  
- Método abstracto `getDetalles()` para obligar a las subclases a proporcionar su propia información.  

**Decisión de diseño:** se declaró como clase abstracta para aplicar herencia y polimorfismo.  

---

## 2. Implementación de subclases de Empleado
Se definieron dos tipos específicos de empleados:  

### `EmpleadoPermanente`
- **Atributo adicional:** `salario`.  
- Implementación de `getDetalles()` mostrando salario y demás datos.  

### `EmpleadoTemporal`
- **Atributo adicional:** `mesesContrato`.  
- Implementación de `getDetalles()` mostrando duración del contrato.  

**Justificación:** aplicar herencia (comparten atributos de Empleado) y polimorfismo (cada clase devuelve su información personalizada).  

---

## 3. Creación de la clase Departamento
**Objetivo:** agrupar empleados bajo un mismo nombre de departamento.  

**Atributos definidos:**
- `nombre` (nombre del departamento).  
- `empleados` (lista de empleados asignados).  

**Métodos principales:**
- `agregarEmpleado(Empleado e)` → asigna un empleado al departamento y actualiza su atributo departamento.  
- `eliminarEmpleado(Empleado e)` → retira al empleado y lo deja como `"Sin asignar"`.  
- `getEmpleados()` → devuelve la lista completa.  

**Decisión de diseño:** se asegura la consistencia entre empleados y su departamento.  

---

## 4. Implementación de la clase GestorEmpresa
**Rol:** actúa como capa de lógica de negocio.  

**Responsabilidades:**
- Crear empleados (permanentes o temporales).  
- Actualizar o eliminar empleados.  
- Crear y eliminar departamentos.  
- Asignar empleados a departamentos.  
- Generar reportes individuales y por departamento.  

**Estructura interna:**
- `Map<Integer, Empleado>` para administrar empleados por ID.  
- `Map<String, Departamento>` para manejar los departamentos.  
- Contador incremental para IDs automáticos.  

**Gestión de excepciones:**
- Validación cuando un ID no existe.  
- Validación cuando el departamento solicitado no existe.  
- Control en la generación de reportes.  

---

## 5. Desarrollo de la clase ReporteDesempeño (opcional)
**Función:** preparar reportes con información detallada del empleado o del departamento.  

En este proyecto: la generación de reportes fue centralizada en `GestorEmpresa`, pero la clase se puede extender para métricas futuras (puntualidad, desempeño, productividad).  

---

## 6. Creación de la interfaz de usuario `AppMenu`
**Objetivo:** permitir al usuario interactuar con el sistema mediante consola.  

**Elementos principales:**
- Menú con opciones numeradas para CRUD de empleados y departamentos.  
- Uso de `Scanner` para recibir datos ingresados por teclado.  
- Llamadas directas a los métodos de `GestorEmpresa`.  
- Validaciones de entradas inválidas o inexistentes.  

**Diseño de flujo:** bucle `while(true)` hasta que el usuario elige la opción de salida.  

---

## 7. Pruebas y validaciones
- Se realizaron pruebas creando empleados y departamentos desde el menú.  
- Se validó la asignación de empleados a departamentos.  
- Se comprobó que los reportes individuales y grupales muestran la información correctamente.  
- Se probó la eliminación de empleados y departamentos, verificando que el sistema actualiza las listas y no genera inconsistencias.  

---

## 8. Principios aplicados
- **POO:** encapsulamiento, herencia, polimorfismo.  
- **Mantenibilidad:** separación en paquetes (`modelo`, `servicio`, `ui`).  
- **Escalabilidad:** preparado para añadir nuevos tipos de empleados y métricas en los reportes.  
- **Reutilización:** clases con responsabilidades claras, listas para extenderse en futuras versiones.  

