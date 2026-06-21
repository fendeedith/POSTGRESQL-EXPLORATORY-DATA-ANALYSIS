# EXPLORATORY-DATA-ANALYSIS-IN-POSTGRESQL
This analysis demonstrates strong SQL proficiency, data exploration techniques, and the ability to derive meaningful business insights from structured datasets.

## Objective
The objective was to transform raw gym-related data into actionable insights by answering 14 business-focused analytical questions covering member behavior, facility utilization, revenue trends, and operational performance.

## Data Sources
Gym dataset from the SQL certification I did a while ago.

## Tools
PostgreSQL and PgAdmin

## Questions answered, queries and results
This section shows the questions that were answered, the queries ran and the results of these queries.

1.	How can you retrieve all the information from the cd.facilities table?
SELECT * FROM cd.facilities
<img width="538" height="179" alt="Question 1" src="https://github.com/user-attachments/assets/5fd0ea9b-033a-496a-a45d-baddddae3aec" />


2.	You want to print out a list of all of the facilities and their cost to members. How would you retrieve a list of only facility names and costs?
SELECT name, membercost FROM cd.facilities
<img width="270" height="271" alt="Question 2" src="https://github.com/user-attachments/assets/002946a5-5342-40ac-9f66-63590fe785b5" />

3.	How can you produce a list of facilities that charge a fee to members?
SELECT name, membercost FROM cd.facilities
WHERE membercost > 0
<img width="265" height="198" alt="Question 3" src="https://github.com/user-attachments/assets/639db50a-b42d-4770-acef-41278e78a681" />

4.	How can you produce a list of facilities that charge a fee to members, and that fee is less than 1/50th of the monthly maintenance cost? Return the facid, facility name, member cost, and monthly maintenance of the facilities in question.
SELECT facid,name,membercost,monthlymaintenance 
FROM cd.facilities
WHERE membercost > 0 AND membercost < ((1/50.0)*monthlymaintenance)
<img width="423" height="142" alt="Question 4" src="https://github.com/user-attachments/assets/0b3efb33-d075-4f08-a170-6c46e46c00eb" />

5.	How can you produce a list of all facilities with the word 'Tennis' in their name?
SELECT * FROM cd.facilities
WHERE name LIKE '%Tennis%'
<img width="543" height="155" alt="Question 5" src="https://github.com/user-attachments/assets/5792ee30-5ea6-44b8-bc51-c6fbb17d9e7d" />

6.	How can you retrieve the details of facilities with ID 1 and 5? Try to do it without using the OR operator.
(With the OR operator)
SELECT * FROM cd.facilities
WHERE facid = 1 OR facid =5
(Without the OR operator)
SELECT * FROM cd.facilities
WHERE facid IN (1,5)
<img width="538" height="140" alt="Question 6" src="https://github.com/user-attachments/assets/095efa8a-44f6-40ff-8f47-6e37efb51069" />

7.	How can you produce a list of members who joined after the start of September 2012? Return the memid, surname, firstname, and joindate of the members in question.
SELECT memid, surname, firstname, joindate 
FROM cd.members
WHERE joindate >= '2012-09-01'
<img width="486" height="281" alt="Question 7" src="https://github.com/user-attachments/assets/076de3ed-41af-452d-8e8a-908b169f898c" />

8.	How can you produce an ordered list of the first 10 surnames in the members table? The list must not contain duplicates.
SELECT DISTINCT surname FROM cd.members
ORDER BY surname
LIMIT 10
<img width="266" height="280" alt="Question 8" src="https://github.com/user-attachments/assets/a2bc0737-b1bf-464e-83c6-861b53988160" />

9.	You'd like to get the signup date of your last member. How can you retrieve this information?
SELECT MAX(joindate) 
FROM cd.members
<img width="272" height="121" alt="Question 9" src="https://github.com/user-attachments/assets/a5b66403-5aff-408f-8113-5d8db55d7e49" />

10.	Produce a count of the number of facilities that have a cost to guests of 10 or more.
SELECT COUNT (*)
FROM cd.facilities
WHERE guestcost >= 10
<img width="256" height="125" alt="Question 10" src="https://github.com/user-attachments/assets/f93af350-71ff-417f-841f-ee3cbf138801" />

11.	Produce a list of the total number of slots booked per facility in the month of September 2012. Produce an output table consisting of facility id and slots, sorted by the number of slots.
SELECT facid, SUM(slots) AS total_slots
FROM cd.bookings
WHERE starttime >= '2012-09-01' AND starttime <= '2012-10-01'
GROUP BY facid ORDER BY SUM(slots)
<img width="249" height="267" alt="Question 11" src="https://github.com/user-attachments/assets/78269cef-b95a-4a6f-bb11-c3fd54055c75" />

12.	Produce a list of facilities with more than 1000 slots booked. Produce an output table consisting of facility id and total slots, sorted by facility id.
SELECT facid, SUM(slots) AS total_slots
FROM cd.bookings
GROUP BY facid 
HAVING SUM(slots)>1000
ORDER BY facid
<img width="243" height="192" alt="Question 12" src="https://github.com/user-attachments/assets/1883403a-e25d-4bee-aa8b-28f37da14254" />

13.	How can you produce a list of the start times for bookings for tennis courts, for the date '2012-09-21'? Return a list of start time and facility name pairings, ordered by the time.
SELECT cd.bookings.starttime, cd.facilities.name
FROM cd.facilities
INNER JOIN cd.bookings 
ON cd.facilities.facid = cd.bookings.facid
WHERE cd.facilities.facid IN (0,1)
AND cd.bookings.starttime >= '2012-09-21'
AND cd.bookings.starttime <'2012-09-22'
ORDER BY cd.bookings.starttime
<img width="443" height="324" alt="Question 13" src="https://github.com/user-attachments/assets/7c9c0997-9b6c-4dd9-8c65-26e2cb1cd658" />

14.	How can you produce a list of the start times for bookings by members named 'David Farrell'?
SELECT cd.bookings.starttime
FROM cd.bookings
INNER JOIN cd.members
ON cd.members.memid = cd.bookings.memid
WHERE cd.members.firstname = 'David'
AND cd.members.surname = 'Farrell'
<img width="496" height="248" alt="Question 14" src="https://github.com/user-attachments/assets/c95122dd-69c4-4eb0-8d5b-d863679803be" />
