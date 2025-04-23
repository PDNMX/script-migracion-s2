# Herramienta de Transformación JSON para el S2 Sistema de los servidores públicos que intervengan en procedimientos de contrataciones públicas  v1 a v1.1

## Descripción

Esta herramienta proporciona un script para facilitar la migración de datos estructurados en formato JSON desde la versión 1.0 hacia la nueva especificación 1.1, diseñada conforme a la normatividad actualizada. La herramienta permite cargar, transformar y almacenar la información original de acuerdo al nuevo estándar establecido.

## Motivación

Debido a cambios en la normatividad, se ha establecido un nuevo formato de captura de datos que requiere una restructuración del esquema JSON original. Esta herramienta facilita la transición entre ambas versiones para que los usuarios puedan actualizar sus datos sin necesidad de realizar una migración manual.

## Características principales

- **Carga de datos**: Importación de archivos JSON con estructura v1.0
- **Transformación automática**: Mapeo y restructuración de datos al formato v1.1
- **Validación**: Verificación de la integridad y conformidad con el nuevo esquema
- **Exportación**: Generación de archivos JSON compatibles con la versión 1.1

## Instalación

```bash
# Clonar el repositorio
git clone https://github.com/[usuario]/json-transform-v1-to-v1.1.git

# Acceder al directorio
cd json-transform-v1-to-v1.1

# Instalar dependencias (si aplica)
npm install
# o
pip install -r requirements.txt
```

## Uso básico

```javascript
// Ejemplo de uso básico
const transformador = require('./transformador');

// Cargar archivo JSON v1.0
const datosOriginales = transformador.cargarJSON('datos-v1.json');

// Transformar a formato v1.1
const datosTransformados = transformador.transformar(datosOriginales);

// Guardar resultado
transformador.guardarJSON(datosTransformados, 'datos-v1.1.json');
```

## Diccionario de datos completo

### Versión 1.0 (Original)

La estructura JSON original (v1.0) contiene los siguientes campos principales:

| Campo | Tipo | Descripción |
|-------|------|-------------|
| id | String (Alfanumérico) | Identificador único del registro |
| fechaCaptura | String (Fecha ISO 8601) | Fecha de captura de la información |
| ejercicioFiscal | String (Alfanumérico) | Año fiscal al que corresponde el registro |
| ramo | Object | Información sobre el ramo |
| ramo.clave | Number | Clave numérica del ramo |
| ramo.valor | String | Valor alfanumérico que describe el ramo |
| rfc | String | RFC del servidor público |
| curp | String | CURP del servidor público |
| nombres | String | Nombres del servidor público |
| primerApellido | String | Primer apellido del servidor público |
| segundoApellido | String | Segundo apellido del servidor público |
| genero | Object | Información sobre el género |
| genero.clave | String (enum) | Clave alfanumérica del género |
| genero.valor | String | Valor descriptivo del género |
| institucionDependencia | Object | Información sobre la institución o dependencia |
| institucionDependencia.nombre | String | Nombre de la institución o dependencia |
| institucionDependencia.siglas | String | Siglas de la institución o dependencia |
| institucionDependencia.clave | String | Clave alfanumérica de la institución |
| puesto | Object | Información sobre el puesto |
| puesto.nombre | String | Nombre del puesto |
| puesto.nivel | String | Nivel jerárquico del puesto |
| tipoArea | Array de Objects | Información sobre el tipo de área |
| tipoArea.clave | String (enum) | Clave alfanumérica del tipo de área |
| tipoArea.valor | String | Valor descriptivo del tipo de área |
| nivelResponsabilidad | Array de Objects | Información sobre el nivel de responsabilidad |
| nivelResponsabilidad.clave | String (enum) | Clave alfanumérica del nivel de responsabilidad |
| nivelResponsabilidad.valor | String | Valor descriptivo del nivel de responsabilidad |
| tipoProcedimiento | Array de Objects | Información sobre el tipo de procedimiento |
| tipoProcedimiento.clave | Integer | Clave numérica del tipo de procedimiento |
| tipoProcedimiento.valor | String | Valor descriptivo del tipo de procedimiento |
| superiorInmediato | Object | Información sobre el superior inmediato |
| superiorInmediato.nombres | String | Nombres del superior inmediato |
| superiorInmediato.primerApellido | String | Primer apellido del superior inmediato |
| superiorInmediato.segundoApellido | String | Segundo apellido del superior inmediato |
| superiorInmediato.curp | String | CURP del superior inmediato |
| superiorInmediato.rfc | String | RFC del superior inmediato |
| superiorInmediato.puesto | Object | Información sobre el puesto del superior inmediato |
| superiorInmediato.puesto.nombre | String | Nombre del puesto del superior inmediato |
| superiorInmediato.puesto.nivel | String | Nivel jerárquico del puesto del superior inmediato |
| observaciones | String | Observaciones adicionales |

