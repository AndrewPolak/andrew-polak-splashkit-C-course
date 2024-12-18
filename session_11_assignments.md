```bash
# Run this command to create all required files for this session.
touch assignment1_stage1.c assignment1_stage1_sol.c assignment1_stage1_test.py assignment1_stage2.c assignment1_stage2_sol.c assignment1_stage2_test.py assignment1_stage3.c assignment1_stage3_sol.c assignment1_stage3_test.py assignment1_stage4.c assignment1_stage4_sol.c assignment1_stage4_test.py assignment2_stage1.c assignment2_stage1_sol.c assignment2_stage1_test.py assignment2_stage2.c assignment2_stage2_sol.c assignment2_stage2_test.py assignment2_stage3.c assignment2_stage3_sol.c assignment2_stage3_test.py assignment2_stage4.c assignment2_stage4_sol.c assignment2_stage4_test.py capstone_milestone1.c capstone_milestone1_sol.c capstone_milestone1_test.py capstone_milestone2.c capstone_milestone2_sol.c capstone_milestone2_test.py capstone_milestone3.c capstone_milestone3_sol.c capstone_milestone3_test.py capstone_milestone4.c capstone_milestone4_sol.c capstone_milestone4_test.py capstone_milestone5.c capstone_milestone5_sol.c capstone_milestone5_test.py
```

# Session 11: Multi-Stage Assignments & Capstone Project (Detailed Specifications)

## Explanations

In previous sessions, you learned individual skills in isolation. Now you’ll apply these skills to **multi-stage assignments** that build incrementally towards small playable demos, and ultimately, to a **capstone project** that integrates all your learned competencies into a feature-complete 2D game.

This session provides **detailed specifications and requirements** for each stage of the multi-stage assignments and for each milestone of the capstone project. The goal is to eliminate vagueness, ensuring you know exactly what to implement and test at each step.

You have two multi-stage assignments followed by a capstone project. Each assignment and project milestone includes:

- **Clear Requirements:** Exactly what features to add or what behaviors to implement.
- **Expected Tests:** Basic guidelines on how the provided or your own tests will verify correctness.
- **Incremental Complexity:** Each subsequent stage or milestone builds on previous work, ensuring a logical progression.

By completing these assignments and the capstone, you’ll demonstrate full proficiency in SplashKit and C, producing a playable, polished 2D application.

---

## Assignment 1: Incremental 2D Game Prototype

**Concept:**  
Start with a simple display, then add interactivity, collision, and scoring. By the end, you have a basic interactive scene—a small game.

### Stage 1: Basic Window and Shapes/Text

**Requirements:**

- Open a window of size 800x600 pixels, title “Assignment 1 - Stage 1”.
- Set background color to black.
- Draw a filled red rectangle at position (100,100) with width=50, height=50.
- Draw the text “Hello, SplashKit!” in white, font size ~20, at coordinates (10,10).
- Press ESC to quit.

**Testing:**

- Automated test may check if the pixel at (100,100) is red (indicating the rectangle is drawn).
- Check if text “Hello, SplashKit!” is rendered at approximately (10,10).
- Verify no crash on ESC press.

### Stage 2: Sprite Movement and Keyboard Control

**Requirements:**

- Continue from Stage 1 setup.
- Load a player sprite from “character.png” (you must have such a file).
- Position player sprite at (400,300).
- Player moves when arrow keys are pressed:
  - LEFT_KEY: move player_x -= 2
  - RIGHT_KEY: move player_x += 2
  - UP_KEY: move player_y -= 2
  - DOWN_KEY: move player_y += 2
- Prevent the player sprite from moving off-screen.
- Press ESC to quit.

**Testing:**

- Run tests that simulate key presses and ensure player’s position changes accordingly.
- Check boundaries: player should stop at window edges.
- Ensure the previous rectangle and text still draw correctly.

### Stage 3: Collision with a Collectible Object

**Requirements:**

- Add a collectible star image “star.png” at position (500,300).
- If player overlaps star (use AABB collision), remove the star (it disappears) and set `star_collected = true`.
- Display “Star Collected!” in green text at (10,40) if star_collected is true.
- Press ESC to quit.

