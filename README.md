# Commands-Config-NET

## Migracion NET6 to NET8

```
Paso 1: Preparar el Entorno de Desarrollo
Antes de realizar cualquier cambio, asegúrate de tener todo lo necesario para trabajar con .NET 8:

Instalar .NET 8 SDK:

Descarga e instala el SDK de .NET 8 desde el sitio oficial.

Verifica que está instalado correctamente con el siguiente comando:

dotnet --version
Actualizar Visual Studio:

Si usas Visual Studio, asegúrate de tener la última versión (Visual Studio 2022 o superior) con soporte para .NET 8.
En Visual Studio, ve a Herramientas -> Obtener herramientas y características y asegúrate de tener las cargas de trabajo necesarias para .NET.
Paso 2: Actualizar los Archivos de Proyecto (.csproj)
Cada capa de tu solución (API, Negocio, Dominio, Infraestructura, Entidades) tiene un archivo .csproj que define el framework objetivo.

Cambiar la versión de .NET 6 a .NET 8 en cada archivo .csproj:
Abre cada archivo .csproj y cambia el TargetFramework de net6.0 a net8.0.

Ejemplo:

De:

xml

<TargetFramework>net6.0</TargetFramework>
A:

xml

<TargetFramework>net8.0</TargetFramework>
Asegúrate de realizar este cambio en todas las capas, es decir, API, Negocio, Dominio, Infraestructura, Entidades.

Actualizar la versión de las dependencias NuGet:
Si tu solución usa paquetes NuGet, asegúrate de actualizarlos a versiones compatibles con .NET 8.

Puedes actualizar los paquetes manualmente desde el archivo .csproj o mediante comandos:

dotnet restore
dotnet outdated
Luego, si es necesario, actualiza los paquetes utilizando:

dotnet add package [NombreDelPaquete] --version [VersiónCompatible]
Paso 3: Revisar y Actualizar el Código Según los Cambios en .NET 8
Aunque la mayor parte de tu código debería funcionar sin modificaciones, es posible que algunos cambios en la API o en
las bibliotecas de .NET hayan afectado tu aplicación. Aquí tienes algunas áreas a revisar:

1. API de ASP.NET Core (si tienes una API en la capa de presentación):
Revisa los métodos y características que puedan haber cambiado en la nueva versión de ASP.NET Core (parte de .NET 8).
Asegúrate de que todo en tu archivo Program.cs o Startup.cs esté correctamente configurado.
2. Inyección de Dependencias:
Verifica que las configuraciones de inyección de dependencias en tu proyecto se sigan realizando correctamente.
Las configuraciones de servicios (middleware, bases de datos, etc.) podrían haber cambiado ligeramente.
3. Entidades y Acceso a Datos:
Si usas Entity Framework Core, asegúrate de actualizar la versión de EF Core a la versión que sea compatible con .NET 8.
Si tu código depende de métodos descontinuados o cambiados, realiza los ajustes necesarios en las consultas o configuraciones de la base de datos.
4. Métodos y Librerías Descontinuadas:
Consulta la documentación de .NET 8 para ver si algunas funciones o clases de .NET 6 han sido descontinuadas o modificadas.
Asegúrate de reemplazar estos métodos con las alternativas apropiadas.
Paso 4: Ejecutar y Probar el Proyecto
Después de realizar todos los cambios en los archivos de proyecto y actualizar el código, es hora de probar la solución:

Compilar el Proyecto:

Ejecuta la compilación del proyecto para asegurarte de que todo esté correctamente configurado y no haya errores de compilación.

dotnet build
Ejecutar Pruebas Unitarias:

Si tienes pruebas unitarias en tu proyecto, ejecútalas para asegurarte de que no haya regresiones después de la migración.

dotnet test
Pruebas Manuales:

Asegúrate de probar de manera manual las funcionalidades más críticas de tu aplicación para garantizar que todo siga funcionando correctamente.
Paso 5: Verificar Desempeño y Optimizaciones
Aprovecha las mejoras de rendimiento y optimizaciones de .NET 8:

Benchmarking:

Si es posible, realiza pruebas de rendimiento para verificar si hay mejoras o cambios en el rendimiento.
Aprovechar las Nuevas Características de .NET 8:

Investiga las nuevas características y mejoras de .NET 8, como mejoras en la gestión de memoria, mejoras en
ASP.NET Core, y nuevos patrones o herramientas que puedas implementar en tu solución.
Paso 6: Desplegar la Aplicación
Una vez que el proyecto esté funcionando correctamente en tu entorno de desarrollo y pruebas, es hora de desplegar la aplicación.

Actualizar Contenedores (si usas Docker): Si tu aplicación está desplegada usando Docker,
asegúrate de actualizar la imagen base del contenedor a una compatible con .NET 8.

Ejemplo en tu Dockerfile:

dockerfile
Copy
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
Desplegar en Producción:

Despliega la nueva versión de tu aplicación en el entorno de producción y monitorea su funcionamiento.
Paso 7: Monitorear el Sistema
Después de la migración y el despliegue, realiza un monitoreo continuo de la aplicación para detectar
cualquier problema de rendimiento o errores que puedan surgir en el entorno de producción.

Resumen
La migración de un proyecto basado en Clean Architecture de .NET 6 a .NET 8 requiere actualizar los archivos de proyecto,
verificar la compatibilidad de dependencias, ajustar el código según las nuevas características o descontinuaciones de la API
y realizar pruebas exhaustivas. Una vez completado, asegúrate de realizar un despliegue cuidadoso y monitorear el rendimiento
de la aplicación. Con una planificación adecuada, la migración a .NET 8 puede traer mejoras significativas en rendimiento y nuevas funcionalidades.

```

