Immersive scroll experience for [Tanit XR](https://tanitxr.org/) heritage models.

## Project Structure

- `index.html`: the app shell, Three.js scene, scroll behavior, QR overlay, and autoplay.
- `data/tanit-xr.png`: Tanit XR logo used in the navigation.
- `data/models/index.json`: ordered list of model metadata files.
- `data/models/<model>/metadata.json`: model title, description, scene transform, Sketchfab links, and QR path.
- `data/models/<model>/model.glb`: local model file.
- `data/models/<model>/qr.png`: optional original Sketchfab AR QR image.

## Add A Model

1. Create a new folder in `data/models/`.
2. Add `model.glb`, `metadata.json`, and optionally `qr.png`.
3. Add the metadata path to `data/models/index.json`.

## Run Locally

```bash
python3 -m http.server 4173
```

Open: <http://127.0.0.1:4173/>

## Deploy To Cloudflare Pages

1. Authenticate Wrangler:

```bash
npx wrangler login
```

2. Create a Pages project once (skip if it already exists):

```bash
npx wrangler pages project create tanitxr-site
```

3. Enable R2 once in Cloudflare Dashboard:

- Dashboard -> R2 -> Get started / Enable R2

4. Build deploy output (excludes local `model.glb` files):

```bash
./scripts/prepare-pages-dist.sh
```

5. Deploy the site:

```bash
npx wrangler pages deploy pages-dist --project-name tanitxr-site
```

The deploy command publishes static files from `pages-dist`, including
`index.html` and `data/` assets except local GLB binaries.
