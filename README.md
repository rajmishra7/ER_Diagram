# ER_Diagram

#Smart Elevator System

<img width="1632" height="1162" alt="diagram-export-11-04-2026-01_04_58" src="https://github.com/user-attachments/assets/4c4b6b26-6ca4-4c1f-a592-46c86dccbcea" />

https://app.eraser.io/workspace/nrydT3ODgKHzwXvUhphm

##Relationships

buildings.building_id < floors.floor_id
buildings.building_id < elevator_shaft.shaft_id

elevator_shaft.shaft_id - elevators.elevator_id

elevators.elevator_id < floors.floor_id

floors.floor_id  < floor_request.requestID
floors.floor_id < floor_request.requestID

floor_request.requestID - ride_assignment.assignment_id

ride_assignment.assignment_id - elevators.elevator_id

elevators.elevator_id < rides.ride_id
elevators.elevator_id < maintenance.maintenance_id
elevators.elevator_id < elevator_status_tracking.status_id
--------------------------------------------------------------------------------------------------------------------------------------------------------------
# Comic-Con Parking system

Link - https://app.eraser.io/workspace/nrydT3ODgKHzwXvUhphm?origin=share

<img width="2175" height="1177" alt="diagram-export-10-04-2026-00_24_15" src="https://github.com/user-attachments/assets/79539de2-71ae-49d5-a6d3-a7d4b1851e88" />

Vehicles [icon: car, color: white] {
  vehicle_id serial PK
  vehicle_number CHAR(12) not null
  created_at TIMESTAMP
  updated_at TIMESTAMP
  owner_id FK
  vehicle_category_id FK
}

Vehicle_categories [color: white, icon: list] {
  vehicle_category_id serial PK
  vehicle_type enum(car, bike, suv, ev, cab)
}

Parking_zones [color: white] {
  zone_id int PK
  zone_name text
}

Parking_spots [color: white] {
  parking_spot_id serial PK
  zone_id FK
  parking_spot_number int not null
  parking_spot_category FK
  is_spot_reserved boolean
}
 
 Parking_spot_categories [icon: menu, color: white]{
  spot_category_id serial PK 
  spot_category_name enum(cosplayers, exhibitors, creators, VIP guests, staff, EV_charging )
 }

 Parking_tickets [icon: ticket, color: white] {
  ticket_id serial PK
  ticket_number int
  parking_session_id FK
  vehicle_id FK 
  parking_spot_id FK
 }

 Parking_sessions [color: white]{
  parking_session_id serial PK
  session_status enum("active", "expired")
  vehicle_id FK
  parking_spot_id FK
  entered_at TIMESTAMP
  exited_at TIMESTAMP 
 }

Payment [icon: money, color: white] {
  payment_id serial PK
  parking_session_id FK
  ticket_id
  amount int 
  payment_status enum("Success", "Pending", "Failed")
  payment_method enum("UPI", "Cash", "Card")
}

--Relationships--

Vehicles.id > Vehicle_categories.vehicle_category_id
Vehicles.vehicle_id < Parking_sessions.parking_session_id

Parking_tickets.ticket_id - Payment.payment_id
Parking_spots.parking_spot_id < Parking_sessions.parking_session_id

Parking_zones.zone_id < Parking_spots.parking_spot_id
Parking_spots.parking_spot_id > Parking_spot_categories.spot_category_id

Parking_sessions.parking_session_id - Parking_tickets.ticket_id

Parking_sessions.parking_session_id - Payment.payment_id

-------------------------------------------------------------------------------------------------------------------------------------------------------

# Mordern Clinic System - https://app.eraser.io/workspace/6ZQKQByTiYmuZIK9LHGG?origin=share&diagram=uMAAmj2eLEC0NMpJZpqa8

<img width="2016" height="1355" alt="diagram-export-08-04-2026-17_39_57" src="https://github.com/user-attachments/assets/3995a396-fd43-4996-a645-1f7c38132bf0" />


users {
  user_id serial PK
  name VARCHAR(50) not null
  email VARCHAR(50) not null
  age int not null
  gender enum("MALE", "FEMALE")
  phone char(10) not null
  role enum("Patient", "Doctor")
  password varchar(20) not null
  created_at timestamp
  updated_at timestamp
}

doctors  {
  doctor_id FK
  specialization_id FK - specializations.specialization_id
} 

specializations {
  specialization_id PK
  name VARCHAR(50) not null
}

patients{
  patient_id FK
  issue text not null
}

appointments {
  appointment_id serial PK
  scheduled_at TIME
  doctor_id FK 
  patient_id FK
  status enum("completed", "pending", "cancelled")
  result varchar(200)
  consultation_needed boolean
}

tests {
  test_id serial PK
  test_name varchar(50) not null
  cost INT not null
}

consultations {
  consultation_id serial PK
  appointment_id PK
  reason text not null
  date_time DATETIME 
  doctor_id FK
  patient_id FK
  test_id FK
  follow_up_needed boolean
  prescription text
  diagnosis text
  notes text
}

reports {
  report_id serial PK
  patient_id FK
  result enum("Positive", "Negative")
  consultation_id FK
  report_file URL
  generated_date date 
}

payments {
  payment_id serial PK
  payment_method enum("CASH", "UPI", "CARD")
  appointment_id FK
  patient_id FK
  consultation_id FK
  status enum("PAID", "PENDING", "FAILED")
  payment_time timestamp
  amount int not null
}


#CARDINALITY##----------


users.user_id - doctors.doctor_id
users.user_id - patients.patient_id

doctors.doctor_id < patients.patient_id
doctors.doctor_id > specializations.specialization_id


appointments.appointment_id - doctors.doctor_id
appointments.appointment_id > patients.patient_id

consultations.consultation_id > doctors.doctor_id
consultations.consultation_id > patients.patient_id
consultations.consultation_id - appointments.appointment_id
consultations.consultation_id < tests.test_id
consultations.consultation_id - reports.report_id
consultations.consultation_id > payments.payment_id

tests.test_id > patients.patient_id
tests.test_id - reports.report_id
tests.test_id > payments.payment_id

patients.patient_id < reports.report_id
patients.patient_id < payments.payment_id







