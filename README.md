# Learning-SQL--Through-Doing

Answers to the exercise found at <br> https://github.com/nashville-software-school/csharp-dotnet-milestones/blob/master/3-database-driven-applications/exercises/database/DBS_SQL_LEARNING-THRU-DOING.md


**1. Provide a query showing Customers (just their full names, customer ID and country) who are not in the US.**
```SQL
SELECT
c.FirstName || " " || c.LastName AS FullName,
c.CustomerId,
c.Country
FROM Customer c
WHERE c.Country != 'USA'
```

**2. Provide a query only showing the Customers from Brazil.**
```SQL
SELECT
c.FirstName || " " || c.LastName AS FullName,
c.CustomerId,
c.Country
FROM Customer c
WHERE c.Country = 'Brazil'
```

**3. Provide a query showing the Invoices of customers who are from Brazil. The resultant table should show the customer's full name, Invoice ID, Date of the invoice and billing country.**
```SQL
SELECT
c.FirstName || " " || c.LastName AS FullName,
i.InvoiceId,
i.BillingCountry,
i.InvoiceDate
FROM Customer c
INNER JOIN Invoice i 
ON c.CustomerId = i.CustomerId
WHERE c.Country = 'Brazil'
```

**4. Provide a query showing only the Employees who are Sales Agents.**
```SQL
SELECT 
* 
FROM Employee e
WHERE e.Title = "Sales Support Agent"
```

**5. Provide a query showing a unique list of billing countries from the Invoice table.**
```SQL
SELECT DISTINCT
i.BillingCountry
FROM Invoice i

```

**6. Provide a query that shows the invoices associated with each sales agent. The resultant table should include the Sales Agent's full name.**
```SQL
SELECT
e.FirstName || " " || e.LastName AS SalesAgent,
i.*
FROM Employee e
INNER JOIN Customer c ON e.EmployeeID = c.SupportRepId
INNER JOIN Invoice i ON c.CustomerId = i.CustomerId
WHERE e.Title = "Sales Support Agent"
ORDER BY SalesAgent
```

**7. Provide a query that shows the Invoice Total, Customer name, Country and Sale Agent name for all invoices and customers.**
```SQL
SELECT
c.FirstName || " " || c.LastName AS Customer,
i.Total AS InvoiceTotal,
i.BillingCountry,
e.FirstName || " " || e.LastName AS SalesAgent
FROM Employee e
INNER JOIN Customer c 
  ON e.EmployeeID = c.SupportRepId
INNER JOIN Invoice i 
  ON c.CustomerId = i.CustomerId
WHERE e.Title = "Sales Support Agent"
ORDER BY Customer
```

**8. How many Invoices were there in 2009 and 2011? What are the respective total sales for each of those years?(include both the answers and the queries used to find the answers)**<br>
Number of Invoices in 2009: 83
```SQL
SELECT COUNT 
(*) 
FROM Invoice i
WHERE i.InvoiceDate LIKE "2009%"
```

Number of Invoices in 2011: 83
```SQL
SELECT COUNT 
(*) 
FROM Invoice i
WHERE i.InvoiceDate LIKE "2011%"
```

Invoice totals for 2009: 449.46
```SQL
SELECT 
sum(Total)
FROM Invoice i
WHERE i.InvoiceDate LIKE "2009%"
```

Invoice totals for 2011: 469.58
```SQL
SELECT 
sum(Total)
FROM Invoice i
WHERE i.InvoiceDate LIKE "2011%"
```

**9. Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for Invoice ID 37.**
```SQL
SELECT COUNT
(InvoiceLineId)
FROM InvoiceLine
WHERE InvoiceId = 37
```

**10. Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for each Invoice. HINT: GROUP BY**
```SQL
SELECT
InvoiceId, 
COUNT(InvoiceLineId)  AS InvoiceCount
FROM InvoiceLine
GROUP BY InvoiceId
```

**11. Provide a query that includes the track name with each invoice line item.**
```SQL
SELECT
il.InvoiceLineId,
t.Name AS TrackName,
il.InvoiceId,
il.TrackId,
il.UnitPrice,
il.Quantity
FROM InvoiceLine il
INNER JOIN Track t ON il.TrackId = t.TrackId

```

**12. Provide a query that includes the purchased track name AND artist name with each invoice line item.**
```SQL
SELECT
il.InvoiceLineId,
t.Name AS TrackName,
a.Name AS ArtistName,
il.InvoiceId,
il.TrackId,
il.UnitPrice,
il.Quantity
FROM InvoiceLine il
INNER JOIN Track t ON il.TrackId = t.TrackId
INNER JOIN Album al ON t.Albumid = al.AlbumId
INNER JOIN Artist a ON al.ArtistId = a.ArtistId

```

