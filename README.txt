CornBox is a Lua script that can take control of your craft in case of imminent collision and steer it to safety.
It will interfere with controls only when absolutely necessary, as defined by settings.
By default, when assessing collitions for ships, script will take movement of all enemy and friendly ships into considerations and will try to predict their future positions, to prevent pile up. For planes/submarines - only current velocity vectors are considered (predicting combat maneuvers during dogfights are not the goal of this script).


Video tutorials on how to use CornBox:
https://discord.com/channels/481245790149279744/528650029683048459/934161892207906826
https://discord.com/channels/481245790149279744/528650029683048459/934492664462704750


With questions, feedback and helpful bug reports - looks for Corn Hollio on discord at Menti's or Arena.


I. Important notes.
1. Read this!
2. Run tests!
3. It's a work in progress! Always use the most recent version!
4. Using CornBox does not guarantee total lack of collisions!
5. You should supplement it by setting different orbits to your crafts and using other reasonable precautions. Or run tests!
6. CornBox is not responsible for keeping craft inside the speed limit. Usual methods should work.
7. CornBox is not responsible for preventing craft from gaining range or altitude DQ. Use some checks for altitude control and prayers for range.
8. The use of CornBox on crafts that will habitually go in reverse is not recommended, unless you have run extensive tests and satisfied with results.
9. CornBox have a check for plane's altitude during collision evasion, but not for its inertia and course afterwards. If your planes go for a swim or a spacewalk too often and altitude settings are not helpful - you can completely disable up/downwards evasion commands.
10. No connection to mainframe required.
11. If you prefab LUA Box block - script inside it will not be saved.
12. You can use multiple CornBoxes on one craft. Additional boxes will have a reasonably small performance cost.
13. Current altitude will define class of the craft. If it's high enough - it a Plane, if it's at some depth - it's a Submarine, overwise - it's a Ship or a Land Unit (if on a Land Map). You can set class for your own craft manually, if necessary.
14. You can define which classes will avoid each other. No reason for Planes to run away from Submarines, etc.
15. Run tests with full fleet to make sure that everything works as it should and not too laggy.


II. First steps.
1. Place LUA Box block in a secure place on your craft.
2. Delete bits of code inside LUA Box and copy/paste full script in their place.
3. Press "Apply changes (SAVE) (F8)" - magic will start happening.
4. Press "Exit (doesn't save changes)" to exit LUA Box.


III. To use CornBox with standard AI.
1. All done. Nothing else is required, script comes configured by default for a craft with standard AI (unless i forgot to do this). You can fiddle with setting, if you really want to.
2. When script takes control of the craft it will overwrite all movement commands from AI (no way around this). If you are using build-in PIDs for roll and hover - they will be disabled too - use General Purpose PIDs.
3. Hybrid AI (breadboard with Behaviour/Manoeuver selectors) counts as standard AI. 


IV. To use CornBox with breadboard AI.
1. Lua cannot take control away from breadboard. So it's your responsibility to make breadboard which can receive and follow instructions from CornBox.
2. When possible collision is detected and actions are required, CornBox will send signals via Complex Controls. You can change letters used for signals in the script.
3. Your breadboard should follow this commands (you can ignore some of them):

      K = Go right

      H = Go left

      L = Pitch up

      O = Pitch down
      
      J = Slow down or stop

4. You should switch CornBox from use with standard AI to breadboard AI. To do this, change this variable in the script as follows:

      TypeOfAiOnTheCraft = 2
      
5. If you are doing roll remap for yaw/pitch outputs in your breadboard - commands from CornBox must not be remapped. Insert them after remap block.
6. Don't forget to press "Apply changes (SAVE) (F8)" to apply and save changes to the script inside CornBox. You can fiddle with setting, if you really want to.


V. Integration test.
1. After you placed CornBox, it's highly recommended that you should run integration test. It will assure that controls on your craft are not inverted, from the CornBox's point of view.
2. Set "IntegrationTestDuration" to more than 0 to activate it (try 10 seconds). CornBox will cycle through all commands so you can test if your craft respond as expected (use force view - '\'): yaw right/left, pitch up/down, slow down.  All directions should be in the current orientation of the craft.
3. During the test script will print:

      - name of the blueprint.
      - is it a water map or a land map (and terrain altitude).
      - what type of craft script think it's running on and what type is expected base on altitude.
      - command it's sending.
      
4. Don't forget to disable integration test after you are done with it, as follows:

      IntegrationTestDuration = 0
      
      
VI. Map and terrain awareness.
1. CornBox can detect and avoid map borders on a Arena-style maps.
2. CornBox can detect and avoid terrain, no more tanks getting stuck on walls and ships/submarines beaching themselves. 



