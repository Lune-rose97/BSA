```mermaid
---
title: exercise04 - UML diagram
---
classDiagram
    direction TB

    class Person {
        - person_id : int [PK]
        - login : varchar [50]
        - password : varchar [255]
        - name : varchar [100]
        - phone : varchar [20]
        - registration_date : datetime
    }

    class Client {
        - client_id : int [PK]
        - person_id : int [FK]
        - registration_date : datetime
        - preferred_contact_channel : varchar [25]
        - is_active : boolean
    }

    class Employee {
        - employee_id : int [PK]
        - person_id : int [FK]
        - registration_date : datetime
        - is_active : boolean
    }

    class EmployeeRole {
        - role_id : int [PK]
        - employee_id : int [FK]
        - role : varchar [8]
    }

    class Service {
        - service_id : int [PK]
        - name : varchar [25]
        - description : varchar [250]
        - duration : int
        - price : decimal
        - is_active : boolean
    }

    class EmployeeService {
        - employee_service_id : int [PK]
        - employee_id : int [FK]
        - service_id : int [FK]
        - is_active : boolean
    }

    class ServiceSlot {
        - slot_id : int [PK]
        - date : date
        - start_time : time
        - employee_id : int [FK]
        - client_id : int [FK]
        - status : varchar [20]
        - duration : int
    }

    class Appointment {
        - appointment_id : int [PK]
        - client_id : int [FK]
        - slot_id : int [FK]
        - service_id : int [FK]
        - status : string
        - created_date : datetime
    }


    %% Связи между классами
    Person "1" -- "1" Client : "является"
    Person "1" -- "1" Employee : "работает как"
    
    Client "1" --> "*" Appointment : "делает"
    
    Employee "1" --> "*" EmployeeRole : "имеет"
    Employee "1" --> "*" EmployeeService : "выполняет"
    Employee "1" --> "*" ServiceSlot : " обслуживает в"
    
    Service "1" --> "*" EmployeeService : "включена в"
    Service "1" --> "*" Appointment : "выбирается в"
    
    ServiceSlot "1" -- "1" Appointment : "rезервируется для"
    
    EmployeeRole "1" --> "*" ServiceSlot : "определяет доступность"