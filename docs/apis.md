## Public REST APIs

Note: This documentation outlines the intended public APIs for the Tourist app. Adjust base URLs and security as per your environment.

Base URL: `https://api.travel-sathi.example.com/v1`
Auth: Bearer token in the `Authorization` header unless noted otherwise.

### Auth

#### POST /auth/login
- Purpose: Exchange user credentials for an access token
- Request body:
```json
{
  "email": "user@example.com",
  "password": "string"
}
```
- Response 200:
```json
{
  "accessToken": "jwt-token",
  "refreshToken": "jwt-refresh",
  "user": {
    "id": "usr_123",
    "name": "Traveler",
    "email": "user@example.com"
  }
}
```

#### POST /auth/refresh
- Purpose: Get a new access token
- Request body:
```json
{ "refreshToken": "jwt-refresh" }
```
- Response 200:
```json
{ "accessToken": "new-jwt-token" }
```

### Destinations

#### GET /destinations
- Purpose: List destinations with filters and pagination
- Query params: `q`, `country`, `category`, `page`, `pageSize`, `sort`
- Response 200:
```json
{
  "items": [
    { "id": "dst_001", "name": "Kathmandu", "country": "Nepal", "rating": 4.7 },
    { "id": "dst_002", "name": "Pokhara", "country": "Nepal", "rating": 4.6 }
  ],
  "page": 1,
  "pageSize": 20,
  "total": 200
}
```

#### GET /destinations/{id}
- Purpose: Fetch destination details
- Response 200:
```json
{
  "id": "dst_001",
  "name": "Kathmandu",
  "country": "Nepal",
  "description": "Historic city...",
  "rating": 4.7,
  "images": ["https://..."],
  "tags": ["culture", "heritage"],
  "location": { "lat": 27.7172, "lng": 85.3240 }
}
```

### Itineraries

#### POST /itineraries
- Purpose: Create an itinerary
- Request body:
```json
{
  "name": "Nepal Highlights",
  "startDate": "2025-10-01",
  "endDate": "2025-10-07",
  "stops": [
    { "destinationId": "dst_001", "days": 2 },
    { "destinationId": "dst_002", "days": 3 }
  ]
}
```
- Response 201:
```json
{ "id": "itr_123", "name": "Nepal Highlights" }
```

#### GET /itineraries/{id}
- Purpose: Fetch itinerary details

### Reviews

#### POST /destinations/{id}/reviews
- Purpose: Add a review for a destination
- Request body:
```json
{ "rating": 5, "comment": "Amazing!" }
```
- Response 201:
```json
{ "id": "rev_123", "rating": 5, "comment": "Amazing!" }
```

### Errors

Errors follow this schema:
```json
{
  "error": {
    "code": "string",
    "message": "string",
    "details": {}
  }
}
```

