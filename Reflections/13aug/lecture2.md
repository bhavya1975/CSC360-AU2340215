Working through this code taught me how custom 2D 
graphics and windows operate in Java Swing. 
I learned that custom rendering requires extending a JPanel and overriding paintComponent, 
always calling super.paintComponent(g) first to clear the background and prevent glitches. 
Casting the default context to Graphics2D unlocks more advanced rendering power. 
Drawing works exactly like a physical paintbrush; you must set your configuration, like Color.RED, before calling drawRect. 
I also learned that Java's coordinate system starts at (0,0) in the top-left corner, 
meaning higher Y values move objects downward. Finally, 
I discovered how to bundle this canvas into a visible JFrame and use 
setDefaultCloseOperation(3) to completely kill the background Java process when the 
window closes.
