# WebWise: Supabase setup
1. In Supabase, open SQL Editor and run:

create table public.leads(
  id bigint generated always as identity primary key,
  created_at timestamptz default now(),
  plan text, name text not null, preferred_contact text, contact_details text,
  email text, whatsapp text, instagram text, message text);
alter table public.leads enable row level security;
create policy "anyone can submit" on public.leads for insert to anon with check (true);

2. In index.html, fill SUPABASE_URL (Project Settings > API > Project URL) and SUPABASE_KEY (anon public key).
3. Deploy on Vercel as before. Bookings appear in Supabase > Table Editor > leads.
