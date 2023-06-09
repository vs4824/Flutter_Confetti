# Flutter Confetti

## Getting Started

To use this plugin, add confetti as a dependency in your pubspec.yaml file.

See the example to get started quickly. To generate the platform folders run:

   ```
   flutter create .
   ```

in the example folder.

To begin you need to instantiate a ConfettiController variable and pass in a Duration argument. The ConfettiController can be instantiated in the initState method and disposed in the dispose method.

In the build method return a ConfettiWidget. The only attribute that is required is the ConfettiController.

Other attributes that can be set are:

1. blastDirectionality -> an enum value to state if the particles shoot in random directions or a specific direction. BlastDirectionality.explosive will shoot in random directions and don't require a blastDirection to be set. BlastDirectionality.directional requires a blastDirection to specify the direction of the confetti.

2. blastDirection -> a radial value to determine the direction of the particle emission. The default is set to PI (180 degrees). A value of PI will emit to the left of the canvas/screen.

3. emissionFrequency -> should be a value between 0 and 1. The higher the value the higher the likelihood that particles will be emitted on a single frame. Default is set to 0.02 (2% chance)

4. numberOfParticles -> the number of particles to be emitted per emission. Default is set to 10

5. shouldLoop -> determines if the emission will reset after the duration is completed, which will result in continues particles being emitted, and the animation looping

6. maxBlastForce -> will determine the maximum blast force applied to a particle within it's first 5 frames of life. The default maxBlastForce is set to 20

7. minBlastForce -> will determine the minimum blast force applied to a particle within it's first 5 frames of life. The default minBlastForce is set to 5

8. displayTarget -> if true a crosshair will be displayed to show the location of the particle emitter

9. colors -> a list of colors can be provided to manually set the confetti colors. If omitted then random colors will be used. A single color, for example [Colors.blue], or multiple colors [Colors.blue, Colors.red, Colors.green] can be provided as an argument in the `ConfettiWidget

10. strokeWidth optionally set to give a stroke to the paint. Needs to be bigger than 0 to be vissible. Default 0.

11. strokeColor optionally set to give a stroke color. Default black.

12. minimumSize -> a Size controlling the minimum possible size of the confetti. To be used in conjuction with maximumSize. For example, setting a minimumSize equal to Size(10,10) will ensure that the confetti will never be smaller than the specified size. Must be positive and smaller than the maximumSize. Can not be null.

13. maximumSize -> a Size controlling the maximum possible size of the confetti. To be used in conjuction with minimumSize. For example, setting a maximumSize equal to Size(100,100) will create confetti with a size somewhere between the minimum and maximum size of (100, 100) [widht, height]. Must be positive and bigger than the minimumSize, Can not be null.

14. gravity -> change the speed at which the confetti falls. A value between 0 and 1. The higher the value the faster it will fall. Default is set to 0.1

15. particleDrag -> configure the drag force to apply to the confetti. A value between 0 and 1. A value of 1 will be no drag at all, while 0.1, for example, will be a lot of drag. Default is set to 0.05

16. canvas -> set the size of the area where the confetti will be shown, by default this is set to full screen size.

17. createParticlePath -> An optional function that retuns a custom Path to generate unique particles. Default returns a rectangular path.

## Example of a custom createParticlePath

   ```
   Path drawStar(Size size) {
    // Method to convert degree to radians
    double degToRad(double deg) => deg * (pi / 180.0);

    const numberOfPoints = 5;
    final halfWidth = size.width / 2;
    final externalRadius = halfWidth;
    final internalRadius = halfWidth / 2.5;
    final degreesPerStep = degToRad(360 / numberOfPoints);
    final halfDegreesPerStep = degreesPerStep / 2;
    final path = Path();
    final fullAngle = degToRad(360);
    path.moveTo(size.width, halfWidth);

    for (double step = 0; step < fullAngle; step += degreesPerStep) {
      path.lineTo(halfWidth + externalRadius * cos(step),
          halfWidth + externalRadius * sin(step));
      path.lineTo(halfWidth + internalRadius * cos(step + halfDegreesPerStep),
          halfWidth + internalRadius * sin(step + halfDegreesPerStep));
    }
    path.close();
    return path;
  }
   ```
