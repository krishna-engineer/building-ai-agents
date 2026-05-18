## 18th May 2026: "Exposing a functionlity -- MCP server vs Python Library"
* This was an important discussion I had with my team mates. E.g. I want to provide a features related to docx handling - text extraction, token count, section detection, etc. Should this be a Python library that consumers import, or an MCP server they call?
  
* What are the cons with exposing Python library?
    * If I have 10 consumers, and I update my library, all 10 will have to do perform library update.
    * My code will become part of consumers' code-base, and if my code is bloated then consumers' code become bloated too.
    * Programming language lock-in exists because my code is in Python.
    * Bigger one - dependency version mis-match can occur if I need v0.1 of xyz library, and consumer's code need v0.5 of same library.

* What are the cons with exposing MCP Server tools?
    * Network hit - something which can be an important metric for latency senstive applications
    * Bigger one - Now because I am running a service, it'll come at cost of Operational Overhead like Monitoring, Infra, Cost, Client Support, etc.

P.S.: For our use-case, we went ahead with MCP server approach.


## 15th March 2026
* With agno, I was using AWS DynamoDB (DDB) as Database for different tables that the framework creates internally e.g. session table to store all session data, or memory table to store memories related to a user, etc.
* But I faced an issue of PutItem operation failing. Digging deeper in it, I found that DDB item has size limit of 400KB. And in my case, that limit was reaching often.
* Hence I moved to AWS RDS Postgres. Also, Postgres is the recommended DB for production use-cases.
* After moving to Postgres, I was also facing issues like:
  * Not all tables were getting created by default which was not the issue with DDB.
  * So to overcome this, I had to run `db._create_all_tables()`
* P.S. - Do read how postgres handles huge size of dataset.

## 15th Dec 2025
* I got to know that with `agno` framework, it's possible to stream internal events that agent is going through, like tool call, reasoing, memory updates, etc.

* It'll be interesting for consumers of your solution, to get glimpse of what agent is doing internally before providing you with final response.
  * Though, you have to be careful of what you're showing to your consumers.
  * For e.g., your business might not like to show which tool is being called.
  
* Check [this](https://docs.agno.com/basics/agents/running-agents#streaming-internal-events) part of doc:
<img width="807" height="484" alt="Screenshot 2025-12-15 at 8 34 30 PM" src="https://github.com/user-attachments/assets/d2bed368-7543-42eb-adbc-67a49fb64a90" />
