# MSAI 5573 · AI Studio II — Individual Sprint Log (Willie Boone)

## 1. Sprint information

| | |
|---|---|
| **Project / Team** | Buddy AI — AI-powered life coach |
| **Sprint number** | Sprint 3 |
| **Week of (start – end)** | 07/14/2026 – 07/20/2026 |
| **Team sprint goal** | Ship user accounts with cross-device sync, and settle which user-model representation the build should use. |
| **My focus this sprint** | Migrate the app to real accounts and a real database. |

## 2. My standup answers

| | |
|---|---|
| **Done since last standup** | Added the Supabase client library via CDN and initialized `createClient()` with the project URL and anon key. Designed and created the Supabase Postgres schema (`profiles` and `conversations` tables) with Row-Level Security policies restricting all access to `auth.uid() = user_id`. Replaced the name-only onboarding screen with an email/password signup and login UI (`signUp()`, `logIn()`, `logOut()`, `afterAuth()`). Migrated `saveProfile()` and `saveHistory()` from synchronous localStorage writes to async Supabase calls, updating every downstream call site. Added a session-persistence check so a returning, logged-in user skips the login screen on reload. Diagnosed and fixed a production bug where newly created Supabase tables weren't exposed to the REST API by default, causing 403 errors on every read/write; wrote and ran the SQL GRANT statements to restore access. Tested and verified signup, login, logout, session persistence, and two-account data isolation. Fixed a bug causing Buddy to report the wrong current date, grounding the coaching prompt in the real device date. Rewrote README.md to reflect the Supabase migration. |
| **Plan before next standup** | Fix the email-confirmation redirect (#8); continue toward the server-side API-key proxy. |
| **Blockers / help needed** | Email confirmation link redirects to a broken origin (#8). |

## 3. Board snapshot

See the team sprint log (`sprint-03-log.md`) for the shared board snapshot as of 07/15.

## 4. Blockers & risks I owned

| Blocker / risk | Impact | Status |
|---|---|---|
| Email confirmation link redirects to a broken origin (localhost:3000) (#8) | Blocks new users from finishing signup | Open — point the Supabase auth URL config at the app's real host |
| Anthropic API key is still held in the browser | Fine for a demo, not safe for real users | Open — move behind a server-side proxy (roadmap) |

## 5. Decisions I made or contributed to

| Decision | Why | Date |
|---|---|---|
| Migrate storage from browser localStorage to per-user Supabase tables with RLS, and add email/password auth. | Enables real accounts and cross-device sync. | 07/12 |

## 6. Action items & next steps

| Action / next step | Due | Link |
|---|---|---|
| Fix the email-confirmation redirect. | Sprint 4 | github.com/wdboone/revised-buddyai-v2/issues/8 |
| Continue toward the server-side API-key proxy. | Sprint 4 | github.com/wdboone/revised-buddyai-v2 |

## 7. My sprint reflection

**What went well:** Real accounts, cross-device sync, and Row-Level Security all shipped in one sprint — the app went from a device-bound demo to something that follows a real user around.

**What slowed me down:** The REST-API permissions bug stopped every read and write cold until I traced it to a Supabase default setting rather than anything in my own code. It cost real time before I stopped guessing and started reading the actual error carefully.

**What I'll change next sprint:** Read infrastructure error messages more carefully before assuming a bug is in my own logic — this one wasn't, and I lost time treating it like it might be.

## 8. Links & artifacts

| | |
|---|---|
| **GitHub repository** | https://github.com/wdboone/revised-buddyai-v2 |
| **Deliverable(s) this sprint** | Supabase client integration; database schema + RLS policies (SQL migration); email/password authentication flow; async Supabase persistence layer; session persistence on reload; API-permissions bug fix; date-grounding fix; README.md v3 update; Week 3 standup slide deck |
