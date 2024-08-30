# Learn Electron Js in Baby Steps

## Table of Contents
1. [Introduction to Electron.js](#introduction-to-electronjs)
2. [How Electron Works](#how-electron-works)
3. [Getting Started with Electron](#getting-started-with-electron)
4. [High-Complexity App](#high-complexity-app)
5. [Advanced Architecture Proposal](#advanced-architecture-proposal)
   - [Shared Module](#shared-module)
   - [Frontend Module](#frontend-module)
   - [Backend Module](#backend-module)
   - [Communication Layer](#communication-layer)
6. [Conclusion](#conclusion)
7. [Resources](#resources)

## Introduction to Electron.js

Electron.js is a popular framework for building cross-platform desktop applications using web technologies like HTML, CSS, and JavaScript. It has been widely adopted by companies like Microsoft, Slack, and Twitch due to its ease of use and the ability to leverage existing web development skills.

## How Electron Works

Electron embeds Chromium and Node.js in its binary, which allows developers to write desktop applications without needing to write native code. The architecture is composed of two types of processes:
- **Main Process**: Manages the application lifecycle, window management, and interactions with native APIs.
- **Renderer Process**: Manages the rendering of each window, with each window running in its isolated renderer process.

## Getting Started with Electron

Electron provides abstractions and uses familiar languages, which reduces development time and costs. It also facilitates building and deploying app updates, making it easy to keep cross-platform apps in sync. However, this ease of use comes with trade-offs, particularly in resource consumption and performance.

## High-Complexity App

High-complexity apps, like batch image processing tools, must handle extensive backend workloads entirely within Electron.

- **Features**:
  - Custom codebase for the desktop app.
  - Separate release cycles.
  - Backend executed within Electron.
  - Potential use of native modules for performance optimization.

- **Example Architecture**:
  - Backend logic executed in a separate Node.js process to avoid UI performance degradation.

![High Complexity Electron App Architecture](https://res.cloudinary.com/practicaldev/image/fetch/s--g-93R0mR--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_800/https://blog.logrocket.com/wp-content/uploads/2021/07/advanced-modularized-architecture-proposal.png)

## Advanced Architecture Proposal

For complex Electron apps, a more modularized and specialized architecture is recommended to tackle performance degradation, communication issues, and developer experience challenges.

### Shared Module

The shared module contains code and types that are used by both the frontend and backend. This enables separate development while maintaining consistency in domain models and utilities.

- **Features**:
  - TypeScript codebase.
  - Typings for message passing.
  - Domain models and shared utilities.

### Frontend Module

The frontend module focuses entirely on UI components and animations, separating it from business logic. It uses React and Redux for building and managing the UI.

- **Features**:
  - TypeScript with shared module access.
  - React for UI with Redux for state management.
  - Communication with the backend via message passing.

### Backend Module

The backend module handles business logic and long-running operations. By running in a separate Node.js process, it ensures that the UI remains responsive.

- **Features**:
  - TypeScript with shared module access.
  - Runs as a forked Node.js process.
  - Access to native dependencies.
  - Pre-build step for matching native dependencies.

### Communication Layer

The communication layer uses `node-ipc` for interprocess communication, allowing async and event-based messaging between the frontend and backend.

- **Features**:
  - Fully typed message payloads and handlers.
  - Supports async and message-based communication.

## Conclusion

Electron.js is a versatile framework for building cross-platform desktop applications. While it simplifies the development process, performance and developer experience can be challenging in complex apps. The proposed modular architecture provides a foundation for building high-performance Electron apps, allowing developers to maintain a clean separation of concerns and optimize for performance.

## Resources

- **Documentation**: [Electron.js Official Documentation](https://www.electronjs.org/docs/latest/)

## Acknowledgements

- Architecture Proposal by by Alain Perkaz.