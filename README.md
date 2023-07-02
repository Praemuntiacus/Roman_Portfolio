# Real Estate Market Analysis in France
--------------------------------------------------------------
- SQL dump: [database.sql](Project2/database.sql)
## SQL project analysing the real estate makret in France during 2020

### The total number of apartments sold during the first semester of 2020
- SQL script: [query1.sql](https://github.com/Praemuntiacus/Real_Estate_Market_Analysis/blob/main/query1.sql)

The query counts the number of apartments (**apparts_vendus**) that were sold (**NatMut** = *'Vente'*) within a specific date range (DatMut BETWEEN '2020-01-01' AND '2020-06-30'). The SELECT statement uses the COUNT function to count the occurrences of *immobilier.id* and aliases it as *apparts_vendus*.

The query joins the *immobilier* table with the *mutation* table using a left join (LEFT JOIN) with the join condition *mutation.id = immobilier.id*. The WHERE clause filters the records to include only apartments (**TypIm** = *'Appartement'*), sales transactions (**NatMut** = *'Vente'*), and a specific date range (DatMut BETWEEN '2020-01-01' AND '2020-06-30').

The query calculates and returns the count of apartments (apparts_vendus) that were sold within the specified date range.






- **Result**:
______________
**apparts_vendus**

         31378
______________

### The proportion of apartment sales based on the number of rooms
- SQL script: [query2.sql](https://github.com/Praemuntiacus/Real_Estate_Market_Analysis/blob/main/query2.sql)


The query provides information about the number of sold apartments grouped by the number of rooms (**NbPiece**). The SELECT statement retrieves the **NbPiece** column as pieces and counts the occurrences of each **NbPiece** value using COUNT(NbPiece) as **nombr_appart**.

The expression (COUNT(NbPiece) * 100 / (SELECT COUNT(id) FROM immobilier WHERE TypIm = 'Appartement')) calculates the percentage of apartments (**prsnt_appart**) for each number of rooms (NbPiece). It divides the count of apartments for a specific number of rooms by the total count of apartments, obtained from a subquery.

The WHERE clause filters the records to include only apartments (**TypIm** = *'Appartement'*). The GROUP BY clause groups the result by the number of rooms (**NbPiece**). The ORDER BY clause orders the result by the number of rooms (**NbPiece**).

The query presents the number of apartments (nombr_appart), grouped by the number of rooms (pieces), and also provides the percentage of apartments (prsnt_appart) for each number of rooms. The results are ordered based on the number of rooms.





- **Result**:
________________________
**pieces** | **apparts**

     0       30
     1     6739
     2     9783
     3     8966
     4     4460
     5     1114
     6      204
     7       54
     8       17
     9        8
    10        2
    11        1
______________________________

### The average price per square meter for real estate properties in each department
- SQL script: [query3.sql](https://github.com/Praemuntiacus/Real_Estate_Market_Analysis/blob/main/query3.sql)

The query calculates the average price per square meter (**prix_m2**) for each department (**CodDept**) based on the price (**ValFon**) and surface area (**SrfIm**) data from the *immobilier* table. The join condition *department.id = immobilier.id_dept* ensures that the corresponding records are matched between the department and immobilier tables. The result is grouped by department (GROUP BY department.CodDept), and the AVG function calculates the average valuation per surface area for each department. The ROUND function is used to round the calculated average price per square meter to 2 decimal places. The results are then ordered in descending order of **prix_m2** using the ORDER BY clause. Finally, the LIMIT 10 clause is used to retrieve only the top 10 departments with the highest average price per square meter.

The query provides the top 10 departments with the highest average price per square meter based on the valuation and surface area data from the immobilier table.


### The average price per square meter for houses in selected departments
- SQL script: [query4.sql](https://github.com/Praemuntiacus/Real_Estate_Market_Analysis/blob/main/query4.sql)

This query calculates the average price per square meter (prix_m2_maison_IDF) for houses (TypIm = 'Maison') in the Île-de-France region (specifically departments with codes '75', '77', '78', '91', '92', '93', '94', '95').

The query uses two subqueries (*tab1* and *tab2*) to calculate the necessary aggregates. The first subquery (*tab1*) calculates the total price (prix_m2_total) for each house (TypIm) in the specified departments, by summing the price (ValFon) from the *immobilier* table. The second subquery (*tab2*) calculates the total surface area (srf_total) for each house (TypIm) in the specified departments, by summing the surface area (SrfIm) from the *immobilier* table.

These two subqueries are joined using the JOIN statement, matching records with the same TypIm (house type). The result is a single row for each house type, with the average price per square meter calculated by dividing the total price by the total surface area, rounded to 2 decimal places.

The final result of the query is the average price per square meter (prix_m2_maison_IDF) for houses (TypIm = 'Maison') in the Île-de-France region.
