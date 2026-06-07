# Dankort Øremærket — Kampagnesite (eksamensversion)

Kampagnesite udviklet som eksamensprojekt på Erhvervsakademi København, 2. semester multimediedesign, 2026.

Kampagnen retter sig mod 18–28-årige danskere og har til formål at skabe interesse for Dankort Øremærket — et initiativ hvor Dankort donerer 1 øre til Den Danske Naturfond ved hver betaling med Dankort.

## Deployed site

[kampagnesiteeksamensversion.netlify.app](https://kampagnesiteeksamensversion.netlify.app/)

Dette er version 2 af kampagnesitet, udviklet som en revideret eksamensversion. En tidligere version findes på [oeremaerket-2026.netlify.app](https://oeremaerket-2026.netlify.app) og kan blive taget ned efter mundtlig eksamen.

## Branch-strategi

| Branch | Formål                                          |
| ------ | ----------------------------------------------- |
| `main` | Produktionsversion — deployet på Netlify        |
| `dev`  | Udviklingsgren — merget ind i `main` ved deploy |

## Tech stack

- [Astro](https://astro.build/) — komponentbaseret statisk site generator med mobilfirst tilgang og 1024px breakpoint
- [Supabase](https://supabase.com/) — PostgreSQL database med `natursteder` tabel og Storage til billeder
- [Netlify](https://www.netlify.com/) — deployment og hosting
- [Adobe Firefly](https://firefly.adobe.com/) — AI-genereret videoindhold til hero-sektion og billeder på sitet

## Projektstruktur

```
/
├── public/
│   ├── images/
│   │   ├── collage/        # Kollage-elementer og baggrundsbilleder
│   │   ├── natursteder/    # Naturstedsbilleder
│   │   └── ui/             # UI-elementer som logo
│   └── video/
│       ├── hero-desktop.mp4
│       └── hero-mobil.mp4
├── src/
│   ├── components/
│   │   ├── Accordeon.astro
│   │   ├── BestilPopup.astro
│   │   ├── CitatKort.astro
│   │   ├── CtaKnap.astro
│   │   ├── Footer.astro
│   │   ├── Header.astro
│   │   ├── HeroSektion.astro
│   │   ├── HvadErSektion.astro
│   │   ├── InfoSektion.astro
│   │   ├── KortKarrusel.astro
│   │   ├── KortSektion.astro
│   │   ├── Layout.astro
│   │   ├── PartnerskabsSektion.astro
│   │   ├── SamarbejdsSektion.astro
│   │   ├── VaerdiCard.astro
│   │   ├── VaerdiFilter.astro
│   │   └── VaerdiSektion.astro
│   ├── lib/
│   │   └── supabase.js
│   ├── pages/
│   │   ├── index.astro
│   │   ├── overblik.astro
│   │   └── natursted/
│   │       └── [slug].astro
│   └── global.css
```

## Kom i gang lokalt

Kræver Node.js 18 eller nyere. Tjek din version med `node -v`.

```sh
# Installer dependencies
npm install

# Start udviklingsserver
npm run dev

# Byg til produktion
npm run build

# Forhåndsvis produktionsbuild
npm run preview
```

Udviklingsserveren starter på `http://localhost:4321`

## Environment variables

Opret en `.env` fil i roden af projektet:

```
PUBLIC_SUPABASE_URL=din-supabase-url
PUBLIC_SUPABASE_ANON_KEY=din-anon-nøgle
```

Projektet er koblet op på en privat Supabase-instans. Hvis du vil køre sitet lokalt skal du oprette dit eget Supabase-projekt på [supabase.com](https://supabase.com) og selv oprette en `natursteder` tabel — se Database-sektionen nedenfor for tabelstruktur og RLS-opsætning.

Nøglerne til dit eget projekt finder du i Supabase dashboard under **Project Settings → API**.

> ⚠️ Sørg for at `.env` er listet i `.gitignore` inden du pusher. Tjek med `cat .gitignore`.

Til deployment på Netlify skal de samme variable sættes i **Site configuration → Environment variables** i Netlify dashboard.

## Database

Projektet bruger Supabase med en `natursteder` tabel der indeholder 20 fiktive natursteder. Row Level Security (RLS) er aktiveret med en `Allow public read` policy der tillader anonyme brugere at læse data.

### Tabelstruktur: `natursteder`

| Kolonne            | Type                     | Påkrævet | Beskrivelse                                 |
| ------------------ | ------------------------ | -------- | ------------------------------------------- |
| `id`               | bigint                   | ja       | Primærnøgle, auto-genereret                 |
| `titel`            | text                     | nej      | Naturstedets navn                           |
| `region`           | text                     | nej      | Dansk region                                |
| `underrubrik`      | text                     | nej      | Kort beskrivelse til kort og listevisning   |
| `brodtekst`        | text                     | nej      | Længere beskrivende tekst                   |
| `unik_natur`       | text                     | nej      | Hvad gør stedet unikt naturmæssigt          |
| `dankort_hjaelper` | text                     | nej      | Hvordan Dankort-midler støtter stedet       |
| `naturoplevelser`  | text                     | nej      | Oplevelser på stedet                        |
| `natur_fakta`      | text                     | nej      | Faktaboks-indhold                           |
| `areal`            | text                     | nej      | Størrelse i relevant enhed                  |
| `oekonomi`         | text                     | nej      | Økonomi og finansiering                     |
| `partnere`         | text                     | nej      | Samarbejdspartnere                          |
| `created_at`       | timestamp with time zone | nej      | Auto-genereret ved oprettelse               |
| `slug`             | text                     | nej      | URL-venligt navn til `[slug].astro` routing |
| `koordinat_x`      | numeric                  | nej      | Longitude til SVG-kort                      |
| `koordinat_y`      | numeric                  | nej      | Latitude til SVG-kort                       |
| `billede`          | text                     | nej      | Filnavn til billede i Supabase Storage      |

Billeder ligger i Supabase Storage — opret en bucket kaldet `billeder` med public adgang og upload billeder med filnavne der matcher `billede`-kolonnen.

## Bemærkning om AI-genereret indhold

Videoindholdet i hero-sektionen, billeder på sitet og i supabase storage er udelukkende produceret i uddannelsesøjemed med generativ AI i Adobe Firefly og må ikke anvendes kommercielt eller reproduceres. De portrætterede personer i video og billedmateriale på sitet er AI-genereret.

## Licens

Projektet er udviklet i uddannelsesøjemed på Erhvervsakademi København og må ikke anvendes kommercielt. Se også bemærkningen om AI-genereret indhold ovenfor.
