# booga-booga-reborn-testing
buffer token writer for dropping items from your inventory / outline for every script i'll ever make for booga booga.|
all this script does is send valid buffer tokens to the server with any necessary details that need to be added into the packet to perform a function.
no specifications have been validated as of 10/8/24, this script is still a W.I.P
if you run this script with remotespy loaded, remotespy will log remotes being triggered, meaning that we're atleast getting to the server with a valid token, but incorrect packet specifications.
in theory, if we can somehow find the correct variables to place inside if the packet we're sending, this script will send valid buffer tokens and perform any action, as long as the variables are specific and correct.
as i said before, by stripping the script down to it's bare parts, it still generates valid tokens; meaning, if we can find the correct specifications for actions we want to proceed with, it's virtually possible.
let's say we want to swing a tool. by replacing every part of the code that says Bloodfruit with SwingTool, and the correct specifications, said action will be performed.
