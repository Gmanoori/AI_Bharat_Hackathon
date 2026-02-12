# Implementation Plan: Woop Woop Learning Tracker

## Overview

This implementation plan breaks down the Woop Woop Learning Tracker into incremental, testable steps. The approach follows a bottom-up strategy: starting with core infrastructure and data models, then building services layer by layer, and finally integrating everything with the frontend. Each major component includes property-based tests to validate correctness properties from the design document.

## Tasks

- [ ] 1. Set up project infrastructure and development environment
  - Create backend directory structure with FastAPI application
  - Create frontend directory structure with React + TypeScript + Vite
  - Set up Docker and docker-compose configuration for PostgreSQL, Redis, and Qdrant
  - Configure environment variables for development, staging, and production
  - Set up pytest and Hypothesis for backend testing
  - Set up Vitest and fast-check for frontend testing
  - Create initial database schema with Alembic migrations
  - _Requirements: 12.1, 13.1, 13.2, 13.5_

- [ ] 2. Implement authentication and user management
  - [ ] 2.1 Create User model and database tables
    - Implement User SQLAlchemy model with email, password_hash, full_name, preferences
    - Create Alembic migration for users table
    - Implement password hashing using bcrypt
    - _Requirements: 10.2, 10.3_
  
  - [ ] 2.2 Implement authentication endpoints
    - Create `/auth/register` endpoint for user registration
    - Create `/auth/login` endpoint with JWT token generation
    - Create `/auth/logout` endpoint
    - Implement JWT token validation middleware
    - _Requirements: 10.3, 12.2_
  
  - [ ]* 2.3 Write property test for authentication
    - **Property 28: Authentication Validation**
    - **Validates: Requirements 10.3**
  
  - [ ]* 2.4 Write property test for credential encryption
    - **Property 27: Credential Encryption**
    - **Validates: Requirements 10.2**
  
  - [ ]* 2.5 Write unit tests for authentication edge cases
    - Test invalid email formats
    - Test weak passwords
    - Test duplicate email registration
    - _Requirements: 10.2, 10.3_

- [ ] 3. Implement onboarding survey and goal definition
  - [ ] 3.1 Create Goal model and onboarding survey schema
    - Implement Goal SQLAlchemy model
    - Create Pydantic schemas for OnboardingSurveyResponse
    - Create Alembic migration for goals table
    - _Requirements: 1.2, 1.3_
  
  - [ ] 3.2 Implement onboarding endpoints
    - Create `/onboarding/survey` POST endpoint to capture survey data
    - Create `/onboarding/complete` endpoint to finalize onboarding
    - Validate that at least one goal is defined
    - _Requirements: 1.1, 1.2, 1.3, 1.4_
  
  - [ ]* 3.3 Write property test for onboarding data capture
    - **Property 1: Onboarding Data Capture and Profile Creation**
    - **Validates: Requirements 1.2, 1.3, 1.4**
  
  - [ ]* 3.4 Write unit tests for onboarding validation
    - Test survey with zero goals (should fail)
    - Test survey with valid goals (should succeed)
    - _Requirements: 1.4_

- [ ] 4. Checkpoint - Ensure authentication and onboarding work
  - Ensure all tests pass, ask the user if questions arise.

- [ ] 5. Implement weekly goal planning system
  - [ ] 5.1 Create WeeklyPlan and PlannedGoal models
    - Implement WeeklyPlan and PlannedGoal SQLAlchemy models
    - Create Alembic migrations for weekly_plans and planned_goals tables
    - _Requirements: 2.1, 2.2_
  
  - [ ] 5.2 Implement weekly planning endpoints
    - Create `/plans` POST endpoint to create weekly plans
    - Create `/plans/{id}` GET endpoint to retrieve plans
    - Create `/plans/{id}` PUT endpoint to modify plans
    - Create `/plans/{id}/duplicate` POST endpoint to duplicate plans
    - Implement time recalculation logic when plans are modified
    - _Requirements: 2.1, 2.2, 2.3, 2.6_
  
  - [ ]* 5.3 Write property test for weekly plan persistence
    - **Property 2: Weekly Plan Persistence and Retrieval**
    - **Validates: Requirements 2.2, 2.5**
  
  - [ ]* 5.4 Write property test for time recalculation
    - **Property 3: Weekly Plan Time Recalculation**
    - **Validates: Requirements 2.3**
  
  - [ ]* 5.5 Write property test for plan duplication
    - **Property 4: Weekly Plan Duplication**
    - **Validates: Requirements 2.6**

