# Dankort Øremærket — Kampagnesite

Kampagnesite udviklet som eksamensprojekt på Erhvervsakademi København, 2. semester multimediedesign, 2026.

Kampagnen retter sig mod 18–28-årige danskere og har til formål at skabe interesse for Dankort Øremærket — et initiativ hvor Dankort donerer 1 øre til Den Danske Naturfond ved hver betaling med Dankort.

## Deployed site

[oeremaerket-2026.netlify.app](https://oeremaerket-2026.netlify.app)

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
│   │   ├── CtaKnap.astro
│   │   ├── SekundaerKnap.astro
│   │   ├── HeroSektion.astro
│   │   ├── HvadErSektion.astro
│   │   ├── SpoergsmaalSektion.astro
│   │   ├── SamarbejdsSektion.astro
│   │   ├── PartnerskabsSektion.astro
│   │   ├── QandASektion.astro
│   │   ├── FordeleSektion.astro
│   │   ├── BestilPopup.astro
│   │   ├── Header.astro
│   │   ├── Footer.astro
│   │   └── Layout.astro
│   └── pages/
│       ├── index.astro
│       ├── overblik.astro
│       └── natursted/
│           └── [slug].astro
└── src/styles/
└── global.css
```

## Kom i gang lokalt

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

Nøglerne finder du i Supabase dashboard under **Project Settings → API**.

## Database

Projektet bruger Supabase med en `natursteder` tabel der indeholder 20 fiktive natursteder. Row Level Security (RLS) er aktiveret med en `Allow public read` policy der tillader anonyme brugere at læse data.

## Bemærkning om AI-genereret indhold

Videoindholdet i hero-sektionen er udelukkende produceret i uddannelsesøjemed med generativ AI i Adobe Firefly og må ikke anvendes kommercielt eller reproduceres. Den portrætterede figur er en AI-genereret person.