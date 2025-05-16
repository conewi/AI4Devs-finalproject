> Detalla en esta sección los prompts principales utilizados durante la creación del proyecto, que justifiquen el uso de asistentes de código en todas las fases del ciclo de vida del desarrollo. Esperamos un máximo de 3 por sección, principalmente los de creación inicial o  los de corrección o adición de funcionalidades que consideres más relevantes.
Puedes añadir adicionalmente la conversación completa como link o archivo adjunto si así lo consideras


## Índice

1. [Descripción general del producto](#1-descripción-general-del-producto)
2. [Arquitectura del sistema](#2-arquitectura-del-sistema)
3. [Modelo de datos](#3-modelo-de-datos)
4. [Especificación de la API](#4-especificación-de-la-api)
5. [Historias de usuario](#5-historias-de-usuario)
6. [Tickets de trabajo](#6-tickets-de-trabajo)
7. [Pull requests](#7-pull-requests)

---

## 1. Descripción general del producto

**Prompt 1:**
Create a brief description of the application with the main goal, the main value and who is the principal type of user.
Use this information to enrich your answer:
- This is an application to manage family and personal budgets.
- The main value is that data is anonimized and is not necessary to link a bank account.

**Prompt 2:**
Based on UseCases describe briefly the main functionalities of this application as a bullet points
**Prompt 3:**

---

## 2. Arquitectura del Sistema

### **2.1. Diagrama de arquitectura:**

**Prompt 1:**
You are an brilliant Software Arquitect, expert in .Net, Azure, Terraform, Containerization (Docker, Kubernetes), Message brokers and queuing systems, Domain Driven Design, Microservices patterns, Database schema design, Data warehousing patterns, API Gateway patterns and Event-driven architectures.
Create a diagram named architecture_overview.md using Mermaid taking into account the following points:
1. Audience-focused: Tailor detail level to your audience (executives, developers, etc.)
2. Layered approach: Provide overview diagrams with drill-down capabilities
3. Consistent notation: Use consistent styles, shapes, and colors across diagrams
4. Visual hierarchy: Use size, color, and positioning to show importance
5. Include context: Always show system boundaries and external dependencies

Reduce the costs of this architecture removing docker and use one Azure app service, use app service slots instead of containers.
For instance, API Gateway will be a YARP (Yet Another Reverse Proxy) from Microsoft and will be deployed in a App Service Slot, Quasar SPA application will be deployed in another slot, and api will be deployed in another Slot. 
Development, staging and Productions will be diferent App Services with the same deployment structure.



**Prompt 2:**
Create C4_flowchart with this information.

**Prompt 3:**


### **2.2. Descripción de componentes principales:**

**Prompt 1:**
Describe the main components by technology used and responsability based on the architecture diagrams.

**Prompt 2:**

**Prompt 3:**

### **2.3. Descripción de alto nivel del proyecto y estructura de ficheros**

**Prompt 1:**
@ddd_best_practices.md @tdd-best-practices.md @C4_classDiagram.mmd @README.md 
Create a high level project description and its folder structure.
**Prompt 2:**

**Prompt 3:**

### **2.4. Infraestructura y despliegue**

**Prompt 1:**
Explain in detail the infrastructure requirements for deployment and and how can we do it with Terraform
**Prompt 2:**

**Prompt 3:**

### **2.5. Seguridad**

**Prompt 1:**
Following the OWASP Security guide and the architecture diagrams, list and descibe the security practices that will be applied. Provide examples if it's necessary (examples must have 15 lins maximum)
**Prompt 2:**

**Prompt 3:**

### **2.6. Tests**

**Prompt 1:**
@tdd-best-practices.md@UseCases.md Based on these documents, enumerate the main test cases that should be written
Write the content in a markdown format that can be copyed and pasted in a markdown file
**Prompt 2:**

**Prompt 3:**

---

### 3. Modelo de Datos

**Prompt 1:**
Create ERD diagram with this information using mermaid.
**Prompt 2:**
Create classDiagram with this information using mermaid.

**Prompt 3:**

---

### 4. Especificación de la API

**Prompt 1:**
Describe 3 API endpoints in OpenAPI format. Add one example of request / response to have more clarity
**Prompt 2:**

**Prompt 3:**

---

### 5. Historias de Usuario

**Prompt 1:**
Manually written
**Prompt 2:**

**Prompt 3:**

---

### 6. Tickets de Trabajo

**Prompt 1:**
As a Product owner , describe the tickets (product backlog items) for the Sign Up use case @UseCases.md  .
Ensure that ticket has the following structure:
1. Title 
2. Detailed description.
3. Acceptance criteria
4. Priority
5. Effort estimation
6. Tags
7. Links or references
Write the content in a markdown format that can be copyed and pasted in a markdown file
**Prompt 2:**
As a Product owner , describe the tickets (product backlog items) for the Create an account use case @UseCases.md  .
Ensure that ticket has the following structure:
1. Title 
2. Detailed description.
3. Acceptance criteria
4. Priority
5. Effort estimation
6. Tags
7. Links or references
Write the content in a markdown format that can be copyed and pasted in a markdown file
**Prompt 3:**
As a Product owner , describe the tickets (product backlog items) for the Create manually a income movement use case @UseCases.md  .
Ensure that ticket has the following structure:
1. Title 
2. Detailed description.
3. Acceptance criteria
4. Priority
5. Effort estimation
6. Tags
7. Links or references
Write the content in a markdown format that can be copyed and pasted in a markdown file
---

### 7. Pull Requests

**Prompt 1:**

**Prompt 2:**

**Prompt 3:**
