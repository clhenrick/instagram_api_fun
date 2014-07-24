# Instagram Mapping Notes

## Resources used
* [Temboo](https://temboo.com)
* [Instagram API](http://instagram.com/developer/)
* [JQuery](http://api.jquery.com/)
* [Leaflet](http://leafletjs.com/)
* [MapBox](http://mapbox.com/)

## To Do
* replace jquery cloning with underscore templating
* ~~look into mapping data with Leaflet JS and~~ having photos appear in pop-ups.
* Use Node JS for real time updates?
* allow for users to search for a geographic area and then show photos for that area.
  * potentially filter by hashtag / keyword

### technical
- compute bounds of tiles and return photos within a tile's bounds
- or compute bounding box of markers and fit to map area on init
  - then link photos to markers somehow
- improve the UI: 
   - have map and photos next to each other?
   - add title, nave, footer, other elements...

## Notes

### location/search
* oakland: 37.804444, -122.270833 

`https://api.instagram.com/v1/locations/search?lat=37.804444&lng=-122.270833&access_token=11799771.95118f4.a53e2bd3820941988ee87c4bfafef4db`


### Real Time photo updates
* read the [documentation](http://instagram.com/developer/realtime/) (to do)

#### create a subscription:
* ~~q: what's a verify token?~~	
* `object` is the type of subscription

```
curl -F 'client_id=CLIENT-ID' \
     -F 'client_secret=CLIENT-SECRET' \
     -F 'object=user' \
     -F 'aspect=media' \
     -F 'verify_token=myVerifyToken' \
     -F 'callback_url=http://YOUR-CALLBACK/URL' \
     https://api.instagram.com/v1/subscriptions/
```

#### to create a geography subscription:

```
 curl -F 'client_id=95118f4fdf914f4895c51c11e0d08fd0' \
      -F 'client_secret=50ef1268ec6744ac8fbe17eb9b19944c' \
      -F 'object=geography' \
      -F 'aspect=media' \
      -F 'lat=37.804444' \
      -F 'lng=-122.270833' \
      -F 'radius=1000' \
      -F 'callback_url=https://boris.temboolive.com/callback/instagram' \
      https://api.instagram.com/v1/subscriptions/
```

#### to see your current subscriptions: 

`https://api.instagram.com/v1/subscriptions?client_secret=<secret_key>&client_id=<client_id>`