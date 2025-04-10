# Algorithm Visualizer

A C++/SFML-based visualizer for the merge and quick sort algorithms, designed to help you see how they work in real-time.

## Features

- Visualizes the sorting processes of merge and quick sort step-by-step
- Compares the performance of the algorithms on a large data set (125,000 entries) in three scenarios
      - Unsorted
      - Already sorted
      - Reverse sorted
- Cross-platform CMake build system
- Minimal setup -- just clone and run!

### Requirements

- CMake 3.8+
- Git (Required for CMake to fetch SFML)
- C++17

The following resource files are included in the repository
- resources/data/2020_taxi_data.csv (Dataset file)
- resources/fonts/Roboto-Bold.ttf (Font file)

### Build & Run
1. Clone the repository: ``` git clone https://github.com/zwright03/Three-Peas-In-a-Pod.git && cd Algorithm-Visualizer ```
2. Create build folder: ``` mkdir build && cd build ```
3. Generate Project: ``` cmake .. ```