**Testing:**

- Move player onto star.
- After overlap, star disappears, “Star Collected!” appears.
- Automated test might check if star pixel no longer visible after collision.
- Ensure no crash on repeated attempts or after star collected.

### Stage 4: Audio and Scoring

**Requirements:**

- Load a sound effect “collect.wav”.
- On star collision (from Stage 3), play the “collect.wav” sound.
- Introduce a `score = 0` integer. Each time a star is collected, `score += 10`.
- Display “Score: X” at (10,70) in white.
- Optionally, respawn a new star at a random location every 5 seconds (use a timer), so the player can collect multiple stars.
- Press ESC to quit.

**Testing:**

- Collect star, verify sound plays (manually).
- After collection, score increments.
- If respawning implemented: ensure stars keep appearing, score accumulates.
- Automated test may check if score updates after star collection events.

---

## Assignment 2: Mini-Platformer

**Concept:**  
Build a small platformer scene with a player, platforms, gravity, enemies, and scoring.

### Stage 1: Animated Player on Static Background

**Requirements:**

- Load a background image “level_bg.png” filling the 800x600 window.
- Load a player sprite with idle animation “player_idle.png” (assume a sprite sheet of multiple frames).
- Display player at (400,300), animate idle frames continuously.
- Press ESC to quit.

**Testing:**

- Check if player is visible at (400,300).
- Animate: frames should cycle every ~100ms.
- No interaction yet, just visuals.

### Stage 2: Platforms and Gravity-Based Movement

**Requirements:**

- Implement gravity: `dy += 0.5` each frame, `y += dy`.
- Player starts above the ground: if player’s bottom hits ground (y+height > 600), stop at 600-height, dy=0.
- Add a platform at (200,400, width=100, height=10). If player lands on it, stop falling: player bottom at platform top, dy=0.
- Press SPACE to make player jump: if on ground/platform, dy = -5.
- Press ESC to quit.

**Testing:**

- Player falls onto platform or ground and stops.
- Jumping from platform or ground works.
- No passing through platform or floating in mid-air.

### Stage 3: Enemies and Collision

**Requirements:**

- Add an enemy sprite at (600,300). Enemy patrols left and right within a 100-pixel range, changing direction at boundaries.
- If player collides with enemy, reduce player health by 1 (start health=3).
- Display health as “Health: X” at top-left.
- If health=0, display “Game Over” and stop player movement.
- Press ESC to quit.

**Testing:**

- Verify enemy moves back and forth.
- On collision, health decreases.
- At health 0, game over text appears, no movement possible.

### Stage 4: Score, Health, and UI Elements

**Requirements:**

- Add collectible coins at random positions on platforms.
- On collection, `score += 10`.
- Display “Score: X” next to health display.
- If player collects all coins (e.g., place 5 coins), display “Level Complete!”.
- Press R to reset level after game over or completion.
- Press ESC to quit.

**Testing:**

- Check score increments correctly on coin pickup.
- After all coins collected, “Level Complete!” appears.
- R resets the scene: health=3, score=0, all coins back.
- Ensure no crashes on resets.

---

## Capstone Project

**Concept:**  
Design your own complete 2D game. The specifics are up to you, but must demonstrate:

- Rendering, animation, input
- Collision, physics if applicable
- Audio integration
- Saving/loading some aspect (score, progress)
- A menu or UI elements
- Some form of incremental complexity (e.g., multiple levels or increasing difficulty)

**Suggestion:**  
A small platformer, top-down shooter, puzzle game, or adventure with multiple screens.

### Milestone 1: Game Concept & Basic World Setup

**Requirements:**

- Document the game concept in comments at top of code.
- Load a main background image and a player sprite.
- Show player at a defined start position.
- Press ESC to quit immediately (no gameplay yet).

**Testing:**

- Run and see if background and player appear.
- No gameplay test yet.

### Milestone 2: Player Controls & State Management

**Requirements:**

