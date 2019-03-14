<h2>Hive</h2>



<h3>statements</h3>

basic:

```
select <columns>
from <table>
join <other tables>
where <filter condition>
group by <grouping>
having <aggregate filter>
order by <column list>
limit <number of rows>
```
exampels:

```select * from <table> limit <num>;```
```select <alias>.<column> from <table> <alias>```
```select distinct <column> from <table>```
```select <column> from <table> where <column> like '%%'``` (% is the wildcard)

<h3>functions</h3>
string:

	concat()
	lower()
	substr()
	trim()
	regexp_replace()
	parse_url()
	locate()
	

maths:

	round()
	rand()
	sqrt()
	abs()
	floor()
	ceiling()

date:

	to_date()
	year(), month(), date()
	datediff()
	date_add(), date_sub()

conditions:

	if()
	coalesce() (detect the first element that is not NULL)
	case...when
	
<h3>join</h3>
inner join

left join

<h3>Examples</h3>
count unique items and sort by descending order

	select <col> count(*) as c
	from <table>
	group by <col>
	order by c desc;
	
todo