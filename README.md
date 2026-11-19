# Minor-Project-Barcoding-of-Inventory-System-for-FIFO-Adherence


A Python Django-based inventory management application designed to automate product identification, warehouse location tracking, and FIFO-based dispatching of manufactured goods using barcode/QR-code generation.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Problem Statement](#problem-statement)
- [Project Objectives](#project-objectives)
- [Key Features](#key-features)
- [Technology Stack](#technology-stack)
- [System Architecture](#system-architecture)
- [Application Workflow](#application-workflow)
- [Database Design](#database-design)
- [FIFO Implementation](#fifo-implementation)
- [Barcode and QR Code Generation](#barcode-and-qr-code-generation)
- [Application Modules](#application-modules)
- [Administrative Functionalities](#administrative-functionalities)
- [Benefits](#benefits)
- [Limitations](#limitations)
- [Future Enhancements](#future-enhancements)
- [Project Information](#project-information)

---

## Project Overview

The **Barcoding of Inventory System for FIFO Adherence** is a web-based inventory management application developed to simplify the storage, identification, tracking, and dispatching of manufactured goods in an industrial environment.

The project addresses the challenges associated with manually tracking manufactured products, production batches, warehouse racks, and storage locations.

The application uses Python and the Django web framework for backend development, with Microsoft PowerApps serving as the frontend interface.

It maintains structured inventory records, generates unique identification codes for production batches, tracks warehouse locations, and helps identify the earliest manufactured products that should be dispatched according to the First In, First Out (FIFO) principle.

The primary objective is to minimize manual inventory tracking, improve product traceability, reduce human errors, and streamline warehouse operations.

## Problem Statement

In manufacturing industries, managing inventory and ensuring the correct dispatch sequence are important for maintaining operational efficiency.

Traditionally, manufactured components are packed into boxes and stored in designated warehouse racks or locations. Employees must manually maintain information about:

- Product and part numbers.
- Manufacturing dates.
- Production quantities.
- Box identification numbers.
- Warehouse rack and storage locations.
- Available and occupied storage spaces.
- Products that must be dispatched first.

This manual process introduces several operational challenges:

1. **Manual inventory tracking:** Employees spend considerable time identifying and locating manufactured products.
2. **FIFO management difficulties:** Identifying the earliest manufactured production batch can become challenging when inventory records are maintained manually.
3. **Human errors:** Incorrect tracking of boxes and storage locations can result in inventory mismatches.
4. **Product wastage:** Delays or errors in identifying older inventory can result in products remaining unused for extended periods.
5. **Limited traceability:** Manually maintained records make it difficult to retrieve production and storage information efficiently.

To address these challenges, this project introduces a centralized web-based inventory management system that automates product identification, production record management, and FIFO-based location retrieval.

## Project Objectives

The major objectives of the application are:

- Develop a centralized database for storing product and production information.
- Import product information provided through Excel datasets.
- Generate unique QR codes/barcodes for manufactured production records.
- Maintain information about warehouse racks and storage locations.
- Track the quantity of manufactured products stored in each location.
- Identify the earliest manufactured production batch using FIFO.
- Retrieve the storage location of products that need to be dispatched first.
- Support administrative operations for managing inventory records.
- Reduce manual effort in product identification and warehouse management.

## Key Features

### 1. Product Management

Maintains information about the components manufactured by the industry.

Product information includes:

- Unique part number.
- Product description.
- Standard box quantity.

### 2. Production Management

Maintains individual manufacturing records for different products.

Each production record contains information such as:

- Associated part number.
- Manufacturing date.
- Production quantity.
- Warehouse storage location.
- Unique barcode/QR-code identifier.

### 3. Automatic QR Code Generation

Generates a unique identification code for newly registered production records using relevant production information.

This allows production batches to be identified and associated with their corresponding inventory records.

### 4. Warehouse Location Management

Maintains information about physical warehouse locations and their availability.

Each location is associated with a storage identifier and an occupancy status indicating whether it is empty or occupied.

### 5. FIFO-Based Inventory Retrieval

Identifies the earliest manufactured production record for a selected product.

The application retrieves the corresponding storage location to help warehouse personnel dispatch older inventory first.

### 6. Administrative Management

Provides an administrative interface with authentication and inventory management operations.

Administrators can manage product records, production records, and warehouse-related information.

### 7. Container Management

Supports the movement and assignment of stored product boxes into containers based on the FIFO inventory workflow.

---

## Technology Stack

| Technology | Purpose |
|---|---|
| Python | Backend programming language |
| Django | Backend web application framework |
| Microsoft PowerApps | Frontend application interface |
| Django ORM | Database interaction and record management |
| Python barcode-generation library | Barcode/QR-code generation functionality |
| Database | Storage of product, production, and location records |
| Excel | Source of initial product information |

**Architecture:** Client-server architecture.

**Backend:** Django.

**Frontend:** Microsoft PowerApps.

**Application design:** Django Model-View-Template (MVT) architecture.

*Note: The original project documentation does not specify the exact database engine or Django version. The report references the `python-barcode` package while describing QR-code generation; the exact library and generated code format should be confirmed against the original implementation.*

---

## System Architecture

The application follows a client-server architecture in which the frontend interacts with the backend to perform inventory-related operations.

The system consists of the following major components:

### 1. Frontend Layer

Microsoft PowerApps provides the user-facing interface through which administrators interact with the inventory management application.

The interface supports operations such as:

- Viewing available products.
- Adding new products.
- Registering new production records.
- Searching for manufactured components.
- Viewing warehouse rack locations.
- Managing container-related information.

### 2. Backend Layer

Python Django handles the application's backend functionality.

Its responsibilities include:

- Processing application operations.
- Managing product and production records.
- Interacting with the database.
- Generating unique identification codes.
- Retrieving product and warehouse information.
- Supporting FIFO-based inventory retrieval.

### 3. Database Layer

The database maintains structured information through three primary models:

- Products
- Productions
- Locations

Django ORM provides the interface for interacting with these database records.

### Architecture Flow

```text
              ADMIN / USER
                   |
                   |
                   v
          MICROSOFT POWERAPPS
              (Frontend)
                   |
                   |
                   v
             PYTHON DJANGO
               (Backend)
                   |
          +--------+--------+
          |        |        |
          v        v        v
       Product Production Location
        Model    Model     Model
          |        |        |
          +--------+--------+
                   |
                   v
              DATABASE
                   |
                   v
        INVENTORY INFORMATION
                   |
          +--------+--------+
          |                 |
          v                 v
      QR Generation    FIFO Retrieval
          |                 |
          v                 v
     Identification    Storage Location
          |                 |
          +--------+--------+
                   |
                   v
             USER RESPONSE
```

---

## Application Workflow

The application follows a structured process to manage manufactured products from registration to dispatch.

### Step 1: Product Data Collection

The initial product information is provided by the industry in Excel format.

The dataset contains important information such as:

- Part number.
- Product description.
- Standard quantity.

### Step 2: Data Preprocessing

The raw dataset is processed before being stored in the application.

The preprocessing stage involves:

- Extracting relevant information.
- Selecting necessary fields.
- Removing unnecessary data.
- Handling incomplete information.

The processed information is then organized into the application's database models.

### Step 3: Product Registration

Product information is stored in the Products model.

Each product is identified using its unique part number.

### Step 4: Production Registration

When a new manufacturing batch is registered, its associated product information, manufacturing date, quantity, and storage location are recorded.

### Step 5: Identification Code Generation

A unique barcode/QR-code identifier is generated using the relevant production information.

The generated identification code is associated with the corresponding production record.

### Step 6: Warehouse Storage

Manufactured product boxes are assigned to designated warehouse locations.

The Locations model maintains the location identifiers and their occupancy status.

### Step 7: FIFO-Based Search

When an administrator searches for a particular part number, the application identifies the earliest manufactured production record.

### Step 8: Location Retrieval

The corresponding warehouse location is retrieved and displayed so that the appropriate production batch can be selected for dispatch.

---

## Database Design

The application organizes inventory information into three primary database models.

### 1. Products Model

The Products model stores information about the different components manufactured by the industry.

| Field | Description |
|---|---|
| partname | Unique part number and primary key |
| description | Description of the manufactured component |
| standard_quantity | Standard quantity of products per box |

**Example:**

| Part Number | Description | Standard Quantity |
|---|---|---:|
| 2-28-1697 | Tube Yoke | 810 |
| 2-28-367 | Tube Yoke | 990 |

The part number uniquely identifies a product in the Products model.

### 2. Productions Model

The Productions model stores individual manufacturing records.

It maintains information about each production batch and its corresponding warehouse location.

| Field | Description |
|---|---|
| partname | Associated product |
| production_date | Manufacturing date |
| quantity | Quantity produced |
| location | Storage location |
| barcode | Unique production identification code |

**Example:**

| Part Number | Production Date | Quantity | Location |
|---|---|---:|---|
| 2-28-1697 | 2022-01-10 | 810 | A01 |
| 2-28-1697 | 2022-01-12 | 810 | A02 |
| 2-28-1697 | 2022-01-15 | 500 | B01 |

Multiple production records can belong to the same product.

This allows the application to maintain separate records for different manufacturing batches.

### 3. Locations Model

The Locations model stores information about the physical storage locations available within the manufacturing facility.

| Field | Description |
|---|---|
| location_name | Unique warehouse location identifier |
| status | Indicates whether the location is empty or occupied |

**Example:**

| Location | Status |
|---|---|
| A01 | Occupied |
| A02 | Occupied |
| A03 | Empty |
| B01 | Occupied |

This model helps maintain information about warehouse space utilization.

### Database Relationships

The logical relationship between the models is:

- One product can have multiple production records.
- Each production record belongs to a particular product.
- Each production record is associated with a warehouse location.
- A location maintains its occupancy status.

The separation of these entities helps organize inventory information and avoid unnecessary duplication.

---

## FIFO (First In, First Out) Implementation

FIFO is the primary business logic of this project.

It ensures that the earliest manufactured products are identified for dispatch before newer production batches.

### Understanding FIFO

Consider the following production records for the same component:

| Production Batch | Manufacturing Date | Location |
|---|---|---|
| Batch 001 | 10 January | A01 |
| Batch 002 | 12 January | A02 |
| Batch 003 | 15 January | B01 |
| Batch 004 | 18 January | B02 |

When a user searches for this component, the application should identify Batch 001 because it has the earliest manufacturing date.

The corresponding location, A01, is then retrieved.

### FIFO Processing Logic

The conceptual FIFO algorithm is:

1. Accept the requested part number.
2. Retrieve production records associated with that part number.
3. Arrange the production records according to manufacturing date in ascending order.
4. Identify the earliest production record.
5. Retrieve its corresponding warehouse location.
6. Display the location information to the user.

### Illustrative Python Implementation

The following example demonstrates how the FIFO selection logic can be implemented using Django ORM.

```python
production = Production.objects.filter(
    partname="2-28-1697"
).order_by(
    "production_date"
).first()

if production:
    print("Earliest Production Found")
    print("Production Date:", production.production_date)
    print("Storage Location:", production.location)
else:
    print("No production records found")
```

**Explanation:**

- `filter()` retrieves production records matching the selected part number.
- `order_by()` sorts the records by manufacturing date.
- Ascending order ensures older production records appear first.
- `first()` retrieves the earliest matching production record.
- The corresponding location is then accessed through the selected record.

*This is an illustrative implementation of the documented FIFO requirement, not a claim that this exact source code was used in the original project.*

---

## Barcode and QR Code Generation

The application includes an identification-code generation module.

The purpose of this module is to uniquely identify manufactured production batches.

The identification information is associated with production details such as:

- Part number.
- Manufacturing date.
- Storage location.

### Generation Process

```text
      PRODUCTION DETAILS
              |
              v
       IDENTIFICATION DATA
              |
              v
      CODE GENERATION MODULE
              |
              v
       UNIQUE CODE IMAGE
              |
              v
     ASSOCIATED PRODUCTION
           RECORD
```

The identification code allows a production batch to be associated with its corresponding inventory information.

This simplifies identification and reduces dependence on manual record searching.

---

## Application Modules

The system consists of two major development modules.

### 1. Barcode Generation Module

This module handles the generation of unique identification codes for manufactured products.

Its responsibilities include:

- Accepting production-related information.
- Generating identification codes.
- Associating generated codes with production records.
- Supporting product identification.

### 2. Portal Development Module

The portal development module handles the web-based inventory management functionality.

Its responsibilities include:

- Database model management.
- Product registration.
- Production registration.
- Administrative authentication.
- Inventory management.
- FIFO-based location retrieval.
- Warehouse location management.
- Container-related operations.

---

## Administrative Functionalities

The application provides administrative operations for managing inventory records.

The documented application functionalities include:

| Functionality | Description |
|---|---|
| Admin Login | Allows administrators to access the application |
| Product Management | Add, view, and manage product records |
| Production Management | Register and manage manufacturing batches |
| QR Code Generation | Generate identification codes for new production records |
| Location Management | Maintain warehouse location information |
| FIFO Search | Identify the earliest manufactured production |
| Rack Location | View stored products and associated locations |
| Container Management | Manage the movement of product boxes into containers |

---

## Benefits of the Project

The application provides several operational advantages.

### Reduced Manual Effort

Automating production identification and location retrieval reduces the need for employees to manually search through inventory records.

### Improved Inventory Traceability

Production batches can be associated with identification codes and warehouse locations.

### FIFO Adherence

The application helps identify the earliest manufactured inventory for dispatch.

### Better Warehouse Organization

Maintaining location and occupancy information helps administrators manage storage locations.

### Reduced Human Errors

Structured database records and automated identification reduce dependence on manually maintained information.

### Improved Operational Efficiency

Centralized inventory management simplifies the process of locating and identifying manufactured components.

---

## Limitations

The original project also identified opportunities for improvement.

Some areas that could benefit from additional development include:

- Further optimization of application performance.
- Expansion of the portal to support additional industrial sections.
- Development of a corresponding mobile application for reading QR codes and displaying production information.
- Additional improvements to inventory management and warehouse operations.

---

## Future Enhancements

The following enhancements could extend the existing system into a more comprehensive industrial inventory management solution.

### 1. REST API Integration

Develop RESTful APIs using Django REST Framework to allow other applications and services to interact with inventory data.

### 2. Mobile QR Code Scanning

Develop a mobile application that can scan product identification codes and retrieve associated production and warehouse information.

### 3. Advanced Inventory Analytics

Introduce reporting dashboards to monitor production quantities, stock availability, dispatch history, and warehouse utilization.

### 4. Database Optimization

Introduce suitable database indexes and optimize frequently executed inventory queries.

### 5. Improved Authentication and Authorization

Implement role-based access control to manage permissions for administrators, warehouse employees, and other users.

### 6. Containerization

Package the backend application using Docker to simplify deployment and maintain consistent development environments.

### 7. Cloud Deployment

Explore deployment on cloud infrastructure to improve application availability, scalability, and accessibility.

---

## Project Information

| Attribute | Details |
|---|---|
| Project Name | Barcoding of Inventory System for FIFO Adherence |
| Project Type | Academic Team Project |
| Degree | Bachelor of Engineering in Computer Science |
| Institution | KLE Technological University, Hubballi |
| Academic Year | 2021–2022 |
| Backend Language | Python |
| Backend Framework | Django |
| Frontend | Microsoft PowerApps |
| Architecture | Client-Server |
| Application Domain | Inventory Management and Warehouse Automation |

---

## Conclusion

The Barcoding of Inventory System for FIFO Adherence demonstrates how Python and Django can be used to address practical inventory management challenges in a manufacturing environment.

By combining structured database management, automated product identification, production record tracking, and FIFO-based location retrieval, the application provides a centralized approach to managing manufactured goods.

The project focuses on reducing manual inventory tracking, improving product traceability, and helping manufacturing facilities maintain the correct dispatch sequence.

It also provides a foundation for further development through REST API integration, mobile QR code scanning, performance optimization, and cloud-based deployment.

---

**Core Concepts Demonstrated:**

`Python` · `Django` · `Django ORM` · `Database Management` · `CRUD Operations` · `FIFO Algorithm` · `QR Code Generation` · `Inventory Management` · `Client-Server Architecture`
