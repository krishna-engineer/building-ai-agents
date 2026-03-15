### 15th March 2026
* With agno, I was using AWS DynamoDB (DDB) as Database for different tables that the framework creates internally e.g. session table to store all session data, or memory table to store memories related to a user, etc.
* But I faced an issue of PutItem operation failing. Digging deeper in it, I found that DDB item has size limit of 400KB. And in my case, that limit was reaching often.
* Hence I moved to AWS RDS Postgres. Also, Postgres is the recommended DB for production use-cases.
* After moving to Postgres, I was also facing issues like:
  * Not all tables were getting created by default which was not the issue with DDB.
  * So to overcome this, I had to run `db._create_all_tables()`
* P.S. - Do read how postgres handles huge size of dataset.

### 15th Dec 2025
* I got to know that with `agno` framework, it's possible to stream internal events that agent is going through, like tool call, reasoing, memory updates, etc.

* It'll be interesting for consumers of your solution, to get glimpse of what agent is doing internally before providing you with final response.
  * Though, you have to be careful of what you're showing to your consumers.
  * For e.g., your business might not like to show which tool is being called.
  
* Check [this](https://docs.agno.com/basics/agents/running-agents#streaming-internal-events) part of doc:
<img width="807" height="484" alt="Screenshot 2025-12-15 at 8 34 30 PM" src="https://github.com/user-attachments/assets/d2bed368-7543-42eb-adbc-67a49fb64a90" />
