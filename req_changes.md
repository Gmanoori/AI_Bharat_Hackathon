# Requirements Document: Woop Woop Learning Tracker

## Introduction

Woop Woop is a gamified student learning consistency tracker web application designed to help students maintain consistent study habits through goal tracking, AI-powered learning tools, and community resource sharing. The system combines weekly goal planning, calendar integration, space-themed gamification, AI-assisted note summarization, flashcard generation, and a collaborative resource platform to create an engaging learning environment.

## Glossary

- **System**: The Woop Woop Learning Tracker web application
- **User**: A student using the application to track learning goals
- **Goal**: A predefined learning or practice objective set by the User
- **Weekly_Plan**: A collection of Goals scheduled for a specific week
- **Consistency_Score**: A metric tracking User adherence to planned Goals
- **AI_Assistant**: The integrated AI component for content generation  <!-- Removed (Gemma/NanoBanana) -->

- **Resource**: Study material, link, or tool shared by Users
TBD: Sanity check the shared resource. 

- **Flashcard_Set**: A collection of question-answer pairs generated for study
- **Presentation**: A slide deck generated from learning materials
- **Baby_Breaking_Mode**: A feature that simplifies AI explanations using analogies
- **Calendar_Integration**: Connection to Google Calendar and Notion for event synchronization
- **Gamification_Engine**: The component managing rewards, themes, and user engagement features
- **Note_Summarizer**: AI component that condenses learning materials
- **Community_Platform**: The resource sharing and discovery system. TBD: Model accuracy checks 

## Requirements

### Requirement 1: User Onboarding and Goal Definition

**User Story:** As a new user, I want to complete an introductory survey, so that I can define my learning goals and customize my experience. 


#### Acceptance Criteria

1. WHEN a new User registers, THE System SHALL present an onboarding survey
2. WHEN the User completes the survey, THE System SHALL capture learning goals, subjects, and preferences
3. WHEN survey data is submitted, THE System SHALL create a User profile with predefined Goals
4. THE System SHALL validate that at least one Goal is defined before completing onboarding
5. WHEN onboarding is complete, THE System SHALL redirect the User to the dashboard

### Requirement 2: Weekly Goal Planning

**User Story:** As a user, I want to plan my weekly learning goals with maximum customization, so that I can organize my study schedule effectively.

#### Acceptance Criteria

1. WHEN a User accesses the planning interface, THE System SHALL display available Goals from the User profile
2. WHEN a User creates a Weekly_Plan, THE System SHALL allow selection of Goals, time allocation, and priority levels
3. WHEN a User modifies a Weekly_Plan, THE System SHALL update the schedule and recalculate time commitments
4. THE System SHALL allow Users to set custom time blocks for each Goal within a week
5. WHEN a Weekly_Plan is saved, THE System SHALL persist the plan and make it visible on the dashboard
6. THE System SHALL allow Users to duplicate previous Weekly_Plans for reuse

### Requirement 3: Calendar Integration

**User Story:** As a user, I want to integrate my Google Calendar and Notion, so that my learning goals sync with my existing schedule.

#### Acceptance Criteria

1. WHEN a User initiates calendar integration, THE System SHALL authenticate with Google Calendar API or Notion API
2. WHEN authentication succeeds, THE System SHALL request permission to read and write calendar events
3. WHEN a User adds a Goal to a Weekly_Plan, THE System SHALL create corresponding events in the connected calendars
4. WHEN a calendar event is modified externally, THE System SHALL sync changes back to the Weekly_Plan
5. WHEN a User disconnects a calendar, THE System SHALL remove the integration and stop synchronization
6. THE System SHALL support bidirectional synchronization between the System and external calendars

### Requirement 4: Goal Tracking and Consistency Monitoring

**User Story:** As a user, I want to track my progress on learning goals, so that I can measure my consistency and identify areas for improvement.

#### Acceptance Criteria

1. WHEN a User completes a Goal, THE System SHALL record the completion timestamp and update the Consistency_Score. 
2. How will we know when a User completes a goal?
    - Reminder in between tasks(mostly two )
    - Journal at EOD(no checkbox, rather, list tasks done)
    - Open to more ideas
2. WHEN a User marks a Goal as incomplete, THE System SHALL reflect this in the Consistency_Score calculation
3. THE System SHALL calculate Consistency_Score based on completed Goals versus planned Goals over time
4. WHEN the Consistency_Score changes, THE System SHALL update the User dashboard in real-time
5. THE System SHALL display historical consistency data for the past 12 weeks
6. WHEN a User views consistency metrics, THE System SHALL show completion rates, streaks, and trends

### Requirement 5: Gamification and Rewards

**User Story:** As a user, I want to earn rewards and experience aesthetic transitions, so that staying consistent feels engaging and motivating.

#### Acceptance Criteria

1. WHEN a User achieves a consistency milestone, THE Gamification_Engine SHALL award points and unlock rewards
2. What are points and rewards at offer?
    - Tokens for premium/better models inside app
    - Gift cards (for future scope)

2. THE System SHALL implement a space/universe theme with visual progression based on User achievements
3. WHEN a User earns rewards, THE System SHALL display aesthetic transitions and celebratory animations
4. THE System SHALL present trivia questions related to the User's learning subjects
5. WHEN a User answers trivia correctly, THE System SHALL award bonus points
6. THE System SHALL display subtle scrolling motivational messages on the homepage
7. WHEN a User reaches new achievement levels, THE System SHALL unlock new visual themes and customization options. We'll think about it

