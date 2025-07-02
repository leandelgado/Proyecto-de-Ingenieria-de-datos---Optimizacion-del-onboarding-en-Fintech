# Proyecto de Ingeniería de Datos: Optimización del Onboarding en Fintech

Este repositorio contiene la implementación de un pipeline ETL (Extracción, Transformación y Carga) para un proyecto de Ingeniería de Datos. [cite_start]El objetivo principal es mejorar el *engagement* de los usuarios con una aplicación Fintech, centrándose en la reducción de la pérdida de usuarios durante la etapa de *onboarding* inicial[cite: 31, 32]. [cite_start]La solución aborda un problema de negocio real mediante el procesamiento y análisis de datos a gran escala, utilizando una arquitectura Big Data distribuida[cite: 29, 62].

## 📝 Descripción del Problema

[cite_start]Una Fintech con operaciones en Latinoamérica busca incrementar el *engagement* de sus usuarios para reducir la pérdida de usuarios registrados [cite: 31][cite_start], especialmente durante los primeros días de uso de la aplicación[cite: 32]. [cite_start]Un análisis previo sugirió que esta pérdida podría estar relacionada con la complejidad de la aplicación y la alta carga cognitiva para los usuarios nuevos[cite: 33].

[cite_start]Para abordar esto, se propuso implementar una etapa de *onboarding* de 30 días de duración [cite: 34][cite_start], guiando a los nuevos usuarios en la creación de productos bancarios y reduciendo la carga cognitiva de la página de inicio durante este período[cite: 34]. [cite_start]Para medir la efectividad de esta propuesta, se diseñó un experimento de tipo A/B Testing [cite: 35][cite_start], observando métricas clave durante seis meses en usuarios de Brasil[cite: 36].

## 🎯 Objetivos del Proyecto

* [cite_start]Desarrollar un proceso ETL robusto utilizando Apache Spark y Apache Cassandra[cite: 62].
* [cite_start]Implementar una arquitectura Big Data distribuida[cite: 62].
* [cite_start]Realizar una exhaustiva etapa de pre-procesamiento para asegurar la consistencia y calidad de los datos[cite: 64].
* [cite_start]Preparar los datos en una etapa de transformación para el análisis del desempeño de la etapa de *onboarding* en el grupo de tratamiento[cite: 66, 67].
* [cite_start]Calcular métricas de negocio clave para evaluar el éxito de la estrategia de *onboarding*[cite: 24].

## 🏗️ Arquitectura Utilizada

[cite_start]Para este trabajo, se implementó una arquitectura Big Data distribuida[cite: 1], aprovechando las siguientes tecnologías:

* [cite_start]**Apache Cassandra / DataStax**: Base de datos NoSQL orientada a columnas, escalable y distribuida[cite: 1]. [cite_start]Su rol en la arquitectura es el almacenamiento persistente de los datos[cite: 2]. [cite_start]DataStax, como plataforma empresarial basada en Cassandra, proporciona herramientas adicionales para gestión, seguridad y análisis en tiempo real[cite: 4].
* [cite_start]**Apache Spark (PySpark)**: Motor de procesamiento distribuido[cite: 3, 6]. [cite_start]Se utilizó PySpark (la interfaz Python de Spark) para la transformación, análisis y limpieza de datos[cite: 3, 7]. [cite_start]Es fundamental para tareas de ETL (extracción, transformación y carga), procesamiento por lotes, limpieza de datos, agregaciones y uniones[cite: 7].

