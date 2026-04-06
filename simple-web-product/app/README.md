# App

This directory will hold a **single** web application (no subfolders for now).

## Tech stack (planned)

- **Vite**
- **TypeScript**
- **React**
- **Radix UI** (accessible primitives)
- **Tailwind CSS** (styling)

## Goals

- Easy local dev: `npm install` + `npm run dev`
- Clean build: `npm run build`
- Simple preview: `npm run preview`
- Deployable as a static site (e.g. **GitHub Pages** or similar)

## Notes

- Keep config minimal and standard.
- Prefer boring defaults and reproducible commands so an agent can run/build reliably.
- If/when the app grows (backend, workers, etc.), we can introduce subfolders then.
