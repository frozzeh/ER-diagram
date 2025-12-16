```mermaid
erDiagram
    AIRPORT {
        int airport_id PK
        string airport_name
        string country
        string state
        string city
        date created_at
        date updated_at
    }

    AIRLINE {
        int airline_id PK
        string airline_code
        string airline_name
        string airline_country
        date created_at
        date updated_at
    }

    FLIGHTS {
        int flight_id PK
        date sch_departure_time
        date sch_arrival_time
        int departing_airport_id FK
        int arriving_airport_id FK
        int airline_id FK
        string departing_gate
        string arriving_gate
        date act_departure_time
        date act_arrival_time
        date created_at
        date updated_at
    }

    PASSENGERS {
        int passenger_id PK
        string first_name
        string last_name
        date date_of_birth
        string gender
        string country_of_citizenship
        string country_of_residence
        string passport_number
        date created_at
        date updated_at
    }

    BOOKING {
        int booking_id PK
        int flight_id FK
        int passenger_id FK
        string booking_platform
        string status
        float ticket_price
        date created_at
        date updated_at
    }

    BOOKING_FLIGHT {
        int booking_flight_id PK
        int booking_id FK
        int flight_id FK
        date created_at
        date updated_at
    }

    BOARDING_PASS {
        int boarding_pass_id PK
        int booking_id FK
        string seat
        date boarding_time
        date created_at
        date updated_at
    }

    BAGGAGE {
        int baggage_id PK
        float weight_in_kg
        int booking_id FK
        date created_at
        date updated_at
    }

    BAGGAGE_CHECK {
        int baggage_check_id PK
        string check_result
        int booking_id FK
        int passenger_id FK
        date created_at
        date updated_at
    }

    SECURITY_CHECK {
        int security_check_id PK
        string check_result
        int passenger_id FK
        date created_at
        date updated_at
    }

    AIRPORT ||--o{ FLIGHTS : departs_from
    AIRPORT ||--o{ FLIGHTS : arrives_to
    AIRLINE ||--o{ FLIGHTS : operates

    FLIGHTS ||--o{ BOOKING_FLIGHT : has
    BOOKING ||--o{ BOOKING_FLIGHT : includes
    BOOKING ||--o{ BOARDING_PASS : generates
    BOOKING ||--o{ BAGGAGE : contains
    BOOKING ||--o{ BAGGAGE_CHECK : triggers

    PASSENGERS ||--o{ BOOKING : makes
    PASSENGERS ||--o{ BAGGAGE_CHECK : undergoes
    PASSENGERS ||--o{ SECURITY_CHECK : passes
```
