# Feature Specification: PokéFusion MVP

**Feature Branch**: `001-pokefusion-mvp`  
**Created**: 2026-03-16  
**Status**: Draft  
**Input**: User description: "Rédige les spécifications de l'MVP de PokéFusion (en Flutter). L'UI doit inclure un écran pour sélectionner 2 Pokémon (via PokéAPI ou des images en locales), un aperçu de la superposition à 50% d'opacité en local, et un bouton 'Fusionner'. Prévois un écran de résultat avec un indicatieur de chargement pendant l'appel à l'API Hugging Face, ainsi que la gestion des erreurs."

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Create a Pokémon Fusion Draft (Priority: P1)

As a user, I want to select two Pokémon and see a local preview of their fusion draft so that I can decide if I want to proceed with the final generation.

**Why this priority**: Core interaction that precedes any external API call. Provides immediate value without network dependency.

**Independent Test**: Can be fully tested by selecting two images and verifying that a blended image (50% opacity each) is rendered on screen.

**Acceptance Scenarios**:

1. **Given** the app is open on the selection screen, **When** I select two Pokémon (one from PokéAPI and one from local storage), **Then** both sprites are displayed.
2. **Given** two Pokémon are selected, **When** I view the preview, **Then** I see an image where both sprites are superposed with 50% opacity.

---

### User Story 2 - Generate Final Fusion via AI (Priority: P2)

As a user, I want to trigger a high-quality AI generation of the fusion draft so that I can see a "natural" looking new Pokémon creature.

**Why this priority**: The primary USP of the app. Transforms a simple blend into a creative output.

**Independent Test**: Can be tested by clicking "Fusionner" and verifying that a loading state is shown, followed by an image response from the Hugging Face API.

**Acceptance Scenarios**:

1. **Given** a fusion draft is visible, **When** I click the "Fusionner" button, **Then** a loading indicator is displayed while the request is being processed.
2. **Given** a successful API response, **When** the generation completes, **Then** the final fusion image is displayed on the result screen.

---

### User Story 3 - Error Handling & Resilience (Priority: P3)

As a user, I want to be informed if something goes wrong during the selection or generation process so that I can try again or fix the issue.

**Why this priority**: Essential for a professional MVP experience, especially with external API dependencies.

**Independent Test**: Can be tested by simulating a network failure during the API call or selecting an invalid image file.

**Acceptance Scenarios**:

1. **Given** a network failure during the AI call, **When** the error occurs, **Then** a clear error message is shown with a "Try Again" option.

---

### Edge Cases

- **Pokémon with no sprite**: If a Pokémon selected via PokéAPI lacks a front sprite, the system SHOULD fall back to a placeholder image or prevent selection.
- **Large local images**: If a user selects a very high-resolution local image, the system MUST downscale it before superposition to prevent memory issues.
- **Hugging Face API timeout**: If the API takes too long to respond, a specific timeout message SHOULD be displayed.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow selecting Pokémon from PokéAPI (list/search).
- **FR-002**: System MUST allow selecting local images (gallery/camera) as source sprites.
- **FR-003**: System MUST generate a local preview by superposing two source images at 50% opacity each.
- **FR-004**: System MUST provide a "Fusionner" button that appears only when two sources are selected.
- **FR-005**: System MUST send the blended "draft" image to the Hugging Face Img2Img API (Stable Diffusion v1.5).
- **FR-006**: System MUST use a `strength` parameter of approximately 0.65 for the Hugging Face request.
- **FR-007**: System MUST display a dedicated loading indicator while waiting for the AI response.
- **FR-008**: System MUST display the final image in a result screen.
- **FR-009**: System MUST handle and display network or API-specific errors (e.g., rate limits, invalid tokens).

### Key Entities

- **Pokémon Sprite**: An image representing a Pokémon (from API or local).
- **Fusion Draft**: The resulting local blend of two sprites.
- **Fusion Result**: The AI-generated Pokémon image.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Users can complete the selection and see a local preview in under 5 seconds.
- **SC-002**: The AI generation result is displayed within 20 seconds of clicking "Fusionner" (on standard network).
- **SC-003**: 100% of API errors are caught and reported to the user via a UI notification.
- **SC-004**: The app maintains 60 FPS during the local superposition process.
