## Data Models

These are the core domain models with JSON schemas for validation.

### User
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://travel-sathi.example.com/schemas/user.json",
  "type": "object",
  "required": ["id", "name", "email"],
  "properties": {
    "id": { "type": "string" },
    "name": { "type": "string", "minLength": 1 },
    "email": { "type": "string", "format": "email" },
    "avatarUrl": { "type": "string", "format": "uri", "nullable": true }
  },
  "additionalProperties": false
}
```

### Destination
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://travel-sathi.example.com/schemas/destination.json",
  "type": "object",
  "required": ["id", "name", "country"],
  "properties": {
    "id": { "type": "string" },
    "name": { "type": "string" },
    "country": { "type": "string" },
    "description": { "type": "string" },
    "rating": { "type": "number", "minimum": 0, "maximum": 5 },
    "images": { "type": "array", "items": { "type": "string", "format": "uri" } },
    "tags": { "type": "array", "items": { "type": "string" } },
    "location": {
      "type": "object",
      "required": ["lat", "lng"],
      "properties": {
        "lat": { "type": "number", "minimum": -90, "maximum": 90 },
        "lng": { "type": "number", "minimum": -180, "maximum": 180 }
      }
    }
  },
  "additionalProperties": false
}
```

### Itinerary
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://travel-sathi.example.com/schemas/itinerary.json",
  "type": "object",
  "required": ["id", "name", "stops"],
  "properties": {
    "id": { "type": "string" },
    "name": { "type": "string" },
    "startDate": { "type": "string", "format": "date" },
    "endDate": { "type": "string", "format": "date" },
    "stops": {
      "type": "array",
      "items": {
        "type": "object",
        "required": ["destinationId", "days"],
        "properties": {
          "destinationId": { "type": "string" },
          "days": { "type": "integer", "minimum": 1 }
        }
      }
    }
  },
  "additionalProperties": false
}
```

### Review
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://travel-sathi.example.com/schemas/review.json",
  "type": "object",
  "required": ["id", "destinationId", "rating"],
  "properties": {
    "id": { "type": "string" },
    "destinationId": { "type": "string" },
    "rating": { "type": "integer", "minimum": 1, "maximum": 5 },
    "comment": { "type": "string" },
    "createdAt": { "type": "string", "format": "date-time" }
  },
  "additionalProperties": false
}
```