### Versión 1.1 (Nueva)

La nueva estructura JSON (v1.1) redefine y reorganiza los campos:

| Nombre del Campo | Ruta JSON | Clasificación | Obligatorio | Tipo de dato |
|------------------|-----------|---------------|-------------|--------------|
| id | / | Público | Sí | String |
| fecha | / | Público | Si | String |
| ejercicio | / | Público | Si | String |
| datosGenerales | / | Público | Si | Object |
| nombre | /datosGenerales | Público | Si | String |
| primerApellido | /datosGenerales | Público | Si | String |
| segundoApellido | /datosGenerales | Público | No | String |
| curp | /datosGenerales | Confidencial | Si | String |
| rfc | /datosGenerales | Confidencial | Si | String |
| sexo | /datosGenerales | Público | Si | String(enum) |
| empleoCargoComision | / | Público | Si | Object |
| entidadFederativa | /empleoCargoComision | Público | Si | String (enum) |
| nivelOrdenGobierno | /empleoCargoComision | Público | Si | String (enum) |
| ambitoPublico | /empleoCargoComision | Público | Si | String(enum) |
| nombreEntePublico | /empleoCargoComision | Público | Si | String |
| siglasEntePublico | /empleoCargoComision | Público | No | String |
| nivelJerarquico | /empleoCargoComision | Público | Si | Object |
| clave | /empleoCargoComision/nivelJerarquico | Público | Si | String (enum) |
| valor | /empleoCargoComision/nivelJerarquico | Público | No | String |
| denominacion | /empleoCargoComision | Público | Si | String |
| areaAdscripcion | /empleoCargoComision | Público | Si | String |
| tipoProcedimineto | / | Público | Sí | String(enum) |
| tipoContratacion | /tipoProcedimineto[] | Público | Sí | Array Object |
| clave | /tipoProcedimineto | Público | Sí | String(enum) |
| contratacionAdquisiones | /tipoProcedimineto | Público | Sí | Object |
| tipoArea | /tipoProcedimiento/contratacionAdquisiones | Público | No | String(enum) |
| valorTipoArea | /tipoProcedimiento/contratacionAdquisiones | Público | No | String |
| nivelesResponsabilidad | /tipoProcedimiento/contratacionAdquisiones | Público | No | Object |
| autorizacionDictamen | /tipoProcedimiento/contratacionAdquisiones/nivelesResponsabilidad | Público | No | String(enum) |
| justificacionLicitacion | /tipoProcedimiento/contratacionAdquisiones/nivelesResponsabilidad | Público | No | String(enum) |
| convocatoriaInvitacion | /tipoProcedimiento/contratacionAdquisiones/nivelesResponsabilidad | Público | No | String(enum) |
| evaluacionProposiciones | /tipoProcedimiento/contratacionAdquisiones/nivelesResponsabilidad | Público | No | String(enum) |
| adjudicacionContrato | /tipoProcedimiento/contratacionAdquisiones/nivelesResponsabilidad | Público | No | String(enum) |
| formalizacionContrato | /tipoProcedimiento/contratacionAdquisiones/nivelesResponsabilidad | Público | No | String(enum) |
| datosGeneralesProcedimientos | /tipoProcedimiento/contratacionAdquisiones[] | Público | No | Array |
| contratacionObra | /tipoProcedimineto | Público | Sí | Object |
| tipoArea | /tipoProcedimineto/contratacionObra | Público | No | String(enum) |
| valorContratacionObra | /tipoProcedimineto/contratacionObra | Público | No | String |
| nivelesResponsabilidad | /tipoProcedimineto/contratacionObra | Público | Sí | Object |
| otorgamientoConcesiones | / | Público | Sí | Object |
| tipoActo | /otorgamientoConcesiones | Público | Sí | String(enum) |
| nivelesResponsabilidad | /otorgamientoConcesiones | Público | Sí | Object |
| enajenacionBienes | / | Público | Sí | Object |
| nivelesResponsabilidad | /enajenacionBienes | Público | Sí | Object |
| avaluosJustipreciacion | / | Público | Sí | Object |
| nivelesResponsabilidad | /dictaminacionAvaluos | Público | Sí | Object |
| observaciones | / | Confidencial | No | String |

