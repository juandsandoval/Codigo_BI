# Codigo_BI
Código Sesión 5 y 6 BUSINESS INTELLIGENCE
¡Hola y bienvenido!

## **Índice de Contenidos**
- [Introducción](#introducción)
- [Funciones Principales](#funciones-principales)
- [Guía de Instalación](#guía-de-instalación)
- [Ejemplo de Configuración de la Base de Datos](#ejemplo-de-configuración-de-la-base-de-datos)
- [Generación y Almacenamiento de Datos de Clientes](#generación-y-almacenamiento-de-datos-de-clientes)
- [Creación y Almacenamiento de Datos de Sucursales](#creación-y-almacenamiento-de-datos-de-sucursales)
- [Creación y Almacenamiento de Tipos de Transacciones](#creación-y-almacenamiento-de-tipos-de-transacciones)
- [Generación y Almacenamiento de Transacciones](#generación-y-almacenamiento-de-transacciones)
- [Validación de Tablas en SQLite3](#validación-de-tablas-en-sqlite3)
- [Acerca del Autor](#acerca-del-autor)

## **Introducción**
Este proyecto está diseñado para la creación y manejo de una base de datos SQLite destinada a almacenar datos financieros simulados. Se hace uso de la biblioteca `Faker` para generar datos realistas, proporcionando un entorno ideal para la simulación y prueba de aplicaciones que manipulan información financiera.

## **Funciones Principales**
- **Generación de Datos Simulados**: Uso de `Faker` para crear datos realistas de clientes, sucursales y transacciones.
- **Gestión de Base de Datos SQLite**: Configuración automática de una base de datos SQLite con tablas interrelacionadas para gestionar datos financieros simulados.
- **Consultas SQL Eficientes**: Función incorporada para ejecutar consultas SQL de manera segura y eficiente.

## **Guía de Instalación**
Para ejecutar este proyecto, es necesario instalar las siguientes librerías:
- sqlite3
- pandas 
- requests
- random
- uuid
- faker
- numpy
- shutil

## **Ejemplo de Configuración de la Base de Datos**
Este proyecto incluye un script que configura una base de datos SQLite para almacenar datos financieros ficticios. A continuación, se explica el propósito de cada sección del código:

1. **Inicialización de Faker**: Se inicializa una instancia de la biblioteca Faker para generar datos ficticios, como nombres de clientes y direcciones.

2. **Conexión a SQLite**: Se establece una conexión con una base de datos SQLite llamada `financial_data.db`. Si el archivo de la base de datos no existe, se crea automáticamente.

3. **Función para ejecutar consultas SQL**: Esta función permite ejecutar consultas SQL de forma segura, asegurando que cualquier cambio en la base de datos se confirme automáticamente.

4. **Creación de Tablas**:
   - **Customer:** Almacena información sobre los clientes, como ID, nombre, dirección, número de teléfono y correo electrónico.
   - **Branches:** Almacena datos sobre las sucursales, como ID, ubicación, nombre del gerente y número de contacto.
   - **transaction_types:** Define los diferentes tipos de transacciones (por ejemplo, "retiro", "depósito") y proporciona una descripción para cada uno.
   - **transactions:** Registra cada transacción realizada, incluyendo detalles como ID, cliente, fecha, monto, ubicación, tipo de transacción, si es fraudulenta, y la sucursal donde ocurrió.

## **Generación y Almacenamiento de Datos de Clientes**
Este proyecto incluye una funcionalidad para obtener datos de clientes ficticios desde la API de Random User y guardarlos en una base de datos SQLite3. A continuación, se describe el proceso y el propósito de cada sección del código:

1. **Función para obtener datos de clientes desde la API Random User**:
   - **Descripción**: Esta función (get_random_users) solicita un número específico de usuarios (por defecto 10) a la API de Random User. La API devuelve datos de usuarios ficticios, como nombres, direcciones, y correos electrónicos.
   - **Funcionamiento**: Se construye una URL que incluye el número de usuarios solicitados (num_users). Se realiza una solicitud GET a la API. Si la solicitud es exitosa, se procesan los datos recibidos en formato JSON y se extraen los resultados. En caso de error, se imprime un mensaje y se retorna una lista vacía.

2. **Función para crear y almacenar la tabla de clientes en SQLite3**:
   - **Descripción**: Esta función (create_customers_table) genera una tabla de clientes basada en los datos obtenidos de la API de Random User y la guarda en una base de datos SQLite3.
   - **Funcionamiento**: Se llama a get_random_users para obtener datos de un número específico de clientes. Se crea un diccionario `customers_data` que organiza la información de los clientes en columnas como `customer_id`, `name`, `address`, `phone_number`, y `email`. Utiliza pandas para convertir este diccionario en un DataFrame (`customers_df`). Finalmente, guarda este DataFrame en una tabla llamada `customers` en la base de datos SQLite.

3. **Creación de la Tabla de Clientes**:
   - **Descripción**: Se crea una tabla de clientes con 100 entradas llamando a la función `create_customers_table`.
   - **Resultado**: Los datos generados se almacenan en la tabla `customers` de la base de datos SQLite3.

## **Creación y Almacenamiento de Datos de Sucursales**
Este proyecto incluye una funcionalidad para generar datos ficticios de sucursales y guardarlos en una base de datos SQLite3. A continuación, se describe el propósito y funcionamiento del código correspondiente.

1. **Función para Crear y Almacenar la Tabla de Sucursales en SQLite3**:
   - **Descripción**: Esta función (create_branches_table) genera una tabla de sucursales utilizando datos ficticios generados por `Faker`. La tabla se guarda en una base de datos SQLite3.
   - **Funcionamiento**:
     - **Generación de Datos**: Se generan `branch_id` (identificador único para cada sucursal usando `uuid.uuid4()`), `branch_location` (ciudad ficticia usando `fake.city()`), `manager_name` (nombre ficticio usando `fake.name()`), y `contact_number` (número de teléfono ficticio usando `fake.phone_number()`).
     - **Creación del DataFrame**: Los datos generados se organizan en un diccionario (`branch_data`) y se convierten en un DataFrame de pandas (`branches_df`). Luego, se guarda en una tabla llamada `branches` en la base de datos SQLite.

2. **Crear la Tabla de Sucursales**:
   - **Descripción**: Se llama a la función `create_branches_table` para crear una tabla con 20 sucursales ficticias.
   - **Resultado**: Los datos generados se almacenan en la tabla `branches` de la base de datos SQLite3.

## **Creación y Almacenamiento de Tipos de Transacciones**
Esta sección del proyecto incluye una funcionalidad para generar una tabla de tipos de transacciones y guardarla en una base de datos SQLite3. A continuación, se detalla el propósito y funcionamiento del código correspondiente.

1. **Función para Crear y Almacenar la Tabla de Tipos de Transacciones en SQLite3**:
   - **Descripción**: Esta función (create_transaction_types_table) crea una tabla que define los tipos de transacciones y sus descripciones, utilizando datos predefinidos.
   - **Funcionamiento**: 
     - **Datos de Transacciones**: Se definen dos tipos de transacciones (`transaction_type`): "online" y "in-store". Se proporcionan descripciones correspondientes para cada tipo de transacción.
     - **Creación del DataFrame**: Los datos se organizan en un diccionario (`transaction_types_data`) y se convierten en un DataFrame de pandas (`transaction_types_df`). Luego, se guarda en una tabla llamada `transaction_types` en la base de datos SQLite.

2. **Crear la Tabla de Tipos de Transacciones**:
   - **Descripción**: Se llama a la función `create_transaction_types_table` para crear y guardar la tabla de tipos de transacciones.
   - **Resultado**: Los tipos de transacciones se almacenan en la tabla `transaction_types` de la base de datos SQLite3.

## **Generación y Almacenamiento de Transacciones**
Esta sección del proyecto incluye una funcionalidad para generar una tabla de transacciones y guardarla en una base de datos SQLite3. A continuación, se detalla el propósito y funcionamiento del código correspondiente.

1. **Función para Crear y Almacenar la Tabla de Transacciones en SQLite3**:
   - **Descripción**: Esta función (create_transactions_table) genera una tabla de transacciones ficticias utilizando datos aleatorios y la guarda en una base de datos SQLite3.
   - **Funcionamiento**:
     - **Generación de Datos**: Se generan `transaction_id`, `customer_id` (aleatorio tomado de `customers_df`), `transaction_date` (fecha aleatoria dentro del año en curso usando `fake.date_time_this_year()`), `transaction_amount` (monto entre 10 y 1000 dólares), `transaction_location` (ciudad ficticia usando `fake.city()`), `transaction_type` (aleatorio entre "online" o "in-store"), y `fraudulent` (inicializado en 0).
     - **Introducción de Transacciones Fraudulentas**: Se seleccionan algunas transacciones aleatorias como fraudulentas, con un

 monto mayor (entre 1000 y 5000 dólares) y tipo "online".
     - **Asignación de `branch_id`**: Solo se asigna `branch_id` a las transacciones "in-store" usando identificadores aleatorios de `branches_df`. Para las transacciones "online", se establece `branch_id` en `None`.
     - Finalmente, se guarda el DataFrame (`transactions_df`) en una tabla llamada `transactions` en la base de datos SQLite.

2. **Crear la Tabla de Transacciones**:
   - **Descripción**: Se llama a la función `create_transactions_table` para generar y guardar una tabla de 500 transacciones ficticias.
   - **Resultado**: Los datos de transacciones se almacenan en la tabla `transactions` de la base de datos SQLite3.

## **Validación de Tablas en SQLite3**
Este fragmento de código permite verificar que las tablas se han creado correctamente en la base de datos SQLite3 y cierra la conexión a la base de datos. A continuación, se describe el propósito y funcionamiento del código.

1. **Verificación de Tablas**:
   - **Descripción**: Este bloque de código consulta la base de datos SQLite para listar todas las tablas existentes y luego imprime los resultados.
   - **Funcionamiento**: La consulta SQL `SELECT name FROM sqlite_master WHERE type='table';` selecciona los nombres de todas las tablas en la base de datos. La consulta se ejecuta usando `pd.read_sql()` y los nombres de las tablas se imprimen en la consola.

2. **Cerrar la Conexión**:
   - **Descripción**: Este comando cierra la conexión a la base de datos SQLite, liberando los recursos asociados.
   - **Importancia**: Cerrar la conexión es esencial para evitar problemas de rendimiento en la base de datos.

  # 📊 Análisis de la Tabla de Transacciones

### 📝 Descripción General:
Este repositorio contiene un análisis detallado de los datos de transacciones descargados. A continuación se presentan diferentes gráficos y sus respectivas interpretaciones para ayudar a comprender la completitud y distribución de los datos.

---

## 📈 Gráficos e Interpretación:

### **Gráfico #1: Conteo de Registros por Columna**
Este gráfico muestra el **conteo de registros** para cada columna de la tabla de transacciones. Cada columna (por ejemplo, `transaction_id`, `customer_id`, etc.) tiene **1000 valores**, indicando que **todas las transacciones están completas**.
![image](https://github.com/user-attachments/assets/cbe0aa7b-36fa-4876-96a2-da73c0456857)

---

### **Gráfico #2: Conteo de Valores No Nulos por Columna**
El gráfico refleja la cantidad de **valores no nulos** para cada columna en la tabla. De manera similar al gráfico anterior, todas las columnas contienen **1000 valores no nulos**, lo que asegura que **no hay datos faltantes** en este conjunto de transacciones.
![image](https://github.com/user-attachments/assets/d94ef124-09c7-4bc0-8028-25e2904c5de0)

---

### **Gráfico #3: Completitud de Variables (%)**
La gráfica, titulada **"Completitud de las variables"**, muestra que para variables como `embarazo_1`, `mamografia_1`, y otras, el **100% de los valores no son nulos**. Esto asegura que los datos están completos y son confiables para estas variables específicas.
![image](https://github.com/user-attachments/assets/18293452-c375-47ea-bacb-de1068d99d03)

---

### **Gráfico #4: Matriz de Estadísticas Descriptivas**
Este gráfico muestra las **estadísticas descriptivas** de las columnas `transaction_amount` y `fraudulent`:

- **`transaction_amount`**: 
  - **Media**: 624.0 
  - **Desviación Estándar**: 659.17 
  - **Mínimo**: 10.15 
  - **Máximo**: 4984.22 (⚠️ resaltado por ser un valor significativamente alto)
  
- **`fraudulent`**: 
  - **Media**: 0.05 
  - **Mínimo**: 0.00 
  - **Máximo**: 1.00
![image](https://github.com/user-attachments/assets/b3d973ec-4355-4afb-8e49-c9a5abefe04b)

---

### **Gráfico #5: Distribución del Monto de Transacciones**
Este histograma muestra la **distribución** de los montos de transacción (`transaction_amount`). Observamos que las **transacciones con montos bajos son más frecuentes**, y la altura de las barras disminuye a medida que el monto aumenta.
![image](https://github.com/user-attachments/assets/63faacf3-2831-4e7b-9cfc-c952bd4f0d7d)

---

### **Gráfico #6: Matriz de Correlación**
La **matriz de correlación** en forma de mapa de calor muestra la relación entre `transaction_amount` y `fraudulent`. 

- **Correlación**: 0.82 entre ambas variables, lo que indica una **relación positiva fuerte

![image](https://github.com/user-attachments/assets/61647f68-c8b9-421d-b97c-b58fe5c3dd88)


---

## 🚀 Conclusión:
Este análisis verifica la **completitud de los datos** y explora la relación entre las transacciones y el fraude, proporcionando una base sólida para análisis más profundos.


## **Acerca del Autor**
Este proyecto fue desarrollado por **Juan Sandoval**.
