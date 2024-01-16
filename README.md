# tables
Students Table:
course table


## Write a query to retrieve the names of students who are enrolled in the 'Math' course.

## Write a query to find the names of students who are not enrolled in any course.

## Write a query to retrieve the names of students who are enrolled in both 'Math' and 'English' courses.

## Write a query to find the names of students who are not enrolled in any course using the NOT IN clause.

## Write a query to retrieve the names of students who are enrolled in at least one course using the EXISTS clause.

## Write a query to find the names of students who are not enrolled in any course using the NOT EXISTS clause.

```
-- 1. Retrieve the names of students who are enrolled in the 'Math' course:
SELECT student_name
FROM Students
WHERE student_id IN (SELECT student_id FROM course WHERE course_name = 'Math');

-- 2. Find the names of students who are not enrolled in any course:
SELECT student_name
FROM Students
WHERE student_id NOT IN (SELECT student_id FROM course);

-- 3. Retrieve the names of students who are enrolled in both 'Math' and 'English' courses:
SELECT student_name
FROM Students
WHERE student_id IN (
    SELECT student_id
    FROM course
    WHERE course_name IN ('Math', 'English')
    GROUP BY student_id
    HAVING COUNT(DISTINCT course_name) = 2
);

-- 4. Find the names of students who are not enrolled in any course using the NOT IN clause:
SELECT student_name
FROM Students
WHERE student_id NOT IN (SELECT student_id FROM course);

-- 5. Retrieve the names of students who are enrolled in at least one course using the EXISTS clause:
SELECT student_name
FROM Students
WHERE EXISTS (SELECT 1 FROM course WHERE Students.student_id = course.student_id);

-- 6. Find the names of students who are not enrolled in any course using the NOT EXISTS clause:
SELECT student_name
FROM Students
WHERE NOT EXISTS (SELECT 1 FROM course WHERE Students.student_id = course.student_id);

```
