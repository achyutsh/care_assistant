# Care Assistance API

## 📌 Project Overview

The **Care Assistance API** is a simple MuleSoft integration flow designed as a proof of concept for a healthcare use case. It demonstrates how MuleSoft can be used to connect patient data stored in a MySQL database, process it, and generate a readiness report for each patient.

## ⚙️ What It Does

This API performs the following steps:

* **Fetch Patients:** Retrieves patient details such as ID, name, email, and medical conditions from a MySQL database.
* **Check Pharmacy Refills:** Looks up the patient’s medication refill status to identify if any refills are overdue.
* **Check Appointments:** Checks upcoming and past appointments to determine if any are overdue.
* **Recommend Specialist:** Based on the patient’s conditions, suggests the type of specialist they should consult.
* **Generate Report:** Produces a JSON readiness summary for each patient, including:

  * Patient ID, name, and email
  * Refill and appointment status (CURRENT or OVERDUE)
  * Next upcoming appointment type
  * Recommended specialist
  * Overall care readiness status (`READY` or `NOT_READY`)

## 🗄️ Database Structure

The API works with three simple MySQL tables:

* **patients**

  * `patient_id` — unique ID for each patient
  * `name` — full name
  * `email` — contact email
  * `conditions` — medical conditions (e.g., diabetes, hypertension)

* **pharmacy\_refills**

  * `patient_id` — foreign key to `patients`
  * `medication_name` — name of the medication
  * `refill_status` — `current` or `overdue`
  * `last_refill_date` — date of last refill

* **appointments**

  * `patient_id` — foreign key to `patients`
  * `appointment_type` — type of appointment (e.g., Follow-up, Endocrinology)
  * `appointment_date` — scheduled date
  * `status` — `completed` or `scheduled`

## ✅ Result
![image](https://github.com/user-attachments/assets/dc87d3fa-b2ec-4f42-b5db-cc9e7b1e96cd)

**When the API runs, it returns a consolidated JSON array of readiness reports for all patients. This output can be used by other systems or a chatbot to provide personalized care guidance to patients.**


## 🔑 How to Run

1. **Database:** Ensure you have a MySQL database with the required tables and sample data.
2. **Configuration:** Update your database credentials in `care.properties`.
3. **Deploy:** Run the Mule application in Anypoint Studio.
4. **Test:** Call the `/care` HTTP endpoint to see the JSON report.

## 📂 Project Structure

* `src/main/mule` — Mule XML flow definition
* `src/main/resources` — Configuration files (`care.properties`)
* `pom.xml` — Maven build configuration
