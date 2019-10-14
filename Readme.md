###Log Analysis reporting tool
<p> it's a python program that answer some questions about database from analyzing data. the 3 questions the program answer is:
<ul>
<li> What are the most popular three articles of all time?</li>
<li>  Who are the most popular article authors of all time?</li>
<li> On which days did more than 1% of requests lead to errors?</li></ul></p>


###Installation
<p>To run this program you have to install:
<ul>
<li>Vagrant</li>
<li>Python</li>
<li>Python3</li></ul></p>

<p> When you run vagrant with `vagrant ssh` and connect the database using `psql dbname`
you should create those **Views**:
<ul>
<li> `create view tresponses as select date(time), count(*) as responses from log group by date(time);`</li>
<li>`create view terrors as select date(time), count(*) as errors from log where status != '200 OK' group by date(time) order by date(time);`</li>
<li> `create view errors_prcentage as select to_char(tresponses.date, 'FMMon FMDD, YYYY'), ((errors*10000)/responses)*0.01 as percentage
from tresponses join terrors on tresponses.date=terrors.date order by percentage desc;`</li></ul></p>
