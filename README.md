# DBMK-Banking

Advanced banking resource for **ESX Legacy (Lua 5.4)** with a modern NUI, rich gameplay modules, staff tooling, and Tebex-ready structure.

![DBMK-Banking Preview](https://i.imgur.com/kzxFtmk.png)

DBMK-Banking keeps player money on the default ESX `bank` account and adds:

- IBAN-based profiles
- transaction journal and daily limits
- savings, loans, investments, cards, ATM flow
- shared/business/offshore account systems
- compliance flags, escalations, and audit tools

---

## Features

### Core Banking

- Personal dashboard: bank, cash, IBAN, credit score, limits, transactions
- Transfer to IBAN / phone-linked targets
- Counter deposit and withdraw with branch proximity checks
- Account status controls: `active`, `restricted`, `frozen`

### Savings

- Savings account with interest accrual
- Savings goals with funding and progress tracking
- Configurable interval-based interest processing

### Loans

- Loan products with APR/term presets
- Manual repayment and automatic collection
- Missed-payment tracking and default handling
- In-game-time loan cycle support

### Cards & ATM

- Card status flow (active/blocked)
- Replacement card request flow with modal UX
- ATM PIN verification and session checks
- Inventory card checks (`ox_inventory` optional)

### Shared, Business, Offshore

- Shared accounts with member roles (`owner`, `manager`, `cashier`, `viewer`)
- Business account per ESX job with configurable grade permissions
- Offshore account with configurable fees, limits, and access points

### Staff / Compliance / Audit

- Compliance rules with severity levels
- Staff actions for account controls and card workflows
- Escalation/case handling
- Combined audit trail across multiple banking events

### UI / UX

- Dark-green modern NUI
- Home market index + animated banner rotator
- Compact layout tuning for no-scroll home fit

---

## Requirements

- `es_extended`
- `oxmysql`
- `ox_lib`
- Optional: `ox_inventory` (for card/token/document item flow)

---

## Installation

1. Import `sql/dbmk_banking.sql` into your database.
2. Optional (bank staff job): import `sql/bank_job.sql`.
3. Ensure resource order in `server.cfg` (after dependencies):
   - `ensure DBMK-Banking`
4. Configure `shared/config.lua`:
   - branch coordinates
   - limits/security modules
   - webhooks/integrations
5. Start server and open banking in-game (`/banking` by default).

---

## Recommended Production Check

1. Restart resource and verify there are no SQL/runtime errors.
2. Test personal flows (transfer, deposit, withdraw).
3. Test card + ATM flow (PIN, blocked card, replacement request).
4. Test staff panel features (flags, cases, status controls).
5. Test webhook output with `Config.Webhooks.Enabled = true`.
6. Test optional item flow with `ox_inventory` running.

For release QA, use `PRE_TEBEX_QA_CHECKLIST.md`.

---

## Configuration Notes

Main config file: `shared/config.lua`

Key sections:

- `Config.BankBranches`
- `Config.Limits`
- `Config.Cards`
- `Config.ATM`
- `Config.Savings`
- `Config.Loans`
- `Config.Investments`
- `Config.Shared`
- `Config.Business`
- `Config.Offshore`
- `Config.Compliance`
- `Config.Items`
- `Config.Webhooks`

---

## Exports

- `exports['DBMK-Banking']:GetPlayerIban(identifier)`
- `exports['DBMK-Banking']:EnsureBankingProfile(identifier)`

---

## Optional ox_inventory Items

Available examples:

- `ox_inventory_bank_card_example.lua`
- `ox_inventory_items_full_example.lua`

Common item keys used by this build:

- `bank_card`
- `bank_token`
- `loan_document`

---

## Related Docs

- `ROADMAP.md`
- `BANK_JOB.md`

---

## Support

If you need setup help, balancing support, or feature extension:

- Open an issue in your project support channel/repo
- Include logs, config snippet, and reproduction steps