![image](https://github.com/user-attachments/assets/5c328e1d-c472-466c-8a2b-232128795c10)

## 💻 Tecnologías y Librerías Utilizadas

* [cite_start]**Apache Cassandra**: Base de datos NoSQL distribuida [cite: 5][cite_start], utilizada como fuente y destino de los datos[cite: 5].
* [cite_start]**DataStax**: Base de datos en la nube [cite: 6] [cite_start](Astra) para el almacenamiento de datos limpios en la "zona Universal"[cite: 23].
* [cite_start]**Apache Spark**: Motor de procesamiento distribuido[cite: 6].
* [cite_start]**PySpark**: Interfaz Python para Apache Spark[cite: 6].
* [cite_start]**Pandas**: Librería Python utilizada[cite: 7].
* [cite_start]**NumPy**: Librería Python utilizada[cite: 7].
* [cite_start]**AstraPy**: Librería Python utilizada[cite: 7].
* [cite_start]**DateTime**: Librería Python utilizada[cite: 7].

## 📊 Datasets Utilizados

Se proporcionaron extractos históricos de los siguientes datasets:

* [cite_start]`dim_users`: Contiene información de usuarios en *onboarding* para una fecha determinada [cite: 48][cite_start], incluyendo `user_id` (identificador único de usuario con prefijo "MLB" para usuarios de Brasil) [cite: 51, 52] [cite_start]y `rubro` (un identificador de rubro de negocio para usuarios del segmento *seller*)[cite: 53].
* [cite_start]`fact_users_transactions`: Contiene todas las transacciones de los usuarios realizadas durante un período determinado [cite: 49][cite_start], incluyendo `transaction_dt` (fecha de una transacción) [cite: 54][cite_start], `type` (identificador de tipo de transacción: 1-7 para pago, 8 y 9 para cobro) [cite: 54][cite_start], y `segment` (1 para *individuals*, 2 para *seller*)[cite: 55].
* [cite_start]`fact_users_onboarding`: Contiene la información del usuario de *onboarding* que permite calcular las métricas de negocio para un período determinado [cite: 50][cite_start], incluyendo `first_login_dt` (fecha histórica del primer inicio de sesión) [cite: 56][cite_start], `habito` (1 para presencia del atributo, 0 en caso contrario) [cite: 57][cite_start], `habito_dt` (fecha en que realiza el evento de hábito) [cite: 57][cite_start], `activacion` (1 para presencia del atributo, 0 en caso contrario) [cite: 57][cite_start], `activacion_dt` (fecha en que realiza el evento de activación) [cite: 59][cite_start], `setup` (1 para presencia del atributo, 0 en caso contrario) [cite: 59][cite_start], `setup_dt` (fecha en que realiza el evento de setup) [cite: 60][cite_start], y `return` (1 si el usuario retornó posteriormente al *first login*)[cite: 61].

## 🧹 Acciones de Pre-procesamiento y Transformación

[cite_start]Se realizó una limpieza y transformación exhaustiva de los datos, respetando siempre criterios basados en la lógica de negocio[cite: 23, 71]. [cite_start]Este proceso aseguró la consistencia de los datos, abordando valores perdidos e inconsistencias[cite: 64], para dejar las tablas `users`, `onboarding` y `transactions` listas para el análisis. [cite_start]Los datos limpios fueron cargados en Astra, en la zona Universal[cite: 23].

## 📈 Hallazgos y Resultados

[cite_start]Se utilizaron consultas SQL con PySpark sobre los datos limpios en la "zona Universal", permitiendo calcular métricas clave que luego alimentaron la "zona Smart"[cite: 24].

[cite_start]Los resultados obtenidos fueron los siguientes[cite: 25]:

| Métrica                 | Valor    |
| :---------------------- | :------- |
| **Drop Rate** | 29.00 %  |
| **Activation Rate** | 11.80 %  |
| **Setup Rate** | 44.60 %  |
| **Habito Individuals** | 4758     |
| **Habito Sellers** | 505      |

### Definiciones Clave:

* [cite_start]**Drop Rate**: Porcentaje de usuarios que no volvieron a usar la aplicación después del registro[cite: 26, 39].
* [cite_start]**Activation Rate**: Porcentaje de usuarios en *onboarding* que realizaron al menos una primera acción transaccional[cite: 39]. [cite_start]Para este proyecto, se consideraron usuarios que realizaron al menos 5 transacciones[cite: 17].
* [cite_start]**Setup Rate**: Porcentaje de usuarios que realizaron al menos una acción de *setup* (por ejemplo, activar llave PIX, cargar tarjeta)[cite: 27, 47].
* [cite_start]**Hábito Individuals**: Usuarios que realizan 5 transacciones en 5 días diferentes, durante el período de *onboarding* (fijado en 30 días)[cite: 28, 44, 45].
* [cite_start]**Hábito Sellers**: Usuarios que realizan 5 transacciones de cobro (sin importar los días), durante el período de *onboarding* (fijado en 30 días)[cite: 28, 45, 46].

## 结论 Conclusión

Se ha implementado un proceso ETL integral y una arquitectura Big Data distribuida utilizando Apache Spark y Apache Cassandra. [cite_start]La limpieza y transformación exhaustiva de los datos, guiadas por la lógica de negocio, han permitido obtener un conjunto de datos consistente y listo para el análisis[cite: 23]. Las métricas calculadas proporcionan una base sólida para evaluar el desempeño de la etapa de *onboarding* y tomar decisiones informadas para mejorar el *engagement* de los usuarios.

---
 
