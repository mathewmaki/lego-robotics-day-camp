# Code Examples

Here are a few code examples :)

## Sounds
```` python
# Initalize hub
hub = PrimeHub()

# Start beeping at note 60
hub.speaker.start_beep(60)

# Stop beeping after 3 seconds
wait_for_seconds(3)
hub.speaker.stop()
````

## Light Matrix
```` python
# Initalize hub
hub = PrimeHub()

# Show the XMAS image on the hub
hub.light_matrix.show_image('XMAS')

# Wait 2 seconds
wait_for_seconds(2)

# Write a message on the screen
hub.light_matrix.write("Code Ninjas!")


# Set pixels to make a striped pattern
for y in range(0, 5, 2):
    for x in range(5):
        hub.light_matrix.set_pixel(x, y)

# Wait for 2 seconds
wait_for_seconds(2)

# Turn off the light matrix
hub.light_matrix.off()
````
[List of images](index.md#spike.LightMatrix.show_image--parameters)

## Status Light
```` python
# Initalize hub
hub = PrimeHub()

# List of status light colors
colors = ['azure', 'black', 'blue', 'cyan', 'green', 'orange', 'pink', 'red', 'violet', 'yellow', 'white']

# Cycle through all the colors
for color in colors:
    hub.status_light.on(color)
    wait_for_seconds(1)

# Turn off the status light
hub.status_light.off()
````

## Motion Sensor
```` python
# Initalize hub
hub = PrimeHub()

# Get a gesture from the hub's motion sensor
gesture = hub.motion_sensor.wait_for_new_gesture()

# Show a different image based on the type of gesture
if gesture == 'shaken':
    hub.light_matrix.show_image('HAPPY')
elif gesture == 'tapped':
    hub.light_matrix.show_image('MEH')
elif gesture == 'doubletapped':
    hub.light_matrix.show_image('SILLY')
elif gesture == 'falling':
    hub.light_matrix.show_image('SURPRISED')
````

## Color Sensor
```` python
# Initalize hub
hub = PrimeHub()

# Initialize the color sensor plugged into port A
color_sensor = ColorSensor('A')

# Get the color from the color sensor
color = color_sensor.get_color()

# Show a ghost if the color is blue
if color == 'blue':
    hub.light_matrix.show_image('GHOST')


# Wait 2 seconds
wait_for_seconds(2)

# Make a spinning animation on the color sensor
for i in range(10):
    color_sensor.light_up(100, 0, 0)
    wait_for_seconds(0.1)
    color_sensor.light_up(0, 100, 0)
    wait_for_seconds(0.1)
    color_sensor.light_up(0, 0, 100)
    wait_for_seconds(0.1)

# Turn off the color sensor light
color_sensor.light_up_all(0)
````
[List of colors](index.md#spike.ColorSensor.wait_until_color--parameters)

## Force Sensor
```` python
# Initalize hub
hub = PrimeHub()

# Initialize the force sensor plugged into port A
button = ForceSensor('A')

# Show a pacman when the button is pressed
button.wait_until_pressed()
hub.light_matrix.show_image('PACMAN')

# Show a pitchfork when the button is released
button.wait_until_released()
hub.light_matrix.show_image('PITCHFORK')
````

## Distance Sensor
```` python
# Initalize hub
hub = PrimeHub()

# Initialize the distance sensor plugged into port A
distance_sensor = DistanceSensor('A')

# Show a duck if the distance is greater than 20cm
distance_sensor.wait_for_distance_farther_than(20, 'cm')
hub.light_matrix.show_image('DUCK')

# Make a light animation when the distance is closer than 20cm
distance_sensor.wait_for_distance_closer_than(20, 'cm')
hub.light_matrix.off()

for i in range(10):
    distance_sensor.light_up(100, 0, 0, 0)
    wait_for_seconds(0.2)
    distance_sensor.light_up(0, 100, 0, 0)
    wait_for_seconds(0.2)
    distance_sensor.light_up(0, 0, 100, 0)
    wait_for_seconds(0.2)
    distance_sensor.light_up(0, 0, 0, 100)
    wait_for_seconds(0.2)

# Turn off the lights
distance_sensor.light_up_all(0)
````

## Single Motor
```` python
# Initalize hub
hub = PrimeHub()

# Initialize the motor plugged into port A
motor = Motor('A')

# Set the motor to position 0
motor.run_to_position(0)

wait_for_seconds(2)

# Start the motor at 100% speed
motor.start(100)

hub.light_matrix.write('Motor started')

# Stop the motor and wait 2 seconds
motor.stop()
wait_for_seconds(2)

# Set the motor speed to 75%
motor.set_default_speed(75)

# Run the motor for 2 rotations
motor.run_for_rotations(2)

wait_for_seconds(1)

# Run the motor 90 degrees counter clockwise
motor.run_for_degrees(-90)

wait_for_seconds(2)

# Run the motor for 2 seconds
motor.run_for_seconds(2)
````

## Motor Pairs
```` python
# Initalize the motors plugged into ports A and B
motors = MotorPair('A', 'B')

# Set the default speed to 75%
motors.set_default_speed(75)

# Drive forward 30cm
motors.move(30, 'cm')

wait_for_seconds(2)

# Drive backwards 30cm and steer right
motors.move(-30, 'cm', 50)

wait_for_seconds(2)

# Start the motors
motors.start()

wait_for_seconds(3)

# Stop the motors
motors.stop()
````