<div align="center">

# 📦 LogiCore Management System

### A cross-platform-oriented C++ console application for managing suppliers and shipments

[![C++](https://img.shields.io/badge/C++-14-00599C?style=flat-square\&logo=c%2B%2B\&logoColor=white)](https://isocpp.org/)
[![CMake](https://img.shields.io/badge/Build-CMake-064F8C?style=flat-square\&logo=cmake\&logoColor=white)](https://cmake.org/)
[![OOP](https://img.shields.io/badge/Architecture-OOP-blueviolet?style=flat-square)](#architecture)
[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Unix-informational?style=flat-square)](#building-the-project)
[![Persistence](https://img.shields.io/badge/Persistence-Local%20Files-success?style=flat-square)](#data-persistence)
[![Purpose](https://img.shields.io/badge/Purpose-Educational-orange?style=flat-square)](#project-status)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)](LICENSE)

<br>

<img src="https://github.com/user-attachments/assets/f7c7e7e7-cf30-4caa-8715-3fdba379ca9b" alt="LogiCore Management System main menu" width="49%">
<img src="https://github.com/user-attachments/assets/08792391-8765-4010-a0b5-1f9e03d23fb6" alt="LogiCore Management System records view" width="49%">

</div>

---

## About the Project

**LogiCore Management System**, or **LCMS**, is an educational C++ console application for managing information about suppliers and shipments.

The application maintains two related types of records:

* suppliers, including contract and payment information;
* shipments, including delivery dates, supply amounts, and payment amounts.

Users can add records, display the complete dataset, search by company name or delivery date, sort records, calculate financial balances, and save the current state to local files.

The project was created to practise object-oriented programming, inheritance, polymorphism, operator overloading, smart pointers, STL containers, file I/O, validation, and portable CMake-based builds.

> [!NOTE]
> LCMS uses local file persistence rather than an external database server. It is a learning project that models a small logistics data-management system, not a production ERP or warehouse platform.

---

## ✨ Features

### Supplier Management

Each supplier record contains:

* company name;
* total contract amount;
* amount already paid;
* calculated outstanding balance.

The application supports adding suppliers, displaying their information, searching by company name, and sorting suppliers by balance.

### Shipment Management

Each shipment record contains:

* supplier or company name;
* delivery date;
* supplied goods amount;
* payment amount;
* calculated balance.

Shipments can be added, displayed, searched by delivery date, and sorted chronologically.

### Search

The application provides several search operations:

* search suppliers and shipments by company name;
* search supplier records in a dynamic collection;
* search shipments by delivery date;
* display matching records directly in the console.

### Sorting

Available sorting operations include:

* sorting suppliers by financial balance;
* sorting shipments by delivery date.

### File Persistence

Supplier and shipment records are loaded from local files when the application starts.

The user can explicitly save the current data through the main menu. Supplier and shipment records are stored separately, keeping persistence logic independent from the domain classes.

### Keyboard-Controlled Menu

The interface provides a navigable console menu with support for:

* Up Arrow;
* Down Arrow;
* Enter;
* Escape.

Platform-specific console input is handled separately for Windows and Unix-like systems.

---

## 🖥️ Available Menu Operations

The main menu provides the following operations:

1. Display all supplier and shipment data
2. Add new suppliers
3. Add new shipments
4. Search by company name
5. Sort stored data
6. Save data to files
7. Demonstrate overloaded operators
8. Search suppliers in a dynamic collection
9. Search shipments by delivery date
10. Exit the application

---

## 🧠 C++ Concepts Demonstrated

The project demonstrates several fundamental and intermediate C++ concepts:

* classes and encapsulation;
* inheritance;
* runtime polymorphism;
* virtual methods;
* virtual destructors;
* operator overloading;
* constructors and assignment operators;
* exception handling;
* input validation;
* STL containers;
* sorting with standard algorithms;
* `std::unique_ptr`;
* automatic resource management;
* file input and output;
* conditional compilation;
* separation of declarations and implementations;
* modular project organization;
* CMake configuration.

---

## 🏗️ Architecture

The domain model is built around the `common` base class.

```text
                         common
                            │
                 ┌──────────┴──────────┐
                 │                     │
              supplier              shipment
                                         │
                                        date
```

### `common`

The shared base class stores the company name and defines the common interface:

* `input()`;
* `output()`;
* `search_by_company()`;
* `get_balance()`.

It also provides stream insertion and extraction operators.

### `supplier`

The `supplier` class extends `common` with:

* contract amount;
* paid amount;
* supplier balance calculation;
* supplier-specific input and output;
* assignment and input operators.

### `shipment`

The `shipment` class extends `common` with:

* delivery date;
* supply amount;
* payment amount;
* shipment balance calculation;
* date-based matching;
* shipment-specific input and output.

### `date`

The custom `date` value type provides:

* day, month, and year storage;
* date validation;
* leap-year handling;
* equality comparison;
* assignment;
* stream input and output.

---

## 📁 Project Structure

```text
LC-Management-System/
├── external/
│   └── emoji.h                 # Header-only emoji-related utility
│
├── src/
│   ├── hierarchy/
│   │   ├── common.cpp          # Shared base-class implementation
│   │   ├── common.h
│   │   ├── date.cpp            # Date validation and operators
│   │   ├── date.h
│   │   ├── shipment.cpp        # Shipment domain logic
│   │   ├── shipment.h
│   │   ├── supplier.cpp        # Supplier domain logic
│   │   └── supplier.h
│   │
│   ├── menu/
│   │   ├── menu_f.cpp          # Console UI and menu helpers
│   │   └── menu_f.h
│   │
│   ├── utils/
│   │   ├── manip_file.cpp      # Loading and saving records
│   │   ├── manip_file.h
│   │   ├── manip_with_base.cpp # Search, sorting, and record operations
│   │   └── manip_with_base.h
│   │
│   └── main.cpp                # Application entry point and main menu loop
│
├── CMakeLists.txt
├── CMakePresets.json
├── LICENSE
└── README.md
```

---

## 🛠️ Technology Stack

| Technology      | Purpose                                                      |
| --------------- | ------------------------------------------------------------ |
| **C++14**       | Application and domain logic                                 |
| **CMake 3.8+**  | Cross-platform-oriented build configuration                  |
| **STL**         | Containers, algorithms, strings, streams, and smart pointers |
| **MSVC**        | Windows compiler support                                     |
| **GCC**         | Unix-like compiler support                                   |
| **Clang**       | Alternative compiler support                                 |
| **Local files** | Supplier and shipment persistence                            |

The CMake configuration enables strict compiler warnings:

* `/W4` when using MSVC;
* `-Wall -Wextra` when using GCC or Clang.

---

## 🚀 Building the Project

### Requirements

* CMake 3.8 or newer
* A compiler with C++14 support:

  * MSVC
  * GCC
  * Clang

### Clone the Repository

```bash
git clone https://github.com/s7shvets7s/LC-Management-System.git
cd LC-Management-System
```

### Configure the Build

```bash
cmake -S . -B build
```

### Build the Application

```bash
cmake --build build --config Release
```

CMake generates an executable named:

```text
LogiCore
```

---

## ▶️ Running the Application

For single-configuration generators on Linux or other Unix-like systems:

```bash
./build/LogiCore
```

For a Visual Studio Release build on Windows:

```powershell
.\build\Release\LogiCore.exe
```

The exact executable path may vary depending on the selected CMake generator and configuration.

---

## 💾 Data Persistence

At application startup, LCMS attempts to load:

* previously saved supplier records;
* previously saved shipment records.

During execution, the records are stored in:

```cpp
std::vector<std::unique_ptr<supplier>>
std::vector<std::unique_ptr<shipment>>
```

Using `std::unique_ptr` gives each collection clear ownership of its objects and ensures automatic resource cleanup.

The persistence layer is separated into dedicated functions:

```cpp
load_suppliers_from_file(...)
load_shipments_from_file(...)
save_suppliers_to_file(...)
save_shipments_to_file(...)
```

---

## ✅ Validation

The project performs validation for several input types.

Examples include:

* rejecting empty company names;
* rejecting negative financial values;
* checking valid day and month ranges;
* supporting leap years;
* restricting years to the supported range;
* detecting invalid stream input;
* reporting incorrect dates through exceptions.

---

## 🎓 Learning Goals

This project was created to gain practical experience with:

* designing a small object-oriented domain model;
* sharing behaviour through a base class;
* overriding virtual functions in derived classes;
* managing polymorphic objects with smart pointers;
* implementing custom value types;
* overloading stream and assignment operators;
* separating menu, domain, persistence, and service logic;
* searching and sorting collections;
* validating interactive console input;
* building the same project with different compilers;
* organizing a multi-file C++ application using CMake.

---

## ⚠️ Project Status

> [!IMPORTANT]
> LCMS is an educational console application and should not be treated as a production-ready logistics, accounting, ERP, or database-management platform.

The current version demonstrates its intended C++ and OOP concepts, but a production system would additionally require:

* a real database;
* automated tests;
* transactional operations;
* authentication and authorization;
* structured logging;
* stronger error recovery;
* internationalized user interfaces;
* stable persistent-data schemas.

The current console interface is primarily written in Russian.

---

## 📄 License

This project is distributed under the **MIT License**.

See the [LICENSE](LICENSE) file for the full license text.

---

<div align="center">

### Built with C++ and CMake

An educational project focused on OOP, STL, file persistence, and console application design.

</div>
