# CodeBreaker

A multiplayer puzzle game built with Java sockets and Swing. Players connect to a central server, join a waiting room, and race to crack the 3-digit code hidden in each image. The first player to enter the correct code wins the round.

## How it works

- **Server** (`GameServer`) listens on port `5555` and accepts any number of client connections, each handled on its own thread (`ClientHandler`).
- **Waiting room:** once 2 players are ready, a 10-second countdown starts. A game begins when the countdown ends or when 5 players have joined.
- **Game room** (`GameRoom`): players see the same puzzle image and have 4 minutes to solve it. A correct answer earns 1 point and moves everyone to the next puzzle.
- **Game over:** after 5 puzzles the player with the most points wins. The game also ends if only one player is left.
- **Client** (`GameClient`) is a Swing GUI that shows connected players, the waiting room, the puzzle, and a live scoreboard.

## Project structure

```
src/codebreaker/
├── GameServer.java     # Accepts connections, manages waiting room and game rooms
├── ClientHandler.java  # One thread per connected player
├── GameRoom.java       # Runs a single game: stages, timer, scoring
├── GameState.java      # Puzzles, answers, and player points
├── GameClient.java     # Swing client GUI
└── NetworkLevels/      # Puzzle images
```

## Requirements

- Java 17 or later
- [Apache NetBeans](https://netbeans.apache.org/) (optional; the project uses NetBeans/Ant)

## Running the game

### With NetBeans
1. Open the project folder in NetBeans.
2. Run `GameServer.java` (the project's main class).
3. Right-click `GameClient.java` and choose **Run File**. Repeat for each player.

### From the command line
Run these from the project root folder (the client loads images from `src/codebreaker/NetworkLevels`):
```bash
javac -d out src/codebreaker/*.java

# Terminal 1 - start the server
java -cp out codebreaker.GameServer

# Terminals 2, 3, ... - start one client per player
java -cp out codebreaker.GameClient
```

The client connects to `localhost:5555` by default. To play across machines, change `HOST` in `GameClient.java` to the server's IP address.