**13. Provide a query that shows the # of invoices per country. HINT: GROUP BY**
```SQL
SELECT
BillingCountry AS Country,
COUNT(InvoiceId)  AS InvoiceCount
FROM Invoice
GROUP BY Country
```

**14. Provide a query that shows the total number of tracks in each playlist. The Playlist name should be include on the resulant table.**
```SQL
SELECT
p.Name AS PlaylistName,
p.PlaylistId,
COUNT(pt.TrackId)
FROM Playlist p
INNER JOIN PlaylistTrack pt ON p.PlaylistId = pt.Playlistid
GROUP BY p.PlaylistId
```

**15. Provide a query that shows all the Tracks, but displays no IDs. The resultant table should include the Album name, Media type and Genre.**
```SQL
SELECT
t.Name AS TrackName,
a.Title AS AlbumTitle,
m.Name AS MediaType,
g.Name AS Genre
FROM Track t
INNER JOIN Album a ON t.AlbumId = a.AlbumId
INNER JOIN MediaType m ON t.MediaTypeId = m.MediaTypeId
INNER JOIN Genre g ON t.GenreId = g.GenreId
```

**16. Provide a query that shows all Invoices but includes the # of invoice line items.**
```SQL
SELECT
i.*,
COUNT(il.InvoiceLineId) AS Invoices
FROM Invoice i
INNER JOIN InvoiceLine il ON i.InvoiceId = il.InvoiceId
GROUP BY i.InvoiceId
```

**17. Provide a query that shows total sales made by each sales agent.**
```SQL
SELECT
e.FirstName || " " || e.LastName AS SalesAgent,
SUM(i.Total) AS TotalSales
FROM Employee e
INNER JOIN Customer c ON e.EmployeeID = c.SupportRepId
INNER JOIN Invoice i ON c.CustomerId = i.CustomerId
WHERE e.Title = "Sales Support Agent"
GROUP BY SalesAgent
```

**18. Which sales agent made the most in sales in 2009? HINT: MAX**<br>
Highest grossing Sales Agent in 2009: Steve Johnson
```SQL
SELECT
SalesAgent, 
Max(TotalSales)
FROM
(SELECT
e.FirstName || " " || e.LastName AS SalesAgent,
SUM(i.Total) AS TotalSales
FROM Employee e
INNER JOIN Customer c ON e.EmployeeID = c.SupportRepId
INNER JOIN Invoice i ON c.CustomerId = i.CustomerId
WHERE e.Title = "Sales Support Agent" AND i.InvoiceDate LIKE "2009%"
GROUP BY SalesAgent)
```

**19. Which sales agent made the most in sales over all?**<br>
Highest grossing Sales Agent: Jane Peacock
```SQL
SELECT
SalesAgent, 
Max(TotalSales)
FROM
(SELECT
e.FirstName || " " || e.LastName AS SalesAgent,
SUM(i.Total) AS TotalSales
FROM Employee e
INNER JOIN Customer c ON e.EmployeeID = c.SupportRepId
INNER JOIN Invoice i ON c.CustomerId = i.CustomerId
WHERE e.Title = "Sales Support Agent"
GROUP BY SalesAgent)
```

**20. Provide a query that shows the # of customers assigned to each sales agent.**
```SQL
SELECT
e.FirstName || " " || e.LastName AS SalesAgent,
COUNT(c.CustomerId) AS TotalCustomers
FROM Employee e
INNER JOIN Customer c ON e.EmployeeID = c.SupportRepId
WHERE e.Title = "Sales Support Agent" 
GROUP BY c.SupportRepId
```

**21. Provide a query that shows the total sales per country. Which country's customers spent the most?**<br>
Sales Total by Country
```SQL
SELECT
i.BillingCountry AS Country,
SUM(i.Total) AS TotalSales
FROM Invoice i
GROUP BY Country
```

Country with highest sales total: USA
```SQL
SELECT
Country, 
Max(TotalSales)
FROM
(SELECT
i.BillingCountry AS Country,
SUM(i.Total) AS TotalSales
FROM Invoice i
GROUP BY Country)
```

**22. Provide a query that shows the most purchased track of 2013.**
```SQL
SELECT
t.Name AS Trackname,
COUNT(il.InvoiceLineId) AS TotalPurchases
FROM Track t
INNER JOIN InvoiceLine il ON t.TrackId = il.TrackId
INNER JOIN Invoice i ON il.InvoiceId = i.InvoiceId
WHERE i.InvoiceDate LIKE "2013%"
GROUP BY t.Name
ORDER BY TotalPurchases DESC
```

**23. Provide a query that shows the top 5 most purchased tracks over all.**
```SQL

```

**24. Provide a query that shows the top 3 best selling artists.**
```SQL

```

**25. Provide a query that shows the most purchased Media Type.**
```SQL

```
