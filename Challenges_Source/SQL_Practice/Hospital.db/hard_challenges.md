# Hard challenges


**1) Show all of the patients grouped into weight groups., Show the total amount of patients in each weight group., Order the list by the weight group decending.**

**For example, if they weight 100 to 109 they are placed in the 100 weight group, 110-119 = 110 weight group, etc.**

```SQL
WITH grouped_weighted AS (
    SELECT
        weight,
        (weight / 10) * 10 AS low_range,
        (weight / 10) * 10 + 9 AS high_range
    FROM
        patients
)
SELECT 
    COUNT(*) AS Count_in_Group,
    low_range AS groups
FROM
    grouped_weighted
WHERE
    weight BETWEEN low_range AND high_range
GROUP BY
    low_range
ORDER BY
    low_range DESC;


-- OR --


SELECT 
    COUNT(*) AS Count_in_Group,
    (weight / 10) * 10 AS groups
FROM
    patients
GROUP BY
    (weight / 10) * 10
ORDER BY
    groups DESC;
```
___

**2) Show patient_id, weight, height, isObese from the patients table. ,Display isObese as a boolean 0 or 1.**

**Obese is defined as weight(kg)/(height(m)2) >= 30.**

**weight is in units kg.**

**height is in units cm.**

```SQL
SELECT 
   patient_id,
   weight,
   height,
   CASE 
     WHEN weight / POWER(height / 100.0, 2)  >= 30 THEN 1 ELSE 0
   END isObese
FROM 
   patients
```
___

**3) Show patient_id, first_name, last_name, and attending doctor's specialty., Show only the patients who has a diagnosis as 'Epilepsy' and the doctor's first name is 'Lisa'**

**Check patients, admissions, and doctors tables for required information.**

```SQL
SELECT 
    patients.patient_id,
    patients.first_name,
    patients.last_name,
    doctors.specialty
FROM patients
JOIN admissions
    ON admissions.patient_id = patients.patient_id
JOIN doctors
    ON admissions.attending_doctor_id = doctors.doctor_id
WHERE diagnosis = 'Epilepsy'
    AND doctors.first_name = 'Lisa';
```
___

**4) All patients who have gone through admissions, can see their medical documents on our site. Those patients are given a temporary password after their first admission. Show the patient_id and temp_password.**

**The password must be the following, in order:**

**1. patient_id**

**2. the numerical length of patient's last_name**

**3. year of patient's birth_date**

```SQL
SELECT DISTINCT
    admissions.patient_id,
    CONCAT(admissions.patient_id,
        LEN(last_name),
        YEAR(birth_date)
    ) password
FROM
   patients
JOIN
   admissions
ON 
  admissions.patient_id = patients.patient_id;
```
___

**5) Each admission costs $50 for patients without insurance, and $10 for patients with insurance. All patients with an even patient_id have insurance.**

**Give each patient a 'Yes' if they have insurance, and a 'No' if they don't have insurance. Add up the admission_total cost for each has_insurance group.**

```SQL
WITH insurance_table AS (
    SELECT
        CASE
            WHEN patient_id % 2 = 0 THEN 'YES' ELSE 'NO'
        END insurance,
        CASE
            WHEN patient_id % 2 = 0 THEN 10 ELSE 50
        END  cost
    FROM
      admissions
)
SELECT
   insurance,
   SUM(cost) total
FROM
   insurance_table
GROUP BY
   insurance;

-- OR --

SELECT
    has_insurance,
    CASE
        WHEN has_insurance = 'Yes' THEN COUNT(has_insurance) * 10 ELSE count(has_insurance) * 50
    END cost_after_insurance
FROM (
    SELECT
        CASE
            WHEN patient_id % 2 = 0 THEN 'Yes' ELSE 'No'
        END AS has_insurance
    FROM
       admissions
  )
GROUP BY
    has_insurance
```

**6) Show the provinces that has more patients identified as 'M' than 'F'. Must only show full province_name**

```SQL
SELECT
   province_name
FROM
   province_names
JOIN 
   patients
ON
  province_names.province_id = patients.province_id
GROUP BY 
   province_name
HAVING
  SUM(gender = 'M') > SUM(gender = 'F');
```
___

**7) We are looking for a specific patient. Pull all columns for the patient who matches the following criteria:**

**- First_name contains an 'r' after the first two letters.**

**- Identifies their gender as 'F'**

**- Born in February, May, or December**

**- Their weight would be between 60kg and 80kg**

**- Their patient_id is an odd number**

**- They are from the city 'Kingston'**

```SQL
SELECT *
FROM
   patients
WHERE
   first_name LIKE '__r%'
AND
   gender = 'F'
AND
   MONTH(birth_date) IN (2, 5, 12)
AND
   weight BETWEEN 60 AND 80
AND
   patient_id % 2 = 1
AND
   city = 'Kingston';
```
___

**8) Show the percent of patients that have 'M' as their gender. Round the answer to the nearest hundreth number and in percent form.**

```SQL
SELECT
    CONCAT(
        ROUND(100.0 * COUNT(CASE WHEN gender = 'M' THEN 1 END) / COUNT(*), 2 ), '%'
    ) AS percent_male
FROM
    patients;

-- OR --

SELECT
   ROUND(100 * AVG(gender = 'M'), 2) + '%' AS percent_of_male_patients
FROM
   patients;
```
___

**9) For each day display the total amount of admissions on that day. Display the amount changed from the previous date**

```SQL
WITH daily_counts AS (
    SELECT
        admission_date,
        COUNT(*) AS total
    FROM admissions
    GROUP BY admission_date
)
SELECT
    admission_date,
    total,
    total - LAG(total) OVER (ORDER BY admission_date) AS diff_from_previous_day
FROM daily_counts;
```
___

**10) Sort the province names in ascending order in such a way that the province 'Ontario' is always on top.**

```SQL
SELECT province_name
FROM province_names
ORDER BY
    CASE WHEN province_name = 'Ontario' THEN 'A' ELSE 'Z' END,
    province_name;
```

**11) We need a breakdown for the total amount of admissions each doctor has started each year. Show the doctor_id, doctor_full_name, specialty, year, total_admissions for that year.**

```SQL
SELECT
    doctor_id,
    CONCAT(first_name, ' ', last_name) name,
    specialty,
    addmission_year,
    total
FROM 
    doctors
JOIN (
    SELECT 
        addmission_year,
        YEAR(admission_date) addmission_year, COUNT(patient_id) total
    FROM 
        admissions
    GROUP BY
        YEAR(admission_date), attending_doctor_id
    )
ON
    doctor_id = attending_doctor_id;    
```