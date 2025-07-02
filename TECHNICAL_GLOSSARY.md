# Technical Glossary & Rationale

## Object-Oriented Programming Terms

### **Class Encapsulation**
**Definition**: The bundling of data (attributes) and methods (functions) that operate on that data within a single unit (class), while restricting direct access to internal components.

**Rationale**: Implemented throughout the project with classes like `GameState`, `Move`, and `CastleRights`. Encapsulation protects game state integrity by controlling how external code can interact with chess rules and game data. Essential for maintaining consistent game behavior and preventing invalid state modifications.

### **Composition Pattern**
**Definition**: A design principle where complex objects are built by combining simpler objects, establishing "has-a" relationships rather than "is-a" relationships.

**Rationale**: The `GameState` class uses composition with `Move` objects and `CastleRights` objects to build comprehensive game functionality. This allows flexible combination of features and easier testing of individual components. Essential for modular design and code reusability.

### **Data Abstraction**
**Definition**: The concept of hiding implementation details while providing a simplified interface for interacting with complex systems.

**Rationale**: The chess engine abstracts complex rule validation behind simple method calls like `getValidMoves()` and `makeMove()`. Users don't need to understand pin detection algorithms or check calculations. Essential for creating usable interfaces and managing system complexity.

### **Method Polymorphism**
**Definition**: The ability to use the same interface (method name) for different underlying implementations, particularly seen in piece movement strategies.

**Rationale**: Each piece type (pawn, rook, knight, etc.) has its own movement logic accessed through the same `moveFunctions` dictionary interface. This allows uniform handling of different piece types while maintaining their unique behaviors. Essential for extensible and maintainable code.

### **Object State Management**
**Definition**: The practice of maintaining and controlling the internal state of objects throughout their lifecycle, ensuring consistency and validity.

**Rationale**: The `GameState` class carefully manages board position, turn information, castling rights, and move history. State changes are controlled through specific methods that maintain game rule compliance. Essential for game integrity and reliable undo/redo functionality.

## Chess Domain Terms

### **Alpha-Beta Pruning**
**Definition**: An optimization technique for the minimax algorithm that eliminates branches in the game tree that cannot possibly influence the final decision.

**Rationale**: Implemented in `chessAi.py` to significantly reduce the number of positions evaluated during AI search. This allows deeper search within reasonable time constraints, making the AI both stronger and more responsive. Essential for making the AI computationally feasible at higher search depths.

### **Board Representation**
**Definition**: The 8x8 2D array structure used to represent the chess board state, where each square contains either a piece identifier or empty marker ('--').

**Rationale**: Uses a simple string-based encoding (e.g., 'wK' for white king, 'bp' for black pawn) that is both human-readable and memory-efficient. This representation facilitates easy piece identification, move validation, and board state manipulation throughout the game engine.

### **Castling Rights**
**Definition**: A tracking system that monitors whether each player can still perform kingside or queenside castling moves.

**Rationale**: Implemented as the `CastleRights` class to maintain chess rule compliance. Castling availability changes based on king and rook movements, requiring persistent state tracking. Essential for proper chess rule implementation and game state integrity.

### **Checkmate**
**Definition**: A game-ending condition where a king is in check and has no legal moves to escape capture.

**Rationale**: Fundamental chess rule requiring sophisticated detection logic. The system must validate that all possible moves still leave the king in check. Critical for determining game outcomes and triggering appropriate UI responses and AI evaluation bonuses.

### **En Passant**
**Definition**: A special pawn capture rule allowing capture of a pawn that has just moved two squares forward, as if it had only moved one square.

**Rationale**: Complex chess rule requiring temporal state tracking (the opportunity only exists for one turn). Implemented with `enpasantPossible` coordinates to maintain rule accuracy. Necessary for complete chess rule compliance and competitive gameplay.

### **Minimax Algorithm**
**Definition**: A decision-making algorithm for two-player games that minimizes the maximum possible loss (or maximizes the minimum possible gain).

**Rationale**: Core of the AI decision-making process in `chessAi.py`. Provides optimal play assuming both players play perfectly. Essential for creating an intelligent chess opponent that can evaluate positions multiple moves ahead and make strategic decisions.

### **Move Validation**
**Definition**: The process of determining whether a proposed move is legal according to chess rules, including checks, pins, and special move conditions.

**Rationale**: Critical for game integrity and preventing invalid game states. Implemented through comprehensive algorithms that consider piece movement patterns, board obstacles, check conditions, and special rules. Ensures fair play and rule compliance.

