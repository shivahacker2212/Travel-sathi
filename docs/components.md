## UI Components

This is a reference for the core reusable components in the Tourist app. If you are using React/React Native, props are typed with TypeScript.

> Note: Since the codebase is not present in this environment, the following documents the intended API for typical components in a travel app. Adjust to your implementation.

### DestinationCard
- **Props**:
  - `id: string` — Destination identifier
  - `name: string`
  - `country?: string`
  - `imageUrl?: string`
  - `rating?: number`
  - `onPress?: (id: string) => void`
- **Usage**:
```tsx
<DestinationCard
  id="dst_001"
  name="Kathmandu"
  country="Nepal"
  imageUrl="https://..."
  rating={4.7}
  onPress={(id) => navigate(`/destinations/${id}`)}
/>
```

### DestinationList
- **Props**:
  - `items: Array<{ id: string; name: string; country?: string; imageUrl?: string; rating?: number }>`
  - `onItemPress?: (id: string) => void`
  - `isLoading?: boolean`
- **Usage**:
```tsx
<DestinationList items={destinations} onItemPress={openDestination} isLoading={loading} />
```

### ItineraryBuilder
- **Props**:
  - `value: { name: string; startDate?: string; endDate?: string; stops: Array<{ destinationId: string; days: number }> }`
  - `onChange: (value) => void`
  - `onSubmit?: () => void`
- **Usage**:
```tsx
<ItineraryBuilder value={itinerary} onChange={setItinerary} onSubmit={saveItinerary} />
```

### ReviewForm
- **Props**:
  - `destinationId: string`
  - `onSubmit: (review: { rating: number; comment?: string }) => Promise<void>`
  - `initialValue?: { rating?: number; comment?: string }`
- **Usage**:
```tsx
<ReviewForm destinationId="dst_001" onSubmit={(r) => client.reviews.create({ destinationId: 'dst_001', ...r })} />
```

### MapView
- **Props**:
  - `markers?: Array<{ id: string; title: string; lat: number; lng: number }>`
  - `onMarkerPress?: (id: string) => void`
  - `center?: { lat: number; lng: number }`
  - `zoom?: number`
- **Usage**:
```tsx
<MapView
  center={{ lat: 27.7172, lng: 85.3240 }}
  zoom={10}
  markers={[{ id: 'dst_001', title: 'Kathmandu', lat: 27.7172, lng: 85.3240 }]}
  onMarkerPress={(id) => navigate(`/destinations/${id}`)}
/>
```

