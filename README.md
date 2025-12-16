erDiagram
    AIRPORT {
        int airportid PK
        varchar airportname
        varchar country
        varchar state
        varchar city
        timestamp createdat
        timestamp updatedat
    }
    
    AIRLINE {
        int airlineid PK
        varchar airlinecode UK
        varchar airlinename
        varchar airlinecountry
        timestamp createdat
        timestamp updatedat
    }
    
    FLIGHTS {
        int flightid PK
        timestamp schdeparturetime
        timestamp scharrivaltime
        int departingairportid FK
        int arrivingairportid FK
        text departinggate
        varchar arrivinggate
        int airlineid FK
        timestamp actdeparturetime
        timestamp actarrivaltime
        timestamp createdat
        timestamp updatedat
    }
    
    PASSENGERS {
        int passengerid PK
        varchar firstname
        varchar lastname
        date dateofbirth
        varchar gender
        varchar countryofcitizenship
        varchar countryofresidence
        varchar passportnumber UK
        timestamp createdat
        timestamp updatedat
    }
    
    BOOKING {
        int bookingid PK
        int flightid FK
        int passengerid FK
        varchar bookingplatform
        timestamp createdat
        timestamp updatedat
        varchar status
        decimal ticketprice
    }
    
    BOOKINGFLIGHT {
        int bookingflightid PK
        int bookingid FK
        int flightid FK
        timestamp createdat
        timestamp updatedat
    }
    
    BOARDINGPASS {
        int boardingpassid PK
        int bookingid FK
        varchar seat
        timestamp boardingtime
        timestamp createdat
        timestamp updatedat
    }
    
    BAGGAGE {
        int baggageid PK
        decimal weightinkg
        timestamp createdat
        timestamp updatedat
        int bookingid FK
    }
    
    BAGGAGECHECK {
        int baggagecheckid PK
        varchar checkresult
        timestamp createdat
        timestamp updatedat
        int bookingid FK
        int passengerid FK
    }
    
    SECURITYCHECK {
        int securitycheckid PK
        varchar checkresult
        timestamp createdat
        timestamp updatedat
        int passengerid FK
    }
    
    %% Relationships
    AIRPORT ||--o{ FLIGHTS : "departure"
    AIRPORT ||--o{ FLIGHTS : "arrival"
    AIRLINE ||--o{ FLIGHTS : "operates"
    PASSENGERS ||--o{ BOOKING : "makes"
    FLIGHTS ||--o{ BOOKING : "has"
    BOOKING ||--o{ BOOKINGFLIGHT : "changes"
    FLIGHTS ||--o{ BOOKINGFLIGHT : "involves"
    BOOKING ||--o{ BOARDINGPASS : "issues"
    BOOKING ||--o{ BAGGAGE : "registers"
    BOOKING ||--o{ BAGGAGECHECK : "checked"
    PASSENGERS ||--o{ BAGGAGECHECK : "owns"
    PASSENGERS ||--o{ SECURITYCHECK : "passes"
