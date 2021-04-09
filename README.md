# Pierce-County-MySQL
```
select year(sale_date) Year, sum(Sale_Price) as Total_sales
from sale_df
group by 1
order by 2 desc;


```