## Pruebas Unitarias NET

```
Para ejecutar pruebas unitarias en un proyecto .NET y ver el porcentaje de cobertura de código junto con otros parámetros,
puedes utilizar el comando dotnet test con algunas opciones adicionales.

Aquí te muestro cómo hacerlo:

Ejecutar pruebas unitarias con cobertura: Para ejecutar las pruebas unitarias de tu proyecto y obtener el porcentaje de cobertura, utiliza el siguiente comando:

bash
Copy
dotnet test --collect:"Code Coverage"
El parámetro --collect:"Code Coverage" indica que se debe recoger la información de cobertura del código durante la ejecución de las pruebas.

Ver resultados de la cobertura: Una vez que hayas ejecutado las pruebas, los resultados de la cobertura de código se
almacenan en un archivo de salida (por lo general en un archivo .coverage o similar en la carpeta TestResults). Para visualizar estos
resultados, puedes usar herramientas como Visual Studio, o puedes utilizar el siguiente comando para generar un informe HTML de la cobertura de código:

bash
Copy
dotnet reportgenerator -reports:TestResults\*.xml -targetdir:coverage-report
Esto generará un informe HTML en el directorio coverage-report.

Especificar parámetros adicionales de dotnet test: A continuación se muestran algunos parámetros adicionales que puedes usar
con dotnet test para obtener más detalles o personalizar el comportamiento de la ejecución de las pruebas:

Ejecutar pruebas en paralelo:

dotnet test --parallel
Especificar un filtro de pruebas: Si deseas ejecutar solo un conjunto específico de pruebas (por ejemplo, por nombre), puedes usar el parámetro --filter:

dotnet test --filter FullyQualifiedName~TestMethodName
Mostrar detalles adicionales: Si quieres ver más detalles sobre la ejecución de las pruebas, puedes usar la opción --verbosity:

dotnet test --verbosity detailed
Especificar un archivo de configuración: Si tienes un archivo de configuración (como un archivo .runsettings), puedes usarlo con el parámetro --settings:

dotnet test --settings mysettings.runsettings
Otros ejemplos:

Especificar un framework de pruebas: Si tienes múltiples frameworks de pruebas (por ejemplo, xUnit, NUnit, MSTest),
puedes especificar el framework a usar:

dotnet test --framework xunit
Resumen del comando básico:

dotnet test --collect:"Code Coverage" --verbosity detailed
Este comando ejecutará las pruebas, recopilará información sobre la cobertura de código y mostrará detalles adicionales.
Luego, podrás generar y analizar los informes de cobertura como desees.

¿Te gustaría más información sobre alguna parte específica?

```
## Resultados de cobertura de código y fichero .coverage

