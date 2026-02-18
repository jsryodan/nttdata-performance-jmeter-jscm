EJERCICIO 3 - PRUEBA DE CARGA (JMeter)

Objetivo
Realizar una prueba de carga al servicio de login:
POST https://fakestoreapi.com/auth/login
Parametrizando credenciales desde un archivo CSV y alcanzando >= 20 TPS,
con validaciones:
- Tiempo de respuesta máximo permitido: 1.5 segundos
- Tasa de error aceptable: < 3%

Tecnologías y versiones
- Apache JMeter: 5.6.3
- Java / JDK: 17
- Sistema operativo: Windows 11

Instalación
- Descargar JMeter desde https://jmeter.apache.org/download_jmeter.cgi en Binaries (Versión ZIP)
- Crear carpeta llamada "jmeter" en raíz C
- Descomprimir apache-jmeter-5.6.3.zip	en carperta jmeter

Estructura del proyecto
- test-plan/login_20tps.jmx : plan de prueba JMeter
- test-plan/users.csv : datos de entrada parametrizados (user,passwd)
- results/ : carpeta de salida para .jtl y reporte HTML (se genera al ejecutar)

Ejecución (no-GUI)
1) Abrir terminal en la raíz del proyecto.
2) Ejecutar:

jmeter -n -t test-plan/login_20tps.jmx -l results/results.jtl -e -o results/report

2.1) En caso de no tener agregado jmeter como variable de entorno ejecutar comando con path:

C:\jmeter\apache-jmeter-5.6.3\bin\jmeter.bat -n -t test-plan\login_20tps.jmx -l results\results.jtl -e -o results\report

3) Abrir el reporte HTML:
results/report/index.html

Notas
- Para ejecución final se recomienda deshabilitar listeners pesados (ej: View Results Tree).
- La prueba incluye validaciones:
  - Response Code (200/201)
  - Presencia de "token" en la respuesta
  - Duration Assertion: <= 1500 ms
- En caso de ejecutar un nuevo reporte se debe eliminar el archivo result/results.jtl y contenido de la carpeta result/report (manteniendo la carpeta result/report creada pues en esta carpeta se generará el nuevo reporte)
- Para modificar / configurar threads/ramp-up/loop/duration se debe ejecutar en C:\jmeter\apache-jmeter-5.6.3\bin\jmeter.bat , una vez en GUI estos valores se pueden modificar desde Thread Groups (Sección lateral izquierdo)