# Seldom Rest Innovations — Public Website
Static site for Apple Developer Program compliance: company info, Privacy Policy, Terms, Support.


## Quick start
1. Clone repo.
2. Edit `privacy.html` and `terms.html` details (address, app names, etc.).
3. Replace email with your real support address in all files.
4. (Optional) Configure Supabase contact form (below).
5. Push to GitHub `main` branch. GitHub Pages deploys via Actions.


## GitHub Pages
- Repo → Settings → Pages → Source: **GitHub Actions**.
- The provided `.github/workflows/pages.yml` handles deployment automatically on push to `main`.
- Site will be served at `https://<username>.github.io/<repo>/` or custom domain once configured.


## Custom domain
1. In Pages settings, add `seldomrestinnovations.com`.
2. In GoDaddy DNS:
- Create A/ALIAS or CNAME per GitHub Pages instructions.
- Create `CNAME` record for `www` → `<username>.github.io`.
3. Wait for DNS to propagate, then enforce HTTPS in Pages.


## Supabase (contact form)
1. Create project → grab **Project URL** and **anon public key**.
2. SQL (create table & RLS):
```sql
create table if not exists public.contact_messages (
id uuid primary key default gen_random_uuid(),
created_at timestamp with time zone default now(),
name text not null,
email text not null,
subject text not null,
message text not null,
user_agent text
);


alter table public.contact_messages enable row level security;


create policy "allow inserts from anon" on public.contact_messages
for insert to anon with check (true);
