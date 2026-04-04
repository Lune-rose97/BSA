```mermaid
---
title: exercise06 - updated UML diagram
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

    class ClientNotification {
        - notification_id : int [PK]
        - client_id : int [FK]
        - notification_type : varchar [20]
        - contact_channel : varchar [20]
        - subject : varchar [255]
        - sent_status : string
        - sent_time : datetime
        - booking_id : int [FK]
        - created_at: datetime
    }

    class ClientDiscount {
        - discount_id : int [PK]
        - client_id : int [FK]
        - discount_type : varchar [50]
        - discount_amount : decimal
        - start_date : date
        - end_date : date
        - is_active : boolean
    }

    %% Связи между классами
    Person "1" -- "1" Client : "является"
    Person "1" -- "1" Employee : "работает как"
    
    Client "1" --> "*" Appointment : "делает"
    Client "1" --> "*" ClientNotification : "получает"
    Client "1" --> "*" ClientDiscount : "имеет"
    
    Employee "1" --> "*" EmployeeRole : "имеет"
    Employee "1" --> "*" EmployeeService : "выполняет"
    Employee "1" --> "*" ServiceSlot : " обслуживает в"
    
    Service "1" --> "*" EmployeeService : "включена в"
    Service "1" --> "*" Appointment : "выбирается в"
    
    ServiceSlot "1" -- "1" Appointment : "rезервируется для"
    
    EmployeeRole "1" --> "*" ServiceSlot : "определяет доступность"

    ClientNotification "*" --> "1" ServiceSlot : "соответсвует"