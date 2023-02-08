# WIP

## wisniowasu.pl but svelte

port of https://github.com/fastfend/homepage-wisniowasu

## Running

to make some older code work, in `/node_modules/progressive-image.js/package.json`:

- `"browser": "./dist/progressive-image.js"` -> `"main": "./dist/progressive-image.js"`
- `""` -> `"type": "module"`

```bash
git clone https://github.com/resultfulness/homepage-wisniowasu-svelte.git
cd homepage-wisniowasu-svelte
npm install

# dev server
npm run dev

# build (untested)
npm run build
```

## Backend

example backend in `/src/lib/backend/`, documentation tba
