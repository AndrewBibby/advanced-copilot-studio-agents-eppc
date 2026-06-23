# Lab 0 — Environment Setup

> **Do this before the workshop.** It takes ~20–30 minutes total, split into short exercises (none longer than 20 min), and removes the single biggest source of delay on the day. If you hit a blocker, note where you got stuck and bring it — we'll triage at the start of the session.

## Objective

Provision the two free pieces you'll build on all day:

1. A **Power Apps Developer Plan** environment that includes **Microsoft Dataverse** (you'll need this for the MCP and tools labs).
2. A **Copilot Studio trial** so you can create and test agents.

By the end you'll be able to open Copilot Studio, create a new agent, and see your own developer environment in the environment picker.

## What you'll have at the end

- A work/school (Microsoft Entra) account you can sign in with.
- A developer environment with a Dataverse database (e.g. *"Your Name's environment"*).
- Access to **copilotstudio.microsoft.com** with a trial licence, able to create and test (not publish) agents.

---

## Prerequisites & key facts

- **Account type matters.** The trial and Developer Plan sign-up flows **reject personal email addresses** (outlook.com, hotmail.com, gmail.com, etc.). You need a **work or school account** backed by Microsoft Entra ID. If you don't have one, use the **Microsoft 365 Developer Program** workaround in the appendix to get a free tenant.
- **Browser.** Use a current Chrome (91+), Edge, Firefox (89+) or Safari (16.4+). **Avoid InPrivate/Incognito** for sign-up — it can break the flow.
- **The Copilot Studio trial lets you *create and test* agents but *not publish* them.** That's fine for every lab in this workshop. The trial runs 30 days, can be extended by 30, and your agent keeps working up to 90 days after expiry.
- **Admin can block self-service sign-up.** If your organisation has disabled "viral" sign-ups, you'll get an error — ask your IT admin to enable it, or use a personal dev tenant (appendix).

> ⚠️ **Never enter real production credentials, customer data or secrets into trial environments.** Treat everything you build today as throwaway.

---

## Exercise A — Power Apps Developer Plan + Dataverse (≈ 10 min)

The Developer Plan gives you a **free** environment with Power Apps, Power Automate and Dataverse, kept as long as you actively use it (it is *not* for production).

1. Open the Developer Plan sign-up page: **https://aka.ms/PowerAppsDevPlan**
   (equivalently: <https://www.microsoft.com/power-platform/products/power-apps/free>).
2. Select **Start free / Sign up**, enter your **work or school email**, and follow the prompts.
   - If your email isn't recognised as a work/school account, you'll be offered to create a free Microsoft Entra account — accept and complete it, or jump to the appendix.
3. After sign-up you're redirected to **https://make.powerapps.com**. A developer environment is created automatically, named after you (e.g. *"Jane Doe's environment"*).
4. **Confirm the environment exists.** In the top-right of make.powerapps.com, open the **environment picker** and select your developer environment.
   - Provisioning can take a couple of minutes. You can watch progress in the **Power Platform admin center** at <https://admin.powerplatform.microsoft.com> → **Environments**.

### Verify Dataverse is present

1. In **make.powerapps.com**, with your developer environment selected, expand **Dataverse** in the left navigation and choose **Tables**.
2. You should see standard tables (Account, Contact, etc.). If you can list tables, Dataverse is ready. ✅

> **Alternative (if the Developer Plan is blocked):** create a 30-day **Trial** environment with a database directly in PPAC — go to <https://admin.powerplatform.microsoft.com> → **Environments** → **New** → set type **Trial**, toggle **Create Database = Yes**, and (optionally) **Deploy sample apps and data = Yes** → **Save**.

---

## Exercise B — Copilot Studio trial (≈ 5 min)

1. Go to the Copilot Studio sign-up: **https://aka.ms/TryCopilotStudio**
   (equivalently the licensing doc's sign-up link, or just <https://copilotstudio.microsoft.com> and sign in).
2. Enter your **work or school email** → **Next**, and follow the instructions. Your free trial starts when sign-up completes.
3. When Copilot Studio opens, **check the environment selector** (top-right) and switch to your **developer environment** from Part A so your agents and Dataverse live together.

### Verify you can build

1. In Copilot Studio select **Create** → **New agent**.
2. Give it a name (e.g. `Lab Smoke Test`). **Before saving for the first time**, confirm the **Solution** and **language** are set the way you want — this is still buggy if left to default.
3. Open the **Test** panel on the right and send a message (e.g. "hello"). If the agent replies, you're ready. ✅
4. You can delete this smoke-test agent afterwards.

---

## Exercise C (recommended, not required) — turn on a Managed Environment (≈ 5 min)

Several Module 3 governance features (sharing controls, pipelines, solution-checker enforcement) and the **Dataverse MCP server** in Lab 2 work best with **Managed Environments** and **generative orchestration** enabled. If you have admin rights on your dev tenant:

1. In **PPAC** → **Environments**, select your developer environment → **Enable Managed Environments**.
2. In **Copilot Studio** → your agent → **Settings**, confirm **Generative orchestration** is on (it's the default in the new experience).

If you don't have admin rights, skip this — we'll cover what it unlocks during Module 3 and provide a shared environment for the MCP exercise if needed.

---

## Completion checklist

- [ ] I can sign in with a **work/school (Entra) account**.
- [ ] I have a **developer environment** visible in the environment picker.
- [ ] I can list **Dataverse tables** in that environment.
- [ ] I can open **copilotstudio.microsoft.com** with my trial.
- [ ] I created a **test agent** and got a reply in the Test panel.
- [ ] *(Optional)* Managed Environment enabled / generative orchestration confirmed.

---

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| "We can't sign you up" / email rejected | You used a personal email (gmail/outlook/hotmail). | Use a work/school account, or create a free tenant via the **Microsoft 365 Developer Program** (appendix). |
| "Sign-up couldn't be completed" | Your org admin disabled self-service ("viral") sign-up. | Ask IT to enable Copilot Studio sign-up, or use a separate dev tenant. |
| No developer environment appears | Provisioning still in progress, or wrong environment selected. | Wait a few minutes; check PPAC → Environments; switch environments in the top-right picker. |
| Dataverse / Tables not visible | Environment has no database. | Use the PPAC **Trial environment with Create Database = Yes** alternative in Part A. |
| Sign-up loops or fails | InPrivate/Incognito or stale cookies. | Use a normal browser window; clear cookies for `microsoft.com`; try a different supported browser. |
| Can't open Power Platform admin center | Signed in with a Microsoft Account (not Entra). | PPAC requires an Entra identity — use the work/school account, not a personal MSA. |

---

## Appendix — no work/school account? Use the Microsoft 365 Developer Program

If you don't belong to an organisation tenant, get a **free Microsoft 365 developer tenant** (includes Entra ID, so the Developer Plan and Copilot Studio sign-ups will accept it):

1. Go to **https://developer.microsoft.com/microsoft-365/dev-program** and join.
2. Set up the instant sandbox; you'll receive an admin account like `you@yourtenant.onmicrosoft.com`.
3. Use **that** account for Part A and Part B above.

> The developer tenant is for learning/testing only — perfect for this workshop, not for production.

---

## Reference links

- Get access to Copilot Studio (trial): <https://learn.microsoft.com/microsoft-copilot-studio/requirements-licensing-subscriptions>
- Sign up for Copilot Studio as an individual: <https://learn.microsoft.com/microsoft-copilot-studio/sign-up-individual>
- Create a developer environment (Power Apps Developer Plan): <https://learn.microsoft.com/power-platform/developer/create-developer-environment>
- Explore Power Apps free for 30 days: <https://learn.microsoft.com/power-apps/maker/signup-for-powerapps>
- Power Platform admin center: <https://admin.powerplatform.microsoft.com>
- Microsoft 365 Developer Program: <https://developer.microsoft.com/microsoft-365/dev-program>

➡ Next: **[Lab 1 — Refine prompts at agent & topic level](lab-01-refine-prompts.md)**
