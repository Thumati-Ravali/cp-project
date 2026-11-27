MULTI AGENT TRAVELLER PLANNER
================================

This project started as a browser-only trip planner. The backend has now been added
using Node.js and Express, and authentication and trip storage use the API.

REQUIREMENTS
------------
- Node.js 18 or newer
- npm
- Internet connection for map tiles, route services and Wikipedia photos

RUN LOCALLY
-----------
1. Extract the ZIP file.
2. Open the extracted project folder in VS Code or a terminal.
3. Install packages: npm install
4. Copy .env.example to .env.
5. Change JWT_SECRET in .env to a long random secret.
6. Start the application: npm start
7. Open http://localhost:5000 in your browser.

For development with automatic server restart, run: npm run dev

BACKEND FEATURES
----------------
- User registration and login with bcrypt password hashing.
- JWT-based authentication (7-day token expiry).
- Forgot-password flow using the user's security question and a hashed answer.
- Authenticated password changes.
- Create/update, list and delete saved trips per user.
- JSON file persistence at server/data/database.json (created automatically).
- Basic authentication rate limiting and request validation.

API ENDPOINTS
-------------
GET    /api/health
POST   /api/auth/signup
POST   /api/auth/login
GET    /api/auth/security-question?email=user@example.com
POST   /api/auth/forgot-password
POST   /api/auth/change-password  (Bearer token required)
GET    /api/auth/me              (Bearer token required)
GET    /api/trips                (Bearer token required)
POST   /api/trips                (Bearer token required)
DELETE /api/trips/:id            (Bearer token required)

NOTES
-----
- Open the site through http://localhost:5000. Do not double-click index.html;
  API requests need the Node server to be running.
- User accounts and trips are stored on the server in server/data/database.json.
  Back up this file if you need to preserve local development data.
- For production, replace JSON-file persistence with a database such as PostgreSQL
  or MongoDB, use HTTPS, configure CORS for trusted origins, and set a strong JWT_SECRET.
- Existing destination listings, route/map calculations, sample hotel/restaurant
  listings and budget estimates are retained from the original frontend.
- Hotels, restaurants and photographers are sample listings; prices are estimates.
- Leaflet is bundled in lib/. Map tiles and photos need an internet connection.


FEATURES ADDED IN THE WORLDWIDE TRAVEL UPDATE
---------------------------------------------
- Expanded curated destination catalogues: France (Paris), Italy, United Kingdom,
  Switzerland, Japan, UAE, Thailand, Singapore, United States, Australia,
  South Africa and Brazil, alongside the existing Indian destinations.
- Worldwide place search: search a city, attraction, country, state or continent.
  Search uses the OpenStreetMap Nominatim service and requires an internet
  connection. Search results can be added to the trip and displayed on the map.
  This provides global place lookup rather than claiming a complete offline
  gazetteer of every place on Earth.
- Trip date validation prevents past travel dates.
- Budget categories: Low Budget, Normal and Premium.
- Transport choices: Train, Bus, Flight, Cab, Scooter and Bike rental.
- Live-search shortcuts for flights, trains, buses, local cabs, scooters,
  bicycles and hotel rates/reviews. Flight searches include the selected origin,
  destination and trip date. Airlines such as IndiGo and Air India are examples;
  actual airline schedules, flight counts, seat inventory, prices and train
  availability are returned by the linked booking provider, not this demo app.
- Hotel room-count selector, sample room inventory and sample review text.
- Veg / Non-Veg / Both food filters, food imagery, photographer listings and
  a destination guide directory search link.
- Budget totals account for the selected room count and chosen transport type.

IMPORTANT BOOKING / DATA LIMITATIONS
------------------------------------
This is a student project/demo. It does NOT currently connect to airline,
IRCTC, bus operator, hotel, restaurant or bike-rental booking APIs and does
not take payments or place confirmed reservations. Fares, hotel inventory,
ratings/reviews, restaurant prices and guide details shown inside the app are
sample planning data. Use the external provider links to verify live availability,
departure/arrival times, current prices, room inventory, reviews and booking
terms. Do not present the in-app estimate or trip reference number as a paid
ticket or confirmed hotel reservation.

Worldwide search sends the search phrase to OpenStreetMap Nominatim. Follow
their usage policy and add a suitable proxy / caching strategy before public
production deployment. Photos may be loaded from Wikipedia when available.
