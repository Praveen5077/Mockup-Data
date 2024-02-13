# Mockup-Data
1)
Top 25 schools (.edu domains):

SELECT SUBSTR(email, INSTR(email, '@') + 1) AS domain, COUNT(*) AS count
FROM users
WHERE email LIKE '%.edu'
GROUP BY domain
ORDER BY count DESC
LIMIT 25;

Number of .edu learners located in New York:

SELECT COUNT(*) AS count
FROM users
WHERE email LIKE '%.edu' AND location = 'New York';

2)
Count of Codecademy learners using the mobile app:

SELECT COUNT(*) AS count
FROM users
WHERE mobile_app = 'mobile-user';

3)
Query for sign up counts for each hour:

SELECT strftime('%H', sign_up_at) AS hour_of_day, COUNT(*) AS sign_up_count
FROM users
GROUP BY hour_of_day
ORDER BY hour_of_day;

4)
Do different schools (.edu domains) prefer different courses?

SELECT s.school, c.course, COUNT(*) AS enrollment_count
FROM enrollments e
JOIN courses c ON e.course_id = c.course_id
JOIN schools s ON e.school_id = s.school_id
WHERE s.school LIKE '%.edu'
GROUP BY s.school, c.course
ORDER BY s.school, enrollment_count DESC;

What courses are the New Yorkers students taking?

SELECT c.course, COUNT(*) AS enrollment_count
FROM enrollments e
JOIN courses c ON e.course_id = c.course_id
JOIN users u ON e.user_id = u.user_id
WHERE u.location = 'New York'
GROUP BY c.course
ORDER BY enrollment_count DESC;

What courses are the Chicago students taking?

SELECT c.course, COUNT(*) AS enrollment_count
FROM enrollments e
JOIN courses c ON e.course_id = c.course_id
JOIN users u ON e.user_id = u.user_id
WHERE u.location = 'Chicago'
GROUP BY c.course
ORDER BY enrollment_count DESC;
