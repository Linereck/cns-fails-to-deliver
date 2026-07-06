# CNS Fails-to-Deliver — consolidated dataset

Every SEC CNS fails-to-deliver record from **2019-01-02** onward, consolidated from the
SEC's half-month files (`cnsfails{YYYYMM}{a,b}.zip`) into one CSV.

**Easiest download: grab the compressed CSV and the original SEC ZIPs from
[Releases](../../releases) — release assets are not subject to Git LFS bandwidth limits.**

## File

`sec_fails_to_deliver_all.csv` (Git LFS) — one row per (settlement date, CUSIP, symbol,
quantity, description, price):

| column | example | notes |
|---|---|---|
| `settlement_date` | `20260612` | YYYYMMDD |
| `cusip` | `36467W109` | |
| `symbol` | `GME` | |
| `quantity_fails` | `525493` | shares failing at NSCC's CNS |
| `description` | `GAMESTOP CORP` | |
| `price` | `24.31` | prior close; empty where SEC reports `.` |

## Coverage & known gaps

- Current through **2026-06-12** (i.e. `cnsfails202606a`).
- **2026-05-01 to 2026-05-15 is missing upstream**: the SEC has not published
  `cnsfails202605a.zip`. If it appears, it will be folded in.
- CNS data is aggregate and anonymous; it understates total economic failure
  (ex-clearing and obligation-warehouse positions do not appear).

## Updating

Data is fetched with a downloader that sets the User-Agent the SEC's fair-access policy
requires (anonymous clients are blocked), then appended — never rewritten — so the file
only grows at the end. Source files are archived as release assets.

Source: https://www.sec.gov/data/foiadocsfailsdatahtm
