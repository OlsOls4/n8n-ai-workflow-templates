# Send appointment reminders from Google Calendar by email 24 hours and 2 hours before, with a Sheets log

## Description (n8n listing)

Fewer no-shows using the Google Calendar you already book into, with no SMS bill. Every appointment with a client e-mail gets a friendly reminder 24 hours and 2 hours before (you choose the hours), sent once from your own Gmail, and logged to Google Sheets so nobody gets the same reminder twice. If an appointment moves, the reminders start again. Each evening you get tomorrow's list, with anyone missing an e-mail address highlighted.

## Who it's for
- Salons, barbers and beauty therapists
- Clinics, physios, dentists and therapists
- Tutors, coaches and consultants who book into Google Calendar

## How it works
1. **Every 15 minutes** reads upcoming events from your bookings calendar.
2. The client comes from `Email:`, `Name:` and `Service:` lines in the event description, or from the first guest on the event.
3. **Pick reminders due** sends the tightest reminder whose window has opened (e.g. booked 5 hours ahead = only the 2-hour reminder) and skips anything already in `Reminders`.
4. **Send reminder e-mail** sends it from Gmail; **Log the reminder** records it.
5. **Every evening at 6pm** e-mails you tomorrow's appointments.

## Setup
1. Connect **Google Calendar**, **Gmail** and **Google Sheets**.
2. Create a Google Sheet with this tab:
   - `Reminders`: `appointment_id | start | client_name | client_email | service | reminders_sent | last_reminder`
3. Fill in **Set reminder settings** (calendar ID, sheet ID, business name and address, timezone, `reminder_hours`, booking page link) and **Set agenda settings**.
4. Add `Email: client@example.com` (and optionally `Name:` / `Service:`) to each booking's description, or invite the client as a guest.
5. Put your e-mail in **Email the error**, pick this workflow under **Workflow settings > Error workflow**, and activate.

## Requirements
- n8n 2.x, cloud or self-hosted (built and import-tested on n8n 2.43.7). Built-in nodes only, no community nodes.
- A Google account (Gmail / Google Workspace). Google credentials in n8n: https://docs.n8n.io/integrations/builtin/credentials/google/

## Customisation
- Three reminders: set `reminder_hours` to `48,24,2`.
- Use a separate bookings calendar: put its ID (Calendar settings > Integrate calendar) in both settings nodes.
- Rewrite the e-mail in **Pick reminders due** (plain HTML).

## Troubleshooting
- **No reminders**: the event needs a start time (not all-day) and a client e-mail; check the calendar ID.
- **Duplicate reminders**: the `appointment_id` column must exist so the upsert can find the row.
- **Times look wrong**: set `timezone` and the workflow timezone (Workflow settings) to your business timezone.

## Import
In n8n: **Workflows > Import from File** and pick `workflow.json` (or copy the file contents and paste onto the canvas). Then follow Setup above.

## Links
- **Pro version** ($29, extra features listed on the page): https://payhip.com/b/2BrJI
- All templates: https://github.com/OlsOls4/n8n-ai-workflow-templates
