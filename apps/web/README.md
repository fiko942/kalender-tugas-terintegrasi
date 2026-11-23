# Tempo — aplikasi web

Aplikasi kalender tugas akademik berbasis Next.js App Router.

## Prasyarat

- Node.js 20.9 atau lebih baru.
- Proyek Supabase dengan Auth dan database PostgreSQL.
- Deploy melalui Vercel dengan **Root Directory** disetel ke `apps/web`.

## Menjalankan lokal

```bash
cp .env.example .env.local
# Isi NEXT_PUBLIC_SUPABASE_URL dan NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY dari Supabase Dashboard
npm install
npm run dev
```

Jalankan semua migrasi secara berurutan melalui Supabase CLI atau SQL Editor:

1. `supabase/migrations/202611230001_initial_schema.sql`
2. `supabase/migrations/202611230002_reminder_processing.sql`
3. `supabase/migrations/202611230003_atomic_reminder_sync.sql`

Untuk development tanpa kredensial, halaman aplikasi menampilkan dataset demo yang hanya tersimpan sementara dalam memori browser.

## Scripts

```bash
npm run dev
npm run lint
npm run typecheck
npm test
npm run build
# Menjalankan hasil production standalone:
node .next/standalone/server.js
```

## Deployment

Buat project Vercel dari repository baru, atur root directory menjadi `apps/web`, dan set environment variables `NEXT_PUBLIC_SUPABASE_URL` serta `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY` pada environment Preview dan Production. Setelah URL deployment tersedia, tambahkan domain tersebut ke redirect URL Supabase Auth. Pengiriman notifikasi masih menunggu provider server-side yang terkonfigurasi; penjadwalan dan state idempotency sudah disiapkan dalam database.
