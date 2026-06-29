# Cajero Automático – Simulador en Python

Trabajo Práctico Grupal Lab. de Python – Algoritmo y estructuras de datos

## Descripción

Este proyecto simula las operaciones básicas de un cajero automático (ATM)
desarrollado en Python. El sistema permite a un usuario autenticarse con su
usuario y contraseña, y luego realizar operaciones bancarias simples:
consulta de saldo, extracción de dinero, depósito y transferencia entre
cuentas.

El sistema contempla además controles de seguridad y de negocio:
validación de acceso con bloqueo por intentos fallidos, control de saldo
insuficiente, límite máximo y minimo de extracción por operación, y un registro
(historial) de las operaciones realizadas durante la sesión.

## Integrantes del grupo

- Romero Marcos Ariel
- Massa Nahuel
- Centurion Juan Agustin
- Arzuaga Nicolas

## Cómo ejecutar el programa

En caso de querer probar el programa por su cuenta, sigue los siguientes pasos:

> **Nota:** esta sección puede actualizarse según lo que finalmente se
> acuerde con la cátedra respecto al entorno de entrega.

1. Cloná o descargá este repositorio
2. Abrí una terminal en la carpeta del proyecto
3. Ejecutá:

```bash
python main.py
```

4. Ingresá con uno de los usuarios de prueba (ver tabla más abajo) cuando el
   programa lo solicite

> **Importante:** el programa requiere ingresar datos por teclado
> (`input()`). Si se ejecuta desde VSCode, debe usarse la **Terminal
> integrada** (no el panel "Output" de Code Runner), ya que ese panel no
> admite entrada interactiva del usuario.

## Usuarios de prueba

| Usuario | Contraseña | Saldo inicial |
|---------|------------|---------------|
| marcos  | 1234       | $1000.000     |
| nicolas | 3456       | $5000.000     |
| nahuel  | 4312       | $10000.000    |
| juan    | 6767       | $-200.000     |

## Funciones implementadas

### Autenticación (Modulo autenticacion.py)
- Validación de usuario y contraseña antes de permitir el acceso al sistema
- Hasta 3 intentos de inicio de sesión
- Bloqueo automático de la cuenta al superar el límite de intentos fallidos
- Distinción entre "usuario no encontrado" y "cuenta bloqueada", con
  mensajes específicos para cada caso

### Consulta de saldo (Modulo datos.py)
- Muestra el saldo actual de la cuenta del usuario autenticado

### Extracción (Modulo Operaciones.py)
- Permite retirar dinero, descontándolo del saldo de la cuenta
- Controla que el monto solicitado no supere el saldo disponible
- Aplica un límite máximo de extracción por operación ($10.000)

### Depósito (Modulo Operaciones.py)
- Permite ingresar dinero a la cuenta, sumándolo al saldo actual

### Transferencia (Modulo Operaciones.py)
- Permite transferir dinero de la cuenta propia a otra cuenta del sistema
- Valida que la cuenta destino exista
- Valida que haya saldo suficiente antes de transferir

### Registro de operaciones (Modulo historial.py)
- Registra cada operación realizada (tipo, monto, fecha/hora)
- Permite consultar el historial de movimientos de la sesión

### Menú principal (Modulo main.py)
- Centraliza el acceso a todas las operaciones disponibles
- Permite cerrar sesión de forma controlada

## Estructura del proyecto

```
cajero/
│
├── main.py             # Punto de entrada del programa y menú principal
├── autenticacion.py     # Login, validación de usuario y contraseña
├── operaciones.py        # Extracción, depósito y transferencia
├── historial.py          # Registro de operaciones realizadas
├── datos.py              # Datos de prueba (usuarios, cuentas, constantes)
└── README.md
```

## Decisiones de diseño

- **Separación en módulos:** cada archivo tiene una responsabilidad
  específica (datos, autenticación, operaciones, historial), siguiendo el
  principio de que cada función/módulo debe encargarse de una sola cosa.
  Esto facilita el trabajo en grupo, ya que distintos integrantes pueden
  trabajar en módulos diferentes.
- **Datos en memoria:** las cuentas y el historial se almacenan en
  estructuras de datos de Python (diccionarios y listas) durante la
  ejecución del programa, sin persistencia en archivo o base de datos, ya
  que no fue un requisito del enunciado.
- **Bloqueo de cuenta:** se optó por bloquear la cuenta tras 3 intentos
  fallidos de inicio de sesión como medida de seguridad básica, en lugar de
  permitir intentos ilimitados.
- **Límite de extracción:** se fijó un monto máximo y minimo por operación de
  extracción, independiente del saldo disponible, simulando una política
  real de cajeros automáticos.

## Limitaciones conocidas

- Los datos no persisten entre ejecuciones: al cerrar el programa, los
  saldos y el historial vuelven a su estado inicial definido en `datos.py`.
- No se contempla la posibiladad que dos usuarios operen la misma cuenta al
  mismo tiempo.
- El sistema utiliza usuarios y contraseñas predefinidos; no existe una
  funcionalidad de alta de nuevos usuarios. Por ahora 

## Estado del proyecto

| Módulo             | Estado        |
|--------------------|---------------|
| `datos.py`         | Completo      |
| `autenticacion.py` | Completo      |
| `main.py`          | En desarrollo |
| `cuenta.py`        | En desarrollo |
| `operaciones.py`   | En desarrollo |
| `historial.py`     | En desarrollo |