# ER_Diagram

# Mordern Clinic System -

users [icon: user] {
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

doctors [icon: doctor] {
  doctor_id FK
  specialization_id FK - specializations.specialization_id
} 

specializations {
  specialization_id PK
  name VARCHAR(50) not null
}

patients [icon: person] {
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







