CornBox is a Lua script that can take control of your craft in case of imminent collision and steer it to safety.
It will interfere with controls only when absolutely necessary, as defined by settings.
When assessing collitions for ships, script will take movement of all enemy and friendly ships into considerations and will try to predict their future positions, to prevent pile up.
For planes - only current velocity vectors are considered. Predicting combat maneuvers during dogfights are not the goal of this script.


Video tutorials on how to use CornBox:
https://discord.com/channels/481245790149279744/528650029683048459/934161892207906826
https://discord.com/channels/481245790149279744/528650029683048459/934492664462704750


With questions, feedback and helpful bug reports - looks for Corn Hollio on discord at Menti's or Arena.


I. Important notes.
1. Read this!
2. Run tests!
3. It's a work in progress! Always use the most recent version!
4. Using CornBox does not guarantee total lack of collisions!
5. You should supplement it by setting different orbits to crafts and use other reasonable precautions. Run tests!
6. CornBox does not responsible for keeping craft inside the speed limit. Usual methods should work.
7. CornBox does not responsible for preventing craft from gaining range or altitude DQ. Use some checks for altitude control and prayers for range.
8. The use of CornBox on crafts that will habitually go in reverse is not recommended, unless you have run extensive tests and satisfied with results.
9. CornBox have a check for plane's altitude during collision evasion, but not for its inertia and course afterwards. If your planes go for a swim or a spacewalk too often and altitude settings are not helpful - you can completely disable up/downwards evasion commands.
10. No connection to mainframe required.
11. If you prefab LUA Box block - script inside it will not be saved.
12. You can use multiple CornBoxes on one craft. Additional boxes will have a reasonably small performance cost.
13. Everything is a ship, unless it goes too fast or is at high altitude (so if a plane falls into the water - it's a ship now). You own construct will self identify as a ship by default and you should change that to a plane as necessary.
14. Ships will never try to avoid planes. Planes will not avoid ships by default, but there is a setting to change that.
15. You can use CornBox with land vehicles or submarines. For this, set AltitudeToBePlane/SpeedToBePlane to something appropriate.
16. Run tests with full fleet to make sure that everything works as it should and not too laggy.


II. First steps.
1. Place LUA Box block in a secure place on your craft.
2. Delete bits of code inside LUA Box and copy/paste full script in their place.
3. Press "Apply changes (SAVE) (F8)" - magic will start happening.
4. Press "Exit (doesn't save changes)" to exit LUA Box.


III. To use CornBox with standard AI.
1. All done. Nothing else is required, script comes configured by default for ship with standard AI (unless i forgot to do this). You can fiddle with setting, if you really want to.
2. When script takes control of the craft it will overwrite all movement commands from AI (no way around this). If you are using build-in PIDs for roll and hover - they will be disabled too - use General Purpose PIDs.
3. Hybrid AI (breadboard with Behaviour/Manoeuver selectors) counts as standard AI. 


IV. To use CornBox with breadboard AI.
1. Lua cannot take control away from breadboard. So it's your responsibility to make breadboard which can receive and follow instructions from CornBox.
2. When possible collision is detected and actions are required, CornBox will send signals via Complex Controls. You can change letters used for signals in the script.
3. Your breadboard on a ship should follow this commands:

      K = Go right

      H = Go left

      J = Slow down or stop
      
4. Your breadboard on a plane should follow this commands:

      K = Go right

      H = Go left

      U = Pitch up

      J = Pitch down

5. You should switch CornBox from use with standard AI to breadboard AI. To do this, change this two variables in the script as follows:

      DoTakeControlFromAiAndSendYawCommand = false

      DoSendComplexControlCommand = true
      
6. If you are doing roll remap for yaw/pitch outputs in your breadboard - commands from CornBox must not be remapped. Insert them after remap block.
7. Don't forget to press "Apply changes (SAVE) (F8)" to apply and save changes to the script inside CornBox. You can fiddle with setting, if you really want to.


V. Integration test.
1. After you placed CornBox, it's highly recommended that you should run integration test. It will assure that controls on your craft are not inverted, from the CornBox's point of view.
2. Set "IntegrationTestDuration" to more than 0 to activate it (try 400 for 10 seconds). CornBox will cycle through all commands so you can test if your craft respond as expected (use force view - '\'). All directions should be in the current orientation of the craft.
      For ships: yaw right/left, stop. 
      For planes: yaw right/left, pitch up/down and their combinations. 
3. Don't forget to disable this after you are done with the test, as follows:
      IntegrationTestDuration = 0
