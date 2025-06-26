# Medium challenges


**1) Show unique birth years from patients and order them by ascending.**

```SQL
SELECT distinct YEAR(birth_date)
FROM patients
ORDER BY birth_date ASC;
```
___

**2) Show unique first names from the patients table which only occurs once in the list.**

**For example, if two or more people are named 'John' in the first_name column then don't include their name in the output list. If only 1 person is named 'Leo' then include them in the output.**

```SQL
SELECT first_name
FROM patients
GROUP BY first_name
HAVING COUNT(first_name) = 1;
```
___

**3) Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.**

```SQL
SELECT patient_id, first_name
FROM patients
WHERE first_name LIKE 's%s' AND LEN(first_name) >= 6;
```
___

**4) Show patient_id, first_name, last_name from patients whos diagnosis is 'Dementia'.**

**Primary diagnosis is stored in the admissions table.**

```SQL
SELECT p.patient_id, first_name, last_name
FROM patients p
JOIN admissions a
ON p.patient_id = a.patient_id
   AND diagnosis = 'Dementia';

-- OR --

SELECT patient_id, first_name, last_name
FROM patients
WHERE patient_id IN (
    SELECT patient_id
    FROM admissions
    WHERE diagnosis = 'Dementia'
);
```
___

**5) Display every patient's first_name.**

**Order the list by the length of each name and then by alphabetically.**

```SQL
SELECT first_name
FROM patients
ORDER BY LEN(first_name), first_name;
```

**6) Show the total amount of male patients and the total amount of female patients in the patients table.**

**Display the two results in the same row.**

```SQL
SELECT
(SELECT count(*) from patients where gender = 'M') Male,
(select COUNT(*) from patients where gender = 'F') Female;

-- OR --

SELECT
  SUM(CASE WHEN gender = 'M' THEN 1 ELSE 0 END) AS Male,
  SUM(CASE WHEN gender = 'F' THEN 1 ELSE 0 END) AS Female
FROM patients;
```
___

**7) Show first and last name, allergies from patients which have allergies to either 'Penicillin' or 'Morphine'. Show results ordered ascending by allergies then by first_name then by last_name.**

```SQL
SELECT first_name, last_name, allergies
FROM patients
WHERE allergies IN ('Penicillin', 'Morphine')
ORDER BY allergies, first_name, last_name;
```
___

**8) Show patient_id, diagnosis from admissions. Find patients admitted multiple times for the same diagnosis.**
```SQL
SELECT patient_id, diagnosis
FROM admissions
GROUP BY patient_id, diagnosis
HAVING COUNT(diagnosis) > 1;
```
___

**9) Show the city and the total number of patients in the city.**

**Order from most to least patients and then by city name ascending.**

```SQL
SELECT city, COUNT(patient_id)
FROM patients
GROUP BY city
ORDER BY COUNT(patient_id) DESC , city;
```
___

**10) Show first name, last name and role of every person that is either patient or doctor.**
**The roles are either "Patient" or "Doctor"**
```SQL
SELECT first_name, last_name , 'Patient' role
FROM patients
UNION ALL
SELECT first_name, last_name , 'Doctor' role
FROM doctors

-- OR --

SELECT 
    COALESCE(p.first_name, d.first_name) AS first_name,
    COALESCE(p.last_name, d.last_name) AS last_name,
    CASE 
        WHEN p.first_name IS NOT NULL THEN 'Patient'
        WHEN d.first_name IS NOT NULL THEN 'Doctor'
        ELSE 'Unknown'
    END AS role
FROM patients p
FULL JOIN doctors d
    ON p.patient_id = d.doctor_id
        AND p.first_name = d.first_name
```

**11) Show all allergies ordered by popularity. Remove NULL values from query.**

```SQL
SELECT allergies, COUNT(allergies)
FROM patients
WHERE allergies IS NOT NULL
GROUP BY allergies
ORDER BY COUNT(allergies) DESC;
```
___

**12) Show all patient's first_name, last_name, and birth_date who were born in the 1970s decade. Sort the list starting from the earliest birth_date.**

```SQL
SELECT first_name, last_name, birth_date
FROM patients
WHERE birth_date LIKE '197%'
ORDER BY birth_date;

-- OR --

SELECT first_name, last_name, birth_date
FROM patients
where YEAR(birth_date) >= 1970 AND YEAR(birth_date) <= 1979
order by birth_date;
```
___

**13) We want to display each patient's full name in a single column. Their last_name in all upper letters must appear first, then first_name in all lower case letters.Separate the last_name and first_name with a comma. Order the list by the first_name in decending order**

**EX: SMITH,jane**

```SQL
SELECT CONCAT(UPPER(last_name), ',', LOWER(first_name)) AS full_name
FROM patients
ORDER BY LOWER(first_name) DESC;

-- OR --

SELECT UPPER(last_name) + ',' + LOWER(first_name) AS full_name
FROM patients
ORDER BY LOWER(first_name) DESC;
```
___

**14) Show the province_id(s), sum of height; where the total sum of its patient's height is greater than or equal to 7,000.**

