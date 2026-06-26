# Lab 0 – Environment Setup

## Objective

Use your workshop-provided login, then confirm:

1. Your workshop login works.
2. You can create or access a **Power Apps Developer Plan** environment with **Dataverse**.
3. You can open Copilot Studio, select your developer environment, create an agent, and test it.

## What you'll have at the end

- A workshop-provided Microsoft Entra login you can sign in with.
- A developer environment with a Dataverse database (e.g. *"Your Name's environment"*).
- Access to Copilot Studio with permissions to create and test agents.

---

## Prerequisites & key facts

- **User Credentials**: You have already claimed your credentials for using Power Platform and creating a developer environment
  If not, the go to **https://cathrinebruvold.github.io/Workshop-Attendee-Application/** and claim a user.

---

## Exercise A – Confirm Power Apps + Dataverse access (≈ 10 min)

The Developer Plan gives each attendee a personal environment with Power Apps, Power Automate and Dataverse.

> Use your assigned workshop account (for example: `user001@eppcagents2026.onmicrosoft.com`).
> If you are an experienced user using your own work account and existing environment, validate your setup and skip sign-up steps already completed.

1. Go to **https://make.powerapps.com/** and sign in.
2. **Check whether you already have a developer environment.** In the top-right, open the **environment picker** and look for an environment labeled **"Developer"** or with a name like **"[Your Name]'s environment"**. If you see one, it's your developer environment.
3. **Only if you do not already have a developer environment:**
   - Open the Developer Plan sign-up page: **https://aka.ms/PowerAppsDevPlan**
     (equivalently: <https://www.microsoft.com/power-platform/products/power-apps/free>).
   - Select **Start free / Sign up**, enter your **work or school email**, and follow the prompts.
   - Return to **https://make.powerapps.com** and refresh until the environment appears.
   - Provisioning can take a few minutes after sign-up.
4. Select the developer environment in the environment picker.

### Verify Dataverse is present

1. In **make.powerapps.com**, with your developer environment selected, expand **Dataverse** in the left navigation and choose **Tables**.
2. You should see standard tables (Account, Contact, etc.). If you can list tables, Dataverse is ready. ✅

---

## Exercise B – Confirm Copilot Studio access (≈ 5 min)

1. Go to <https://copilotstudio.microsoft.com> and sign in with your provided workshop account.
2. Select the same developer environment you created/confirmed in Exercise A.
3. If Copilot Studio access is not enabled or the service prompts for registration, use the fallback sign-up link: **https://aka.ms/TryCopilotStudio**.

> **Troubleshooting note (Exercise B):** if Copilot Studio only shows a spinning circle, raise this with the workshop instructors. We'll tell you how to fix it by entering the environment ID in the Copilot Studio URL.

### Verify you can build

1. In Copilot Studio select **Create** → **New agent**.
2. Give it a name (e.g. `Lab Smoke Test`). Tip: check **Solution** and **language** before continuing so your agent lands in the right place.
3. Open the **Test** panel on the right and send a message (e.g. "hello"). If the agent replies, you're ready. ✅
4. You can delete this smoke-test agent afterwards.

---

## Completion checklist

- [ ] I can sign in with my **provided lab login** (or approved work login).
- [ ] I have a **developer environment** visible in the environment picker.
- [ ] I can list **Dataverse tables** in that environment.
- [ ] I can open **copilotstudio.microsoft.com** with my assigned lab login (or approved work login).
- [ ] I created a **test agent** and got a reply in the Test panel.

---

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| Copilot Studio opens but keeps spinning | Licence or session issue, wrong environment, or browser/cache issue. | Confirm Copilot Studio licence is assigned; confirm Usage location is set to **United Kingdom**; try Microsoft Edge; clear Microsoft cookies or use a fresh private window; confirm the correct developer environment is selected. |
| Copilot Studio licence missing | Workshop licence assignment did not complete for that user. | Tell the workshop team. Provided lab users should have licences assigned centrally. |
| "We can't sign you up" / email rejected | You used a personal email (gmail/outlook/hotmail) on an own-tenant path. | Use a work/school account for own-tenant setup, or switch to your provided workshop account. |
| "Sign-up couldn't be completed" | Self-service sign-up blocked in your organisation tenant. | For own-tenant setups, ask your IT admin to enable sign-up or use a different work tenant. For workshop users, contact the workshop team. |
| No developer environment appears | Developer Plan flow not completed yet, provisioning still in progress, or wrong environment selected. | Complete the Developer Plan flow, refresh make.powerapps.com, and re-check the environment picker after a few minutes. |
| Dataverse / Tables not visible | Environment selected is wrong, or database provisioning is incomplete. | Confirm the correct developer environment is selected and retry after provisioning completes. |
| Sign-up loops or fails | InPrivate/Incognito or stale cookies. | Use a normal browser window; clear cookies for `microsoft.com`; try a different supported browser. |

> If you chose to use your own work login/environment, workshop support is limited for tenant-specific issues.

---

## Reference links

- Get access to Copilot Studio (trial): <https://learn.microsoft.com/microsoft-copilot-studio/requirements-licensing-subscriptions>
- Sign up for Copilot Studio as an individual: <https://learn.microsoft.com/microsoft-copilot-studio/sign-up-individual>
- Create a developer environment (Power Apps Developer Plan): <https://learn.microsoft.com/power-platform/developer/create-developer-environment>
- Explore Power Apps free for 30 days: <https://learn.microsoft.com/power-apps/maker/signup-for-powerapps>

## Appendix – Own-tenant path (limited support)

Use this path only if you are intentionally working in your own work tenant rather than the workshop-provided login. This is an experienced-user path with limited workshop support for tenant-specific issues.

1. Use a work or school account with access to Power Apps, Copilot Studio and Dataverse.
2. Complete the Power Apps Developer Plan flow: visit <https://aka.ms/PowerAppsDevPlan>, select **Start free**, and follow the prompts to create your personal developer environment for that tenant.
3. If sign-up is blocked by your organisation, contact your IT admin or use the workshop-provided login instead.
4. Personal email accounts are not supported for this path.

➡ Next: **[Lab 1 – Instruction Tuning & Grounding](lab-01-instruction-tuning-grounding.md)**
