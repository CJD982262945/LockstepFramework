Lockstep Framework (Alpha)
------------------------
The Lockstep Framework (LSF) is a framework designed for games that especially need lockstep simulations. It includes a deterministic 2D physics engine, pathfinding, behavior system, and more. LSF is integrated with Unity but can be abstracted away.

Under development by [John Pan](https://github.com/SnpM).

Quick Setup
-----------
1. Import the framework into a Unity project and open Lockstep-Framework/Example/ExampleScene
2. Set up the database and settings by navigating to the Lockstep/Database window or pressing Control - Shift - L.
3. In the Settings foldout of the database window, click Load and navigate to Lockstep-Framework/Example/ExampleDatabase/Example_Database.asset to load the preconfigured database for the example.
4. Play!

Note: The example only shows the basic functionality of the framework. Comprehensive examples will be added close to the end of core development.

Ability Pattern
----------------
Abilities are moddable behaviors that can be easily attached, detached, and moddified on prefab game objects. They follow the following pattern:
- The overridable Initialize() method is called when the agent the ability belongs to is created and initialized. It provides an argument that is the agent the ability belongs to. Because LSF uses object pooling, the Ability must also be reset in Initialize(). Note: Lockstep varaibles are implemented but not tested. These will make resetting in Initialize obsolete.
- Simulate() is called every single simulation frame (FixedUpdate frames).
- Visualize is called every render frame (Update frames).
- Deactivate() is called when the ability's agent is deactivated (i.e. killed). Note that Simulate() will not be called until after Initialize() is called again.

ActiveAbility Pattern
_____________________________
ActiveAbility inherits from Ability and includes all the patterns described above. In addition ActiveAbilitys can be interacted with by players through Commands.
- Execute () is called when a Command is received and activates the ability. This method provides an argument that is the Command responsible for the ability's activation.
 
TODO:
______
These are high priority issues that are significantly big or complicated. Any help on these aspects (as well as on any other lacking parts of the framework) would be very appreciated.
- Interpolation. Currently, interpolation between the position of the last simualtion frame and the current simulation frame for a unit causes stuttering. To mitigate this issue, another layer of interpolation is used. The current code for smoothing interpolation and communicating the positions to Unity's transform system is in LSBody.Visualize, around line 506. Note that setting LerpDamping to 1 will remove the extra layer of interpolation and uncover the stuttering.
- Pathfinding around corners. Even explaining to me a solution to this problem will help a lot.
- (After Lockstep Variables are fully tested) Lockstep Variable integration. Currently, no abilities use Lockstep Variables which are used to track determinism and also reset values upon re-initialization of the unit. A lot of work must be done to mark as many value-type deterministic variables as possible [Lockstep] and move their initialization to Setup () since LSVariables automatically handle resetting.

License
--------
The MIT License (MIT)

Copyright (c) 2015 John Pan

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
