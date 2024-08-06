# WorldLine API v1.0 Documentation

## Table of Contents

1. [Introduction](#introduction)
2. [Core Concepts](#core-concepts)
3. [Authentication](#authentication)
4. [Versioning](#versioning)
5. [Base URL](#base-url)
6. [Endpoints](#endpoints)
7. [Pagination](#pagination)
8. [Webhooks](#webhooks)
9. [Error Handling](#error-handling)
10. [Rate Limiting](#rate-limiting)
11. [SDKs and Client Libraries](#sdks-and-client-libraries)
12. [Data Models](#data-models)
13. [Optimization Algorithms](#optimization-algorithms)
14. [Compliance and Regulations](#compliance-and-regulations)
15. [Changelog](#changelog)

## Introduction

The WorldLine API optimizes the movement of atomic clusters across scales, from Earth-based construction to interplanetary missions. This documentation covers v1.0 of the API.

## Core Concepts

- **Worldline**: A 4D spacetime path of an object.
- **Atomic Cluster**: Any entity from a single object to a planet.
- **Project**: A collection of related worldlines and operations.

## Authentication

We use OAuth 2.0 for secure authentication. Obtain your client credentials from the developer portal.

Example:
```
curl -X POST https://api.worldline.space/v1/oauth/token \
  -d grant_type=client_credentials \
  -d client_id=YOUR_CLIENT_ID \
  -d client_secret=YOUR_CLIENT_SECRET
```

Use the returned access token in the Authorization header:
```
Authorization: Bearer YOUR_ACCESS_TOKEN
```

## Versioning

The current version is v1.0. We use semantic versioning (MAJOR.MINOR.PATCH). APIs are versioned in the URL, e.g., `/v1/worldlines`.

## Base URL

```
https://api.worldline.space/v1
```

## Endpoints

### Worldlines

#### Create a Worldline

```http
POST /worldlines
```

Request body:
```json
{
  "type": "CRANE_LIFT",
  "payload": {
    "type": "STEEL_BEAM",
    "mass": 2000,
    "dimensions": {
      "length": 10,
      "width": 0.5,
      "height": 0.5
    }
  },
  "start": {
    "x": 0, "y": 0, "z": 0,
    "t": "2023-07-01T10:00:00Z"
  },
  "end": {
    "x": 10, "y": 20, "z": 30,
    "t": "2023-07-01T10:01:00Z"
  },
  "equipment": {
    "type": "TOWER_CRANE",
    "model": "XL5000"
  },
  "constraints": {
    "max_speed": 0.5,
    "max_acceleration": 0.2
  }
}
```

Response:
```json
{
  "id": "wl_123abc",
  "status": "PLANNED",
  "energy_required": 500,
  "risk_factors": ["WIND_SPEED", "PAYLOAD_SWING"],
  "path": [
    {"x": 0, "y": 0, "z": 0, "t": "2023-07-01T10:00:00Z"},
    {"x": 5, "y": 10, "z": 15, "t": "2023-07-01T10:00:30Z"},
    {"x": 10, "y": 20, "z": 30, "t": "2023-07-01T10:01:00Z"}
  ],
  "_links": {
    "self": {"href": "/v1/worldlines/wl_123abc"},
    "execute": {"href": "/v1/worldlines/wl_123abc/execute"}
  }
}
```

### Projects

#### Create a Mars Construction Project

```http
POST /projects
```

Request body:
```json
{
  "name": "Mars Pyramid Alpha",
  "type": "MARS_CONSTRUCTION",
  "location": {
    "planet": "MARS",
    "coordinates": {"latitude": 4.5, "longitude": 137.4}
  },
  "timeline": {
    "start_date": "2028-01-01T00:00:00Z",
    "estimated_duration": 157680000
  },
  "objectives": [
    {
      "type": "CONSTRUCT_PYRAMID",
      "specifications": {
        "base_width": 230,
        "height": 146,
        "material": "MARS_REGOLITH"
      }
    }
  ],
  "resources": {
    "construction_robots": 1000,
    "human_personnel": 50,
    "energy_production_capacity": 10000
  }
}
```

Response:
```json
{
  "id": "proj_mars_789xyz",
  "status": "INITIATED",
  "estimated_completion_date": "2033-01-01T00:00:00Z",
  "critical_path_summary": [
    {"phase": "RESOURCE_GATHERING", "duration": 31536000},
    {"phase": "FOUNDATION_CONSTRUCTION", "duration": 15768000},
    {"phase": "PYRAMID_ASSEMBLY", "duration": 94608000}
  ],
  "_links": {
    "self": {"href": "/v1/projects/proj_mars_789xyz"},
    "worldlines": {"href": "/v1/projects/proj_mars_789xyz/worldlines"},
    "simulations": {"href": "/v1/projects/proj_mars_789xyz/simulations"}
  }
}
```

## Pagination

For endpoints returning multiple items, use `limit` and `offset` query parameters:

```
GET /worldlines?limit=20&offset=40
```

Response includes pagination info:

```json
{
  "data": [...],
  "pagination": {
    "total_items": 243,
    "limit": 20,
    "offset": 40,
    "next": "/v1/worldlines?limit=20&offset=60"
  }
}
```

## Webhooks

Register webhooks to receive real-time updates:

```http
POST /webhooks
```

```json
{
  "url": "https://your-server.com/worldline-events",
  "events": ["worldline.completed", "project.phase_started"]
}
```

## Error Handling

We use standard HTTP status codes. Error responses include:

```json
{
  "error": {
    "code": "RESOURCE_NOT_FOUND",
    "message": "The specified worldline could not be found.",
    "details": {
      "worldline_id": "wl_nonexistent"
    }
  }
}
```

## Rate Limiting

- 1000 requests per minute per API key.
- Headers include `X-RateLimit-Limit`, `X-RateLimit-Remaining`, and `X-RateLimit-Reset`.

## SDKs and Client Libraries

Official SDKs:
- Python: `pip install worldline-api`
- JavaScript: `npm install worldline-api`
- Java: Available on Maven Central

## Data Models

Key data models (simplified):

```yaml
Worldline:
  id: string
  type: string
  payload: Object
  start: Coordinate4D
  end: Coordinate4D
  status: string
  path: Array<Coordinate4D>

Project:
  id: string
  name: string
  type: string
  location: Location
  timeline: Timeline
  objectives: Array<Objective>
  status: string

Coordinate4D:
  x: number
  y: number
  z: number
  t: string (ISO8601 datetime)
```

## Optimization Algorithms

We use a combination of:
- A* pathfinding for spatial optimization
- Genetic algorithms for multi-objective optimization
- Physics-based simulations for accurate motion prediction

Details available under NDA.

## Compliance and Regulations

- GDPR compliant: We do not store personal data.
- Adheres to UN Outer Space Treaty regulations.
- Regular security audits and penetration testing.

## Changelog

- 2023-07-01: v1.0 released
  - Initial public API release
  - Basic worldline and project management
- 2023-08-15: v1.1 released
  - Added multi-fleet coordination endpoints
  - Improved Mars atmospheric modeling

For full documentation, interactive API explorer, and additional resources, visit our [Developer Portal](https://developers.worldline.space).
