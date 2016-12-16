#  LiD-Online layout repo

## Tools
### Hyperlink usage
Detects invalid and inefficient links on webpages. 
hyperlink http://landschaften-in-deutschland.net -r | tee logfile.log

## Build related

After `~/lid-frontend$ npm run build` do this in the created `/dist` folder:
- `cd /dist`
- `mkdir frontend`, `cd frontend || mv img frontend/img || mv assets frontend/assets`
- `cp frontend/assets/images lid-site/static`
- `cp /dist lid-site/dist`

NOTE: Hack to ember-leaflet assets folder
All lid-frontend assets are served with prefix `frontend/`.
Ember-leaflet expects assets in an equally named folder, to hack:
Copy `lid-frontend/dist/assets/images` folder to repos `static/` folder 