```SQL
SELECT p.province_id, SUM(p.height)
FROM patients p
GROUP BY p.province_id
HAVING SUM(p.height) >= 7000;
```

**15) Show the difference between the largest weight and smallest weight for patients with the last name 'Maroni'**

```SQL
SELECT MAX(weight) - MIN(weight) AS diff
FROM patients
WHERE last_name = 'Maroni'
GROUP BY last_name;
```
___

**16) Show all of the days of the month (1-31) and how many admission_dates occurred on that day. Sort by the day with most admissions to least admissions.**

```SQL
SELECT DAY(admission_date) day, COUNT(1) num_Of_days 
FROM admissions
GROUP BY DAY(admission_date)
ORDER BY COUNT(1) DESC;
```

___

**17) Show all columns for patient_id 542's most recent admission_date.**

```SQL
SELECT TOP 1 *
FROM admissions
WHERE patient_id = 542
ORDER BY admission_date DESC;
```
___

**18) Show patient_id, attending_doctor_id, and diagnosis for admissions that match one of the two criteria:**
**1. patient_id is an odd number and attending_doctor_id is either 1, 5, or 19.**
**2. attending_doctor_id contains a 2 and the length of patient_id is 3 characters.**

```SQL
SELECT patient_id, attending_doctor_id, diagnosis
FROM admissions
WHERE 
    (patient_id % 2 != 0 AND attending_doctor_id IN (1, 5, 19))
    OR 
    (CAST(attending_doctor_id AS VARCHAR(10)) LIKE '%2%' AND patient_id BETWEEN 100 AND 999);
```
___

**19) Show first_name, last_name, and the total number of admissions attended for each doctor.**

**Every admission has been attended by a doctor.**

```SQL
SELECT doctors.first_name, doctors.last_name, COUNT(admission_date)
FROM admissions
JOIN doctors
ON admissions.attending_doctor_id = doctors.doctor_id
GROUP BY doctors.first_name, doctors.last_name;
```
___

**20) For each doctor, display their id, full name, and the first and last admission date they attended.**

```SQL
SELECT doctor_id,
       CONCAT(first_name,' ', last_name) full_name,
       MIN(admission_date) first_admission,
       MAX(admission_date) last_admission
FROM doctors
JOIN admissions
ON attending_doctor_id = doctor_id
GROUP BY doctor_id;
```
___

**21) Display the total amount of patients for each province. Order by descending.**

```SQL
SELECT province_name, COUNT(1) count_of_patients
FROM patients
JOIN province_names
ON patients.province_id = province_names.province_id
GROUP BY province_names.province_name
order by count_of_patients desc;
```

**22) For every admission, display the patient's full name, their admission diagnosis, and their doctor's full name who diagnosed their problem.**

```SQL
SELECT 
  patients.first_name + ' ' + patients.last_name patient_name,
  diagnosis,
  doctors.first_name + ' ' + doctors.last_name Doc_name
FROM admissions
JOIN patients
  ON patients.patient_id = admissions.patient_id
JOIN doctors
  ON doctors.doctor_id = admissions.attending_doctor_id;
```
___

**23) display the first name, last name and number of duplicate patients based on their first name and last name.**

**Ex: A patient with an identical name can be considered a duplicate.**

```SQL
SELECT first_name, last_name, COUNT(1) num_of_duplicates
FROM patients
GROUP BY first_name, last_name
HAVING COUNT(1) > 1
```
___

**24) Display patient's full name, height in the units feet rounded to 1 decimal, weight in the unit pounds rounded to 0 decimals, birth_date, gender non abbreviated.**

**Convert CM to feet by dividing by 30.48.**

**Convert KG to pounds by multiplying by 2.205.**

```SQL
SELECT 
  CONCAT(first_name,' ', last_name) full_name,
  ROUND(height / 30.48, 1) height,
  ROUND(weight * 2.205, 0) weight,
  birth_date,
  CASE WHEN gender = 'M' THEN 'MALE' ELSE 'FEMALE' END gender
FROM patients
```
___

**25) Show patient_id, first_name, last_name from patients whose does not have any records in the admissions table. (Their patient_id does not exist in any admissions.patient_id rows.)**

```SQL
SELECT 
   patient_id,
   first_name,
   last_name
FROM patients
WHERE patient_id NOT IN (select patient_id FROM admissions)
```
___

**26) Display a single row with max_visits, min_visits, average_visits where the maximum, minimum and average number of admissions per day is calculated. Average is rounded to 2 decimal places.**

```SQL
WITH daily_counts AS (
  SELECT COUNT(*) AS cnt
  FROM admissions
  GROUP BY admission_date
)
SELECT 
   MAX(daily_counts.cnt) max_visits,
   MIN(daily_counts.cnt) min_visits,
   ROUND(AVG(1.0 * daily_counts.cnt), 2) avg_visits
FROM daily_counts; 

-- OR --

SELECT 
	MAX(number_of_visits) max_visits, 
	MIN(number_of_visits) min_visits, 
  ROUND(AVG(number_of_visits),2) average_visits 
FROM (
  SELECT admission_date, COUNT(*) number_of_visits
  FROM admissions 
  GROUP BY admission_date
```
