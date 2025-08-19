## Client SDK

The SDK wraps the public APIs for easier usage in web or mobile clients.

### Setup

```ts
import { TravelSathi } from '@travel-sathi/sdk';

const client = new TravelSathi({ baseUrl: 'https://api.travel-sathi.example.com/v1', token: 'YOUR_TOKEN' });
```

### Auth

```ts
await client.auth.login({ email: 'user@example.com', password: 'secret' });
await client.auth.refresh();
```

### Destinations

```ts
const destinations = await client.destinations.list({ country: 'Nepal', page: 1 });
const destination = await client.destinations.getById('dst_001');
```

### Itineraries

```ts
const itineraryId = await client.itineraries.create({
  name: 'Nepal Highlights',
  startDate: '2025-10-01',
  endDate: '2025-10-07',
  stops: [
    { destinationId: 'dst_001', days: 2 },
    { destinationId: 'dst_002', days: 3 },
  ],
});
```

### Reviews

```ts
await client.reviews.create({ destinationId: 'dst_001', rating: 5, comment: 'Amazing!' });
```

### Error handling

```ts
try {
  await client.destinations.getById('bad');
} catch (e) {
  if (e.isHttpError) {
    console.error(e.status, e.body?.error?.message);
  }
}
```

