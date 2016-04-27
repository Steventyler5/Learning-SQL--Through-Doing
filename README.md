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

```

**8. How many Invoices were there in 2009 and 2011? What are the respective total sales for each of those years?(include both the answers and the queries used to find the answers)**
```SQL

```

**9. Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for Invoice ID 37.**
```SQL

```

**10. Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for each Invoice. HINT: GROUP BY**
```SQL

```

**11. Provide a query that includes the track name with each invoice line item.**
```SQL

```

**12. Provide a query that includes the purchased track name AND artist name with each invoice line item.**
```SQL

```

**13. Provide a query that shows the # of invoices per country. HINT: GROUP BY**
```SQL

```

**14. Provide a query that shows the total number of tracks in each playlist. The Playlist name should be include on the resulant table.**
```SQL

```

**15. Provide a query that shows all the Tracks, but displays no IDs. The resultant table should include the Album name, Media type and Genre.**
```SQL

```

**16. Provide a query that shows all Invoices but includes the # of invoice line items.**
```SQL

```

**17. Provide a query that shows total sales made by each sales agent.**
```SQL

```

**18. Which sales agent made the most in sales in 2009? HINT: MAX**
```SQL

```

**19. Which sales agent made the most in sales over all?**
```SQL

```

**20. Provide a query that shows the # of customers assigned to each sales agent.**
```SQL

```

**21. Provide a query that shows the total sales per country. Which country's customers spent the most?**
```SQL

```

**22. Provide a query that shows the most purchased track of 2013.**
```SQL

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
