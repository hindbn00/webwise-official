# WebWise: Supabase setup
1. In Supabase, open SQL Editor and run:

create table public.leads(
  id bigint generated always as identity primary key,
  created_at timestamptz default now(),
  plan text, name text not null, preferred_contact text, contact_details text,
  email text, whatsapp text, instagram text, message text);
alter table public.leads enable row level security;
create policy "anyone can submit" on public.leads for insert to anon with check (true);
create policy "admin can read" on public.leads for select to authenticated
  using ((auth.jwt() ->> 'email') = 'webwisee.official@gmail.com');

2. Supabase > Authentication > Users > Add user: email webwisee.official@gmail.com, choose a password, tick "Auto Confirm User".
   Also turn off public sign-ups (Authentication > Sign In / Providers > "Allow new users to sign up").
3. Paste your Project URL and anon public key (Project Settings > API) into SUPABASE_URL and SUPABASE_KEY in BOTH index.html (lines 195-196) and admin/index.html.
4. Deploy on Vercel. Log in at yoursite.com/admin with the email and password from step 2.