- [ ] 6. Implement goal tracking and consistency monitoring
  - [ ] 6.1 Create consistency tracking service
    - Implement ConsistencyTracker class with score calculation logic
    - Create endpoint `/goals/{id}/complete` to mark goals complete
    - Create endpoint `/goals/{id}/incomplete` to mark goals incomplete
    - Implement consistency score calculation based on completed vs planned goals
    - _Requirements: 4.1, 4.2, 4.3_
  
  - [ ] 6.2 Create consistency metrics endpoints
    - Create `/users/{id}/consistency` GET endpoint for current consistency score
    - Create `/users/{id}/consistency/history` GET endpoint for 12-week historical data
    - Include completion rates, streaks, and trends in response
    - _Requirements: 4.5, 4.6_
  
  - [ ]* 6.3 Write property test for consistency score calculation
    - **Property 7: Consistency Score Calculation**
    - **Validates: Requirements 4.1, 4.2, 4.3**
  
  - [ ]* 6.4 Write property test for historical data retrieval
    - **Property 8: Historical Consistency Data Retrieval**
    - **Validates: Requirements 4.5, 4.6**

- [ ] 7. Checkpoint - Ensure goal planning and tracking work
  - Ensure all tests pass, ask the user if questions arise.

- [ ] 8. Implement calendar integration service
  - [ ] 8.1 Create calendar connection models and OAuth flow
    - Implement CalendarConnection SQLAlchemy model
    - Create Alembic migration for calendar_connections table
    - Implement OAuth 2.0 flow for Google Calendar
    - Implement OAuth 2.0 flow for Notion
    - Store encrypted access and refresh tokens
    - _Requirements: 3.1, 3.2, 10.2_
  
  - [ ] 8.2 Implement calendar synchronization service
    - Create CalendarConnector abstract base class
    - Implement GoogleCalendarConnector with event CRUD operations
    - Implement NotionConnector with event CRUD operations
    - Create SyncManager for bidirectional synchronization
    - Implement Celery task for periodic sync
    - _Requirements: 3.3, 3.4_
  
  - [ ] 8.3 Create calendar integration endpoints
    - Create `/calendar/connect/{provider}` endpoint to initiate OAuth
    - Create `/calendar/callback/{provider}` endpoint for OAuth callback
    - Create `/calendar/disconnect/{provider}` endpoint to remove integration
    - Create `/calendar/sync` endpoint to trigger manual sync
    - _Requirements: 3.1, 3.2, 3.5_
  
  - [ ]* 8.4 Write property test for calendar event synchronization
    - **Property 5: Calendar Event Synchronization**
    - **Validates: Requirements 3.3, 3.4**
  
  - [ ]* 8.5 Write property test for calendar disconnection
    - **Property 6: Calendar Disconnection Cleanup**
    - **Validates: Requirements 3.5**
  
  - [ ]* 8.6 Write unit tests for OAuth flow
    - Test successful authentication
    - Test failed authentication
    - Test token refresh
    - _Requirements: 3.1, 3.2_

- [ ] 9. Implement gamification engine
  - [ ] 9.1 Create gamification models
    - Implement UserGameProfile SQLAlchemy model
    - Implement Achievement and UserAchievement models
    - Create Alembic migrations for gamification tables
    - Define achievement criteria in configuration
    - _Requirements: 5.1, 5.7_
  
  - [ ] 9.2 Implement reward system
    - Create RewardSystem class to award points and unlock achievements
    - Implement milestone detection logic
    - Create endpoint `/gamification/profile` to get user game profile
    - Create endpoint `/gamification/achievements` to list all achievements
    - _Requirements: 5.1, 5.7_
  
  - [ ] 9.3 Implement trivia engine
    - Create TriviaQuestion model and database table
    - Seed database with subject-specific trivia questions
    - Create endpoint `/trivia/question` to get random question for user's subjects
    - Create endpoint `/trivia/answer` to validate answer and award points
    - _Requirements: 5.4, 5.5_
  
  - [ ]* 9.4 Write property test for milestone rewards
    - **Property 9: Milestone Rewards**
    - **Validates: Requirements 5.1**
  
  - [ ]* 9.5 Write property test for subject-relevant trivia
    - **Property 10: Subject-Relevant Trivia**
    - **Validates: Requirements 5.4, 5.5**
  
  - [ ]* 9.6 Write property test for achievement unlocks
    - **Property 11: Achievement Level Unlocks**
    - **Validates: Requirements 5.7**

