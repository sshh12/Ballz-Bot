# Ballz Bot

A python based bot for the mobile game [Ballz](https://play.google.com/store/apps/details?id=com.ketchapp.ballz).

## Dependencies
* [PIL](http://www.pythonware.com/products/pil/)
* [Pytesser](https://pypi.python.org/pypi/PyTesser)
* [Pygame](https://www.pygame.org/)

## Usage
1. Clone Repo.
2. Install all dependencies
3. Install [adb](https://developer.android.com/studio/command-line/adb.html)
4. Connect Android device (with 1080p screen)
5. Open Ballz App and start a game
6. Run ballz.py

## How it works
The task of playing the game is split into 3 different steps and in game
interaction is carried out using command line adb tools.
##### 1. Get the Current Game State
The program uses adb to take a screenshot of the device's screen. The image is then processed by [PIL](http://www.pythonware.com/products/pil/) to extract important features. Using [Pytesser](https://pypi.python.org/pypi/PyTesser), the program uses the processed screenshot to read the numbers on every block to create a 2D array that represents the board as well as read the number of balls available for the round.
##### 2. Simulate
For every possible angle, a digital environment is constructed based on the captured game state. Using a lite physics engine the trajectories of the balls are calculated as well as the blocks they will collide with. After running each simulation until all balls have returned to the bottom of the screen, they each return the resultant board.
##### 3. Heuristic and Execution
Using the game state retrieved from every angle, the program uses a simple algorithm to determine the cost (in essence how bad the swipe was). It then chooses the angle from the simulation with the lowest cost and then calculated the physical swipe needed to perform it. Using the Android command line, the swipe is executed, and the program waits until it thinks that the round is over (roughly calculated using the number of frames in the physics engine and the actual frame rate of the device) before starting again.

![equation](https://user-images.githubusercontent.com/6625384/27922057-6c8ada9e-623f-11e7-9429-f4e8dfa65b6f.gif)

##### Screenshot

![screenshot](https://cloud.githubusercontent.com/assets/6625384/25557899/f4b1f0fe-2ce0-11e7-9245-463100049ea3.gif)
