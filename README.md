```mermaid
graph TD;
    User -->|Interacts| Frontend(Next.js)
    Frontend -->|API Calls| Backend(Node.js)
    Backend -->|Auth Requests| Auth(NextAuth / Clerk)
    Backend -->|Reads/Writes| Database(Supabase)
    Backend -->|Processes| Payment(Stripe)
