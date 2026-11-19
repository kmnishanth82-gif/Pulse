# V-Star PPMS (PWA – same architecture as QA Inspector)
Static PWA (GitHub Pages) + Google Apps Script + Google Sheets. No servers, no AI services, no paid hosting.

## Setup
1. Open your PPC Google Sheet (tab `INHOUSE-NEW-1-11-26`). Extensions > Apps Script. Paste `Code.gs`.
2. Run `setup()` once (authorise). It creates the tabs USER_MASTER, DAILY_PRODUCTION, VERIFICATION_LOG, PLAN_REVISION_HISTORY, AUDIT_LOG and adds a unique `Order ID` column to the planning tab.
3. Add users: in the editor run e.g. `addUser("planning1","Planning Admin","planning","","4821")`, `addUser("line2","Line 2 Supervisor","inhouse","Line 2","1357")`, `addUser("jwa","JW-A Coordinator","jobwork","JW-A","2468")`, `addUser("mgmt","Management","management","","9753")`. Unit must equal the planning sheet's `Line No` value exactly. Delete the PIN from the code after running.
4. Deploy > New deployment > Web app > Execute as: Me, Access: Anyone. Copy the URL, paste it into `API` at the top of the script in `index.html`.
5. Create a GitHub repo, upload `index.html`, `manifest.json`, `sw.js`, `icon.svg`. Settings > Pages > deploy from main branch. Open the link on a phone and use "Add to Home screen".

## Check with Planning before use
- Sheet dates should be real dates or `yyyy-MM-dd`; other text formats are shown as-is.
- A planning row counts as Delivered only if `Final Delivery to Pkg` has a value.
- Production users see only rows whose `Line No` equals their unit. All checks run in the script, not the browser.
- Not built yet: dispatch/receipt, capacity, delay analysis, exports, notifications.
## Security note
"Anyone" access is how Apps Script web apps work; the script requires a login token for every action and PINs are stored hashed. Do not put real data in a public sheet; keep the sheet private.

## Update: job-work dispatch & receipt
If you already deployed an earlier version: paste the new `Code.gs`, run `setup()` again (adds the JOBWORK_TRACKING tab; nothing is overwritten), then Deploy > Manage deployments > Edit > New version > Deploy. Replace `index.html` in GitHub and refresh the app twice.
Job-work units are the units assigned to users with the `jobwork` role, so their unit name must match the planning sheet's `Line No` exactly.
