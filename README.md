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
