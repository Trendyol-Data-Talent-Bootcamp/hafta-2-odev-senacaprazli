### Soru 1) 1980’den itibaren spor grubu bazında en çok madalya alan 1. 3. 5. ülkeyi bulalım.
```sql 
  with medals as (
  select country, sport, count(1) as madalya_sayisi, 
  row_number() over(partition by sport order by count(1) desc) as siralama
  from sample.summer_medals
  where year>=1980
  group by country, sport
  order by sport, madalya_sayisi desc )
  select * from medals 
  where siralama in (1,3,5)
  ```