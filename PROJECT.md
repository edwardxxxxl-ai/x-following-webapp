# Project Context

## Name

Xfinder

## Type

Content infrastructure

## Subtype

Social graph discovery and audience research tool

## Positioning

This is a local automation tool that maps X follow graphs by reusing an authenticated Arc browser session on macOS. It supports multi-account overlap analysis, structured profile export, and heuristic discovery ranking.

## Primary Use Cases

- Analyze who multiple seed accounts jointly follow
- Turn follow graph data into reusable Markdown, JSON, and briefing assets
- Support content workflows, audience mapping, trend tracking, and hidden-node discovery
- Provide a local-first alternative to building against the official X API

## Current Scope

- Input one or more X handles
- Fetch following lists through Arc/X session reuse
- Build structured profile records
- Compute overlap and `followed_by_count`
- Compute heuristic `discovery_score`
- Render Markdown, JSON, and research brief outputs in a local web UI

## Non-Goals For Now

- Hosted multi-user SaaS
- Long-term stable API abstraction over X
- Support for browsers other than Arc
- Official X API integration