## Cambios principales entre versiones

### Estructura principal

| Versión 1.0 | Versión 1.1 | Observaciones |
|-------------|-------------|---------------|
| id | id | Se mantiene igual |
| fechaCaptura | fecha | Se simplifica el nombre |
| ejercicioFiscal | ejercicio | Se simplifica el nombre |
| rfc | datosGenerales/rfc | Se mueve a objeto datosGenerales, ahora confidencial |
| curp | datosGenerales/curp | Se mueve a objeto datosGenerales, ahora confidencial |
| nombres | datosGenerales/nombre | Cambio a singular y se mueve a datosGenerales |
| primerApellido | datosGenerales/primerApellido | Se mueve a datosGenerales |
| segundoApellido | datosGenerales/segundoApellido | Se mueve a datosGenerales, ahora opcional |
| genero | datosGenerales/sexo | Cambio de nombre y estructura simplificada |
| institucionDependencia | empleoCargoComision | Reorganizado en nueva estructura |
| puesto | empleoCargoComision/nivelJerarquico | Reorganizado en nueva estructura |
| tipoArea | tipoProcedimineto/contratacionAdquisiones/tipoArea | Reorganizado por tipo de procedimiento |
| nivelResponsabilidad | Múltiples rutas según el tipo de procedimiento | Segregado por tipo de procedimiento |
| tipoProcedimiento | tipoProcedimineto | Reorganizado con estructura específica por tipo |
| superiorInmediato | Eliminado | No se incluye en la nueva versión |
| observaciones | observaciones | Se mantiene pero ahora es confidencial |

### Nuevas secciones en la versión 1.1

1. **Segregación por tipo de procedimiento**:
   - contratacionAdquisiones
   - contratacionObra
   - otorgamientoConcesiones
   - enajenacionBienes
   - avaluosJustipreciacion (dictaminacionAvaluos)

2. **Información sobre beneficiarios finales**:
   - datosBeneficiariosFinales (para diferentes tipos de procedimientos)

3. **Más información sobre procedimientos**:
   - datosGeneralesProcedimientos (con detalles específicos según el tipo)

4. **Clasificación explícita de información**:
   - Público vs. Confidencial
   - Obligatorio vs. Opcional

## Diferencias en la estructura jerárquica

- **Versión 1.0**: Estructura relativamente plana con anidación limitada.
- **Versión 1.1**: Mayor profundidad y segmentación por tipo de procedimiento.

### Cambios en estructura jerárquica

- **Datos generales**: Se consolidan datos personales en el objeto `datosGenerales`
- **Empleo y cargo**: Se reorganiza en `empleoCargoComision` con estructura mejorada
- **Procedimientos**: Se especifica por tipo en `tipoProcedimineto` 
  - contratacionAdquisiones
  - contratacionObra
  - otorgamientoConcesiones
  - enajenacionBienes
  - avaluosJustipreciacion
- **Responsabilidades**: Se redefine la estructura para mejor clasificación por niveles y tipos

## Consideraciones importantes para la migración

- **Seguridad de datos**: La nueva versión marca explícitamente datos como "Confidencial" (rfc, curp, observaciones).
- **Campos obligatorios**: Se especifican claramente los campos obligatorios en la versión 1.1.
- **Valores enumerados**: Múltiples campos utilizan valores enumerados (enum) que deben respetarse.
- **Estructuras anidadas**: La versión 1.1 tiene estructuras más profundamente anidadas.
- **Relaciones entre datos**: Mayor relación entre niveles de responsabilidad y tipos de procedimientos.
- **Validación**: Es necesario validar los datos transformados según los requisitos de la nueva estructura.

## Ejemplos

### JSON Versión 1.0
```json
{
  "id": "REG12345",
  "fechaCaptura": "2023-05-15T10:30:00Z",
  "ejercicioFiscal": "2023",
  "ramo": {
    "clave": 12,
    "valor": "Secretaría de Salud"
  },
  "rfc": "XAXX010101000",
  "curp": "XEXX010101HNEXXXA4",
  "nombres": "Juan Carlos",
  "primerApellido": "Pérez",
  "segundoApellido": "López",
  "genero": {
    "clave": "M",
    "valor": "Masculino"
  },
  "institucionDependencia": {
    "nombre": "Hospital General",
    "siglas": "HG",
    "clave": "HG123"
  },
  "puesto": {
    "nombre": "Director General",
    "nivel": "DIRECTOR_GENERAL"
  },
  "tipoArea": [
    {
      "clave": "T",
      "valor": "TÉCNICA"
    }
  ],
  "nivelResponsabilidad": [
    {
      "clave": "A",
      "valor": "ATENCIÓN"
    }
  ],
  "tipoProcedimiento": [
    {
      "clave": 1,
      "valor": "CONTRATACIONES"
    }
  ],
  "superiorInmediato": {
    "nombres": "Ana María",
    "primerApellido": "Rodríguez",
    "segundoApellido": "Gómez",
    "curp": "ROGA680519MDFMRN09",
    "rfc": "ROGA680519ABC",
    "puesto": {
      "nombre": "Subsecretario",
      "nivel": "SUBSECRETARIO"
    }
  },
  "observaciones": "Persona encargada de la dirección general desde enero 2023."
}
```

