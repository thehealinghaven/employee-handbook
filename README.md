# The Healing Haven — Employee Manual

Source for the employee manual of The Healing Haven (Helen DeLovely LCSW PLLC), Salt Lake City. Built as a Mintlify docs site; content is plain Markdown in `.mdx` files so it can move to any docs platform without rewriting.

**Status:** v1.1, September 3, 2026. **Ready for attorney review.** Not yet adopted. Twelve of fourteen open items are resolved; the two that remain (DOPL supervisor approval, new suite details) are facts waiting on outside parties, not policy gaps. Takes effect when Helen adopts it after the attorney pass.

Maintained by the practice manager (Sonja Scriven). This README is for whoever maintains or deploys it; it is not employee-facing.

## Layout

```
docs.json           Mintlify config + navigation (the deployable one; must sit at repo root)
nav.yaml            Same navigation tree, platform-neutral
theme-tokens.md     Brand colors, fonts, dark mode, callout mapping
introduction.mdx    Welcome page
acknowledgment.mdx  Single signature page covering the whole manual
welcome/  employment/  pay-and-time-off/  conduct/  privacy-and-security/
clinical-practice/  operations/  leaving/  reference/
favicon.svg  logo/  .gitignore
```

## Deploying on Mintlify

1. Push this folder as the root of the GitHub repo `thehealinghaven/employee-handbook` (default branch `main`). Mintlify refuses a repo whose default branch has no `docs.json` at the root, so the first push must include it.
2. In the Mintlify dashboard, connect the repo (Settings → Deployment → Git settings) and install the Mintlify GitHub App. Deploys happen on push to the configured branch; PRs get preview builds.
3. Local preview: `npm i -g mint` then `mint dev` in this folder. `mint validate` checks the nav schema; `mint broken-links` checks internal links. (The old `mintlify` package is deprecated; uninstall it if present.)
4. Replace `logo/light.svg` and `logo/dark.svg` with the real wordmark, or remove the `logo` block from `docs.json`.
5. Custom domain (likely `team.helendelovely.com`) is set in the Mintlify dashboard, not in this repo. No domain is hardcoded anywhere in the content.

**Access:** This manual contains no client information, but it does describe internal procedures. Keep the repo private and, on Mintlify, put the site behind authentication before sharing the URL with the team.

## Editing content

- One page per `.mdx` file. Plain CommonMark bodies: no JSX components, no HTML comments (`<!-- -->` breaks MDX; use `{/* */}` if you must).
- Every page has frontmatter with `title`, `sidebarTitle`, `description`, and `icon` (Lucide icon names; `docs.json` sets `icons.library` to `lucide`).
- **No `#` H1 in the body.** Mintlify renders the frontmatter `title` as the H1. Sections start at `##`. Never skip a heading level.
- Blank line before every list and after every heading.
- Internal links: root-relative, no extension: `[text](/privacy-and-security/breach-and-incident-reporting)`.
- Callouts are blockquotes with a bolded lead. Three are used:
  - `> **Important.**` for rules with consequences
  - `> **Why.**` for reasoning
  - `> **Not yet set.**` for undecided policy (see below)
- Adding a page: create the file, add it to **both** `docs.json` and `nav.yaml`, add a changelog line.
- Removing or renaming a page: update both nav files and grep for links to the old slug.

### Callout conversion (optional)

If you want native Mintlify callouts later, this is the mapping. Do it with a script, not by hand, and keep the blockquote form in the source if you ever want to move platforms.

| Blockquote | Mintlify | Starlight |
|---|---|---|
| `> **Important.** text` | `<Warning>text</Warning>` | `:::caution\ntext\n:::` |
| `> **Why.** text` | `<Info>text</Info>` | `:::note\ntext\n:::` |
| `> **Not yet set.** text` | `<Note>text</Note>` | `:::tip\ntext\n:::` |

## Open items

Undecided policy is marked inline:

