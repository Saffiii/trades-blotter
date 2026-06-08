# Financial Trades Blotter

A full-stack real-time FX trading platform 
demonstrating production patterns from 
institutional trading systems.

Built as a portfolio project to showcase 
real-time data architecture, virtualised 
rendering, and trading UI patterns.

## Tech Stack

**Frontend**
- React 18 + TypeScript
- Redux Toolkit
- Ag-Grid Enterprise
- WebSocket / STOMP
- D3.js

**Backend**
- Java 21 + Spring Boot 3
- STOMP over WebSocket
- RESTful APIs

## Architecture

Real-time price updates flow from a Java 
Spring Boot backend via STOMP over WebSocket 
to the React frontend. Updates are accumulated 
in a Map (last-write-wins per symbol) and 
flushed once per requestAnimationFrame — 
converting high-frequency ticks into 
60 renders per second.

The blotter uses a viewport-based rendering 
pattern — only visible rows exist in the DOM 
at any time, keeping render cost constant 
regardless of dataset size.

## Key Features
- Real-time price feed via WebSocket/STOMP
- Viewport-based virtualised blotter
- Redux Toolkit state management
- Live P&L and position tracking
- WebSocket reconnection with exponential backoff

## Running Locally

**Frontend**
cd client
npm install
npm start

**Backend**
cd server
mvn spring-boot:run

## Design Decisions

**Why Redux Toolkit**
Consistent with institutional trading platform 
patterns. Per-symbol selectors ensure components 
only re-render when their specific data changes.

**Why viewport rendering**
Keeps DOM node count proportional to viewport 
size — O(visible rows) not O(dataset size). 
Critical for large instrument universes.

**Why STOMP over raw WebSocket**
Pub/sub semantics — subscription management, 
channel routing, and reconnection handling 
without custom protocol implementation.
