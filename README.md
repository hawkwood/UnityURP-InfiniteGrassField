# UnityURP-InfiniteGrassField
An Infinite GPU Instanced Grass Field that doesn't require storing trillions of positions in memory

The idea is simple, we generate a uniform grid of points in an area and make it move with the camera
The trick is moving it in a way that doesn't let the player feel it moving
This is simply done by the famous steps formula "floor(value / step) * step"
In simple words, imagine having a grid that covering the whole space, and the points can only exist on this grid. So in order to follow the camera, we get the closest point to it in the grid and consider it the center of our square, and then we generate the other points around this point.

After this, we do a frustrum test to every point before adding it to the PositionsBuffer (I'm using and AppendStructuredBuffer)
Then we pass this buffer to the material, and inside of the material we add a small random offset (that is based on the world pos) to the position to give the grass some randomness

This project is mostly based on this repo of Colin Leung:
https://github.com/ColinLeung-NiloCat/UnityURP-MobileDrawMeshInstancedIndirectExample
