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
If country server 1 is down --> fallback to server 2

Frontend loads:
Azure Static Web Apps delivers HTML, JS, CSS
HTTPS enforced. Custom domain & managed cert
App runs in the browser

App needs data:
Frontend says, “I need data for profile/posts/data”
Frontend → API Request → Supabase

Supabase Responds:
Auth check
Queries database
Returns JSON file

UI Updates
Frontend renders the UI with the retrieved data