```markdown
> **Not yet set.** What's undecided. Owner: Name. Needed before X. — `OPEN-2026-09-03-NN`
```

Every marker is collected in `reference/open-items.mdx`. To resolve one: update the page, remove the callout, move the row to "Resolved" with the date, and add a changelog line. Check nothing was missed:

```
grep -rn "OPEN-2026" --include=*.mdx . | grep -v reference/open-items
```

## Attorney review before adoption

This manual is a strong draft, not legal advice. A Utah employment attorney should review these before it's adopted. Each one is a place where being wrong costs more than the review.

1. **Time-off model and the FLSA salary basis.** The practice has no PTO bank; exempt clinicians can bank days by working a fifth day, take up to four days on credit, and take unpaid time only in full-week blocks. Confirm the banked-day and credit mechanics can't be read as improper deductions under 29 CFR § 541.602, and that "days on credit settled by schedule, never by deduction" holds at separation. `pay-and-time-off/time-off-and-the-four-day-week.mdx`, `leaving/final-pay.mdx`.
2. **Benefits elections model.** Cash allowance by default; elective benefits deducted pre-tax under a Section 125 plan with a 10% (or provider pass-through) administration fee charged to the employee. Confirm: the plan document requirement, whether an employer-charged admin fee is permissible and how it's characterized, Utah Code § 34-28-3(6) authorization form, the $684 floor guard. Accountant and attorney both. `pay-and-time-off/benefits-elections.mdx`, `pay-and-time-off/benefits-allowance.mdx`.
3. **Exempt classification duties test.** Base salaries clear $684/week on base alone. Social workers are not a listed example in 29 CFR § 541.301 and § 541.600(e) expressly denies them the no-salary-test carve-out; confirm the learned-professional analysis holds for a supervised CSW. `employment/employment-classifications.mdx`.
4. **At-will and acknowledgment language.** Confirm the at-will statement, the acknowledgment page, and the "steps aren't a contract" language in corrective action don't create contractual obligations. `employment/at-will-employment.mdx`, `acknowledgment.mdx`, `leaving/corrective-action.mdx`.
5. **FCRA background-check flow.** Vendor is expected to be the one integrated with Gusto (Checkr). Confirm the disclosure form is standalone, the authorization wording, the pre-adverse waiting period, and the Utah § 34-46-201 timing. `employment/background-checks.mdx`.
6. **Records retention schedule.** Confirm R156-60e-502.1(10)(d) 10-year rule, the practice's minors policy (age 28) since no Utah rule exists, and interaction with HIPAA's 6-year documentation rule. `privacy-and-security/records-retention.mdx`.
7. **NLRA Section 7 and workplace rules.** Stericycle (2023) is still the NLRB standard as of September 2026 and a generic savings clause does not cure an overbroad rule. Review confidentiality, social media, civility, and internal-messaging rules for narrowness. NLRB's jurisdictional standard for healthcare offices is $250,000 gross annual volume. `conduct/your-rights-at-work.mdx`, `conduct/code-of-conduct.mdx`, `privacy-and-security/social-media.mdx`, `privacy-and-security/devices-mobile-and-texting.mdx`.
8. **Utah 2025 and 2026 session changes.** SB 86 (2025) amended § 34A-5-114 (confidentiality clauses about sexual harassment void), with a further version effective January 1, 2027. HB 130 (2026) bars requiring employees to pay for employer-required medical exams; enrolled text not read this session. Confirm neither touches the manual. `conduct/anti-harassment.mdx`, `employment/background-checks.mdx`.
9. **PLLC operating rules.** Utah Code § 48-3a-1101 et seq. renumbers to Title 16, Chapter 20 on October 1, 2026 (SB 41). Confirm the manual's statements about licensed-only services and unlicensed staff, and the R156-60e-305.1(3) supervisor-independence language for an owner supervising employee CSWs. `welcome/who-we-are.mdx`, `clinical-practice/scope-of-practice.mdx`, `employment/clinical-supervision.mdx`.
10. **Payer contract compliance obligations.** Whether Medicaid managed-care or commercial contracts impose FWA or compliance training beyond federal minimums at our size. The manual does not imply Medicaid claims are being submitted today. `operations/billing-basics-for-clinicians.mdx`.
11. **Crisis protocol, no-after-hours policy, and mandatory reporting pages.** Not legal drafting questions, but the highest-consequence pages. Helen reads all three personally. A clinical-risk consultant or attorney confirms the duty-to-warn procedure matches § 78B-3-502 as applied and that the informed consent matches the no-after-hours position. `clinical-practice/crisis-and-safety-protocol.mdx`, `clinical-practice/emergency-and-after-hours-coverage.mdx`, `clinical-practice/mandatory-reporting.mdx`.
12. **Pregnancy accommodation notice.** Utah Code § 34A-5-106(7)(e) requires the notice in the handbook at 15+ employees; the accommodations page carries it now. Confirm wording. `employment/accommodations.mdx`.

