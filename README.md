# Plantilla CloudFormation para Infraestructura en Alta Disponibilidad con NGINX

Este repositorio contiene una plantilla YAML diseñada para desplegar automáticamente una infraestructura de alta disponibilidad en AWS utilizando **AWS CloudFormation**.

## 📄 Descripción

La plantilla `infraestructura.yaml` define los recursos necesarios para crear:

- Una VPC con subredes en múltiples zonas de disponibilidad.
- Dos instancias EC2 tipo `t2.micro` (Free Tier) con **NGINX** instalado automáticamente mediante `UserData`.
- Un Load Balancer (ELB) que distribuye tráfico entre las instancias.
- Grupos de Seguridad para permitir tráfico HTTP.
- Outputs para obtener el DNS del Load Balancer.

Todo el despliegue está automatizado y puede completarse en minutos desde la consola de AWS.

## 🚀 Uso de la plantilla

### 1. Prerrequisitos

- Cuenta activa en AWS con acceso al servicio CloudFormation.
- Par de llaves SSH creado previamente en la región deseada.
- Conocimiento básico de la consola de AWS.

### 2. Despliegue en AWS

1. Accede a la consola de AWS: [https://console.aws.amazon.com/](https://console.aws.amazon.com/)
2. Ve al servicio **CloudFormation**.
3. Selecciona **Crear pila** > *Con recursos nuevos (estándar)*.
4. En *Especificar plantilla*, elige **Cargar un archivo** y selecciona `infraestructura.yaml`.
5. Completa los parámetros solicitados:
   - Nombre de la pila.
   - Nombre del KeyPair SSH.
6. Haz clic en **Siguiente** y luego en **Crear pila**.
7. Espera a que la pila finalice con el estado `CREATE_COMPLETE`.

### 3. Verificación

- Revisa que se crearon dos instancias EC2 en diferentes zonas de disponibilidad.
- Accede al sitio web cargado en NGINX desde el **DNS del Load Balancer**, disponible en la pestaña **Salidas (Outputs)** de la pila.
- Puedes detener una instancia y comprobar que el ELB redirige correctamente el tráfico a la otra.

## ⚙️ Personalización

Puedes modificar lo siguiente en el archivo YAML:
- El contenido del `UserData` para instalar o configurar otras aplicaciones.
- Los nombres de los recursos.
- Las subredes o regiones de despliegue.
- La imagen AMI (por defecto suele usarse Amazon Linux 2).

## 📦 Estructura de la plantilla

La plantilla define secciones típicas de CloudFormation:

- `Parameters`: para ingresar el KeyPair.
- `Resources`: define todos los componentes (VPC, Subnets, EC2, ELB, Security Groups).
- `Outputs`: muestra información útil como el DNS público del Load Balancer.

## 📄 Licencia

Uso académico. Puede modificarse libremente para prácticas de aprendizaje sobre infraestructura como código (IaC) en AWS.