### **Piece-Square Tables**
**Definition**: Evaluation matrices that assign positional values to pieces based on their location on the board.

**Rationale**: Provides strategic knowledge to the AI beyond simple material counting. Different tables for each piece type (knights prefer center, pawns advance toward promotion) encode centuries of chess strategy. Essential for creating an AI that understands positional play.

### **Pin Detection**
**Definition**: Identification of pieces that cannot move because doing so would expose the king to check.

**Rationale**: Complex but essential chess mechanic requiring line-of-sight analysis between attacking pieces and the king. Properly implemented in move generation to prevent illegal moves. Critical for maintaining game rule accuracy and realistic chess behavior.

### **Stalemate**
**Definition**: A draw condition where a player has no legal moves but is not in check.

**Rationale**: Important chess rule that prevents certain endgame positions from being winning. Requires detection logic to identify when all moves would result in check. Essential for complete chess implementation and proper game outcome determination.

## Technical Architecture Terms

### **Event-Driven Programming**
**Definition**: A programming paradigm where program flow is determined by events such as user inputs, sensor outputs, or messages from other programs.

**Rationale**: Pygame's event system drives the main game loop, handling mouse clicks, keyboard input, and system events. This architecture provides responsive user interaction and clean separation between input handling and game logic. Essential for interactive game applications.

### **Game Loop**
**Definition**: The central control structure that continuously processes input, updates game state, and renders output while the game is running.

**Rationale**: Implemented in `main.py` as the core execution pattern. Provides consistent frame rate, smooth animation, and responsive input handling. Essential architecture pattern for real-time interactive applications like games.

### **Game State**
**Definition**: The complete set of information describing the current condition of the game, including board position, turn to move, castling rights, and move history.

**Rationale**: Centralized in the `GameState` class to maintain consistency and enable features like undo, move validation, and game analysis. Provides single source of truth for all game information and enables complex operations like position evaluation.

### **Multiprocessing**
**Definition**: The use of multiple CPU processes to execute tasks concurrently, particularly for AI computation while maintaining UI responsiveness.

**Rationale**: Prevents the UI from freezing during AI calculation by running move search in a separate process. Essential for user experience when AI performs deep searches that can take several seconds. Allows the game to remain interactive during AI thinking time.

### **Object-Oriented Design**
**Definition**: A programming paradigm organizing code into classes and objects that encapsulate data and behavior, promoting code reusability and maintainability.

**Rationale**: Used throughout the project with classes like `GameState`, `Move`, and `CastleRights`. Provides clear code organization, encapsulation of related functionality, data hiding, and easier maintenance. Essential for managing the complexity of chess rules, game state, and creating extensible, professional-quality software architecture.

### **Rendering Pipeline**
**Definition**: The sequence of operations that convert game state into visual output, including board drawing, piece placement, and UI elements.

**Rationale**: Implemented in `main.py` drawing functions to provide visual feedback to players. Includes layers for board, pieces, highlights, and move indicators. Essential for user interface and game visualization.

## AI & Algorithm Terms

### **Depth-Limited Search**
**Definition**: A search strategy that explores the game tree only to a predetermined depth to limit computation time.

**Rationale**: Balances AI strength with response time by limiting how many moves ahead the AI considers. Configurable depth allows adjustment of difficulty level. Essential for making AI computation practical within reasonable time constraints.

### **Evaluation Function**
**Definition**: A function that assigns a numerical value to a game position, indicating how favorable it is for a particular player.

**Rationale**: Combines material value and positional factors to guide AI decision-making. Implemented in `scoreBoard()` function with piece values and position tables. Essential for AI to make intelligent decisions when it cannot search to the end of the game.

### **Negamax**
**Definition**: A variant of the minimax algorithm that simplifies implementation by using the mathematical property that max(a,b) = -min(-a,-b).

**Rationale**: Reduces code complexity by eliminating separate maximize and minimize functions. Implemented in `findMoveNegaMaxAlphaBeta()` for cleaner, more maintainable AI code. Provides identical results to minimax with simpler implementation.

### **Position Scoring**
**Definition**: The process of evaluating a chess position numerically, considering both material and positional factors.

**Rationale**: Enables AI to make strategic decisions beyond simple piece counting. Incorporates chess knowledge through piece-square tables and special conditions. Essential for creating an AI that plays strategically rather than just tactically.

### **Search Tree**
**Definition**: A tree structure representing all possible sequences of moves from a given position, where each node represents a game state.