- Implement full player movement (e.g., left/right move, maybe jumping if platformer).
- Introduce a player state machine (IDLE, MOVING, JUMPING, etc.).
- Press keys to move player, update state accordingly.
- Press ESC to quit.

**Testing:**

- Check that state changes with movement keys.
- Player animates according to state.

### Milestone 3: Environment & Level Progression

**Requirements:**

- Add multiple scenes or levels.
- When player reaches a condition (e.g., right edge), load next level.
- Implement saving/loading: Press S to save current level to “save.txt”, on start read “save.txt” if it exists and start from saved level.
- ESC to quit.

**Testing:**

- Reach level end, load next level.
- Press S to save.
- Restart game, should resume from saved level.

### Milestone 4: Enemies, Obstacles, & Collisions

**Requirements:**

- Add enemies with simple AI (patrol or follow player).
- Add obstacles that harm player.
- Player loses health on collision with enemies or obstacles.
- If health=0, show “Game Over”, allow restart (R key).
- ESC to quit.

**Testing:**

- Ensure collisions reduce health.
- At health=0, “Game Over” displays, R resets game or level.

### Milestone 5: Audio, UI, & Polish

**Requirements:**

- Add background music (looping).
- Sound effects for player actions (jump, coin pickup, enemy hit).
- Display HUD: health bar, score, level number.
- Add a pause menu (press P to pause/resume).
- Polish animations, transitions, ensure stable framerate.

**Testing:**

- Check audio plays at correct moments.
- Pause menu works, HUD updates properly.
- Everything feels consistent and polished.

### (Optional) Milestone 6: Advanced Features & Final Release

**Requirements:**

- Add optional advanced features: networked high score submission, extra animations, special effects.
- Final bug fixes, optimization passes.
- Package the game: provide instructions, ensure it runs smoothly without debug logs.

**Testing:**

- Test advanced features manually.
- Confirm stable release.

---

## Reference Solutions and Automated Tests

Because these assignments and the capstone are more open-ended and complex, reference solutions will focus on minimal but correct implementations of each requirement. Automated tests will check for key conditions (e.g., correct score increment, correct screen output), but due to complexity, manual testing will also be necessary.

For each assignment stage and capstone milestone, a corresponding `.c` file (e.g., `assignment1_stage1.c`) and test script (e.g., `assignment1_stage1_test.py`) are provided. The tests can check basic output conditions. You should also run the application and verify behavior manually.

---

## Final Checklist

- **Detailed Explanations:**  
  This session clearly details what each stage and milestone requires, removing vagueness. Each requirement is explicit: what to draw, what to respond to, how to handle states, scoring, saving/loading, audio, and UI.

- **All Concepts Explained Before Use:**  
  Previous sessions covered all foundational skills (graphics, input, audio, collisions, physics, advanced features). Now you apply them in a structured, cumulative manner.

- **3–5 Exercises per Concept:**  
  This session does not have simple exercises but multi-stage assignments and a capstone with multiple milestones. Each stage/milestone is a substantial task.

- **Starter Code and Tests:**  
  The command at the top creates all required files. Each stage’s `.c` file starts as a template you fill in. Automated tests for each stage ensure basic correctness.

- **Reference Solutions and Autotests:**  
  Minimal reference solutions will be provided as examples. Tests verify key behaviors like screen output, score changes, and file creation. Some testing requires manual playtesting.

- **Consistent Filenames and Structures:**  
  File naming follows a clear pattern: `assignment1_stageX.c` for each stage of Assignment 1, similarly for Assignment 2 and `capstone_milestoneX.c` for the capstone.

- **No Unmet Dependencies:**  
  All required techniques have been introduced in earlier sessions.

- **Self-Contained Materials:**  
  This session serves as a final roadmap, listing exact specifications. Students have a clear path to integrate all learned skills into comprehensive projects.

This completes Session 11, giving you a detailed blueprint for multi-stage assignments and the capstone project. By following these specifications, you’ll gradually build and refine complete, polished games that demonstrate mastery of SplashKit and C programming.