### JSON Versión 1.1 (Transformado)
```json
{
  "id": "REG12345",
  "fecha": "2023-05-15T10:30:00Z",
  "ejercicio": "2023",
  "datosGenerales": {
    "nombre": "Juan Carlos",
    "primerApellido": "Pérez",
    "segundoApellido": "López",
    "curp": "XEXX010101HNEXXXA4",
    "rfc": "XAXX010101000",
    "sexo": "M"
  },
  "empleoCargoComision": {
    "entidadFederativa": "09",
    "nivelOrdenGobierno": "FEDERAL",
    "ambitoPublico": "EJECUTIVO",
    "nombreEntePublico": "Hospital General",
    "siglasEntePublico": "HG",
    "nivelJerarquico": {
      "clave": "DIR_GRAL",
      "valor": "DIRECTOR GENERAL"
    },
    "denominacion": "Director General",
    "areaAdscripcion": "Dirección General"
  },
  "tipoProcedimineto": "CONTRATACIONES_PUBLICAS",
  "contratacionAdquisiones": {
    "tipoArea": "TECNICA",
    "valorTipoArea": "TÉCNICA",
    "nivelesResponsabilidad": {
      "autorizacionDictamen": "SI",
      "justificacionLicitacion": "NO",
      "convocatoriaInvitacion": "SI",
      "evaluacionProposiciones": "SI",
      "adjudicacionContrato": "SI",
      "formalizacionContrato": "SI"
    },
    "datosGeneralesProcedimientos": [
      {
        "numeroExpedienteFolio": "CONT-2023-001",
        "tipoProcedimiento": "LICITACION_PUBLICA",
        "materia": "ADQUISICIONES"
      }
    ]
  },
  "contratacionObra": {
    "tipoArea": "TECNICA",
    "valorContratacionObra": "TÉCNICA",
    "nivelesResponsabilidad": {
      "autorizacionDictamen": "NO",
      "justificacionLicictacion": "NO",
      "convocatoriaInvitacion": "NO",
      "evaluacionProposiciones": "NO",
      "adjudicacionContrato": "NO",
      "formalizacionContrato": "NO"
    }
  },
  "otorgamientoConcesiones": {
    "tipoActo": "NO_APLICA",
    "nivelesResponsabilidad": {
      "convocatoriaLicitacion": "NO",
      "dictamenesOpiniones": "NO",
      "visitasVerificacion": "NO",
      "evaluacionCumplimiento": "NO",
      "determinacionOtorgamiento": "NO"
    }
  },
  "enajenacionBienes": {
    "nivelesResponsabilidad": {
      "autorizacionesDictamenes": "NO",
      "analisisAutorizacion": "NO",
      "modificacionBases": "NO",
      "presentacionOfertas": "NO",
      "evaluacionOfertas": "NO",
      "adjudicacionBienes": "NO",
      "formalizacionContrato": "NO"
    }
  },
  "avaluosJustipreciacion": {
    "nivelesResponsabilidad": {
      "propuestasAsignaciones": "NO",
      "asignacionAvaluos": "NO",
      "emisionDictamenes": "NO"
    }
  },
  "observaciones": "Persona encargada de la dirección general desde enero 2023."
}
```

## Contribución

Las contribuciones son bienvenidas. Para contribuir:

1. Haz un fork del repositorio
2. Crea una rama para tu característica (`git checkout -b feature/nueva-caracteristica`)
3. Realiza tus cambios
4. Ejecuta las pruebas
5. Haz commit de tus cambios (`git commit -m 'Añadir nueva característica'`)
6. Haz push a la rama (`git push origin feature/nueva-caracteristica`)
7. Abre un Pull Request

## Licencia

Este proyecto está licenciado bajo [especificar licencia] - ver archivo LICENSE para más detalles.

## Contacto

Para dudas o sugerencias, contactar a [correo o información de contacto].
