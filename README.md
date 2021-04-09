# Pierce County MySQL

## Query 1
Average sale price over the year


```
select year(sale_date) Year, sum(Sale_Price) as Total_sales
from sale_df
group by 1
order by 2 desc;
```

| Year| Total_sales |                                                                                                                                     
|-----------|-------------|
|	2018	|	683505715	|
|	2011	|	643486619	|
|	2005	|	532610371	|
|	2020	|	497813211	|
|	2006	|	441521844	|
|	2013	|	439750355	|
|	2016	|	438861062	|
|	2004	|	433853134	|
|	2010	|	432894178	|
|	2015	|	372505980	|
|	2019	|	365431541	|
|	2001	|	343208462	|
|	2017	|	337680944	|
|	2002	|	277734364	|
|	2007	|	251873415	|
|	2014	|	212755494	|
|	2009	|	196400503	|
|	2012	|	179802322	|
|	2008	|	152102063	|
|	2003	|	124468571	|
|	1998	|	78928390	|
|	2000	|	67988045	|
|	2021	|	60692980	|
|	1999	|	57678051	|
|	1997	|	32839184	|


## Query 2
Median of sales price by attribute

```
with a as (SELECT l.attribute, s.Sale_Price 
   	 from sale_df s
	inner join land_df l on s.Parcel_Number = l.Parcel_Number)
  
SELECT
   t.attribute as Property_attribute, AVG(t.sale_price) as median_sale_price
FROM
   (SELECT attribute, sale_price,
    row_number() over(partition by attribute order by sale_price) rn,
    count(*) over(partition by attribute) cnt
    from a
    ) t
where rn in ( FLOOR((cnt + 1) / 2), FLOOR( (cnt + 2) / 2) )
group by attribute
order by 2 desc;

```
|Property_attribute|	median_sale_price |
|-----------|-----------|
|	C MA 4 TACOMA N	|	17502500	|
|	C MA 9 CENTRAL	|	14000000	|
|	C MA 8 PORT	|	3500000	|
|	C MA 3 PENINSULA	|	3268000	|
|	C MA 5 NORTH	|	750000	|
|	C STREETS	|	480000	|
|	C UTILITIES	|	434875	|
|	R WATERFRONT	|	429500	|
|	C AMENITIES	|	421750	|
|	C ECONOMIC	|	375000	|
|	C MA 7 CBD	|	314900	|
|	R VIEW	|	305000	|
|	R SIZE	|	287450	|
|	R AMENITIES	|	265000	|
|	R FUNCTIONAL	|	239975	|
|	R ECONOMIC	|	233900	|
|	R UTILITIES	|	204120	|
|	C ZONING	|	172000	|
|	C USE	|	170000	|
|	C MA 2 TACOMA S	|	100000	|
|	R SITE DEVELOPMENT	|	100000	|
|	C FUNCTIONAL	|	99500	|
|	R STREETS	|	46250	|