- [ ] 10. Checkpoint - Ensure calendar and gamification work
  - Ensure all tests pass, ask the user if questions arise.

- [ ] 11. Set up vector database and embedding service
  - [ ] 11.1 Configure Qdrant and create collections
    - Set up Qdrant Docker container in docker-compose
    - Create collections for user_notes and resources
    - Configure vector dimensions (384 for sentence-transformers)
    - _Requirements: 11.1_
  
  - [ ] 11.2 Implement embedding service
    - Create EmbeddingService class using sentence-transformers
    - Implement generate_embedding method
    - Create VectorStore class to interact with Qdrant
    - Implement store_embedding and search_similar methods
    - _Requirements: 11.1, 11.2_
  
  - [ ]* 11.3 Write property test for vector embedding generation
    - **Property 29: Vector Embedding Generation**
    - **Validates: Requirements 11.1**

- [ ] 12. Implement AI note summarization service
  - [ ] 12.1 Set up AI model integration
    - Configure Gemma or NanoBanana AI model connection
    - Create AIService base class
    - Implement document parsing for PDF, DOCX, and TXT formats
    - _Requirements: 6.1, 6.3_
  
  - [ ] 12.2 Implement note summarizer
    - Create NoteSummarizer class
    - Implement summarization logic with configurable max length
    - Create endpoint `/ai/summarize` to upload and summarize documents
    - Create endpoint `/summaries` to list saved summaries
    - Store summaries in generated_content table
    - Generate and store vector embeddings for summaries
    - _Requirements: 6.1, 6.2, 6.5, 11.1_
  
  - [ ]* 12.3 Write property test for note summarization round trip
    - **Property 12: Note Summarization Round Trip**
    - **Validates: Requirements 6.1, 6.2, 6.5**
  
  - [ ]* 12.4 Write property test for summarization error handling
    - **Property 13: Summarization Error Handling**
    - **Validates: Requirements 6.6**
  
  - [ ]* 12.5 Write unit tests for file format support
    - Test PDF parsing
    - Test DOCX parsing
    - Test plain text parsing
    - _Requirements: 6.3_

- [ ] 13. Implement AI presentation and flashcard generation (CRITICAL)
  - [ ] 13.1 Implement clarification engine
    - Create ClarificationEngine class to detect unclear content
    - Implement logic to generate clarifying questions
    - Create state management for multi-turn clarification conversations
    - _Requirements: 8.2_
  
  - [ ] 13.2 Implement presentation generator
    - Create PresentationGenerator class
    - Create endpoint `/ai/presentation/request` to initiate generation
    - Return clarification questions if content is unclear
    - Create endpoint `/ai/presentation/clarify` to answer questions
    - Generate presentation after clarification is complete
    - Support PPTX export format
    - _Requirements: 8.1, 8.2, 8.3, 8.7_
  
  - [ ] 13.3 Implement flashcard generator
    - Create FlashcardGenerator class
    - Create endpoint `/ai/flashcards/request` to initiate generation
    - Extract key concepts and create Q&A pairs
    - Support CSV export format
    - _Requirements: 8.4, 8.7_
  
  - [ ]* 13.4 Write property test for AI clarification questions (CRITICAL)
    - **Property 19: AI Clarification Questions**
    - **Validates: Requirements 8.2**
  
  - [ ]* 13.5 Write property test for presentation generation
    - **Property 20: Presentation Generation After Clarification**
    - **Validates: Requirements 8.3**
  
  - [ ]* 13.6 Write property test for flashcard structure
    - **Property 21: Flashcard Structure**
    - **Validates: Requirements 8.4**
  
  - [ ]* 13.7 Write property test for generated content persistence
    - **Property 22: Generated Content Persistence**
    - **Validates: Requirements 8.6**

