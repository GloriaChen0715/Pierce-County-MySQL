# Pierce-County-MySQL

## Query 1
Average sale price over the year


```
select year(sale_date) Year, sum(Sale_Price) as Total_sales
from sale_df
group by 1
order by 2 desc;
```
Year | Total_sales
2020 | 1000
