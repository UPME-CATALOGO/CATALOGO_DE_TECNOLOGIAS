<div align="center">

  <table width="100%">
    <tr>
      <td align="left" width="20%">
        <img src="https://raw.githubusercontent.com/UPME-CATALOGO/CATALOGO_DE_TECNOLOGIAS/main/logo_UPME_2025.jpg" width="150">
      </td>
      <td align="center" width="60%">
        <h1 style="margin: 0;">Catálogo de Tecnologías 2025</h1>
      </td>
      <td align="right" width="20%">
        <img src="https://raw.githubusercontent.com/UPME-CATALOGO/CATALOGO_DE_TECNOLOGIAS/main/Logos_CIO.png" width="150">
      </td>
    </tr>
  </table>

</div>






## Índice
- [Conceptos generales](#conceptos-generales)
- [Librería Python](#librería-python)
  - [Instalación](#instalación)
  - [Objetos TechsCatalog](#objetos-techscatalog)
    - [Catálogos de Tecnologías](#catálogos-de-tecnologías)
    - [Conjuntos de datos disponibles](#conjuntos-de-datos-disponibles)
    - [¿Cuál conjunto contiene una variable?](#cuál-conjunto-contiene-una-variable)
    - [Ejemplo de uso](#ejemplo-de-uso)
- [Endpoints API](#endpoints-api)

<a id='conceptosGenerales'></a>
# Conceptos generales

Para evaluar la evolución del sector y desarrollar ejercicios de planeación energética de largo plazo se necesitan datos tecnoeconómicos para una variedad de tecnologías. Estos datos están consolidados en el catálogos de tecnologías que resultó de la cooperación Colombia-Dinamarca, a través del Ministerio de Minas y Energía, la Unidad de Planeación Minero-Energética, y la Agencia Danesa de Energía. Los datos contenidos el Catálogo representan valores tecnoeconómicos representativos de las tecnologías.

Este repositorio se crea con el fin de proporcionar herramientas para consultar y obtener información relacionada con las tecnologías de generación y almacenamiento almacenadas en el Catálogo. A través de este paquete, los usuarios pueden acceder a catálogos y conjuntos de datos que describen diversas tecnologías, variables y sus relaciones.

> **Nota**: Para interactuar con los datos disponibles, no es necesario gestionar ningún usuario ni clave de acceso.

Las herramientas están disponibles en los siguientes lenguajes:

| Lenguaje | Nombre | Tipo | Instalación | Habilidad requerida |
|----------|--------|------|-------------|---------------------|
| Python   | [pytccol](https://pypi.org/project/pytccol/) | Librería | <code> $ pip install pytccol </code> | Low Code |

# Pytccol: Paquete Python

> [!WARNING]
> **La librería pytccol es compatible con versiones de Python 3.10.4 y superiores.**

<a id='instalacion'></a>
## Instalación

Para instalar la librería, ejecuta el siguiente comando:

```console
pip install pytccol --index-url https://__token__:<your_personal_token>@gitlab.com/api/v4/projects/68535300/packages/pypi/simple
```

<a id='objetosTechsCatalog'></a>
## Objetos TechsCatalog

**Importación en proyecto**
```python
from pytccol import TechsCatalog
```

<a id='catalogosTecnologias'></a>
### Catálogos de Tecnologías

> [!IMPORTANT]
> El objeto de los catálogos funciona de manera diferente al objeto de lectura de conjuntos de datos.

Puedes acceder a la información utilizando el objeto asociado a los catálogos. Instanciar la clase guarda toda la información en atributos que pueden leerse utilizando las funciones `.get_atributo`.

### Conjuntos de datos disponibles

```python
# Importación
from pytccol import TechsCatalog

# Crear una instancia de catálogo
techs_catalog = TechsCatalog()

# Obtener información de los conjuntos de datos
techs = techs_catalogue.get_data("technologies")
variables = techs_catalogue.get_data("variables")
techs_data = techs_catalogue.get_data("techs_year")

# Obtener información de los conjuntos de datos
print("Tecnologías: ", techs)
print("Variables: ", variables)
print("Información de tecnologías: ", techs_data)
```

<a id='catalogovariables'></a>
### ¿Cuál conjunto contiene una variable?

```python
# Importación
from pytccol import TechsCatalog

# Crear una instancia de catálogo con las variables
techs_variables = TechsCatalog()

# Extraer información sobre las variables
print("Nombre: ", techs_variables.get_name())
print("Metadata: ", techs_variables.get_metadata())
print("Columnas: ", techs_variables.get_columns())

# Dataframe con información de las variables
data = techs_variables.get_data()
print(data)
```

### Ejemplo de uso

> [!NOTE]
> La ejecución del siguiente código puede tardar entre 1 y 2 minutos en completarse, dependiendo del conjunto de datos consultado. Se recomienda usar un cuaderno Jupyter para facilitar la ejecución.

El siguiente código consulta el conjunto de datos asociado con tecnologías de energía y realiza una consulta para fechas arbitrarias sin usar filtros.

```python
# Importación
from pytccol import TechsCatalog

# Buscar el conjunto de datos relacionado con "Fotovoltaicas"
techs_data_filtered = techs_catalogue.get_data(
                        "techs_year", 
                        filters={
                            "technology": "InstFotovResidencial",
                            "variable": "CapGenCentral"
                        }
                    )# Crear una instancia para leer el conjunto de datos

# Recuperar datos
print(techs_data_filtered)
```

# Endpoints API

También puedes consultar los datos directamente a través de la API utilizando los enlaces disponibles. 

> [!WARNING]
> Ambas API tienen **restricciones** para evitar la congestión del servicio. Asegúrate de revisar las limitaciones de cada tipo de consulta.

```
https://www.upme.gov.co/catalogotecnologico/api/technologies/
https://www.upme.gov.co/catalogotecnologico/api/units/
https://www.upme.gov.co/catalogotecnologico/api/categories/
https://www.upme.gov.co/catalogotecnologico/api/variables/


```
## Examples
Data for a specific technology:
```
https://www.upme.gov.co/catalogotecnologico/api/techs_year/?technology=<tech_id>
Example: https://www.upme.gov.co/catalogotecnologico/api/techs_year/?technology=2
```
Data for a specific variable:
```
https://www.upme.gov.co/catalogotecnologico/api/techs_year/?variable=<variable_id>
Example: https://www.upme.gov.co/catalogotecnologico/api/techs_year/?variable=10
```

Data for a specific technology and variable:
```
https://www.upme.gov.co/catalogotecnologico/api/techs_year/?technology=<tech_id>&variable=<variable_id>
Example: https://www.upme.gov.co/catalogotecnologico/api/techs_year/?technology=2&variable=10
```

## Technologies Dictionary
|   ID_TEC | TECNOLOGIA                                                                 | KEY                    | TECH_SHORT_NAME                     |
|---------:|:---------------------------------------------------------------------------|:-----------------------|:------------------------------------|
|        1 | Instalación fotovoltaica a escala residencial, techo - conectada a la red  | InstFotovResidencial   | PV residencial                      |
|        2 | Instalación fotovoltaica a escala industrial, techo - conectada a la red   | InstFotovIndustrial    | PV industrial                       |
|        3 | Planta fotovoltaica a pequeña escala                                       | PlantaFotovPeq         | PV flotante pequeña esc.            |
|        4 | Planta fotovoltaica a gran escala                                          | PlantaFotovGran        | PV flotante gran esc..              |
|        5 | Planta fotovoltaica flotante                                               | PlantaFotovFlotante    | PV flotante                         |
|        6 | Energía eólica – Terrestre a gran escala                                   | EolicaTerresGran       | Eólica terrrestre gran esc.         |
|        7 | Energía eólica – Terrestre a gran escala                                   | EolicaTerresGran2      | Eólica terrrestre gran esc. 2       |
|        8 | Energía eólica - Pequeñas turbinas eólicas terrestres < 1 MW               | PeqTurbEolicaTerrestre | Eólica terrestres pequeñas turbinas |
|        9 | Energía eólica – costa afuera con cimentación fija                         | EolicaCostaCimentFija  | Eólica cimentación fija             |
|       10 | Energía eólica costa afuera - flotante                                     | EolicaCostaFlotante    | Eolica costa afuera flotante        |
|       11 | Central hidroeléctrica a filo de agua – gran escala                        | HidroFiloAguaGran      | Hidroeléctrica filo de agua grande  |
|       12 | Central hidroeléctrica a filo de agua – Mediana/Pequeña escala             | HidroFiloAguaMedPeq    | Hidroeléctrica filo de agua pequeña |
|       13 | Central hidroeléctrica a filo de agua – Mini/Micro                         | HidroFiloAguaMiniMicro | Hidroeléctrica filo de agua mini    |
|       14 | Central hidroeléctrica de embalse                                          | HidroEmbalse           | Central hidroeléctrica de embalse   |
|       15 | Planta geotérmica flash                                                    | GeotFlash              | Geotérmica flash                    |
|       16 | Planta geotérmica binaria                                                  | GeotBinaria            | Geotérmica binaria                  |
|       17 | Central de biomasa – (aceite de palma / caña de azúcar / cáscara de arroz) | CentBiomasa            | Biomasa aceite                      |
|       18 | Central de biogás                                                          | CentBiogas             | Central de biogás                   |
|       19 | Central supercrítica eléctrica de carbón                                   | CentElectCarbon        | Carbón supercrítica                 |
|       20 | Ciclo combinado con turbina de gas                                         | CicloCombTurbGas       | Ciclo combinado gas                 |
|       21 | Turbina de gas de ciclo simple (o convencional)                            | TurbGasCicloSimp       | Turbina de gas ciclo simple         |
|       22 | Planta de incineración de residuos (Waste-to-Energy)                       | IncinResiduos          | Waste to energy                     |
|       23 | Nuclear – Reactores convencionales (PWR)                                   | NuclRectConvenc        | Nuclear reactores convencionales    |
|       24 | Nuclear – Pequeños reactores modulares                                     | NucPeqRectModu         | Nuclear pequeños reactores          |
|       25 | Almacenamiento en baterías de iones de litio – Gran escala                 | AlmacBateLitioGran     | Baterías litio gran escala          |
|       26 | Almacenamiento en baterías de iones de litio – Pequeña escala              | AlmacBateLitioPeq      | Baterías litio pequeña escala       |
|       27 | Almacenamiento hidráulico por bombeo – reservorios naturales               | AlmacHidraReservNatu   | Almacenamiento bombeo reservorios   | 

## Variables Dictionary
|   ID_VAR |   ID_CAT | VARIABLE                                                           | CATEGORIA                                    | KEY                      |
|---------:|---------:|:-------------------------------------------------------------------|:---------------------------------------------|:-------------------------|
|        2 |        1 | Capacidad de generación de toda la central                         | Datos energéticos/técnicos                   | CapGenCentral            |
|        9 |        1 | Interrupción forzada                                               | Datos energéticos/técnicos                   | InterrupForzada          |
|       10 |        1 | Interrupción planificada                                           | Datos energéticos/técnicos                   | InterrupPlanificada      |
|       17 |        1 | Vida útil técnica                                                  | Datos energéticos/técnicos                   | VidaUtilTec              |
|       18 |        1 | Tiempo de construcción                                             | Datos energéticos/técnicos                   | TiempoConstr             |
|       19 |        1 | Espacio requerido                                                  | Datos energéticos/técnicos                   | EspacioRequer            |
|        1 |        2 | Factor de planta teórico                                           | Datos adicionales para plantas no térmicas   | FactPlantaTeorico        |
|        2 |        2 | Factor de planta incluidas las interrupciones                      | Datos adicionales para plantas no térmicas   | FactPlantaInterrup       |
|        1 |        3 | Velocidad de rampa                                                 | Capacidad de regulación                      | VelRampa                 |
|        2 |        3 | Carga mínima                                                       | Capacidad de regulación                      | CargaMin                 |
|        3 |        3 | Tiempo de arranque en caliente                                     | Capacidad de regulación                      | TiempoArrCaliente        |
|        4 |        3 | Tiempo de arranque en frío                                         | Capacidad de regulación                      | TiempoArrFrio            |
|        1 |        4 | PM 2.5                                                             | Medio ambiente                               | PM25                     |
|        2 |        4 | SO2                                                                | Medio ambiente                               | SO2                      |
|        3 |        4 | NOx                                                                | Medio ambiente                               | Nox                      |
|        4 |        4 | CH4                                                                | Medio ambiente                               | CH4                      |
|        5 |        4 | N2O                                                                | Medio ambiente                               | N2O                      |
|        1 |        5 | Horas de carga completa                                            | Salida                                       | HrsCargaCompl            |
|        2 |        5 | Horas de carga máxima                                              | Salida                                       | HrsCargaMax              |
|        1 |        6 | Inversión específica - sistema total                               | Datos financieros                            | InvEspecSisTotal         |
|        2 |        6 | Inversión específica - sistema total por DC                        | Datos financieros                            | InvEspecSisTotalDc       |
|       10 |        6 | Costo del módulo PV                                                | Datos financieros                            | CostoModPv               |
|       11 |        6 | Costo del inversor PV                                              | Datos financieros                            | CostoInvPv               |
|       14 |        6 | Balance del costo de la planta                                     | Datos financieros                            | BalCostoPlanta           |
|       12 |        6 | Costo de instalación                                               | Datos financieros                            | CostInst                 |
|       15 |        6 | O&M fijas                                                          | Datos financieros                            | OMFijas                  |
|       16 |        6 | O&M variables                                                      | Datos financieros                            | OMVariables              |
|       13 |        6 | Costo de puesta en marcha                                          | Datos financieros                            | CostoPuestaMarcha        |
|        1 |        8 | Irradiancia horizontal global                                      | Datos específicos de la tecnología           | IrrHorizGlobal           |
|        8 |        8 | Factor de dimensionamiento DC/AC                                   | Datos específicos de la tecnología           | FactDimDcAc              |
|       13 |        8 | Factor de transposición                                            | Datos específicos de la tecnología           | FactTransposicion        |
|       16 |        8 | Ratio de rendimiento                                               | Datos específicos de la tecnología           | RatRendimiento           |
|       18 |        8 | Eficiencia de conversión del módulo PV                             | Datos específicos de la tecnología           | EficConvModPV            |
|       19 |        8 | Vida útil del inversor                                             | Datos específicos de la tecnología           | VidaUtilInv              |
|       20 |        8 | Degradación media anual de las horas a plena carga                 | Datos específicos de la tecnología           | DegraAnualPlenaCarga     |
|        9 |        7 | Inversión nominal                                                  | Datos financieros - por capacidad pico de DC | InvNominalDc             |
|       10 |        7 | Costo del módulo PV                                                | Datos financieros - por capacidad pico de DC | CostoModPVDc             |
|       11 |        7 | Costo del inversor PV                                              | Datos financieros - por capacidad pico de DC | CostoInvPVDc             |
|       14 |        7 | Balance del costo de la planta                                     | Datos financieros - por capacidad pico de DC | BalCostoPlantaDc         |
|       12 |        7 | Costo de instalación                                               | Datos financieros - por capacidad pico de DC | CostInstDc               |
|       15 |        7 | O&M fijas                                                          | Datos financieros - por capacidad pico de DC | OMFijasDc                |
|       16 |        7 | O&M variables                                                      | Datos financieros - por capacidad pico de DC | OMVariablesDc            |
|        9 |        6 | Inversión nominal                                                  | Datos financieros                            | InvNominal               |
|        1 |        1 | Capacidad de generación de una unidad                              | Datos energéticos/técnicos                   | CapGenUnidad             |
|       15 |        1 | Media anual de horas a plena carga                                 | Datos energéticos/técnicos                   | MedAnualHrsPlenaCarga    |
|        3 |        6 | Inversión específica - de la cual equipo                           | Datos financieros                            | InvEspecEquipo           |
|        4 |        6 | Inversión específica - de la cual instalación                      | Datos financieros                            | InvEspecInst             |
|        5 |        8 | Altura del eje                                                     | Datos específicos de la tecnología           | AlturaEje                |
|        2 |        8 | Diámetro del rotor                                                 | Datos específicos de la tecnología           | DiamRotor                |
|       12 |        8 | Potencia específica                                                | Datos específicos de la tecnología           | PotenciaEspec            |
|       11 |        1 | Altura del cubo                                                    | Datos energéticos/técnicos                   | AlturaCubo               |
|       12 |        1 | Potencia específica                                                | Datos energéticos/técnicos                   | PotenciaEspec2           |
|        7 |        6 | Inversión específica - de conexión a la red                        | Datos financieros                            | InvEspecConex            |
|       17 |        8 | Disponibilidad                                                     | Datos específicos de la tecnología           | Disponibilidad           |
|        6 |        1 | Eficiencia eléctrica neta nominal                                  | Datos energéticos/técnicos                   | EficElecNetaNom          |
|        7 |        1 | Eficiencia eléctrica neta media anual                              | Datos energéticos/técnicos                   | EficElecNetaMedAnual     |
|        3 |        8 | Costos de exploración                                              | Datos específicos de la tecnología           | CostosExploracion        |
|       10 |        8 | Costo de expansión de capacidad de la inversión nominal            | Datos específicos de la tecnología           | CostosExpansionCapInvNom |
|        5 |        3 | Tiempo mínimo de funcionamiento                                    | Capacidad de regulación                      | TiempoMinFuncion         |
|        6 |        3 | Tiempo mínimo de inactividad                                       | Capacidad de regulación                      | TiempoMinActiv           |
|        6 |        8 | Capacidad de tratamiento de residuos                               | Datos específicos de la tecnología           | CapTratResiduos          |
|       11 |        8 | Calor específico                                                   | Datos específicos de la tecnología           | CalorEspecifico          |
|        5 |        1 | Capacidad de almacenamiento de energía para una unidad             | Datos energéticos/técnicos                   | CapAlmacEnergiaUnidad    |
|        3 |        1 | Capacidad de entrada de una unidad                                 | Datos energéticos/técnicos                   | CapacEntradaUnidad       |
|        4 |        1 | Capacidad de salida de una unidad                                  | Datos energéticos/técnicos                   | CapacSalidaUnidad        |
|       13 |        1 | Tiempo de descarga                                                 | Datos energéticos/técnicos                   | TiempoDescarga           |
|        8 |        1 | Eficiencia de ciclo completo AC                                    | Datos energéticos/técnicos                   | EficCicloCompletAc       |
|       14 |        1 | Tasa de autodescarga                                               | Datos energéticos/técnicos                   | TasaAutodescarga         |
|       16 |        1 | Densidad de energía                                                | Datos energéticos/técnicos                   | DensEnergia              |
|        7 |        3 | Tiempo de respuesta desde inactivo hasta descarga nominal completa | Capacidad de regulación                      | TiempoInacDescNomComplet |
|        8 |        3 | Tiempo de respuesta desde carga nominal completa hasta descarga    | Capacidad de regulación                      | TiempoRespCargaDescarga  |
|        5 |        6 | Inversión específica - componente energético                       | Datos financieros                            | InvEspecCompEnerg        |
|        6 |        6 | Inversión específica - capacidad                                   | Datos financieros                            | InvEspecCapacidad        |
|        8 |        6 | Inversión específica - proyecto                                    | Datos financieros                            | InvEspecProyecto         |
|        4 |        8 | Costo de expansión del almacenamiento de energía                   | Datos específicos de la tecnología           | CostoExpansAlmacEnergia  |
|        9 |        8 | Costo de expansión de la capacidad de salida                       | Datos específicos de la tecnología           | CostoExpansCapSalida     |
|       15 |        8 | Inversión total                                                    | Datos específicos de la tecnología           | InvTotal                 |
|        7 |        8 | Tamaño del reservorio                                              | Datos específicos de la tecnología           | TamanoReservorio         |
|       14 |        8 | Tiempo de carga/descarga                                           | Datos específicos de la tecnología           | TiempoCargaDescarga      |
</div>
