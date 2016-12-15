#  LiD-Online layout repo

## Tools
### Hyperlink usage
Detects invalid and inefficient links on webpages. 
hyperlink http://landschaften-in-deutschland.net -r | tee logfile.log

## Build related
### Hack to ember-leaflet assets folder
All lid-frontend assets are served with prefix `frontend/`.
Ember-leaflet expects assets in an equally named folder, to hack:
Copy `lid-frontend/dist/assets/images` folder to repos `static/` folder 
