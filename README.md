# Directional Dodge/Roll System for Unreal Engine

Below is a clear, step-by-step guide to setting up a Directional Dodge system using IA_Move values and Atan2. This approach follows the tutorial by Brotherwolf but incorporates a more accurate controller-friendly system, by me. Watch the original video by Brotherwolf to understand the system, and later come back for the upgraded version here.

Brotherwolf 8 Directional Video: https://www.youtube.com/watch?v=vhQmYIYBAdE&t=2s

# My upgraded version

![image](https://github.com/user-attachments/assets/a569766c-8de8-4873-80c9-e5d64941a4cb)

# 1. Use the IA_Move Values

Why: Relying on IA_Move (Enhanced Input) ensures consistent and accurate float values from -1 to 1, rather than manually reading X and Y from input events.

How: Drag the IA_Move node into your Get Direction function and connect the X and Y outputs as shown in the first image.

# 2. Convert to Degrees with Atan2

Why: Atan2 calculates an angle based on X and Y values.

How: Pass the IA_Move X (horizontal) and Y (vertical) into the Atan2 (Degrees) node.

Note: Atan2 will return an angle in the range -180° to 180°.

# 3. Shift the Angle from -180 to 180 Into 0 to 360

Why: It's often easier to handle angles in a 0–360 range.

How: Simply add 180 to the Atan2 output. This converts the angle to 0°–360°.

# 4. Decide How Many Dodge Directions You Want

For 16 Directions
Divide your 0–360 angle by 22.5 (because 360/16 = 22.5).
The resulting float will be in the range 0–16.
You will need 16 dodge animations or montage sections if you choose this approach.

For 8 Directions
Divide your 0–360 angle by 45 (because 360/8 = 45).
The resulting float will be in the range 0–8.
You will need 8 dodge animations or montage sections if you choose this approach.

# 5. Round to Get an Integer

Why: To cleanly select a montage section (or animation) based on these angles, convert the float to an integer.

How: Pass the result of the division (either 0–16 or 0–8) into a Round node. This returns an integer.

# 6. Use a ‘Select’ Node with the Rounded Value

Why: The Select node outputs a specific value (e.g., the name of a montage section) based on the incoming integer.

How: Create a Select node with enough pins to match your number of directions (e.g., 0–16 or 0–8).
Plug the Rounded integer into the Select node’s Index.
Assign each pin to the correct animation section name in your roll (dodge) montage.

# Example for 8 Directions

If you’re using 8 directions, you’ll have pins numbered from 0 to 8. The image below shows how it might look. Ensure your montage has section names that match these directions.

![image](https://github.com/user-attachments/assets/e1c86783-39a0-4537-81f9-38b1038c92b1)

# Example for 16 Directions

If you’re using 16 directions, you’ll have pins numbered from 0 to 16. The image below shows how it might look. Ensure your montage has section names that match these directions.

![image](https://github.com/user-attachments/assets/e80f3180-8167-42ee-8d50-32d7654271a0)


# Tip: If you don’t understand how the Select node’s pins correspond to directions:

The middle options often correspond to Forward.
The first and last pins typically correspond to Backward.
Arrange them so that negative X/Y inputs match backward/left directions, and positive X/Y inputs match forward/right directions, as shown in the images.

# Final Notes

This setup gives you a robust directional dodge system that works smoothly with both keyboard/mouse and controllers.
Make sure all montage sections are correctly named and match the integer values coming from the Round node.
Adjust the angle division (22.5 for 16 directions, 45 for 8 directions) depending on how many unique dodge directions and animations you want to support.
With this approach, you’ll have an upgraded version of the Brotherwolf roll system that fully supports controllers and allows for more accurate directional input.
