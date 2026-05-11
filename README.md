# Flappy Bird Clone - React Native & Matter.js

An authentic, fully functional clone of the classic Flappy Bird game built from scratch using **React Native**, **Expo**, and the **Matter.js** 2D physics engine.

This project demonstrates how to build high-performance mobile games using web technologies by decoupling game physics from React's rendering cycle.

## Tech Stack

* **Framework:** [React Native](https://reactnative.dev/) / [Expo](https://expo.dev/)
* **Game Engine:** [React Native Game Engine](https://github.com/bberak/react-native-game-engine)
* **Physics Engine:** [Matter.js](https://brm.io/matter-js/)
* **Animations:** React Native `Animated` API

## Key Features

* **Rigid Body Physics:** Utilizes `Matter.js` for realistic gravity, velocity, and collision detection.
* **Continuous Game Loop:** Powered by `react-native-game-engine` running at a smooth 60 FPS.
* **Dynamic Obstacle Generation:** Infinite procedural generation of pipes with randomized vertical gaps.
* **Sprite Animation:** Custom frame-by-frame rendering for the bird's wing-flapping animation.
* **State Management:** Seamless transitions between Idle, Playing, Paused, and Game Over states.
* **Score Tracking:** Real-time score tracking and persistent "Best Score" logic.

## Technical Highlights

Building a game in React Native requires overcoming unique performance challenges. Here is how I solved them:

1. **Decoupling Physics from React State:** To avoid stale closures and React re-render lag, the core `PhysicsSystem` interacts directly with mutable module-level variables (like `_birdFrame` and `pair.topH`). React is only used as a presentation layer to paint the current physical state on the screen.
2. **Efficient Collision Detection:** Implemented `Matter.js` collision filters (bitmasking) alongside an AABB (Axis-Aligned Bounding Box) fallback system to ensure collisions register exactly once without bogging down the engine.
3. **Memory Management:** Instead of infinitely creating new pipe bodies as the game progresses, pipes are recycled and repositioned once they leave the left side of the screen, keeping memory usage flat.
4. **Native Animations:** The scrolling ground effect uses React Native's `Animated` API with `useNativeDriver: true` to offload the animation work to the native UI thread, ensuring zero frame drops.

## Installation & Running

To run this project locally on your iOS or Android device:

```bash
# Clone the repository
git clone <your-repo-url>
cd mobiledev-flappybird

# Install dependencies
npm install

# Start the Expo development server
npx expo start

```

*Scan the QR code with the Expo Go app on your phone to play!*

## What I Learned

This project was a fantastic deep dive into the bridge between standard React Native component rendering and constant-tick game loops. 
It reinforced the importance of reference stability, garbage collection in JavaScript, and using tools like `Matter.js` to handle
complex math and spatial logic under the hood!
