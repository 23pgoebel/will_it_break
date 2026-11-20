# Will it Break?

## Purpose
- The app will allow users to design and build a a cost effective 2D virtual bridge and drive various vehicles across it. The app will show the cost of the bridge, the stress in each member through color as the vehicles drive across, and a message if the bridge exceeds the allowable stresses.

## Inputs
- User has a 60ft by 25ft grid with a point at every foot to build a bridge using members and joints. Joints may be located on the intersection of the grid where members meet. No joints may be on the bridge except for at every 10ft interval. User chooses which vehicle will drive across their bridge in test mode.
- Give the user the option to park a vehicle at a given location 'x'. This is where the front axle will be
- These vehicles, with axle loads in lb measured back from the front axle. Each axle load is split between the two deck joints on either side of it, with the nearer joint taking more.

    Vehicle	Axles:
    Car	2,000 at 0 ft; 2,000 at 10 ft
    Loaded dump truck	12,000 at 0 ft; 17,000 at 14 ft; 17,000 at 18.5 ft
    Semi (AASHTO HS20 design truck)	8,000 at 0 ft; 32,000 at 14 ft; 32,000 at 28 ft
    Fire engine	20,000 at 0 ft; 27,000 at 17 ft; 27,000 at 21.5 ft
- Include tools to build the bridge including an eraser to click on a member to delete it, an option build with the members, a button to erase the whole bridge, the ability to drag joints to new intersections on the bridge.
- Add a vehicle dropdown for Car, Loaded Dump Truck, Semi, and Fire Engine.
- Add a numeric front-axle position field with a synchronized slider or step buttons.
- Constrain x to the bridge length and account for axle positions that fall outside the 60 ft span.
- Add Park, Drive Across, and Pause/Resume controls.
- Connect each member between two joints and prevent duplicate members.
- Show existing and proposed member lengths in the hint/status area.
- Use click-to-place on allowed intersections and show a live cursor hint.
- Disable placement on the roadway/deck except at the fixed 10 ft deck joints

## Calculations
- A truss solver using the method of joints as one linear system, with a message instead of numbers when the truss is unstable (it needs members + 3 = 2 × joints, and a system that isn't nearly singular)
    - Member capacities of 90,000 lb in tension and 75,000 lb in compression. In Test mode, members are colored by how close they are to capacity.
- Cost is calculated by multiplying the number of user-added structural joints outside the deck by $500, and the total ft of user-added structural members outside the deck by $100, then summing the two products. The deck joints, support joints, and deck members do not count toward the cost.
- Member forces use positive values for tension and negative values for compression.
- Axle loads are calculated every 0.5 ft of vehicle travel and from axle loads only; bridge weight and vehicle weight beyond the listed axle loads are not included.

## Outputs
- The app has only Build mode and Test mode. In Build mode, the user places joints on a 1 ft grid and connects them with members, and a hint on screen says what the next click will do. In Test mode, the drawing tools are hidden and the user picks a vehicle and drives it across.
- A bridge site has deck joints every 10 ft from x = 0 to x = 60, a pin at x = 0, and a roller at x = 60. These joints cannot be moved or deleted.
- Build mode displays and updates the bridge cost, joint count, member count, and structural stability status.
- Test mode displays the selected vehicle, its front-axle position, and whether the bridge is currently safe or has failed. Member forces and utilization values are not displayed on the bridge or beside individual members during Test mode.
- A details panel remains closed by default. It contains separate joint reaction and member force tables, plus labels showing positive as tension and negative as compression. Member forces are reported in pounds.
- The member force table shows each member's maximum force experienced during each selected vehicle crossing. It does not show peak utilization or where that peak occurs.
- In parked mode, the user selects the front-axle position x and the details panel shows the forces for each member at that position. It does not display member force values on the bridge.
- Member colors are the only live stress indication during Test mode: brown indicates a safety factor of at least 2, yellow through red indicates increasing closeness to the applicable tension or compression capacity, and black indicates that the member has exceeded capacity.
- When a member exceeds capacity, the vehicle stops and a visible failure state appears with the message "Your Bridge Failed", the failed member, and a Restart button. Restart returns to Build mode with the previous bridge intact.
- If the vehicle completes a crossing safely, show a success state and provide a button to drive another vehicle. The next vehicle option can return to Test mode with the vehicle selector and position controls available.
- All controls and status messages have keyboard-accessible alternatives, visible focus states, and text descriptions for screen readers.

## Look and feel
- App will open to the 60x25ft grid with the bridge deck and joints every 10ft already showing. It will be in build mode. There will be a road on either side of the bridge deck. This will all be 2D with images of the vehicles being 2D from the side, showing 2 wheels. Images of the vehicles will be to scale if possible. Members will look like brown wood when they are withing a safety factor of 2. They will then start turning yellow all the way to bright red when they are near the point of failure. Once the member exceeds the allowable stress, it will turn black, the vehicle will stop, and a message will appear that says "Your Bridge Failed". There will be a button below the message that says "Restart" that will return the user to the build screen where their previous bridge will still be intact.
- Include a little white circle with a black outline where each joint has been placed.

## Validation
- Build a 60 ft Pratt truss, 10 ft tall, with six 10 ft panels and diagonals sloping down toward the center. Park the semi with its front axle at x = 44 ft, compute the reactions by hand, and use the method of sections to compute the forces in the top chord, bottom chord, and diagonal in the panel from x = 20 to 30. 

The answer should be:
- Top Chord: 80,000 lb
- Bottom Chord: 70,400 lb
- Diagonal 13,576.45 lb

## Out of scope
- The app will not have any 3D elements
- Members are all made of the same material, no options to change thickness or strength of members will be added
- The app will only contain the test mode and build mode. No other modes will exist.