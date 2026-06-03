# Adwaves Post-booking VSL Landing Page V2

Single-file landing page for prospects who have just booked a sales call. The page uses `index.html` with inline CSS plus the three visual proof assets in `/images/`.

## Customization checklist

Replace these placeholders before going live:

- The local MP4 URL in the video player and the Loom share URL in the fallback link.
- The SMS cancellation link currently points to `+33781574955`.
- Pass `bookingUid=BOOKING_UID` in the landing page URL to generate the Cal.com rescheduling URL: `https://cal.com/adwaves/15min?rescheduleUid=BOOKING_UID`.

The Open Graph and Twitter preview image is `images/site-preview-hero.png`.

The public GitHub Pages URL is `https://thefaon.github.io/landing-vsl/`.

## Case study images

The page uses these optimized files:

- `/images/ramzi-whatsapp-soft-rounded.webp`
- `/images/acdj-avant.webp`
- `/images/acdj-apres.webp`

Original PNG files are backed up in `/images/originals/` and excluded from Vercel deploys via `.vercelignore`.

To swap the proofs later, replace the WebP files with new optimized images using the same filenames. Keep the ACDJ before and after images in a 16:10 desktop screenshot format so the comparison slider stays clean.

## Vercel deployment

Two simple options:

- Drag and drop this folder into the Vercel dashboard as a static project.
- Or run `vercel deploy` from this folder with the Vercel CLI.

No build step is required. `index.html` is the entry point, with no Tailwind CDN or client-side CSS generation.

## Custom domain setup

In Vercel, add `rdv.adwaves.fr` as a custom domain for the project, then create the DNS record Vercel gives you at your DNS provider.

## Test URLs

- With all params: `/?firstname=Christophe&datetime=2026-05-12T14:00&phone=+33612345678&bookingUid=BOOKING_UID`
- With only firstname: `/?firstname=Christophe`
- Without any params: `/`

## Tracking note

When the page loads with a `bookingUid` URL parameter, it sends a `vsl_opened` event to the n8n webhook at `https://n8n.contactfidezy.fr/webhook/vsl_clicked`. The request body is form-urlencoded and includes `event`, `firstname`, `datetime`, `bookingUid`, `openedAt`, `url`, `referrer`, and `userAgent`.

Each page load is counted. Visits without `bookingUid` do not trigger the webhook. The `phone` URL parameter is still parsed and stored in JavaScript as `window.adwavesLeadPhone`, but it is not sent to the webhook or displayed on the page.
