# Power_BI_DAX_Quiery
## Top more than 30 queries of Power BI

## 1. Show all the orders of customer HANNA MOOS?
``` DAX
EVALUATE
GROUPBY(SELECTCOLUMNS(FILTER(CROSSJOIN(Orders,Customers),Orders[CustomerID]==Customers[Cust
omerID] && Customers[ContactName]=="HANNA MOOS"),
Customers[ContactName],Orders[OrderID]),Customers[ContactName],Orders[OrderID])
```
![Image](https://github.com/user-attachments/assets/6ec02637-c42b-4d8c-a6e2-662790de0d37)
## 2. Show all the products which purchase under 11011?
``` DAX
EVALUATE
GROUPBY(SELECTCOLUMNS(FILTER(CROSSJOIN(Products,Orders),Orders[ProductID]==Products[Product
ID] && Orders[OrderID]<11011),
Orders[OrderID],Products[ProductName]),Orders[OrderID],Products[ProductName])
```
![Image](https://github.com/user-attachments/assets/ab39576b-6889-46db-a7cf-2f00cfab7282)
## 3. Show total amount of order 11011?
``` DAX
DEFINE
MEASURE Products[Total 
Amount]=SUMX(SELECTCOLUMNS(FILTER(CROSSJOIN(Products,Orders),Orders[ProductID]==Products[Pr
oductID] && Orders[OrderID]<11011),Orders[_Sales]),Orders[_Sales])
```
![Image](https://github.com/user-attachments/assets/04899996-a132-4217-aa73-18c51a14b233)
## 4. Show all the orders between two date,include customername & employee name also?
``` DAX
EVALUATE
SUMMARIZE(FILTER(Orders,Orders[OrderDate]>DATE(2020,12,1) && 
Orders[OrderDate]<DATE(2021,3,31)),Orders[OrderDate],Customers[ContactName],Employees[Full 
Name])
```
![Image](https://github.com/user-attachments/assets/1b897622-2a49-4330-bb9e-5a013067d6be)
## 5. Count Orders of each country?
``` DAX
EVALUATE
SUMMARIZE(Customers,Customers[Country],"Orders",COUNT(Orders[ShipCountry]))
```
![image](https://github.com/user-attachments/assets/6226d698-64b5-42d0-ae0f-d5d7ebe48d63)
## 6. Max category sale in whole database?
``` DAX
EVALUATE
TOPN(1,GROUPBY(FILTER(CROSSJOIN(Categories,Products),Products[CategoryID]==Categories[Categ
oryID]),Categories[CategoryName],"Total 
Count",COUNTX(CURRENTGROUP(),Categories[CategoryName])),[Total Count],DESC)
```
![image](https://github.com/user-attachments/assets/dc3a15a3-f1fd-4746-9e8d-640a58776044)

## 7. Max Product Sale in Whole Database?
``` DAX
EVALUATE
TOPN(1,GROUPBY(FILTER(CROSSJOIN(Products,Orders),Orders[ProductID]==Products[ProductID]),Pr
oducts[ProductName],
"Total Count",COUNTX(CURRENTGROUP(),Products[ProductName])),[Total Count],DESC)
```
![image](https://github.com/user-attachments/assets/275e40cd-8b96-4342-a4a5-e44e2e5c6440)

## 8. Total Sale in whole Database?
``` DAX
DEFINE
MEASURE Products[Total]=SUMX(Orders,Orders[Total sales])
```
![image](https://github.com/user-attachments/assets/b74bd46e-3e2a-4ed1-b576-0ed50e8322bc)

## 9. Show total amout of particuler order include productname,qtysale,price & total amount?
``` DAX
EVALUATE
SELECTCOLUMNS(FILTER(CROSSJOIN(Products,Orders),Orders[ProductID]==Products[ProductID] && 
Orders[OrderID]==11011),
Orders[OrderID],Products[ProductName],Orders[Quantity],Products[UnitPrice],Orders[_Sales])
```
![image](https://github.com/user-attachments/assets/ef84eb06-34da-4dc1-8cb4-57bf80983ed0)

## 10. Show all the orders made by Laura?
``` DAX
EVALUATE
GROUPBY(SELECTCOLUMNS(FILTER(CROSSJOIN(Employees,Orders),Orders[EmployeeID]==Employees[Empl
oyeeID] && Employees[FirstName]=="Laura"),
Employees[FirstName],Orders[OrderID]),Employees[FirstName],Orders[OrderID])
```
![image](https://github.com/user-attachments/assets/47c2af2a-a2b8-4823-92d9-0dd1257f5d9a)

## 11. Show all the orderid,customername which ordered ‘Tofu’ product
``` DAX
EVALUATE
GROUPBY(SELECTCOLUMNS(FILTER(CROSSJOIN(Customers,Products,Orders),Orders[CustomerID]==Custo
mers[CustomerID] && Orders[ProductID]==Products[ProductID] && 
Products[ProductName]=="Tofu"),"Order No",Orders[OrderID],"Customer 
Name",Customers[ContactName]),[Order No],[Customer Name])
```
![image](https://github.com/user-attachments/assets/4b95e493-4491-4369-9808-e92bcd25174d)

## 12. Show all the supplier names which supplies ‘Tofu’ & ‘Ipoh Coffee’
``` DAX
EVALUATE
SELECTCOLUMNS(FILTER(CROSSJOIN(Products,Suppliers),Products[SupplierID]==Suppliers[Supplier
ID] && Products[ProductName] in {"Tofu","Ipoh Coffee"}),
Suppliers[ContactName])
```
![image](https://github.com/user-attachments/assets/a4b30c06-16df-4928-9596-2f78ed092ce6)

## 13. List all the customers of city ‘London’ who ordered products more then one time
``` DAX
EVALUATE
DISTINCT(SELECTCOLUMNS(FILTER(CROSSJOIN(Customers,Products,Orders),Orders[CustomerID]==Cust
omers[CustomerID] && Orders[ProductID]==Products[ProductID]
&& Customers[City]=="London" && COUNT(Products[ProductName])>1),"Customer 
Name",Customers[ContactName]))
```
![image](https://github.com/user-attachments/assets/e565e601-cbc4-4a24-bf0d-042017539621)

## 14. Show all the customer name & employee name having same cities
``` DAX
EVALUATE
GROUPBY(SELECTCOLUMNS(FILTER(CROSSJOIN(Customers,Employees,Orders),Orders[CustomerID]==Cust
omers[CustomerID] && Orders[EmployeeID]==Employees[EmployeeID]
&& Customers[City]==Employees[City]),"Customers Name",Customers[ContactName],"Employees 
Name",Employees[Full Name]),[Customers Name],[Employees Name])
```
![image](https://github.com/user-attachments/assets/29ac6323-2fc7-47fd-820e-1e2f796b0af0)

## 15. Show all the customer who are owner of company
``` DAX
EVALUATE
SELECTCOLUMNS(FILTER(Customers,Customers[ContactTitle]=="Owner"),
"Customer Name",Customers[ContactName],"Company Name",Customers[CompanyName])
```
![image](https://github.com/user-attachments/assets/0acc5819-3b87-44b4-8942-5321261c7401)

## 16. Show all orders which sale by employee ‘Anne’
``` DAX
EVALUATE
GROUPBY(SELECTCOLUMNS(FILTER(CROSSJOIN(Employees,Orders),Orders[EmployeeID]==Employees[Empl
oyeeID] && Employees[FirstName]=="Anne"),"Employee Name",
Employees[Full Name],"Order No",Orders[OrderID]),[Employee Name],[Order No])
```
![image](https://github.com/user-attachments/assets/f8e0126f-271d-4911-9d9d-11c52bb2cc9f)

## 17. Show Most productive employee of NorthwindSale
``` DAX
EVALUATE
DISTINCT(SELECTCOLUMNS(FILTER(CROSSJOIN(Employees,Orders),Orders[EmployeeID]==Employees[Emp
loyeeID] && COUNT(Orders[OrderID])>2),Employees[Full Name]))
```
![image](https://github.com/user-attachments/assets/112f142c-bd7f-4336-b6b1-81bd47c993e7)

## 18. Show all the product sale by company ‘Tokyo Traders’
``` DAX
EVALUATE
SELECTCOLUMNS(FILTER(CROSSJOIN(Suppliers,Products),Products[SupplierID]==Suppliers[Supplier
ID] && Suppliers[CompanyName]=="Tokyo Traders")
,"Products",Products[ProductName],"Company Name",Suppliers[CompanyName])
```
![image](https://github.com/user-attachments/assets/3bff7fd1-3b04-425c-9f4b-dbbdc69e1119)

## 19. Show Total Sale of each Month
``` DAX
EVALUATE
SUMMARIZE(Orders,'Calendar'[Month Name],"Total Sales",SUMX(Orders,Orders[_Sales]))
```
![image](https://github.com/user-attachments/assets/0efe88d9-e1bb-4a57-b4b6-279be89ae208)

## 20. Show Total sale of each Sunday
``` DAX
EVALUATE
FILTER(SUMMARIZE(Orders,'Calendar'[Day Name],"Total 
Sales",SUMX(Orders,Orders[_Sales])),'Calendar'[Day Name]=="Sun")
```
![image](https://github.com/user-attachments/assets/3543ffe8-f891-439d-9222-dcacf0743591)


