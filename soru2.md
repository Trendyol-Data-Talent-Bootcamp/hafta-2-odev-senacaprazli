
### Soru 2) 1980’den itibaren herhangi bir spor grubunda üst üste 3 veya daha fazla madalya almış atletleri bulalım.

```sql
with medals as(   
select athlete,
lead(year) over (partition by athlete order by year) as year1,
lead(year) over(partition by athlete order by year ) as year2
from dsmbootcamp.sample.summer_medals
where year >= 1980 
group by athlete, year
order by athlete,year )

select distinct athlete 
from medals 
where year1 is not null and year2 is not null 
order by athlete;
```