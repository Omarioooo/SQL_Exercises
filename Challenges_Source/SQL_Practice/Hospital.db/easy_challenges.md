# Easy challenges


**1) Show first name, last name, and gender of patients whose gender is 'M'**

```SQL
SELECT first_name, last_name, gender
FROM patients
WHERE gender = 'M';
```
___

**2) Show first name and last name of patients who does not have allergies. (null)**

```SQL
SELECT first_name, last_name
FROM patients
WHERE allergies IS NULL;
```
___

**3) Show first name of patients that start with the letter 'C'**

```SQL
SELECT first_name
FROM patients
WHERE first_name LIKE 'C%';
```
___

**4) Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)**

```SQL
SELECT first_name, last_name
FROM patients
WHERE weight BETWEEN 100 AND 120;
```
___

**5) Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'**

```SQL
UPDATE patients
SET allergies = 'NKA'
WHERE allergies IS NULL;
```

**6) Show first name and last name concatinated into one column to show their full name.**

```SQL
SELECT first_name + ' ' + last_name AS full_name
FROM patients;
```
___

**7) Show first name, last name, and the full province name of each patient.**

**Example: 'Ontario' instead of 'ON'**'

```SQL
SELECT first_name, last_name, n.province_name
FROM patients p
JOIN province_names n
ON p.province_id = n.province_id;
```
___

**8) Show how many patients have a birth_date with 2010 as the birth year.**
```SQL
SELECT COUNT(*)
FROM patients
WHERE YEAR(birth_date) = 2010;

-- OR --

SELECT COUNT(*)
FROM patients
WHERE birth_date LIKE '2010%'
```
___

**9) Show the first_name, last_name, and height of the patient with the greatest height.**
```SQL
SELECT TOP(1) first_name, last_name, height
FROM patients
ORDER BY height desc ;

-- OR --

SELECT first_name, last_name
FROM patients
WHERE height = (SELECT MAX(height) FROM patients)
```
___

**10) Show all columns for patients who have one of the following patient_ids: 1,45,534,879,1000**
```SQL
SELECT *
FROM patients
WHERE patient_id IN (1,45,534,879,1000);
```

**11) Show the total number of admissions**

```SQL
SELECT COUNT(p.patient_id)
FROM patients p
JOIN admissions a
ON p.patient_id = a.patient_id;
```
___

**12) Show all the columns from admissions where the patient was admitted and discharged on the same day.**

```SQL
SELECT *
FROM admissions
WHERE admission_date = discharge_date;
```
___

**13) Show the patient id and the total number of admissions for patient_id 579.**

```SQL
SELECT patient_id, COUNT(admission_date)
FROM admissions
WHERE patient_id = 579
GROUP BY patient_id;
```
___

**14) Based on the cities that our patients live in, show unique cities that are in province_id 'NS'**

```SQL
SELECT distinct city
FROM patients
WHERE province_id = 'NS';
```

**15) Write a query to find the first_name, last name and birth date of patients who has height greater than 160 and weight greater than 70**

```SQL
SELECT DISTINCT first_name, last_name, birth_date
FROM patients
WHERE height > 160 AND weight > 70;
```
___

**16) Write a query to find list of patients first_name, last_name, and allergies where allergies are not null and are from the city of 'Hamilton'**

```SQL
SELECT distinct first_name, last_name, allergies
FROM patients
WHERE allergies IS NOT NULL AND city = 'Hamilton';
```