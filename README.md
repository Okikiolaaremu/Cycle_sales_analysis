# Cycle_sales_analysis
## Data Introduction
A bike, or bicycle, is a human-powered vehicle with two wheels, a frame, handlebars for steering, a seat, and pedals used to propel the rider forward, allowing them to travel on land by pedaling; essentially, a two-wheeled vehicle powered by the rider's legs. 
## Data Overview
This is a dataset which deals with the sales focus of an organization that deals with bikes and it’s accessories.
## Data focus
- This dataset engulfs around generating insights on the sales activities of the organization.
- How much of impact the firm's suppliers brings upon the revenues of the business.
- Likewise insights on how the products contributes to the revenue of the firm.
## Data Standardization
Before embarking on analysing the dataset, there was an action of standardizing the tables by checking and correcting the data types, data names, removing unwanted spaces in the data and many others.
- Under the table (product_order), there were changes made to various columns by effecting the right data type in place and removing unwanted columns.
- Under the table (sales_order), there was various adjustments to various columns, as NETAMOUNT and TAXAMOUNT COLUMNS were rounded to 2 decimal places. Also, columns such as delivery date, currency, QUANTTITYUNIT were all dropped as they were not required. Likewise, the Delivery_date column was changed to the DATE data type from INT.
### Checking and removing duplicates:
- There was a check-in on the various tables to see if there was any form of duplicate value using the SQL syntax;
select*,
row_number() over(partition by PRODUCTID,TYPECODE,PRODCATEGORYID,CREATEDBY,created_at,CHANGEDBY,changed_at,
SUPPLIER_PARTNERID,SUPPLIER_PARTNERID,TAXTARIFFCODE,WEIGHTMEASURE,WEIGHTUNIT,CURRENCY,PRICE) as Row_num from product_order_new;
- To confirm if there is no duplicate in the dataset, the following syntax was used:
with duplicate_cte as (select*,
row_number() over(partition by PRODUCTID,TYPECODE,PRODCATEGORYID,CREATEDBY,created_at,CHANGEDBY,changed_at,
SUPPLIER_PARTNERID,SUPPLIER_PARTNERID,TAXTARIFFCODE,WEIGHTMEASURE,WEIGHTUNIT,CURRENCY,PRICE) as Row_num from product_order_new)
select *
from duplicate_cte
where Row_num>1;
- It was discovered that there isn’t any duplicate value in the dataset after careful look in the three tables.
## Data tools
The project was carried out using MySQL workbench as an analyzing tool, using various syntaxs to carry out necessary actions.
- Codes such as;
- SELECT 
    SUM(GROSSAMOUNT) tot_gross_amt, sales_order_id
FROM
    sales_order
GROUP BY sales_order_id
ORDER BY tot_gross_amt DESC;
-SELECT 
    product_id, Product_category_name
FROM
    product_order po
        JOIN
    productcategorytext pct ON po.PRODCATEGORYID = pct.prod_category_id
WHERE
    Product_category_name = 'mountain bike';

- SELECT 
    SUM(QUANTITY) Highest_qty_sold,
    so.PRODUCTID,
    Product_category_name
FROM
    sales_order so
        JOIN
    product_order po ON so.PRODUCTID = po.product_id
        JOIN
    productcategorytext pct ON po.PRODCATEGORYID = pct.prod_category_id
GROUP BY so.PRODUCTID , Product_category_name
ORDER BY Highest_qty_sold DESC;

-SELECT 
    ROUND(SUM(NETAMOUNT), 0) Tot_revenue, Product_category_name
FROM
    sales_order so
        JOIN
    product_order po ON so.PRODUCTID = po.product_id
        JOIN
    productcategorytext pct ON po.PRODCATEGORYID = pct.prod_category_id
WHERE
    Product_category_name IN ('Mountain Bike' , 'BMX')
GROUP BY Product_category_name;
## Data Tools
The dataset was analysed using the MySQL workbench, where the dataset was manipulated, cleaned, and explored to infer meaning decision making process
- [MySQL workbook] (https://github.com/user-attachments/assets/5d3260e7-df88-4376-bc99-9b7bf711a240)


 
 



 
## Data Visualization
This data was visualized with the aid of Business intelligence tool which is Power-BI
###Power_BI 
 



## Data Insights
- It was discovered that products (ebike and racing bike) top the most expensive products.
- There were only 4 products under the Mountain-bike category.
- ebike, Racing Bike and Mountain Bike ranks top as the products which rakes in the highest gross amount with values of $1,318,200/ $1,142,194 and $405,328 respectively.
- Five suppliers ranked highest in contributing to the gross income of the organization identified with suppliers ID as 100000032, 100000029, 100000031, 100000019, 100000014 with a gross amount of $395,000/ $321,600/ $255,000/ $243,939/$252,954.
- Sales made with sales_id (500000242) had the highest gross amount with a value of $28,196 
- Five products which are eBike, Racing Bike, Mountain Bike, Cyclo-cross Bike and Hybrid Bike collectively tops the as products which brings in the highest net amount to the organization with values of $1,153,425/ $999,418/ $354,662/ $173,027/$160,953.
- Product_id (BX-1013) with product_category_name as BMX has the highest quantity sold of 510.
- Mountain Bike and BMX products both contributed $354,662 and $ 114,486 respectively to the revenue.
## Recommendations
- An elaborate and intensive marketing should be made on the E-bike product as there isn’t much quantity of sales made on the various products.
- Whereas, the BMX product has much quantity been sold, but more can be achieved with a deep reach into the market where more can be sold to better more revenue. To achieve this, more promotion can be done and also expand the market operation and make much more enticing the product to the market it serves.
- More coordination, collaboration, communication and competence should be engaged upon to improve the relationships with the suppliers, and also ensure there is an avenue for quality test control for the goods supplied, this is to make sure very high quality are been supplied with the right description of goods sent to the firm.
