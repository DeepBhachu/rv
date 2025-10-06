# revrental-fullstack

**RVezy-style RV rental clone (demo)** — Next.js 14 + Tailwind + Prisma (SQLite dev) + NextAuth + API routes.

## 1) Setup
```bash
cp .env.example .env
npm install
npm run db:push
npm run seed
npm run dev
```
Open http://localhost:3000

### Demo accounts
- Host: host@example.com / password123
- Guest: guest@example.com / password123

## 2) API (examples)
- `GET /api/search?q=Toronto&type=Towable&delivery=true&maxPrice=120`
- `GET /api/rvs` — list RVs
- `POST /api/rvs` — create RV (host)
```json
{
  "hostId": "<HOST_ID>",
  "title": "Sprinter Van w/ Solar",
  "type": "Drivable",
  "description": "Off-grid capable vanlife rig.",
  "nightlyPrice": 139,
  "deliverySupported": true,
  "rules": "No smoking.",
  "lat": 43.65, "lng": -79.38,
  "address": "Toronto, ON",
  "photos": ["https://.../photo.jpg"]
}
```
- `GET /api/rvs/[id]` — get RV with photos/reviews/availability
- `PUT /api/rvs/[id]` — update RV
- `DELETE /api/rvs/[id]` — delete RV (and dependents)
- `POST /api/bookings` — quote + create booking
```json
{ "rvId":"<RV_ID>", "guestId":"<GUEST_ID>", "startDate":"2025-11-01", "endDate":"2025-11-05" }
```
- `PUT /api/bookings/[id]` — update booking status (CONFIRMED/CANCELLED/COMPLETED)
- `GET /api/messages?bookingId=<ID>` — list
- `POST /api/messages` — create

## 3) Auth (demo)
Visit `/api/auth/signin` for Credentials login (NextAuth). For production, add email/OAuth and CSRF hardening.

## 4) Payments (skeleton)
`POST /api/stripe` placeholder for:
- Create PaymentIntent for total (in cents)
- Optional security deposit hold
- Stripe Connect transfers to hosts

## 5) Notes
- SQLite for dev; switch to Postgres by changing `datasource` in `schema.prisma` + DATABASE_URL.
- Add rate limiting (Upstash/Redis) & file uploads (S3) for production.
- Geo search can be optimized with PostGIS or geohash indexing.