```
Paso 1: Ejecuta las pruebas con la cobertura
El primer paso es ejecutar las pruebas y asegurarte de que la cobertura de código se está generando correctamente.
Si ya ejecutaste el siguiente comando, esto debería haber generado el archivo .coverage en la carpeta TestResults:

bash
Copy
dotnet test --collect:"Code Coverage"
Este comando ejecuta las pruebas y crea los archivos de cobertura dentro de la carpeta TestResults, que es lo que ya tienes.

Paso 2: Entender el archivo .coverage
El archivo .coverage que se genera (123456789asdfghjk.coverage en tu caso) contiene los datos de la cobertura de código,
pero no es legible directamente. Necesitamos procesarlo para verlo en un formato más amigable.

Paso 3: Usar ReportGenerator para visualizar la cobertura
Una forma común de visualizar la cobertura de código es utilizando una herramienta llamada ReportGenerator,
que convierte esos archivos .coverage (o los archivos de resultados de las pruebas en formato XML) en un reporte HTML.

Instalación de ReportGenerator:
Si no tienes instalada la herramienta ReportGenerator, puedes hacerlo usando el siguiente comando en la terminal:

bash
Copy
dotnet tool install --global dotnet-reportgenerator-globaltool
Generar el informe HTML de cobertura:
Ahora, necesitas generar un reporte HTML de los resultados de las pruebas. ReportGenerator
puede leer los archivos de cobertura y producir un informe en HTML que puedes abrir en cualquier navegador.

Ejecuta el siguiente comando, apuntando a los archivos de resultados generados en TestResults:

bash
Copy
reportgenerator "-reports:OrqServiceTest/TestResults/**/*.xml" "-targetdir:coverage-report"
Aquí te explico los parámetros:

"-reports:OrqServiceTest/TestResults/**/*.xml": Especifica la ubicación de los archivos XML que
contienen los resultados de las pruebas, que incluyen los datos de cobertura. **/*.xml es una forma de
incluir todos los archivos .xml dentro de cualquier subcarpeta.

"-targetdir:coverage-report": Especifica la carpeta donde se generará el reporte HTML. En este caso,
el reporte se guardará en una carpeta llamada coverage-report.

Paso 4: Abrir el reporte
Una vez que hayas ejecutado el comando de ReportGenerator, se habrá creado una carpeta coverage-report que
contiene un archivo index.html.

Abre ese archivo index.html en un navegador, y podrás ver un reporte detallado con el porcentaje de cobertura,
las clases y métodos cubiertos, y más.

Alternativa: Usar Visual Studio
Si prefieres no usar la línea de comandos, también puedes abrir el proyecto en Visual Studio y visualizar los
resultados de la cobertura de código de forma gráfica:

Abre el proyecto en Visual Studio.
En el menú superior, ve a Test > Analyze Code Coverage.
Asegúrate de que el proyecto esté configurado para realizar pruebas con cobertura.
Luego de ejecutar las pruebas, Visual Studio te mostrará los resultados de la cobertura directamente
en una ventana con gráficos y detalles.
Resumen:
Ejecuta las pruebas con cobertura: dotnet test --collect:"Code Coverage".
Usa ReportGenerator para generar un reporte HTML: reportgenerator "-reports:OrqServiceTest/TestResults/**/*.xml" "-targetdir:coverage-report".
Abre el archivo index.html en el directorio coverage-report para ver los resultados.
```

## Commands CLI - DOTNET

```
Revisar el archivo .nuspec del paquete

dotnet list package # Usar la herramienta dotnet list package
dotnet add package <nombre-del-paquete> # Usar el dotnet add package y revisar las versiones disponibles
dotnet nuget list source  # Comprobar las dependencias de cada versión del paquete

<TargetFramework>net8.0</TargetFramework> # Modifica el archivo del proyecto (.csproj) para que apunte a .NET 8

Actualizar los paquetes NuGet:

dotnet restore
dotnet nuget update 

Configurar el Proyecto para .NET 6 (soporte ambos entornos NET6 y NET8):

<TargetFrameworks>net6.0;net8.0</TargetFrameworks> # Modificar el archivo .csproj para que sea multiplataforma
dotnet restore # Actualizar los paquetes NuGet para .NET 6

Compilar el Proyecto para Ambas Versiones de .NET:

dotnet build --framework net8.0
dotnet build --framework net6.0

dotnet list package # Para verificar las versiones compatibles de los paquetes NuGet (específico para una versión de .NET)

dotnet --list-sdks # Lista de todas las versiones del SDK de .NET
dotnet --version # Verificar una versión específica

```

## Versiones del SDK de .NET instaladas (SDK 6, SDK 8 y SDK 9)

```
1. Verificar la versión de SDK en uso

Puedes verificar la versión de SDK que está utilizando el proyecto actualmente con el siguiente comando:

dotnet --version

Este comando te devolverá la versión de SDK activa en ese momento. Si es la versión que deseas (por ejemplo, 8.0),
estás listo. Si no, hay varias formas de cambiarla.

2. Especificar la versión del SDK para tu proyecto

Si tienes varios SDKs instalados y deseas asegurarte de que tu proyecto utilice un SDK específico,
puedes establecer la versión deseada de SDK en tu proyecto usando un archivo global.json.

Crear o actualizar un archivo global.json

Si no tienes un archivo global.json en la raíz de tu proyecto, puedes crear uno con el siguiente comando:

dotnet new globaljson --sdk-version 8.0.x
Esto indicará que el proyecto debe usar el SDK 8.0. Si prefieres usar la versión 6.0 o 9.0, solo
reemplaza 8.0.x con la versión deseada.

Ejemplo de global.json:

json
Copy
{
  "sdk": {
    "version": "8.0.100"
  }
}

Este archivo asegurará que, cuando trabajes en tu proyecto, se utilice la versión especificada del SDK.

3. Verificar que el archivo global.json esté funcionando

Una vez creado o actualizado el archivo global.json, puedes verificar si el SDK correcto está siendo utilizado de nuevo con:

dotnet --version

El comando debe devolver la versión especificada en el archivo global.json.

4. Cambiar de SDK sin global.json

Si prefieres no usar un archivo global.json, también puedes cambiar la versión del SDK activando un entorno diferente,
pero la forma más fiable es mediante el global.json para garantizar que el proyecto siempre use el
SDK correcto, sin importar el entorno de desarrollo.

```





