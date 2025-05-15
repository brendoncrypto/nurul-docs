# Nurul Project Build Summary

## Core Components

### Website (Next.js 14)
- **Global Layout**: Includes responsive design with light/dark mode support
- **Hero Section**: Branded hero section with headline and CTAs
- **Background**: Light mode uses `#F5F7F9` (bg-surface) for a clean, professional look

## Features

### Psychology-Driven Prompt Builder
- **Path**: `/prompt`
- **Technology**: Server Components with Client-side Form (React Hook Form + Zod)
- **Structure**: 8-step form wizard with animated transitions
  - 6 dropdown selection pages (required)
  - 2 optional text input pages
- **Data Flow**: 
  - Form state persisted across steps using React Hook Form
  - User can navigate back/forward and skip optional steps
  - Final submission produces a formatted prompt
- **Styling**: Uses Tailwind with custom page transition animations
- **Schema**: Defined in `apps/web/app/prompt/schema.ts`

### Two-Layer Prompt Construction
- **Clinical/Psychological Layer**:
  - Evidence-based therapeutic frameworks (CBT, ACT, psychodynamic)
  - Neuroscience-informed understanding of cognition and emotion
  - Trauma-informed, culturally responsive approaches
  - Ethical boundaries and appropriate scope of care

- **Computer Science Layer**:
  - Structured reasoning with explicit steps
  - Token-optimized responses with high signal-to-noise ratio
  - Systems thinking with causal models
  - Surface hidden assumptions and dependencies

### API Implementation
- **OpenAI Integration**: Uses GPT-4o model with carefully crafted system prompts
- **Prompt Building**: Separate module for constructing system and user prompts
- **Token Management**: Optimized for token efficiency (max_tokens: 2048)
- **Response Structure**: Returns both prompt text and usage information

## Design System

### Colors
- **Primary**: `nurul` - Brand primary color
- **Surface**: `#F5F7F9` - Background color for light mode
- **Ink**: Dark text and dark mode background
- **Accent**: `gold` - Used for highlights and accents

### Animations
- **Page Transitions**: Fade-in effect with slight vertical movement
  - Keyframe: opacity 0 to 1, translateY 8px to 0
  - Duration: 0.3s with ease-out timing

## Future Enhancements
- Implement user accounts for saved prompts and history
- Add analytics to track most common prompt patterns
- Expand prompt builder with additional psychology frameworks 