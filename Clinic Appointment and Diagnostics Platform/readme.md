# Clinic Appointment and Diagnostics Platform

## Overview

This stores information about the clinic appointment and diagnostics details.

---

## Database Schema

### Users

```
//stores user information role differentiates between doctor and patient
users [icon: user, color: blue] {
id string pk
first_name string
last_name string
email string
phone string
address_line1 string
address_line2 string
postcode string
role string //patient,doctor,admin
is_active boolean
created_at timestamp
updated_at timestamp
}
```

### Departments

```
//master table for departments
departments[icon: department, color:blue]{
id int pk
name string
description string
}
```

### Patients

```
//store patient information
patients [icon: users, color: blue] {
id pk
user_id int fk
date_of_birth date
blood_group string
}
```

### Doctors

```
//store doctor information
doctors [icon: home] {
id pk
user_id int fk
specailization string
department_id int fk
}
```

### Appointments

```
//store appoitments for patient
appoitments [icon: folder] {
id int pk
patient_id int fk
department_int int fk
doctor_id int fk (user table)
comments string
appoitment_date date
created_at timestamp
}
```

### Consultations

```
//store consultation details
consultations{
id int pk
doctor_id (user table)
patient_id (user table)
appoitment_id int fk
daignosis text
consultation_date date
notes string
}
```

### Payments

```
//store information about payments
payments{
id int pk
appoitment_id int fk
amount decimal
method string
status string
paid_at timestamp
}
```

### Test Types

```
//master table for the test eb. blood tests
test_types [icon: message-circle, color: green] {
id int pk
name string
description string
base_price decimal
}
```

### Prescribed Tests

```
//store inforation about perscribted tests
prescribed_tests{
id int pk
consultation_id fk
test_types_id int fk
status string
comment string
precribed_at timestamp
}
```

### Diagnostic Reports

```
//store information about the results of test
diagontic_reports{
id int pk
precribed_test_id int fk
result_summary string
findings string
file blob
reported_at timestamp
}
```

---

## Entity Relationships

```
users.id - patients.user_id
users.id - doctors.user_id
users.id < appoitments.patient_id
users.id < consultations.patient_id
appoitments.id - consultations.appoitment_id
consultations.id < prescribed_tests.consultation_id
```

test_types.id < prescribed_tests.report_id
departments.id < doctors.department_id
prescribed_tests.id < diagontic_reports.precribed_test_id
appoitments.id - payments.appoitment_id
