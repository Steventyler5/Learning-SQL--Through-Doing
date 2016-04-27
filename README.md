# Learning-SQL--Through-Doing

Answers to the exercise found at <br> https://github.com/nashville-software-school/csharp-dotnet-milestones/blob/master/3-database-driven-applications/exercises/database/DBS_SQL_LEARNING-THRU-DOING.md


**1. Provide a query showing Customers (just their full names, customer ID and country) who are not in the US.**
SELECT
c.FirstName || " " || c.LastName AS FullName,
c.CustomerId,
c.Country
FROM Customer c
WHERE c.Country != 'USA'