- [ ] 14. Implement Baby Breaking Mode
  - [ ] 14.1 Add Baby Breaking Mode to user preferences
    - Add baby_breaking_mode boolean field to User model (already in schema)
    - Create endpoint `/users/preferences` to update preferences
    - _Requirements: 9.1, 9.5_
  
  - [ ] 14.2 Implement prompt modification logic
    - Create BabyBreakingModeProcessor class
    - Modify all AI service calls to check user preference
    - Append "Explain this like I am a 3 YO" when mode is enabled
    - _Requirements: 9.2, 9.4_
  
  - [ ]* 14.3 Write property test for prompt modification
    - **Property 23: Baby Breaking Mode Prompt Modification**
    - **Validates: Requirements 9.2**
  
  - [ ]* 14.4 Write property test for mode toggle
    - **Property 24: Baby Breaking Mode Toggle**
    - **Validates: Requirements 9.4**
  
  - [ ]* 14.5 Write property test for preference persistence
    - **Property 25: Baby Breaking Mode Persistence**
    - **Validates: Requirements 9.5**

- [ ] 15. Checkpoint - Ensure AI services work correctly
  - Ensure all tests pass, ask the user if questions arise.

- [ ] 16. Implement community resource sharing platform
  - [ ] 16.1 Create resource models and database tables
    - Implement Resource and ResourceRating SQLAlchemy models
    - Create Alembic migrations for resources and resource_ratings tables
    - _Requirements: 7.1, 7.2_
  
  - [ ] 16.2 Implement resource management endpoints
    - Create `/resources` POST endpoint to submit resources
    - Create `/resources` GET endpoint to list resources with filtering
    - Create `/resources/{id}` GET endpoint to get resource details
    - Create `/resources/{id}/rate` POST endpoint to rate resources
    - Implement automatic flagging for resources with rating < 2.0
    - _Requirements: 7.1, 7.2, 7.6_
  
  - [ ] 16.3 Implement resource search with vector DB
    - Create ResourceSearchEngine class
    - Generate embeddings for resource descriptions
    - Implement semantic search using Qdrant
    - Create `/resources/search` endpoint with subject, tags, and rating filters
    - _Requirements: 7.4, 11.2, 11.3_
  
  - [ ] 16.4 Implement resource bookmarking
    - Create user_bookmarks table
    - Create `/resources/{id}/bookmark` POST endpoint
    - Create `/resources/{id}/unbookmark` DELETE endpoint
    - Create `/users/bookmarks` GET endpoint
    - _Requirements: 7.7_
  
  - [ ]* 16.5 Write property test for resource organization
    - **Property 14: Resource Organization and Display**
    - **Validates: Requirements 7.1**
  
  - [ ]* 16.6 Write property test for resource submission validation
    - **Property 15: Resource Submission Validation**
    - **Validates: Requirements 7.2**
  
  - [ ]* 16.7 Write property test for resource search correctness
    - **Property 16: Resource Search Correctness**
    - **Validates: Requirements 7.4, 11.2, 11.3**
  
  - [ ]* 16.8 Write property test for resource flagging
    - **Property 17: Resource Flagging**
    - **Validates: Requirements 7.6**
  
  - [ ]* 16.9 Write property test for bookmarking round trip
    - **Property 18: Resource Bookmarking Round Trip**
    - **Validates: Requirements 7.7**

