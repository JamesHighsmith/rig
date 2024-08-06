# WorldLine API Documentation

## Table of Contents

1. [Introduction](#introduction)
2. [Core Concept: Worldlines](#core-concept-worldlines)
3. [Authentication](#authentication)
4. [Endpoints](#endpoints)
   - [Level 1: Single Lift Operation](#level-1-single-lift-operation)
   - [Level 2: Building Construction](#level-2-building-construction)
   - [Level 3: City-Scale Operations](#level-3-city-scale-operations)
   - [Level 4: Earth to Mars Operations](#level-4-earth-to-mars-operations)
5. [Advanced Features](#advanced-features)
6. [Error Handling and Rate Limiting](#error-handling-and-rate-limiting)

## Introduction

The WorldLine API optimizes the movement of atomic clusters at any scale, from lifting a steel beam on Earth to building a pyramid on Mars. It provides a unified system for planning, executing, and monitoring complex projects in both terrestrial and space environments.

## Core Concept: Worldlines

A worldline is the path an object takes through 4D spacetime, representing the journey of any atomic cluster (object, person, or planet) through space and time.

## Authentication

Include your API key in the header of each request:

```
Authorization: Bearer YOUR_API_KEY
```

## Endpoints

### Level 1: Single Lift Operation

#### Plan a Lift

```http
POST /worldlines
```

Request body:
```json
{
  "type": "CRANE_LIFT",
  "payload": {"type": "STEEL_BEAM", "mass": 2000},
  "start": {"x": 0, "y": 0, "z": 0, "t": 1625000000},
  "end": {"x": 10, "y": 20, "z": 30, "t": 1625000060},
  "equipment": {"type": "TOWER_CRANE", "model": "XL5000"}
}
```

#### Execute the Lift

```http
POST /worldlines/{worldline_id}/execute
```

#### Check Lift Status

```http
GET /worldlines/{worldline_id}/status
```

### Level 2: Building Construction

#### Create a Project

```http
POST /projects
```

Request body:
```json
{
  "name": "Downtown Skyscraper Alpha",
  "location": {"city": "New York", "coordinates": {"latitude": 40.7128, "longitude": -74.0060}},
  "type": "SKYSCRAPER",
  "height": 300,
  "estimated_duration": 94608000
}
```

#### Plan Multiple Lifts

```http
POST /projects/{project_id}/worldlines
```

#### Check Project Status

```http
GET /projects/{project_id}/status
```

### Level 3: City-Scale Operations

#### Create a City Plan

```http
POST /city-plans
```

Request body:
```json
{
  "name": "New Manhattan Project",
  "location": {"city": "New York", "area": {"top_left": {"latitude": 40.7831, "longitude": -73.9712}, "bottom_right": {"latitude": 40.7002, "longitude": -74.0212}}},
  "projects": [
    {"type": "SKYSCRAPER", "quantity": 3},
    {"type": "BRIDGE", "quantity": 1},
    {"type": "SUBWAY_EXTENSION", "quantity": 1}
  ],
  "duration": 315360000
}
```

#### Simulate City Development

```http
POST /city-plans/{city_plan_id}/simulate
```

### Level 4: Earth to Mars Operations

#### Plan Mars Mission

```http
POST /space-projects
```

Request body:
```json
{
  "name": "Mars Pyramid Construction",
  "phases": [
    {"name": "Earth Launch", "payload": {"construction_robots": 1000, "3d_printers": 50, "human_crew": 20}},
    {"name": "Interplanetary Transit", "duration": 21600000},
    {"name": "Mars Landing", "location": {"latitude": 4.5, "longitude": 137.4}},
    {"name": "Pyramid Construction", "dimensions": {"base_width": 230, "height": 146}, "material_source": "LOCAL_REGOLITH"}
  ]
}
```

#### Track Interplanetary Fleet

```http
GET /space-projects/{project_id}/fleet-status
```

#### Simulate Mars Pyramid Construction

```http
POST /space-projects/{project_id}/simulate-construction
```

## Advanced Features

### Dependency Tracking

```http
GET /worldlines/{worldline_id}/dependencies
```

### Multi-Fleet Management

```http
POST /projects/{project_id}/coordinate-fleets
```

## Error Handling and Rate Limiting

- Standard HTTP response codes indicate success or failure.
- Error responses include a JSON object with additional information.
- Rate limit: 100 requests per minute.

For full documentation and examples, visit our [API Reference](https://api.worldline.space/docs).
