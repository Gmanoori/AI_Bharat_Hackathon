# Woop Woop Learning Tracker

> "Woop Woop! It's da sound of da police" - Stay consistent, stay on track.

## What We're Building

Woop Woop is a gamified learning consistency tracker that helps students stay accountable to their study goals through smart planning, AI-powered tools, and community support.

## Core Features

**Goal Tracking & Planning**
- Personalized onboarding survey to capture learning goals
- Customizable weekly planning with time blocks
- Consistency scoring and streak tracking
- Calendar integration (Google Calendar, Notion)

**Gamification**
- Space/universe themed interface with aesthetic transitions
- Points, levels, and achievement system
- Subject-specific trivia with rewards
- Motivational messages and progress visualization

**AI-Powered Tools**
- Note summarization for study materials (PDF, DOCX, TXT)
- Presentation generator with clarifying questions
- Flashcard generator for quick reviews
- "Baby Breaking Mode" - simplified explanations for complex topics

**Community Platform**
- Resource sharing across student communities
- Semantic search for discovering lesser-known materials
- Rating and bookmarking system
- Quality moderation

## Tech Stack

**Backend**
- FastAPI (Python 3.11+)
- PostgreSQL (data persistence)
- Qdrant (vector database for semantic search)
- Redis (caching, rate limiting)
- Celery (background tasks)

**Frontend**
- React 18+ with TypeScript
- Vite (build tool)
- TailwindCSS (styling)
- Framer Motion (animations)

**AI/ML**
- Gemma/NanoBanana (LLM)
- sentence-transformers (embeddings)

**Infrastructure**
- Docker & Docker Compose
- Nginx (reverse proxy)
- OAuth 2.0 (calendar integrations)

## Getting Started

See `.kiro/specs/woop-woop-learning-tracker/` for detailed requirements, design, and implementation tasks.

## Project Status

Currently in specification phase. Implementation tasks are ready to begin.
