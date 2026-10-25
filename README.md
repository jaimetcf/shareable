# Shareable

Host `.html` files for signed-in users, and share each page behind a keypass.

## Local development

Postgres is expected at `DATABASE_URL`. A Neon connection string (host ending in `neon.tech`) uses the Neon serverless driver. Any other Postgres URL uses a normal Postgres connection, which is what local Docker uses.

```bash
docker run -d --name shareable-pg \
  -e POSTGRES_USER=postgres \
  -e POSTGRES_PASSWORD=postgres \
  -e POSTGRES_DB=shareable \
  -p 5432:5432 postgres:16

cp .env.example .env
# Fill in DATABASE_URL and a long random BETTER_AUTH_SECRET

npm run db:push
npm run dev
```

## Neon on Vercel

Sign in with the Vercel CLI, link this project, and add the Neon integration so `DATABASE_URL` is provisioned:

```bash
npx vercel login
npx vercel link
npx vercel integration add neon
npx vercel env pull .env --yes
```

Also set `BETTER_AUTH_SECRET` (32+ random bytes) and `BETTER_AUTH_URL` (the public app URL) for Development, Preview, and Production.


## License

MIT License

Copyright (c) 2026 Jaime Santo

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
