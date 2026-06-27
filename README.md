Glossary: 

JWT - JSON Web Token. Industry standard way to safely share information between the frontend and backend as a single string of text.
Private Endpoints - Hidden network connection that allows backend to connect to database, preventing public access.

Every modern application can be boiled down to 5 layers:

1. Frontend (UI)
2. Backend (logic)
3. Database (data)
4. Identity (login/security)
5. Infrastructure & Networking

Cloud engineering is effectively: “how do these layers communicate with each other reliably, securely, and cost-effectively”

Step 1: What happens when the app is opened:

DNS lookup:
User types the domain
Browser asks, “Where is this hosted?”
Azure DNS returns: “Azure edge server (Country)”
TTL: 300s (cached by ISP)

Edge Security:
Azure Front Door terminates SSL
WAF inspects requests: no SQL injection, no XSS
Static content served from edge cache (cheaper & faster)
If country server 1 is down → fallback to server 2

Frontend loads:
Azure Static Web Apps delivers HTML, JS, CSS
HTTPS enforced. Custom domain & managed cert
App runs in the browser

App needs data:
Frontend says, “I need data for profile/posts/data”
Frontend → HTTPS → API Management (rate limit, logging)
→ Azure App Service (VNet subnet, NSG allows 443 only)
App Service uses System-Assigned Managed Identity
→ No secrets in code

Identity Check:
JTW token sent in Authorisation header
Microsoft Entra ID validatres signature & claims
Conditional Access: MFA required for admin roles
Invalid token → 401, request stops

Database Query:
App Service → Private Endpoint → Azure SQL (private subnet)
Connection string pulled from Azure Key Vault at runtime
Query executes → JSON returned

UI Updates
Frontend renders the UI with the retrieved data

Monitoring:
Azure Monitor logs every step
Application Insights traces latency per component
Alert fired if response time > 2s
Cost dashboard: £47/day, database is 60%


