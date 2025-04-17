In one word it means trouble.
If this vulnerability exists then it allows the attacker to make queries to the database of the web application and then they are able to retrieve the data that they are not normally able to retrieve and not supposed to retrieve as well.
If the attacker escalates this then he will be able compromise the underlying server and the backend applications and can perform Denial of Service.

First do a manual test to understand if the vulnerability exists or not : - 
1. Do a `'` single quote.
2. Check  for some SQL index (I don't know what this means)
3. Try some of the Boolean conditions like `OR 1 = 1` . Look for differences in the application
4. Payloads designed to trigger time delays when executed within a SQL query, and look for differences in the time taken to respond.
5. OAST payloads designed to trigger an out-of-band network interaction when executed within a SQL query, and monitor any resulting interactions.

Most common vulnerability is the `WHERE` clause of the Query.
- In `UPDATE` statements, within the updated values or the `WHERE` clause.
- In `INSERT` statements, within the inserted values.
- In `SELECT` statements, within the table or column name.
- In `SELECT` statements, within the `ORDER BY` clause.

