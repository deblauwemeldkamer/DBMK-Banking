# DBMK-Banking

Advanced banking resource for **ESX Legacy (Lua 5.4)** with a modern NUI, modular gameplay systems, and built-in staff/compliance tooling.

✅ ESX Legacy resource only  
✅ No VPS required  
💶 Tebex-ready package structure

![DBMK-Banking Preview](https://i.imgur.com/kzxFtmk.png)

---

## Overview

DBMK-Banking keeps player balances on the default ESX `bank` account and adds:

- IBAN-based profiles  
- transaction journal and daily limits  
- savings, loans, investments, cards, and ATM flows  
- shared, business, and offshore account systems  
- compliance flags, escalations, and audit tools  

Designed for production RP servers that need both clean UX and deeper financial gameplay.

---

## Features

### Core Banking
- Personal dashboard (bank, cash, IBAN, limits, score, transactions)  
- IBAN / phone-linked transfers  
- Counter deposit and withdraw with branch proximity checks  
- Account state controls: `active`, `restricted`, `frozen`  

### Savings
- Separate savings account  
- Configurable interest accrual  
- Savings goals with add/remove/fund workflows  
- Optional post-deposit lock behavior  

### Loans
- Configurable loan products (APR, terms, limits)  
- Manual repayments  
- Automatic collection cycle  
- Missed-payment/default handling  

### Investments
- Asset list with dynamic market ticks  
- Buy/sell flows  
- Position tracking and PnL view  
- Daily trade limits and compliance hooks  

### Cards & ATM
- Card status flow (`active` / `blocked`)  
- Replacement card issuance flow  
- ATM PIN verification + session logic  
- Optional physical card checks via `ox_inventory`  

### Shared / Business / Offshore
- Shared accounts with role permissions (`owner`, `manager`, `cashier`, `viewer`)  
- Job-based business account system with grade-based controls  
- Offshore account module with configurable fees/access points  

### Staff / Compliance / Audit
- Staff portal for account controls  
- Compliance flags by severity  
- Escalation/case workflows  
- Audit trail for key actions  

### UI / UX
- Modern dark-green NUI  
- Home market pulse and rotating banners  
- Compact player-first layout  

---

## Requirements

Required dependencies:
- `es_extended` (ESX Legacy)  
- `oxmysql`  
- `ox_lib`  

Optional:
- `ox_inventory` (card/token/document items + vault inventory sync)

---

## Installation

1. Place `DBMK-Banking` in your server `resources` folder.  
2. Import `sql/dbmk_banking.sql`.  
3. Optional: import `sql/bank_job.sql` for bank staff job setup.  
4. Configure `shared/config.lua` (branches, limits, modules, integrations, webhooks).  
5. Add `ensure DBMK-Banking` to `server.cfg` after dependencies.  
6. Restart resource/server.  
7. Test in-game with `/banking` (default command).  

---

## Business Account Setup

If you see:  
`No account for your current job...`

You must add your ESX job names in `Config.Business.Jobs` (lowercase), and they must match the values in `users.job` exactly.  
Keep `AutoEnsure = true` so business accounts are automatically created for configured jobs.

After editing config, restart `DBMK-Banking`.

---

## Configuration

Main file: `shared/config.lua`

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

## Commands

- `/banking` — Open banking app  
- `/bankjob` — Open bank job menu (if enabled)

---

## Exports

- `exports['DBMK-Banking']:GetPlayerIban(identifier)`  
- `exports['DBMK-Banking']:EnsureBankingProfile(identifier)`

---

## ox_inventory Integration

Example files:
- `ox_inventory_bank_card_example.lua`  
- `ox_inventory_items_full_example.lua`  

Common item names:
- `bank_card`  
- `bank_token`  
- `loan_document`  

Vault behavior:
- Store item in vault -> item is removed from player inventory  
- Take item from vault -> item is returned to player inventory  

---

## Recommended QA Flow

1. Restart resource and confirm no SQL/runtime errors.  
2. Test transfers/deposits/withdrawals.  
3. Test card + ATM PIN flow.  
4. Test savings and goals.  
5. Test loans and repayment cycle.  
6. Test investments and positions.  
7. Test shared/business/offshore modules.  
8. Test staff flags/escalations/audit workflows.  

Use `PRE_TEBEX_QA_CHECKLIST.md` for release validation.

---

## Related Docs

- `ROADMAP.md`  
- `BANK_JOB.md`  
- `PRE_TEBEX_QA_CHECKLIST.md`  
- `TEBEX_ESCROW_READY.md`  

---

## Support

For setup help or expansion work:
- Open an issue in your support repo/channel  
- Include logs, config snippet, and reproduction steps

# DBMK-Banking

Advanced banking resource for **ESX Legacy (Lua 5.4)** with a modern NUI, rich gameplay modules, staff tooling, and Tebex-ready structure.

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
- `TEBEX_ESCROW_READY.md`
- `PRE_TEBEX_QA_CHECKLIST.md`

---

## Support

If you need setup help, balancing support, or feature extension:

- Open an issue in your project support channel/repo
- Include logs, config snippet, and reproduction steps