- [ ] 17. Implement API infrastructure and middleware
  - [ ] 17.1 Implement rate limiting
    - Create rate limiting middleware using Redis
    - Configure limits (e.g., 100 requests per minute per user)
    - Return 429 status code when limit exceeded
    - _Requirements: 12.5_
  
  - [ ] 17.2 Implement error handling and response formatting
    - Create global exception handler
    - Implement consistent error response format
    - Add request_id to all responses for tracing
    - _Requirements: 12.3, 12.4_
  
  - [ ] 17.3 Implement health check endpoint
    - Create `/health` endpoint
    - Check database connection, Redis connection, Qdrant connection
    - Return service status information
    - _Requirements: 13.4_
  
  - [ ]* 17.4 Write property test for API authentication
    - **Property 30: API Authentication**
    - **Validates: Requirements 12.2**
  
  - [ ]* 17.5 Write property test for API response format
    - **Property 31: API Response Format**
    - **Validates: Requirements 12.3**
  
  - [ ]* 17.6 Write property test for API error messages
    - **Property 32: API Error Messages**
    - **Validates: Requirements 12.4**
  
  - [ ]* 17.7 Write property test for rate limiting
    - **Property 33: Rate Limiting**
    - **Validates: Requirements 12.5**
  
  - [ ]* 17.8 Write property test for health check endpoint
    - **Property 34: Health Check Endpoint**
    - **Validates: Requirements 13.4**

- [ ] 18. Implement data persistence property test
  - [ ]* 18.1 Write property test for data persistence round trip
    - **Property 26: Data Persistence Round Trip**
    - **Validates: Requirements 10.1**

- [ ] 19. Checkpoint - Ensure backend is complete and tested
  - Ensure all tests pass, ask the user if questions arise.

- [ ] 20. Implement frontend authentication and routing
  - [ ] 20.1 Set up React app structure
    - Create React app with TypeScript and Vite
    - Set up React Router for navigation
    - Configure TailwindCSS with space theme colors
    - Set up Redux Toolkit for state management
    - _Requirements: 1.5_
  
  - [ ] 20.2 Implement authentication pages
    - Create Login page with form validation
    - Create Register page with form validation
    - Implement JWT token storage in localStorage
    - Create protected route wrapper component
    - _Requirements: 10.3_
  
  - [ ] 20.3 Implement API client with React Query
    - Create axios instance with authentication interceptor
    - Set up React Query for data fetching and caching
    - Implement automatic token refresh logic
    - _Requirements: 12.2_

- [ ] 21. Implement onboarding survey UI
  - [ ] 21.1 Create onboarding survey components
    - Create multi-step survey form
    - Implement subject selection with checkboxes
    - Implement goal input with dynamic add/remove
    - Implement time commitment slider
    - _Requirements: 1.1, 1.2_
  
  - [ ] 21.2 Connect survey to backend
    - Submit survey data to `/onboarding/survey` endpoint
    - Redirect to dashboard on completion
    - _Requirements: 1.3, 1.5_

- [ ] 22. Implement dashboard and goal planning UI
  - [ ] 22.1 Create dashboard layout
    - Create main dashboard with sidebar navigation
    - Display consistency score and current streak
    - Show upcoming planned goals
    - Display motivational scrolling messages
    - _Requirements: 4.4, 5.6_
  
  - [ ] 22.2 Create weekly planning interface
    - Create calendar view for weekly planning
    - Implement drag-and-drop goal scheduling
    - Allow time block customization
    - Display total planned hours
    - _Requirements: 2.1, 2.2, 2.3_
  
  - [ ] 22.3 Implement goal completion tracking
    - Add checkboxes to mark goals complete
    - Update consistency score in real-time
    - Display visual feedback on completion
    - _Requirements: 4.1, 4.4_

- [ ] 23. Implement gamification UI
  - [ ] 23.1 Create space theme visual system
    - Implement theme progression based on user level
    - Create achievement unlock animations using Framer Motion
    - Display points and level on dashboard
    - _Requirements: 5.2, 5.3_
  
  - [ ] 23.2 Create trivia component
    - Display trivia questions as pop-ups or cards
    - Implement answer validation with visual feedback
    - Show points awarded for correct answers
    - _Requirements: 5.4, 5.5_
  
  - [ ] 23.3 Create achievements page
    - Display all achievements with unlock status
    - Show progress toward locked achievements
    - Display unlocked themes and customization options
    - _Requirements: 5.7_

