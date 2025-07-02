# Proyecto de Ingeniería de Datos: Optimización del Onboarding en Fintech

Este repositorio contiene la implementación de un pipeline ETL (Extracción, Transformación y Carga) para un proyecto de Ingeniería de Datos. El objetivo principal es mejorar el *engagement* de los usuarios con una aplicación Fintech, centrándose en la reducción de la pérdida de usuarios durante la etapa de *onboarding* inicial. La solución aborda un problema de negocio real mediante el procesamiento y análisis de datos a gran escala, utilizando una arquitectura Big Data distribuida.

## 📝 Descripción del Problema

Una Fintech con operaciones en Latinoamérica busca incrementar el *engagement* de sus usuarios para reducir la pérdida de usuarios registrados, especialmente durante los primeros días de uso de la aplicación. Un análisis previo sugirió que esta pérdida podría estar relacionada con la complejidad de la aplicación y la alta carga cognitiva para los usuarios nuevos.

Para abordar esto, se propuso implementar una etapa de *onboarding* de 30 días de duración, guiando a los nuevos usuarios en la creación de productos bancarios y reduciendo la carga cognitiva de la página de inicio durante este período. Para medir la efectividad de esta propuesta, se diseñó un experimento de tipo A/B Testing, observando métricas clave durante seis meses en usuarios de Brasil.

## 🎯 Objetivos del Proyecto

* Desarrollar un proceso ETL robusto utilizando Apache Spark y Apache Cassandra.
* Implementar una arquitectura Big Data distribuida.
* Realizar una exhaustiva etapa de pre-procesamiento para asegurar la consistencia y calidad de los datos.
* Preparar los datos en una etapa de transformación para el análisis del desempeño de la etapa de *onboarding* en el grupo de tratamiento.
* Calcular métricas de negocio clave para evaluar el éxito de la estrategia de *onboarding*.

## 🏗️ Arquitectura Utilizada

Para este trabajo, se implementó una arquitectura Big Data distribuida, aprovechando las siguientes tecnologías:

* **Apache Cassandra / DataStax**: Base de datos NoSQL orientada a columnas, escalable y distribuida. Su rol en la arquitectura es el almacenamiento persistente de los datos. DataStax, como plataforma empresarial basada en Cassandra, proporciona herramientas adicionales para gestión, seguridad y análisis en tiempo real.
* **Apache Spark (PySpark)**: Motor de procesamiento distribuido. Se utilizó PySpark (la interfaz Python de Spark) para la transformación, análisis y limpieza de datos. Es fundamental para tareas de ETL (extracción, transformación y carga), procesamiento por lotes, limpieza de datos, agregaciones y uniones.

## 💻 Tecnologías y Librerías Utilizadas

* **Apache Cassandra**: Base de datos NoSQL distribuida [cite: 5][cite_start], utilizada como fuente y destino de los datos.
* **DataStax**: Base de datos en la nube  (Astra) para el almacenamiento de datos limpios en la "zona Universal".
* **Apache Spark**: Motor de procesamiento distribuido.
* **PySpark**: Interfaz Python para Apache Spark.
* **Pandas**: Librería Python utilizada.
* **NumPy**: Librería Python utilizada.
* **AstraPy**: Librería Python utilizada.
* **DateTime**: Librería Python utilizada.

## 📊 Datasets Utilizados

Se proporcionaron extractos históricos de los siguientes datasets:

* `dim_users`: Contiene información de usuarios en *onboarding* para una fecha determinada, incluyendo `user_id` (identificador único de usuario con prefijo "MLB" para usuarios de Brasil) y `rubro` (un identificador de rubro de negocio para usuarios del segmento *seller*).
* `fact_users_transactions`: Contiene todas las transacciones de los usuarios realizadas durante un período determinado , incluyendo `transaction_dt` (fecha de una transacción) , `type` (identificador de tipo de transacción: 1-7 para pago, 8 y 9 para cobro), y `segment` (1 para *individuals*, 2 para *seller*).
* `fact_users_onboarding`: Contiene la información del usuario de *onboarding* que permite calcular las métricas de negocio para un período determinado, incluyendo `first_login_dt` (fecha histórica del primer inicio de sesión), `habito` (1 para presencia del atributo, 0 en caso contrario), `habito_dt` (fecha en que realiza el evento de hábito), `activacion` (1 para presencia del atributo, 0 en caso contrario), `activacion_dt` (fecha en que realiza el evento de activación), `setup` (1 para presencia del atributo, 0 en caso contrario), `setup_dt` (fecha en que realiza el evento de setup), y `return` (1 si el usuario retornó posteriormente al *first login*).

## 🧹 Acciones de Pre-procesamiento y Transformación

Se realizó una limpieza y transformación exhaustiva de los datos, respetando siempre criterios basados en la lógica de negocio. Este proceso aseguró la consistencia de los datos, abordando valores perdidos e inconsistencias, para dejar las tablas `users`, `onboarding` y `transactions` listas para el análisis. Los datos limpios fueron cargados en Astra, en la zona Universal.

## 📈 Hallazgos y Resultados

Se utilizaron consultas SQL con PySpark sobre los datos limpios en la "zona Universal", permitiendo calcular métricas clave que luego alimentaron la "zona Smart".

Los resultados obtenidos fueron los siguientes:

| Métrica                 | Valor    |
| :---------------------- | :------- |
| **Drop Rate** | 29.00 %  |
| **Activation Rate** | 11.80 %  |
| **Setup Rate** | 44.60 %  |
| **Habito Individuals** | 4758     |
| **Habito Sellers** | 505      |

### Definiciones Clave:

* **Drop Rate**: Porcentaje de usuarios que no volvieron a usar la aplicación después del registro.
* **Activation Rate**: Porcentaje de usuarios en *onboarding* que realizaron al menos una primera acción transaccional. Para este proyecto, se consideraron usuarios que realizaron al menos 5 transacciones.
* **Setup Rate**: Porcentaje de usuarios que realizaron al menos una acción de *setup* (por ejemplo, activar llave PIX, cargar tarjeta).
* **Hábito Individuals**: Usuarios que realizan 5 transacciones en 5 días diferentes, durante el período de *onboarding* (fijado en 30 días).
* **Hábito Sellers**: Usuarios que realizan 5 transacciones de cobro (sin importar los días), durante el período de *onboarding* (fijado en 30 días).

## 📌 Conclusión

Se ha implementado un proceso ETL integral y una arquitectura Big Data distribuida utilizando Apache Spark y Apache Cassandra. La limpieza y transformación exhaustiva de los datos, guiadas por la lógica de negocio, han permitido obtener un conjunto de datos consistente y listo para el análisis. Las métricas calculadas proporcionan una base sólida para evaluar el desempeño de la etapa de *onboarding* y tomar decisiones informadas para mejorar el *engagement* de los usuarios.

---
 