### Requirement 6: AI Note Summarization

**User Story:** As a user, I want to upload learning materials and receive AI-generated summaries, so that I can quickly review key concepts.

#### Acceptance Criteria

1. WHEN a User uploads a document or text, THE Note_Summarizer SHALL process the content
2. WHEN the Note_Summarizer completes processing, THE System SHALL generate a concise summary
3. THE System SHALL support multiple file formats including PDF, DOCX, and plain text
4. WHEN a summary is generated, THE System SHALL display it alongside the original material
5. THE System SHALL allow Users to save summaries for future reference
6. WHEN summarization fails, THE System SHALL provide a descriptive error message


```Read from here```

### Requirement 7: Community Resource Sharing

**User Story:** As a user, I want to discover and share learning resources with other students, so that I can access high-quality study materials.

#### Acceptance Criteria

1. WHEN a User accesses the Community_Platform, THE System SHALL display shared Resources organized by subject and popularity
2. WHEN a User submits a Resource, THE System SHALL validate the submission and add it to the platform
3. THE System SHALL allow Users to rate and review Resources
4. WHEN a User searches for Resources, THE System SHALL return relevant results based on subject, tags, and ratings
5. THE System SHALL display both popular and lesser-known Resources to promote discovery
6. WHEN a Resource receives negative ratings, THE System SHALL flag it for review
7. THE System SHALL allow Users to bookmark Resources for quick access

### Requirement 8: AI Presentation and Flashcard Generation

**User Story:** As a user, I want to generate presentations and flashcards from my learning materials, so that I can prepare for exams efficiently.

#### Acceptance Criteria

1. WHEN a User requests a Presentation, THE AI_Assistant SHALL analyze the provided content
2. WHEN the content is unclear or insufficient, THE AI_Assistant SHALL ask clarifying questions before generating output
3. WHEN clarifying questions are answered, THE AI_Assistant SHALL generate a structured Presentation with slides
4. WHEN a User requests a Flashcard_Set, THE AI_Assistant SHALL extract key concepts and create question-answer pairs
5. THE System SHALL allow Users to edit generated Presentations and Flashcard_Sets
6. WHEN generation is complete, THE System SHALL save the output and make it available for download
7. THE System SHALL support export formats including PPTX for Presentations and CSV for Flashcard_Sets

### Requirement 9: Baby Breaking Mode

**User Story:** As a user, I want to enable Baby Breaking Mode, so that I can receive simplified explanations using analogies.

#### Acceptance Criteria

1. THE System SHALL provide a toggle for Baby_Breaking_Mode in the User settings
2. WHEN Baby_Breaking_Mode is enabled, THE System SHALL append "Explain this like I am a 3 YO" to all AI_Assistant prompts
3. WHEN the AI_Assistant generates content with Baby_Breaking_Mode enabled, THE System SHALL provide analogy-based explanations
4. WHEN Baby_Breaking_Mode is disabled, THE System SHALL revert to standard explanation complexity
5. THE System SHALL persist the Baby_Breaking_Mode preference across User sessions

### Requirement 10: Data Persistence and Security

**User Story:** As a user, I want my data to be securely stored and accessible, so that I can trust the system with my learning information.

#### Acceptance Criteria

1. WHEN a User creates or modifies data, THE System SHALL persist changes to the database immediately
2. THE System SHALL encrypt sensitive User data including authentication credentials
3. WHEN a User logs in, THE System SHALL authenticate credentials using secure hashing
4. THE System SHALL implement session management with automatic timeout after 24 hours of inactivity
5. WHEN a User requests data deletion, THE System SHALL remove all associated data within 30 days
6. THE System SHALL perform daily backups of all User data

### Requirement 11: Vector Database for Semantic Search

**User Story:** As a user, I want to search my notes and resources semantically, so that I can find relevant information even without exact keyword matches.

#### Acceptance Criteria

1. WHEN a User uploads content, THE System SHALL generate vector embeddings and store them in the vector database
2. WHEN a User performs a search, THE System SHALL query the vector database for semantically similar content
3. THE System SHALL return search results ranked by semantic similarity
4. THE System SHALL support search across notes, summaries, and shared Resources
5. WHEN new content is added, THE System SHALL update vector embeddings within 5 minutes

### Requirement 12: API and Integration Architecture

**User Story:** As a developer, I want a well-structured API, so that the frontend can interact efficiently with backend services.

#### Acceptance Criteria

1. THE System SHALL implement a RESTful API using FastAPI
2. WHEN an API request is received, THE System SHALL validate authentication tokens
3. THE System SHALL return responses in JSON format with appropriate HTTP status codes
4. WHEN an API error occurs, THE System SHALL return descriptive error messages
5. THE System SHALL implement rate limiting to prevent abuse
6. THE System SHALL document all API endpoints using OpenAPI specification

### Requirement 13: Deployment and Containerization

**User Story:** As a system administrator, I want the application containerized, so that deployment is consistent across environments.

#### Acceptance Criteria

1. THE System SHALL be packaged using Docker containers
2. THE System SHALL provide a docker-compose configuration for local development
3. WHEN the System is deployed, THE System SHALL start all required services automatically
4. THE System SHALL implement health check endpoints for monitoring
5. THE System SHALL support environment-based configuration for development, staging, and production
