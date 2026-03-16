<!--
Sync Impact Report:
- Version change: [ALL_CAPS_IDENTIFIER] -> 1.0.0
- List of modified principles: Initial definition of PokéFusion principles.
- Added sections: Core Principles (Local Image Processing, AI Integration, Separation of Concerns, Test-First, Simplicity & UX).
- Removed sections: Placeholder tokens.
- Templates requiring updates: 
    - .specify/templates/plan-template.md (Checked: generic, no update needed)
    - .specify/templates/spec-template.md (Checked: generic, no update needed)
    - .specify/templates/tasks-template.md (Checked: generic, no update needed)
- Follow-up TODOs: None.
-->

# PokéFusion Constitution

## Core Principles

### I. Mobile-First Local Processing
All initial image manipulations, specifically the superposition of two Pokémon sprites at 50% opacity, MUST be performed locally on the mobile device. This ensures immediate visual feedback and minimizes unnecessary network traffic for "draft" states.

### II. AI-Driven Generation (Img2Img)
The final Pokémon fusion MUST be generated using the Hugging Face Img2Img API (specifically the `stable-diffusion-v1-5/stable-diffusion-v1-5` model). A fixed `strength` parameter of approximately 0.65 SHOULD be used to maintain a balance between the original sprites' silhouettes and the AI's creative output.

### III. Strict Separation of Concerns
The application architecture MUST strictly decouple the local mobile logic (image selection, local superposition, UI state) from the AI integration layer (API requests, payload formatting, response handling). This separation facilitates independent testing and potential future model swaps.

### IV. Test-First Mandatory
All logic related to image processing (superposition algorithms) and API payload preparation MUST be covered by unit tests before implementation. This guarantees the reliability of the "draft" sent to the AI and the correct handling of external service data.

### V. Seamless User Experience (UX)
The workflow from Pokémon selection to final fusion MUST be fluid and intuitive. The transition between the local "brouillon" and the AI-generated final result should be handled with appropriate loading states to maintain perceived performance.

## Technical Constraints

### Technology Stack
The project targets mobile platforms (Android/iOS) using a modern framework (e.g., React Native or Flutter). The AI component relies exclusively on the Hugging Face inference API.

## Development Workflow

### Feature Implementation
Every new feature or refinement must start with a specification that aligns with the Core Principles. Implementation follows the Red-Green-Refactor cycle, prioritizing the local processing logic before AI integration.

## Governance
This constitution supersedes all other informal practices within the PokéFusion project. Any amendments to these principles require a version bump and updated documentation. Compliance is verified during code reviews and automated testing gates.

**Version**: 1.0.0 | **Ratified**: 2026-03-16 | **Last Amended**: 2026-03-16
