# Table of Contents

- [Table of Contents](#table-of-contents)
- [About](#about)
- [Difficulty: Easy](#difficulty-easy)
  - [Question 1](#question-1)
  - [Question 2](#question-2)
  - [Question 3](#question-3)
  - [Question 4](#question-4)
  - [Question 5](#question-5)
  - [Question 6](#question-6)
  - [Question 6](#question-6-1)
  - [Question 7](#question-7)
  - [Question 8](#question-8)
  - [Question 9](#question-9)
  - [Question 10](#question-10)
  - [Question 11](#question-11)
  - [Question 12](#question-12)
  - [Question 13](#question-13)
  - [Question 14](#question-14)
  - [Question 15](#question-15)
- [Difficulty: Medium](#difficulty-medium)
  - [Question 1](#question-1-1)
  - [Question 2](#question-2-1)
  - [Question 3](#question-3-1)
  - [Question 4](#question-4-1)
  - [Question 5](#question-5-1)
  - [Question 6](#question-6-2)
  - [Question 7](#question-7-1)
  - [Question 8](#question-8-1)
  - [Question 9](#question-9-1)
  - [Question 10](#question-10-1)
  - [Question 11](#question-11-1)
  - [Question 12](#question-12-1)
  - [Question 13](#question-13-1)
  - [Question 14](#question-14-1)
  - [Question 15](#question-15-1)
  - [Question 16](#question-16)
  - [Question 17](#question-17)
  - [Question 18](#question-18)
  - [Question 19](#question-19)
  - [Question 20](#question-20)
  - [Question 21](#question-21)
  - [Question 22](#question-22)
  - [Question 23](#question-23)
  - [Question 24](#question-24)
  - [Question 25](#question-25)
- [Difficulty: Hard](#difficulty-hard)
  - [Question 1](#question-1-2)
  - [Question 2](#question-2-2)
  - [Question 3](#question-3-2)
  - [Question 4](#question-4-2)
  - [Question 5](#question-5-2)
  - [Question 5](#question-5-3)
  - [Question 6](#question-6-3)
  - [Question 7](#question-7-2)
  - [Question 8](#question-8-2)
  - [Question 9](#question-9-2)
  - [Question 10](#question-10-2)

---

# About

Solutions for [sql-practice.com](www.sql-practice.com)

---

# Difficulty: Easy

## Question 1

> **Show first name, last name, and gender of patients whose gender is 'M'**

```sql
SELECT first_name, last_name, gender FROM patients WHERE gender="M"
```

---

## Question 2

> **Show first name and last name of patients who does not have allergies. (null)**

```sql
SELECT first_name, last_name FROM patients WHERE allergies IS NULL
```

---

## Question 3

> **Show first_name of patients that start with the letter 'C'**

**Solution 1**:

```sql
SELECT first_name FROM patients WHERE SUBSTRING(first_name, 1,1) IS "C"
```

**Solution 2**:

```sql
SELECT first_name FROM patients WHERE first_name LIKE 'C%'
```

---

## Question 4

> **Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)**

**Solution 1**:

```sql
SELECT first_name, last_name FROM patients WHERE weight BETWEEN 100 AND 120
```

**Solution 2**:

```sql
SELECT first_name, last_name FROM patients WHERE weight >=100 AND weight <=120
```

---

## Question 5

> **Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'**

**Solution 1**:

```sql
UPDATE patients
SET allergies = "NKA"
WHERE allergies IS NULL;
```

---

## Question 6

> **Show first name and last name concatenated into one column to show their full name.**

**Solution 1**:

```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM patients;
```

**Solution 2**:

```sql
SELECT first_name || ' ' || last_name FROM patients;
```

---

## Question 6

> **Show first name, last name, and the full province name of each patient. Example: 'Ontario' instead of 'ON'**

**Solution 1**:

```sql
SELECT first_name, last_name, province_name FROM patients
JOIN province_names ON province_names.province_id = patients.province_id;
```

**Solution 2**:

```sql
SELECT patients.first_name, patients.last_name, province_names.province_name FROM patients
INNER JOIN province_names ON patients.province_id=province_names.province_id
```

---

## Question 7

> **Show first name and last name concatenated into one column to show their full name.**

**Solution 1**:

```sql
SELECT COUNT(patient_id) from patients WHERE YEAR(birth_date) IS 2010
```

**Solution 2**:

```sql
SELECT COUNT(*) AS total_patients FROM patients WHERE YEAR(birth_date) = 2010;
```

**Solution 3**:

```sql
SELECT count(first_name) AS total_patients FROM patients WHERE birth_date >= '2010-01-01' AND birth_date <= '2010-12-31'
```

---

## Question 8

> **Show the first_name, last_name, and height of the patient with the greatest height.**

**Solution 1**:

```sql
SELECT first_name, last_name, MAX(height) as height from patients
```

**Solution 2**:

```sql
SELECT first_name, last_name, height
FROM patients
WHERE height = (
    SELECT max(height)
    FROM patients
  )
```

**Solution 3**:

```sql
SELECT first_name, last_name, height from patients order by height DESC LIMIT 1
```

---

## Question 9

> **Show all columns for patients who have one of the following patient_ids: 1,45,534,879,1000**

**Solution 1**:

```sql
SELECT * from patients WHERE patient_id IN (1, 45, 534, 879, 1000)
```

---

## Question 10

> **Show the total number of admissions**

**Solution 1**:

```sql
SELECT COUNT(patient_id) AS total_admissions from admissions
```

---

## Question 11

> **Show all the columns from admissions where the patient was admitted and discharged on the same day.**

```sql
SELECT * from admissions WHERE admission_date=discharge_date
```

---

## Question 12

> **Show the patient id and the total number of admissions for patient_id 579.**

**Solution 1**:

```sql
SELECT patient_id, COUNT(*) AS total_admissions
from admissions
WHERE patient_id = 579
```

---

## Question 13

> **Based on the cities that our patients live in, show unique cities that are in province_id 'NS'?**

**Solution 1**:

```sql
SELECT DISTINCT city FROM patients WHERE province_id = "NS"
```

---

## Question 14

> **Write a query to find the first_name, last name and birth date of patients who has height greater than 160 and weight greater than 70**

**Solution 1**:

```sql
SELECT first_name, last_name, birth_date
from patients
WHERE height > 160 AND weight > 70
```

---

## Question 15

> **Write a query to find list of patients first_name, last_name, and allergies from Hamilton where allergies are not null**

**Solution 1**:

```sql
SELECT first_name, last_name, allergies
from patients
WHERE city = "Hamilton" AND allergies IS NOT NULL
```

---

# Difficulty: Medium

## Question 1

> **Show unique birth years from patients and order them by ascending.**

**Solution 1**:

```sql
SELECT DISTINCT YEAR(birth_date) as birth_year from patients ORDER BY birth_date
```

**Solution 2**:

```sql
SELECT year(birth_date) FROM patients GROUP BY year(birth_date)
```

---

## Question 2

> **Show unique first names from the patients table which only occurs once in the list.**
>
> **For example, if two or more people are named 'John' in the first_name column then don't include their name in the output list. If only 1 person is named 'Leo' then include them in the output.**

**Solution 1**:

```sql
SELECT first_name FROM
	(SELECT first_name, count(first_name) as frequency from patients GROUP BY first_name)
    WHERE frequency = 1
```

**Solution 2**: The `HAVING` clause was added to SQL because the `WHERE` keyword cannot be used with aggregate functions.

```sql
SELECT first_name FROM patients GROUP BY first_name HAVING COUNT(first_name) = 1
```

---

## Question 3

> **Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.**

**Solution 1**:

```sql
SELECT patient_id, first_name from patients WHERE first_name LIKE 'S____%s'
```

**Solution 2**:

```sql
SELECT patient_id, first_name FROM patients
WHERE
  first_name like 's%'
  AND first_name like '%s'
  AND LEN(first_name) >= 6;
```

**Solution 3**: Using `LEN`

```sql
SELECT patient_id, first_name FROM patients
WHERE
  first_name LIKE 's%s'
  AND LEN(first_name) >= 6;
```

---

## Question 4

> **Show patient_id, first_name, last_name from patients whos diagnosis is 'Dementia'.**
>
> **Primary diagnosis is stored in the admissions table.**

**Solution 1**:

```sql
SELECT patients.patient_id, first_name, last_name from patients
JOIN admissions ON patients.patient_id=admissions.patient_id WHERE diagnosis="Dementia"
```

**Solution 2**: Using `LEN`

```sql
SELECT patient_id, first_name, last_name FROM patients
WHERE patient_id IN (
    SELECT patient_id
    FROM admissions
    WHERE diagnosis = 'Dementia'
  );
```

---

## Question 5

> **Display every patient's first_name. Order the list by the length of each name and then by alphbetically**

**Solution 1**:

```sql
SELECT first_name from patients ORDER BY LEN(first_name), first_name
```

---

## Question 6

> **Show the total amount of male patients and the total amount of female patients in the patients table. Display the two results in the same row.**

**Solution 1**: `SELECT`

```sql
SELECT
  (SELECT count(*) FROM patients WHERE gender='M') AS male_count,
  (SELECT count(*) FROM patients WHERE gender='F') AS female_count;
```

**Solution 2**: Using `SUM`

```sql
SELECT
  SUM(Gender = 'M') as male_count,
  SUM(Gender = 'F') AS female_count
FROM patients
```

**Solution 3**: Using `SUM` and `CASE`

```sql
SELECT
    SUM(CASE WHEN gender = 'M' THEN 1 ELSE 0 END) AS male_count,
    SUM(CASE WHEN gender = 'F' THEN 1 ELSE 0 END) AS female_count
FROM
    patients;
```

---

## Question 7

> **Show first and last name, allergies from patients which have allergies to either 'Penicillin' or 'Morphine'. Show results ordered ascending by allergies then by first_name then by last_name.**

**Solution 1**:

```sql
SELECT first_name, last_name, allergies from patients
WHERE allergies IN ("Penicillin", "Morphine")
ORDER BY allergies, first_name, last_name
```

**Solution 2**:

```sql
SELECT first_name, last_name, allergies
FROM patients
WHERE  allergies = 'Penicillin'  OR allergies = 'Morphine'
ORDER BY
  allergies ASC,
  first_name ASC,
  last_name ASC;
```

---

## Question 8

> **Show patient_id, diagnosis from admissions. Find patients admitted multiple times for the same diagnosis.**

**Solution 1**:

```sql
SELECT patient_id, diagnosis FROM admissions
GROUP BY patient_id, diagnosis
HAVING COUNT(diagnosis) > 1
```

---

## Question 9

> **Show the city and the total number of patients in the city. Order from most to least patients and then by city name ascending.**

**Solution 1**:

```sql
SELECT city, COUNT(patient_id) AS num_patients FROM patients
GROUP BY city
ORDER BY
  num_patients desc,
  city ASC
```

---

## Question 10

> **Show first name, last name and role of every person that is either patient or doctor. The roles are either "Patient" or "Doctor"**

**Solution 1**:

```sql
SELECT first_name, last_name, "Patient" as role FROM patients
UNION ALL
SELECT first_name, last_name, "Doctor" FROM doctors;
```

---

## Question 11

> **Show all allergies ordered by popularity. Remove NULL values from query.**

**Solution 1**:

```sql
SELECT allergies, COUNT(allergies) AS total_diagnosis from patients WHERE allergies IS NOT NULL
GROUP BY allergies
ORDER BY total_diagnosis DESC
```

**Solution 2**:

```sql
SELECT allergies, COUNT(allergies) AS total_diagnosis FROM patients
GROUP BY allergies
HAVING allergies IS NOT NULL
ORDER BY total_diagnosis DESC
```

---

## Question 12

> **Show all patient's first_name, last_name, and birth_date who were born in the 1970s decade. Sort the list starting from the earliest birth_date.**

**Solution 1**:

```sql
SELECT first_name, last_name, birth_date from patients WHERE YEAR(birth_date) BETWEEN 1970 AND 1979
ORDER BY birth_date
```

**Solution 2**:

```sql
SELECTfirst_name, last_name, birth_date FROM patients
WHERE birth_date >= '1970-01-01' AND birth_date < '1980-01-01'
ORDER BY birth_date
```

**Solution 3**:

```sql
SELECT first_name, last_name, birth_date
FROM patients
WHERE YEAR(birth_date) LIKE '197%'
ORDER BY birth_date ASC
```

---

## Question 13

> **We want to display each patient's full name in a single column. Their last_name in all upper letters must appear first, then first_name in all lower case letters. Separate the last_name and first_name with a comma. Order the list by the first_name in decending order**

> **EX: SMITH,jane**

**Solution 1**:

```sql
SELECT CONCAT(UPPER(last_name), ',', LOWER(first_name)) AS new_name_format FROM patients
ORDER BY first_name DESC;
```

**Solution 2**:

```sql
SELECT ( UPPER(last_name) || "," || LOWER(first_name) ) AS new_name_format from patients
ORDER BY first_name DESC
```

---

## Question 14

> **Show the province_id(s), sum of height; where the total sum of its patient's height is greater than or equal to 7,000.**

**Solution 1**:

```sql
SELECT province_id, SUM(height) AS sum_height from patients
GROUP BY province_id
HAVING sum_height >= 7000
```

---

## Question 15

> **Show the difference between the largest weight and smallest weight for patients with the last name 'Maroni'**

**Solution 1**:

```sql
SELECT MAX(weight) - MIN(weight) AS weight_delta from patients WHERE last_name="Maroni"
```

---

## Question 16

> **Show all of the days of the month (1-31) and how many admission_dates occurred on that day. Sort by the day with most admissions to least admissions.**

**Solution 1**:

```sql
SELECT DAY(admission_date) AS day_number, COUNT(*) as number_of_admissions from admissions
GROUP BY day_number
ORDER BY number_of_admissions DESC
```

---

## Question 17

> **Show all columns for patient_id 542's most recent admission_date.**

**Solution 1**:

```sql
SELECT * FROM admissions WHERE patient_id = 542
GROUP BY patient_id
HAVING admission_date = MAX(admission_date);
```

**Solution 2**:

```sql
SELECT *
FROM admissions
GROUP BY patient_id
HAVING
  patient_id = 542
  AND max(admission_date)
```

**Solution 3**:

```sql
SELECT * from admissions WHERE patient_id=542 ORDER BY admission_date DESC LIMIT 1
```

---

## Question 18

> **Show patient_id, attending_doctor_id, and diagnosis for admissions that match one of the two criteria:**
>
> 1. **patient_id is an odd number and attending_doctor_id is either 1, 5, or 19.**
> 2. **attending_doctor_id contains a 2 and the length of patient_id is 3 characters.**

**Solution 1**:

```sql
SELECT patient_id, attending_doctor_id, diagnosis from admissions
WHERE
	patient_id %2 = 1 AND attending_doctor_id IN (1, 5, 19) or attending_doctor_id LIKE '%2%' AND LEN(patient_id) = 3
```

---

## Question 19

> **Show first_name, last_name, and the total number of admissions attended for each doctor. Every admission has been attended by a doctor.**

**Solution 1**:

```sql
SELECT first_name, last_name, COUNT(attending_doctor_id) as admissions_total from admissions
JOIN doctors ON doctor_id = attending_doctor_id
GROUP BY attending_doctor_id
```

**Solution 2**:

```sql
SELECT first_name, last_name, COUNT(*)
FROM doctors p, admissions a
WHERE a.attending_doctor_id = p.doctor_id
GROUP BY p.doctor_id;
```

---

## Question 20

> **For each doctor, display their id, full name, and the first and last admission date they attended.**

**Solution 1**:

```sql
SELECT
	doctor_id,
	first_name || " " || last_name AS full_name,
    MIN(admission_date) AS first_admission_date,
    MAX(admission_date) AS last_admission_date
FROM admissions
JOIN doctors ON doctor_id = attending_doctor_id
GROUP BY doctor_id
```

---

## Question 21

> **Display the total amount of patients for each province. Order by descending.**

**Solution 1**:

```sql
SELECT province_name, COUNT(*) as patient_count FROM patients pa
JOIN province_names pr ON pr.province_id = pa.province_id
GROUP BY province_name
ORDER BY patient_count DESC
```

---

## Question 22

> **For every admission, display the patient's full name, their admission diagnosis, and their doctor's full name who diagnosed their problem.**

**Solution 1**:

```sql
SELECT
	p.first_name || " " || p.last_name AS patient_name,
    diagnosis,
    a.first_name || " " || a.last_name as doctor_name
FROM
  	(SELECT
   		patient_id, attending_doctor_id, diagnosis, first_name, last_name
   		from admissions
     	INNER JOIN doctors ON doctor_id = attending_doctor_id
    ) a
JOIN patients p ON p.patient_id = a.patient_id
```

**Solution 2**:

```sql
SELECT
  CONCAT(patients.first_name, ' ', patients.last_name) as patient_name,
  diagnosis,
  CONCAT(doctors.first_name,' ',doctors.last_name) as doctor_name
FROM patients
  JOIN admissions ON admissions.patient_id = patients.patient_id
  JOIN doctors ON doctors.doctor_id = admissions.attending_doctor_id;
```

---

## Question 23

> **Display the number of duplicate patients based on their first_name and last_name.**

**Solution 1**:

```sql
SELECT first_name, last_name, COUNT(*) as num_of_duplicates from patients
GROUP BY first_name, last_name
HAVING num_of_duplicates > 1
```

---

## Question 24

> **Display patient's full name, height in the units feet rounded to 1 decimal, weight in the unit pounds rounded to 0 decimals, birth_date, gender non abbreviated.**
>
> **Convert CM to feet by dividing by 30.48.** > **Convert KG to pounds by multiplying by 2.205.**

**Solution 1**:

```sql
SELECT
	first_name || " " || last_name AS patient_name,
    ROUND(height/30.48, 1),
    ROUND(weight*2.205),
    birth_date,
    (CASE WHEN gender = "M" THEN "MALE" ELSE "FEMALE" END) as gender_type
FROM patients
```

---

## Question 25

> **Show patient_id, first_name, last_name from patients whose does not have any records in the admissions table. (Their patient_id does not exist in any admissions.patient_id rows.)**

**Solution 1**: Using `LEFT JOIN` to match by `patient_id` then making sure `patient_id` in admissions is `NULL`

```sql
SELECT p.patient_id, first_name, last_name from patients p
LEFT JOIN admissions a ON a.patient_id = p.patient_id
WHERE a.patient_id IS NULL
```

**Solution 2**: Using `NOT IN` with a SELECT statement

```sql
SELECT patients.patient_id, first_name, last_name
FROM patients
WHERE patients.patient_id NOT IN (
    SELECT admissions.patient_id
    FROM admissions
  )
```

**Solution 3**: Using `NOT EXISTS`

```sql
SELECT p.patient_id, first_name, last_name from patients p
WHERE NOT EXISTS (
    SELECT patient_id
    FROM admissions a
    WHERE a.patient_id = p.patient_id
);
```

---

# Difficulty: Hard

## Question 1

> **Show all of the patients grouped into weight groups. Show the total amount of patients in each weight group.** > **Order the list by the weight group decending.**

> **For example, if they weight 100 to 109 they are placed in the 100 weight group, 110-119 = 110 weight group, etc.**

**Solution 1**:

```sql
SELECT
	COUNT(*) AS patients_in_group,
    FLOOR(weight / 10) * 10 AS weight_group
FROM patients
GROUP BY weight_group
ORDER BY weight_group DESC;
```

**Solution 2**: Using `TRUNCATE`

```sql
SELECT
  COUNT(*) AS patients_in_group,
  TRUNCATE(weight, -1) AS weight_group
FROM patients
GROUP BY weight_group
ORDER BY weight_group DESC;
```

**Solution 3**:

```sql
SELECT
  COUNT(patient_id) AS patients_in_group,
  weight - weight % 10 AS weight_group
FROM patients
GROUP BY weight_group
ORDER BY weight_group DESC;
```

---

## Question 2

> **Show patient_id, weight, height, `isObese` from the patients table. Display `isObese` as a boolean 0 or 1. Obese is defined as weight(kg)/(height(m)2) >= 30. `weight` is in units kg. `height` is in units cm.**

**Solution 1**:

```sql
SELECT
	patient_id,
    weight,
    height,
    CASE WHEN weight/POWER((height * 1.0 / 100), 2) >= 30 THEN 1 ELSE 0 END AS isObese
FROM patients
```

**Solution 2**: Use `CAST` to typecast integer to float

```sql
SELECT
  patient_id,
  weight,
  height,
  weight / power(CAST(height AS float) / 100, 2) >= 30 AS obese
FROM patients
```

---

## Question 3

> **Show patient_id, weight, height, `isObese` from the patients table. Display `isObese` as a boolean 0 or 1. Obese is defined as weight(kg)/(height(m)2) >= 30. `weight` is in units kg. `height` is in units cm.**

**Solution 1**:

```sql
SELECT
	p.patient_id,
    p.first_name AS patient_first_name,
    p.last_name AS patient_last_name,
    j.specialty AS attending_doctor_specialty
FROM patients p
JOIN (
      SELECT
        patient_id, diagnosis, attending_doctor_id,
        d.first_name AS doctor_first_name,
  		d.specialty
      FROM admissions
      JOIN doctors d ON attending_doctor_id = d.doctor_id
  	) AS j
On j.patient_id = p.patient_id
WHERE j.diagnosis = "Epilepsy" AND j.doctor_first_name = "Lisa"
```

**Solution 2**:

```sql
SELECT
  p.patient_id,
  p.first_name AS patient_first_name,
  p.last_name AS patient_last_name,
  ph.specialty AS attending_doctor_specialty
FROM patients p
  JOIN admissions a ON a.patient_id = p.patient_id
  JOIN doctors ph ON ph.doctor_id = a.attending_doctor_id
WHERE
  ph.first_name = 'Lisa' and
  a.diagnosis = 'Epilepsy'
```

**Solution 3**:

```sql
SELECT
  a.patient_id,
  a.first_name,
  a.last_name,
  b.specialty
FROM
  patients a,
  doctors b,
  admissions c
WHERE
  a.patient_id = c.patient_id
  AND c.attending_doctor_id = b.doctor_id
  AND c.diagnosis = 'Epilepsy'
  AND b.first_name = 'Lisa';
```

**Solution 4**: Using `WITH`.

```sql
with patient_table as (
    SELECT
      patients.patient_id,
      patients.first_name,
      patients.last_name,
      admissions.attending_doctor_id
    FROM patients
      JOIN admissions ON patients.patient_id = admissions.patient_id
    WHERE
      admissions.diagnosis = 'Epilepsy'
  )
SELECT
  patient_table.patient_id,
  patient_table.first_name,
  patient_table.last_name,
  doctors.specialty
FROM patient_table
  JOIN doctors ON patient_table.attending_doctor_id = doctors.doctor_id
WHERE doctors.first_name = 'Lisa';
```

---

## Question 4

> **All patients who have gone through admissions, can see their medical documents on our site. Those patients are given a temporary password after their first admission. Show the `patient_id` and `temp_password`.**
>
> **The password must be the following, in order:**
>
> 1. `patient_id`
> 2. the numerical length of patient's `last_name`
> 3. year of patient's `birth_date`

**Solution 1**:

```sql
SELECT DISTINCT
    p.patient_id,
	CONCAT(p.patient_id, LEN(p.last_name), YEAR(birth_date)) AS temp_password
FROM patients p
JOIN admissions a ON p.patient_id = a.patient_id
```

**Solution 2**:

```sql
select DISTINCT
  p.patient_id,
  p.patient_id || FLOOR(LEN(last_name)) || FLOOR(YEAR(birth_date)) as temp_password
FROM patients p
  JOIN admissions a ON p.patient_id = a.patient_id
```

**Solution 3**: Using `SELECT` and `GROUP BY`

```sql
SELECT
  p.patient_id,
  a.patient_id || FLOOR(LEN(pa.last_name)) || FLOOR(YEAR(p.birth_date)) as temp_password
FROM patients p
  JOIN admissions a ON p.patient_id = a.patient_id
GROUP BY p.patient_id;
```

---

## Question 5

> **Each admission costs `$50` for patients without insurance, and `$10` for patients with insurance. All patients with an even `patient_id` have insurance.**
>
> **Give each patient a 'Yes' if they have insurance, and a 'No' if they don't have insurance. Add up the `admission_total` cost for each `has_insurance` group.**

**Solution 1**:

```sql
SELECT
	CASE WHEN patient_id % 2 = 0 THEN "Yes" ELSE "No" END AS has_insurance,
    SUM(CASE WHEN patient_id % 2 = 0 THEN 10 ELSE 50 END) AS cost_after_insurance
FROM admissions
GROUP BY has_insurance
```

---

## Question 5

> **Show the provinces that has more patients identified as 'M' than 'F'. Must only show full province_name**

**Solution 1**:

```sql
SELECT province_name FROM (
  SELECT
  	province_name,
  	SUM(gender = "M") AS male_count,
    SUM(gender = "F") AS female_count
  FROM patients pa
  JOIN province_names pr ON pr.province_id = pa.province_id
  GROUP BY province_name
  HAVING male_count > female_count
)
```

**Solution 2**: Using `HAVING`, `COUNT` and `CASE` to determine which rows to pick.

```sql
SELECT pr.province_name
FROM patients AS pa
  JOIN province_names AS pr ON pa.province_id = pr.province_id
GROUP BY pr.province_name
HAVING
  COUNT( CASE WHEN gender = 'M' THEN 1 END) > COUNT( CASE WHEN gender = 'F' THEN 1 END);
```

**Solution 3**: Using `HAVING` with `SUM`

```sql
SELECT pr.province_name
FROM patients AS pa
  JOIN province_names AS pr ON pa.province_id = pr.province_id
GROUP BY pr.province_name
HAVING
  SUM(gender = 'M') > SUM(gender = 'F');
```

**Solution 5**: Selecting `province_names` first (Long way)

```sql
SELECT
	province_name
FROM province_names pr
	JOIN (
      (SELECT
      	patient_id,
      	province_id,
      	COUNT(gender) AS male_count
      from patients
      WHERE gender = "M"
      GROUP BY province_id) m

      JOIN (
        SELECT patient_id, province_id, COUNT(gender) AS female_count
        from patients
        WHERE gender = "F"
        GROUP BY province_id
      ) f
      ON m.province_id = f.province_id
      ) j
  	ON pr.province_id = j.province_id
    WHERE male_count > female_count
```

---

## Question 6

> **We are looking for a specific patient. Pull all columns for the patient who matches the following criteria:**
>
> - **First_name contains an 'r' after the first two letters.**
> - **Identifies their gender as 'F'**
> - **Born in February, May, or December**
> - **Their weight would be between 60kg and 80kg**
> - **Their patient_id is an odd number**
> - **They are from the city 'Kingston'**

**Solution 1**:

```sql
SELECT * FROM patients
WHERE
	first_name LIKE '__r%' AND
    gender = "F" AND
    MONTH(birth_date) IN (2, 5, 12) AND
    weight BETWEEN 60 AND 80 AND
    patient_id % 2 = 1 AND
    city = "Kingston"
```

---

## Question 7

> **Show the percent of patients that have 'M' as their gender. Round the answer to the nearest hundreth number and in percent form.**

**Solution 1**:

```sql
SELECT DISTINCT
	CONCAT(ROUND(CAST(SUM(gender = "M") as float) / COUNT(*) * 100, 2), "%") AS percent_of_male_patients
FROM patients
```

---

## Question 8

> **For each day display the total amount of admissions on that day. Display the amount changed from the previous date.
> ** > **Solution 1**: Using `LAG` and `OVER`. View https://www.scaler.com/topics/lag-function-in-sql/

```sql
SELECT
	admission_date,
    COUNT(patient_id) AS admission_day,
    COUNT(admission_date) - LAG(COUNT(admission_date)) OVER(ORDER BY admission_date) AS admission_count_change
FROM admissions
GROUP BY admission_date
```

**Solution 2**: Using `WITH` to create a temporary table with `LAG` and `OVER`.

```sql
WITH admission_counts_table AS (
  SELECT admission_date, COUNT(patient_id) AS admission_count
  FROM admissions
  GROUP BY admission_date
  ORDER BY admission_date DESC
)
SELECT
  admission_date,
  admission_count,
  admission_count - LAG(admission_count) OVER(ORDER BY admission_date) AS admission_count_change
FROM admission_counts_table
```

---

## Question 9

> **Sort the province names in ascending order in such a way that the province 'Ontario' is always on top.**

**Solution 1**: Using `UNION ALL`

```sql
SELECT province_name FROM province_names pr WHERE province_name = "Ontario"
UNION ALL
SELECT province_name FROM province_names WHERE province_name IS NOT "Ontario"
```

**Solution 2a**: Using `WHERE`, `CASE`

```sql
select province_name
from province_names
ORDER BY
  (CASE WHEN province_name = 'Ontario' THEN 0 ELSE 1 END),
  province_name
```

**Solution 2b**: Using `WHERE`, `CASE`

```sql
SELECT province_name
FROM province_names
ORDER BY
  CASE
    WHEN province_name = 'Ontario' THEN 1
    ELSE province_name
  END
```

**Solution 3**: Using `ORDER BY`, `NOT`

```sql
SELECT province_name
FROM province_names
ORDER BY
  (NOT province_name = 'Ontario'),
  province_name
```

**Solution 4**: Using ORDER BY, DESC

```sql
SELECT province_name
FROM province_names
ORDER BY
  province_name = 'Ontario' DESC,
  province_name
```

---

## Question 10

> **We need a breakdown for the total amount of admissions each doctor has started each year. Show the doctor_id, doctor_full_name, specialty, year, total_admissions for that year.**

**Solution 1**:

```sql
SELECT
	doctor_id,
    first_name || " " || last_name AS doctor_name,
    specialty,
    selected_year,
    total_admissions
FROM doctors
JOIN
  (SELECT
          YEAR(admission_date) AS selected_year,
          attending_doctor_id,
          COUNT(*) AS total_admissions
  FROM admissions
  GROUP BY selected_year, attending_doctor_id)
ON attending_doctor_id = doctor_id
ORDER BY doctor_id
```

**Solution 2**:

```sql
SELECT
  d.doctor_id as doctor_id,
  CONCAT(d.first_name,' ', d.last_name) as doctor_name,
  d.specialty,
  YEAR(a.admission_date) as selected_year,
  COUNT(*) as total_admissions
FROM doctors as d
  LEFT JOIN admissions as a ON d.doctor_id = a.attending_doctor_id
GROUP BY
  doctor_name,
  selected_year
ORDER BY doctor_id, selected_year
```
