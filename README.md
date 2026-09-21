# fortunata-uptime

Dead man's switch for the Hotel Fortunata demo, deliberately hosted **off** the Mac
that runs the OpenClaw scheduler. If that Mac dies, the local health sweep dies
silently with it — this repo keeps watching.

- **What it does:** every 6 hours, `GET https://hotel-fortunata-booking.vercel.app/hr`.
- **Pass:** HTTP 200, 307 or 308.
- **Fail:** anything else (including no answer) → the job fails → GitHub emails the
  repo owner.
- **Manual test:** Actions → *Fortunata uptime* → *Run workflow*.

No secrets, no tokens, no deploy rights. It only makes one anonymous GET.

## Keep it alive

GitHub **disables scheduled workflows after 60 days without repo activity** and
emails a warning first. If that mail arrives, push any commit (or press *Run
workflow*) to re-arm the schedule. Scheduled runs also queue on shared runners, so
treat the 6-hour cadence as approximate.
