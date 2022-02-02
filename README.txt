Video tutorials on how to use CornBox:
https://discord.com/channels/481245790149279744/528650029683048459/934161892207906826
https://discord.com/channels/481245790149279744/528650029683048459/934492664462704750


Partially outdated readme.


I. Important notes.

Read this!

Using CornBox does not guarantee total lack of collisions!

You should supplement it by setting different orbits to crafts and use other reasonable precautions. Run tests!

CornBox does not responsible for keeping craft inside the speed limit. Usual methods will work.

No connection to mainframe required.

You can use multiple CornBoxes on one craft, but they do have a performance cost - so run tests with full fleet to make sure you will pass the Lag Test.

II. First steps.
1. Place LUA Box block in a secure place on your craft.
2. Delete bits of code inside LUA Box and copy/paste script in their place.
3. Press "Apply changes (SAVE) (F8)" - magic will start happening.
4. Press "Exit (doesn't save changes)" to exit LUA Box.

III. To use CornBox with standard AI.
1. All done. Nothing else is required, since script comes configured by default for this case. You can fiddle with setting, if you really want to.

IV. To use CornBox with breadboard AI.
1. LUA cannot take control away from breadboard. So it's your responsibility to make breadboard which can receive and follow instructions from CornBox.
2. When possible collision is detected and actions are required, CornBox will send signals via Complex Controls. You can change letters used for signals in the script.
3. Your breadboard should follow this commands:

      K = Go right

      H = Go left

      J = Stop

4. You should switch CornBox from use with standard AI to breadboard AI. To do this change this two variables in the script:

      DoTakeControlFromAiAndSendYawCommand = false

      DoSendComplexControlCommand = true

5. Don't forget to press "Apply changes (SAVE) (F8)" to apply and save changes to the script inside CornBox. You can fiddle with setting, if you really want to.
