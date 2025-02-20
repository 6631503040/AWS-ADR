# AWS-ADR
I'm super handsome.
Context
Our application requires a reliable and scalable relational database. Managing a database on EC2 requires manual updates, backups, and scaling, which increases operational complexity.

Decision
We choose Amazon RDS (Relational Database Service) for handling structured data instead of self-managing a database on EC2.

Rationale
Fully managed: AWS handles maintenance, backups, and updates.
High availability: RDS supports Multi-AZ deployment for failover.
Scalability: Can scale read replicas to handle increased traffic.
Security: Integrated with AWS IAM and encryption.
Consequences
✅ Pros:

Automated backups, patching, and maintenance.
High availability and disaster recovery support.
Better security features than self-managed databases.
❌ Cons:

More expensive than setting up a database on EC2.
Less control over system configurations.
Scaling storage may require downtime for certain DB engines.
Sample Code
Example of connecting to an RDS database using Python and psycopg2 (PostgreSQL):

python
Copy
Edit
import psycopg2

conn = psycopg2.connect(
    dbname="mydatabase",
    user="admin",
    password="mypassword",
    host="mydb-instance.c1q2w3e4r5.us-east-1.rds.amazonaws.com",
    port="5432"
)

cursor = conn.cursor()
cursor.execute("SELECT * FROM users;")
rows = cursor.fetchall()
print(rows)

cursor.close()
conn.close()