Closed since v1.0: the pay-notice-at-hire cite (it is Utah Code § 34-28-4, now cited); non-solicitation (the practice decided not to use one); health stipend tax treatment (folded into item 2).

## Compliance verification 2026-09-03

Every cite in the manual was re-verified on September 3, 2026 against primary sources (statute text, eCFR, or the agency's own page). Re-verify before publishing any later version. Items marked "changed" moved in 2025 or 2026.

### Federal

| Fact | Cite | Status |
|---|---|---|
| Exempt salary floor $684/week; 2024 increase vacated; DOL technical amendment restored 2019 text May 15, 2026 | 29 CFR § 541.600; 91 FR 27833 | changed 2026 |
| Learned-professional duties test; social workers not a listed example; no-salary-test carve-out excluded for social workers | 29 CFR § 541.301, § 541.600(e) | verified |
| Salary basis: full salary for any week with work; full-week absences unpaid; partial-week deductions prohibited outside § 541.602(b) | 29 CFR § 541.602 | verified |
| Overtime over 40; records; federal and Utah minimum wage $7.25 | 29 USC §§ 206, 207; 29 CFR Part 516; Utah Code § 34-40-103 | verified |
| Intern primary-beneficiary test | DOL Fact Sheet #71 | verified |
| Title VII, ADA, GINA at 15 employees; ADEA at 20; ADA interactive process | 42 USC § 2000e(b); § 12111(5); 29 USC § 630(b); 29 CFR § 1630.2(o)(3) | verified |
| PWFA at 15 employees; EEOC rule in force except elective-abortion accommodation (vacated W.D. La. May 2025); NPRM narrowing the rule expected late 2026 | 42 USC § 2000gg; 29 CFR Part 1636 | caution |
| PUMP Act: breaks and space for 1 year; all FLSA employers; under-50 undue-hardship exemption only | 29 USC § 218d | verified |
| USERRA, no size threshold | 38 USC §§ 4303, 4311, 4312, 4334 | verified |
| FCRA: standalone disclosure, authorization, pre-adverse and adverse action | 15 USC § 1681b(b), § 1681m(a) | verified |
| Form I-9: Section 2 within 3 business days; retention 3 years/1 year; use only the edition expiring 05/31/2027 | 8 CFR § 274a.2 | changed 2026 |
| EPPA | 29 USC § 2001 et seq. | verified |
| NLRA § 7; Stericycle (2023) still the standard; savings clause doesn't cure; healthcare-office jurisdiction $250,000 | 29 USC §§ 157, 158; 372 NLRB No. 113 | verified; exposed to Board change |
| OSHA general duty; recordkeeping partial exemption at 10 or fewer and NAICS 6213/6214 low-hazard; fatality/hospitalization reporting still required | 29 USC § 654; 29 CFR §§ 1904.1, 1904.2, 1904.39 | verified |
| FMLA at 50; COBRA at 20 with a group plan; Utah continuation is a group-policy mandate | 29 USC § 2611; 29 USC § 1161; Utah Code § 31A-22-722 | verified |
| Federal posters: FLSA, OSHA, EPPA, USERRA; EEOC at 15; FMLA at 50 | DOL Poster Advisor | verified |
| Exclusion screening: § 455.436 binds the state agency; provider duty from Utah Medicaid manual and OIG 2013 bulletin; CMP exposure | 42 CFR § 455.436; 42 USC § 1320a-7a(a)(6) | verified, scope corrected |
| FCA written-policy mandate at $5M Medicaid | 42 USC § 1396a(a)(68) | verified |
| HIPAA training, sanctions, 6-year documentation, breach notification 60 days, under-500 annual log; Security Rule NPRM (Jan 2025) still not final | 45 CFR §§ 164.530, 164.308, 164.316, 164.400-414 | verified |
| 42 CFR Part 2 applies to programs holding themselves out as SUD providers; compliance date Feb 16, 2026 passed | 42 CFR § 2.11 | verified |

### Utah employment

| Fact | Cite | Status |
|---|---|---|
| Semimonthly pay within 10 days of period close | Utah Code § 34-28-3(1) | verified |
| Notice of pay rate and payday at hire and before changes | Utah Code § 34-28-4 | verified (corrected from v1.0) |
| Deductions only by law, court order, or express written authorization; itemized | Utah Code § 34-28-3(6); R610-3-18, -20 | verified |
| Final pay: 24 hours if employer separates; next regular payday on resignation | Utah Code § 34-28-5 | verified |
| Pay records 1 year (hourly); federal 3 years | Utah Code § 34-28-10; 29 CFR Part 516 | verified |
| Antidiscrimination Act at 15 employees; protected classes incl. sexual orientation and gender identity; 180-day UALD filing | Utah Code §§ 34A-5-102, -106, -107 | verified (SB 86 2025 kept the threshold) |
| Pregnancy, childbirth, breastfeeding accommodation; handbook notice required | Utah Code § 34A-5-106(1)(g), (7) | verified (corrected from (6)) |
| Off-duty religious, political, personal expression protected | Utah Code § 34A-5-112 | verified |
| Healthcare non-compete ban effective May 6, 2026; CSW/LCSW/mental health therapists covered; non-solicit allowed but patient-notice clause void; fee-shifting | Utah Code §§ 34-51-102, -201, -202, -203, -301 (HB 270) | changed 2026 |
| Workers' comp coverage; report to carrier within 7 days; employee 180-day notice; Form 122 | Utah Code §§ 34A-2-201, -407; R612-200-1 | verified (7-day rule is in the rule, not the statute) |
| UOSH; poster | Utah Code § 34A-6-201; R614-1-6 | verified |
| New-hire reporting within 20 days | Utah Code § 35A-7-104 | verified |
| Voting leave 2 hours | Utah Code § 20A-3a-105 | verified |
| Jury duty protection; can't force use of leave; no pay mandate | Utah Code § 78B-1-116 | verified |
| Firearms locked in vehicles | Utah Code § 34-45-103 | verified |
| Internet Employment Privacy Act | Utah Code § 34-48-201 | verified |
| Employment Selection Procedures Act (SSN/DOB/DL timing) | Utah Code § 34-46-201 | verified (sunset flag 7/1/2027) |
| Drug and Alcohol Testing Act: written policy required for testing | Utah Code §§ 34-38-3, -6, -7 | verified |
| No paid sick mandate; municipalities preempted | Utah Code § 10-8-84.5 | verified |
| UI coverage at first employee; poster | Utah Code § 35A-4-203 | verified |
| E-Verify at 150 employees; chapter contingently repealed by July 1, 2027 | Utah Code § 13-47-201 | verified |
| No adult meal/rest break mandate | R610-2-3 (minors only); Labor Commission FAQ | verified |
| Required Utah posters: workers' comp, UOSH, UI, pregnancy (updated June 2024) | Utah Labor Commission; DWS | verified |
| HB 130 (2026): employer-required medical exam costs | enrolled text not read | on attorney list |

### Utah licensing and entity

| Fact | Cite | Status |
|---|---|---|
| PLLC provides professional services only through licensed individuals; unlicensed staff permitted for non-licensed work; members licensed-only; automatic conversion if no licensed member | Utah Code §§ 48-3a-1105, -1107, -1109, -1112 (renumbered to Title 16, Ch. 20 eff. Oct 1, 2026, SB 41) | changed 2026 |
| Practice of mental health therapy defined; clinical supervisor defined with Jan 1, 2027 deadline | Utah Code § 58-60-102(17), (4) | changed 2026 |
| Mental health unprofessional conduct list (incl. unlicensed assistants, client notice); general unprofessional conduct; unlawful to employ unlicensed person to practice | Utah Code § 58-60-110; § 58-1-501 | verified (58-60-109 is unlawful conduct) |
| LCSW: 1,200 direct client care hours incl. 100 supervision, 25 direct observation, max 25 group; 3,000 hours or two years only where Medicare requires; 2 hrs suicide prevention | Utah Code § 58-60-205(1) (2025) | verified |
| CSW practices only under supervision | Utah Code § 58-60-202(3) | verified |
| R156-60e (eff. Jan 1, 2026; amended May 26, 2026): supervisor approval -305.1; training -306.1; contract incl. AI-use plan -307.1; supervisor duties -308.1; supervisee 30-day filings -309.1; records 10 years -502.1(10)(d); NASW Code incorporated -502.2; CE 40 hrs -402.1; students' hours don't count -304.1 | Utah Admin. Code R156-60e | changed 2026 (replaces R156-60, -60a) |
| No Utah rule for minors' records; no delegation rule in R156-60e | R156-60e (searched) | verified by absence |
| Duty to warn | Utah Code § 78B-3-502 | verified |
| Child abuse reporting; penalty; DOPL complaint; DCFS 1-855-323-3237 | Utah Code §§ 80-2-602, -609 | verified |
| Vulnerable adult reporting; APS 1-800-371-7897 | Utah Code § 26B-6-205 | verified |
| Telehealth: same standard of care; Utah license; identity and location each encounter; informed consent | Utah Code § 26B-4-704; R156-1-602 | verified |
| Social Work Licensure Compact enacted; no multistate licenses issued as of May 2026 FAQ | Utah Code Title 58, Ch. 60b; swcompact.org | verified |
| Suicide prevention training 2 hrs per renewal | Utah Code § 58-60-105(3); R156-60e-402.1 | verified |
| NASW Code of Ethics 2021 incorporated | R156-60e-502.2 | verified |
| Utah Medicaid manual: monthly OIG checks, 5-year records, fraud reporting; PRISM is the enrollment system | Utah Medicaid Provider Manual Section I (July 2026) | verified |

## Relationship to the SOP library

The manual states policy; SOPs state procedure. Where they overlap, the manual links to the SOP. If you find a conflict, fix it in both rather than letting one silently win. The SOP library lives on the Operations shared drive (`Standard Operating Procedures/`), authored on HD at `Admin/Operations/SOPs/` until the Drive migration completes.

## Source of truth

Authored on HD at `Admin/Operations/Employee_Manual/`, mirrored to the Operations shared drive under `Human Resources/Employee Handbook/employee-handbook/` (the git clone), and pushed to the GitHub repo. Until the repo is live, HD is the working copy per the workspace's CLAUDE.md. Once the repo is live, the repo becomes the source of truth and HD/Drive become mirrors; note that switch in the workspace DECISIONS log when it happens.