**Rationale**: Fundamental data structure for game AI, allowing systematic exploration of possible futures. Pruning techniques reduce the effective size. Essential for look-ahead planning and optimal move selection.

### **Turn Multiplier**
**Definition**: A value (+1 or -1) used in negamax to automatically handle the alternating maximize/minimize behavior for different players.

**Rationale**: Simplifies score evaluation by automatically adjusting perspective based on whose turn it is. Eliminates need for separate maximize and minimize logic. Essential component of the negamax algorithm implementation.

## Pygame & UI Terms

### **Asset Loading**
**Definition**: The process of loading external resources (images, sounds) into memory for use during gameplay.

**Rationale**: Implemented in `loadImages()` function to preload piece graphics and sound effects. Prevents loading delays during gameplay and ensures smooth user experience. Essential for performance and user interface quality.

### **Collision Detection**
**Definition**: Determining whether user input (mouse clicks) intersects with game objects (board squares, pieces).

**Rationale**: Translates mouse coordinates to board positions for piece selection and movement. Essential for user interaction and converting screen coordinates to game logic coordinates.

### **Double Buffering**
**Definition**: A rendering technique that draws to an off-screen buffer before displaying, preventing visual artifacts.

**Rationale**: Pygame's `pygame.display.flip()` provides smooth visual updates without flickering. Essential for professional-looking graphics and smooth animation in the user interface.

### **Frame Rate Control**
**Definition**: Limiting the number of screen updates per second to maintain consistent performance and prevent excessive CPU usage.

**Rationale**: `MAX_FPS = 15` provides sufficient smoothness for chess while conserving system resources. Chess doesn't require high frame rates like action games. Essential for performance optimization and battery life on portable devices.

### **Sprite**
**Definition**: A 2D image or animation that represents a game object, in this case chess pieces.

**Rationale**: Piece images loaded and scaled for board display. Provides visual representation of game state and enhances user experience. Essential component of the graphical user interface.

### **Surface**
**Definition**: Pygame's fundamental object for representing images, including the main screen and individual piece graphics.

**Rationale**: All visual elements are drawn onto surfaces, which are then composed to create the final display. Essential Pygame concept for graphics management and rendering pipeline.

## Data Structure Terms

### **2D Array**
**Definition**: A two-dimensional data structure used to represent the chess board as rows and columns of squares.

**Rationale**: Natural mapping to the chess board's 8x8 grid structure. Allows efficient access to any square using row/column coordinates. Essential for board representation and move calculation algorithms.

### **Move History Stack**
**Definition**: A list structure (`moveLog`) that maintains the sequence of moves played, enabling undo functionality and game analysis.

**Rationale**: Provides complete game state reconstruction and undo capability. Essential for features like move reversal, game replay, and position analysis. Maintains game integrity and user experience.

### **Queue**
**Definition**: A first-in-first-out data structure used for inter-process communication between the main game thread and AI computation process.

**Rationale**: Safely passes AI move decisions from the background process to the main game thread. Essential for multiprocessing implementation and maintaining thread safety in concurrent execution.

### **String Encoding**
**Definition**: The representation of chess pieces as two-character strings (color + piece type).

**Rationale**: Compact, human-readable piece identification system. Easy to parse for AI evaluation and user interface display. Essential for efficient board representation and piece manipulation.

## Configuration & Constants

### **Bot Configuration**
**Definition**: Global variables (`SET_WHITE_AS_BOT`, `SET_BLACK_AS_BOT`) that determine which players are controlled by AI.

**Rationale**: Enables flexible game modes (human vs human, human vs AI, AI vs AI) without code changes. Essential for supporting different play scenarios and testing AI behavior.

### **Color Themes**
**Definition**: Predefined color combinations for board squares and UI elements.

**Rationale**: Provides visual customization options and accessibility considerations. Multiple commented theme options show extensibility. Essential for user preference accommodation and visual appeal.

### **Magic Numbers**
**Definition**: Hard-coded numerical constants throughout the code (board dimensions, piece values, search depth).

**Rationale**: While not ideal practice, these constants define game behavior and display characteristics. Should be moved to configuration files for better maintainability. Essential for game functionality but could be better organized.

### **Search Depth**
**Definition**: The `DEPTH` constant that controls how many moves ahead the AI searches.

**Rationale**: Primary difficulty control mechanism. Higher values create stronger but slower AI. Set to 2 by default for balance between strength and response time. Essential for AI behavior tuning and user experience.