- [ ] 24. Implement AI tools UI
  - [ ] 24.1 Create note summarization interface
    - Create file upload component for documents
    - Display summarization progress
    - Show summary alongside original content
    - Allow saving summaries
    - _Requirements: 6.1, 6.2, 6.4, 6.5_
  
  - [ ] 24.2 Create presentation generator interface
    - Create content input form
    - Display clarifying questions when needed
    - Show presentation preview with slides
    - Implement PPTX download
    - _Requirements: 8.1, 8.2, 8.3, 8.7_
  
  - [ ] 24.3 Create flashcard generator interface
    - Create content input form
    - Display generated flashcards in card format
    - Implement flashcard flip animation
    - Implement CSV download
    - _Requirements: 8.4, 8.7_
  
  - [ ] 24.4 Implement Baby Breaking Mode toggle
    - Add toggle switch in user settings
    - Display mode status indicator
    - Persist preference across sessions
    - _Requirements: 9.1, 9.5_

- [ ] 25. Implement community resource platform UI
  - [ ] 25.1 Create resource discovery page
    - Display resources organized by subject
    - Implement search with filters (subject, type, rating)
    - Show resource cards with title, description, rating
    - _Requirements: 7.1, 7.4_
  
  - [ ] 25.2 Create resource submission form
    - Implement form with title, description, URL, subject, tags
    - Validate required fields
    - Show success/error messages
    - _Requirements: 7.2_
  
  - [ ] 25.3 Implement resource rating and bookmarking
    - Add star rating component
    - Add bookmark button
    - Create bookmarks page to view saved resources
    - _Requirements: 7.3, 7.7_

- [ ] 26. Implement calendar integration UI
  - [ ] 26.1 Create calendar settings page
    - Display connected calendars
    - Add "Connect Google Calendar" button with OAuth flow
    - Add "Connect Notion" button with OAuth flow
    - Add disconnect buttons for each calendar
    - Show last sync timestamp
    - _Requirements: 3.1, 3.2, 3.5_
  
  - [ ] 26.2 Display calendar sync status
    - Show sync status indicator on dashboard
    - Display sync errors if any
    - Add manual sync button
    - _Requirements: 3.3, 3.4_

- [ ] 27. Implement consistency metrics visualization
  - [ ] 27.1 Create consistency charts
    - Implement 12-week consistency chart using Recharts
    - Display completion rate trend line
    - Show streak information
    - Highlight milestones and achievements
    - _Requirements: 4.5, 4.6_

- [ ] 28. Checkpoint - Ensure frontend is complete
  - Ensure all features work end-to-end, ask the user if questions arise.

- [ ] 29. Integration and deployment preparation
  - [ ] 29.1 Set up Nginx reverse proxy
    - Create Nginx configuration for API and frontend
    - Configure SSL with Let's Encrypt
    - Set up rate limiting at proxy level
    - _Requirements: 13.1_
  
  - [ ] 29.2 Create production Docker configuration
    - Create production Dockerfile for backend
    - Create production Dockerfile for frontend
    - Update docker-compose for production deployment
    - Configure health checks in Docker
    - _Requirements: 13.1, 13.3, 13.4_
  
  - [ ] 29.3 Set up CI/CD pipeline
    - Create GitHub Actions workflow for testing
    - Run all unit tests and property tests on PR
    - Build and push Docker images on merge to main
    - _Requirements: Testing Strategy_
  
  - [ ]* 29.4 Run extended property test suite
    - Run all property tests with 1000+ iterations
    - Verify all 34 properties pass
    - _Requirements: Testing Strategy_

- [ ] 30. Final checkpoint - Complete system verification
  - Ensure all tests pass, verify end-to-end user flows, ask the user if questions arise.

## Notes

- Tasks marked with `*` are optional property-based and unit tests that can be skipped for faster MVP
- Each property test references a specific correctness property from the design document
- Property tests should run minimum 100 iterations with randomized inputs
- The critical AI clarification requirement (Property 19) must be thoroughly tested
- Calendar integration requires OAuth credentials from Google and Notion
- AI model selection (Gemma vs NanoBanana) should be finalized before task 12
- Vector database (Qdrant) must be running before tasks 11 and 16
- Frontend tasks (20-27) can be parallelized with backend tasks after task 19 is complete
