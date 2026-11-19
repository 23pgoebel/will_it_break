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

## Calculations
- A truss solver using the method of joints as one linear system, with a message instead of numbers when the truss is unstable (it needs members + 3 = 2 × joints, and a system that isn't nearly singular)
    - Member capacities of 90,000 lb in tension and 75,000 lb in compression. In Test mode, members are colored by how close they are to capacity.
- Cost is calculated by multiplying the number of joints by $500, and the total ft of members by $100, then summing the two products.

## Outputs
- Two modes. In Build mode, the user places joints on a 1 ft grid and connects them with members, and a hint on screen says what the next click will do. In Test mode, the drawing tools are hidden and the user picks a vehicle and drives it across.
- A bridge site with deck joints every 10 ft from x = 0 to x = 60, a pin at x = 0, and a roller at x = 60, which can't be moved or deleted
- Cost will be displayed and updated as the bridge is being built.
- A details panel, closed by default, with the joint and member force tables that show the maximum force each member will experience when each vehicle crosses the bridge.
- In test mode, include an option to park a vehicle at any location x on the bridge, x being the location of the front axle and display a table with the stresses of each member.

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