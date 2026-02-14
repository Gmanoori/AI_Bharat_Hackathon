# Woop Woop - Process Flow & Use Case Diagrams

## 1. User Journey Process Flow

```mermaid
flowchart TD
    Start([New User]) --> Signup[Sign Up / Login]
    Signup --> Survey[Complete Onboarding Survey]
    Survey --> Goals[Define Learning Goals]
    Goals --> Dashboard[Enter Dashboard]
    
    Dashboard --> Plan[Create Weekly Plan]
    Dashboard --> AI[Use AI Tools]
    Dashboard --> Community[Browse Resources]
    Dashboard --> Track[Track Progress]
    
    Plan --> Calendar[Sync to Calendar]
    Calendar --> Reminders[Receive Reminders]
    Reminders --> Complete[Complete Goals]
    
    AI --> Summarize[Summarize Notes]
    AI --> Generate[Generate PPT/Flashcards]
    Generate --> Clarify{AI Asks Questions?}
    Clarify -->|Yes| Answer[Provide Answers]
    Clarify -->|No| Download[Download Content]
    Answer --> Download
    
    Community --> Search[Search Resources]
    Community --> Share[Share Resources]
    Search --> Rate[Rate & Bookmark]
    
    Complete --> Points[Earn Points]
    Track --> Points
    Points --> Rewards[Unlock Achievements]
    Rewards --> Theme[New Themes/Levels]
    
    Theme --> Dashboard
    Download --> Dashboard
    Rate --> Dashboard
```

## 2. Use Case Diagram

```mermaid
graph TB
    Student((Student))
    System[Woop Woop System]
    Calendar[Calendar Apps]
    AI[AI Engine]
    Community((Other Students))
    
    Student -->|registers| UC1[Complete Onboarding]
    Student -->|creates| UC2[Plan Weekly Goals]
    Student -->|tracks| UC3[Mark Goals Complete]
    Student -->|views| UC4[Check Consistency Score]
    Student -->|connects| UC5[Integrate Calendar]
    Student -->|uploads| UC6[Summarize Notes]
    Student -->|requests| UC7[Generate Presentations]
    Student -->|requests| UC8[Create Flashcards]
    Student -->|toggles| UC9[Enable Baby Breaking Mode]
    Student -->|searches| UC10[Find Resources]
    Student -->|shares| UC11[Submit Resources]
    Student -->|rates| UC12[Rate Resources]
    Student -->|earns| UC13[Collect Rewards]
    Student -->|answers| UC14[Solve Trivia]
    
    UC1 --> System
    UC2 --> System
    UC3 --> System
    UC4 --> System
    UC5 --> Calendar
    UC6 --> AI
    UC7 --> AI
    UC8 --> AI
    UC9 --> System
    UC10 --> System
    UC11 --> Community
    UC12 --> System
    UC13 --> System
    UC14 --> System
    
    Calendar -.syncs.-> System
    AI -.asks clarifying questions.-> Student
    Community -.discovers.-> UC10
```

## 3. Simplified Linear Flow (For Presentation Slide)

```mermaid
flowchart LR
    A[Sign Up] --> B[Set Goals]
    B --> C[Plan Week]
    C --> D[Sync Calendar]
    D --> E[Study & Track]
    E --> F[Use AI Tools]
    F --> G[Earn Rewards]
    G --> H[Stay Consistent]
    H --> C
    
    style A fill:#667eea
    style H fill:#f093fb
```

## 4. AI Clarification Flow (Key Feature)

```mermaid
flowchart TD
    Start[User Requests PPT/Flashcards] --> Upload[Upload Content]
    Upload --> Analyze[AI Analyzes Content]
    Analyze --> Check{Content Clear?}
    Check -->|No| Questions[AI Asks Clarifying Questions]
    Questions --> UserAnswer[User Provides Answers]
    UserAnswer --> Analyze
    Check -->|Yes| Generate[Generate Content]
    Generate --> Review[User Reviews]
    Review --> Download[Download PPT/Flashcards]
    
    style Questions fill:#ffd700
    style Generate fill:#90EE90
```

---


3. **Recommended for your presentation**:
   - Use diagram #3 (Simplified Linear Flow) for overview slide
   - Use diagram #4 (AI Clarification Flow) to highlight USP
   - Use diagram #2 (Use Case) for technical audience
