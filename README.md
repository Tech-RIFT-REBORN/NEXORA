# NEXORA

NEXORA + SUPABASE — PUBLIC ACCOUNTS EDITION

FILES
- index.html  = public NEXORA website + Sign In / Sign Up
- admin.html  = private admin dashboard
- schema.sql  = database + secure RLS policies

SETUP
1. Create/open your Supabase project.
2. Open SQL Editor.
3. Run schema.sql.
4. IMPORTANT: create your admin user in Supabase Authentication.
5. In Supabase Authentication > Users, copy your admin user's UUID.
6. Open schema.sql and replace YOUR_ADMIN_USER_ID with that UUID.
7. Run the policy section again (or run the whole edited file in a fresh project).
8. Copy your Supabase Project URL and public anon key.
9. Replace YOUR_SUPABASE_URL and YOUR_SUPABASE_ANON_KEY in BOTH HTML files.
10. Publish index.html and keep admin.html at your private/admin URL.

HOW IT WORKS
Public visitor -> creates NEXORA account -> signs in -> submits Hire an Expert request
-> request stores the Supabase Auth user_id -> admin dashboard shows the user ID.

IMPORTANT
- Supabase Auth handles account passwords; NEXORA does not store passwords itself.
- Never put a Supabase service_role/secret key in HTML.
- The public anon key is intended for frontend use when RLS is configured correctly.
- The admin UUID policy is what prevents ordinary signed-in NEXORA users from reading,
  updating, or deleting the request list.
- If Supabase email confirmation is enabled, users may need to confirm their email before signing in.
- Do not collect Discord passwords, tokens, or other private credentials.

EXISTING DATABASE UPGRADE
If your old requests table already exists, schema.sql adds user_id, but existing anonymous
rows will have no user_id. The new insert policy only allows authenticated users to create
new requests. You may need to handle old rows separately before adding the NOT NULL constraint
if your existing table already contains data.
