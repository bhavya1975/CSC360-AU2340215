q) what is Github.
-> it is  a basically a tool which helps us manage code and different contributors 
can also contribute to the code.


Q) How is computer graphic different from image processing
-> graphic is generation of images using geometry and
image processing is acquisation and algorithm

Q) what are the geometry premitive of graphics
-> lines, point, curves and areas.

Q) describe the graphical framework in java
AWT, spring, javafx

Q) what is the design pattern for creating user interface(eg clicking button).
we make events listner

Q) static graphic and interactive graphic
static graphic is done without cursor movement
while interactive is done with cursor movement.

Q) what is SSH vs HTTPs ?
-> SSH (Secure Shell) and HTTPS (Hypertext Transfer Protocol Secure) are both cryptographic 
network protocols used to encrypt data sent over a network, 
but they serve entirely different purposes and operate in distinct ways.
While SSH is designed for remote machine management and executing terminal commands, 
HTTPS is built for securely transmitting web page data between a web browser and a website.

-> SSH keygen, it will create a folder under your home directory
in linux by default you go there or else you can go to your user directory
or cd ~
similar window will also have it's own

Q) How is curves connected to calculus. 
-> Calculus is the tool used to analyze and measure curves.The Derivative finds the exact steepness (slope)
at any single point on a curve.The Integral calculates the exact area trapped underneath a bending 
curve. Optimization locates the exact peaks and valleys where a curve changes direction.

Q) public vs private keys
Visibility: public key is Shared openly with anyone in the world while private keyKept 
strictly secret by the owner.


//tried making a simple perpendicular line to another line:

import javax.swing.*;
import java.awt.*;

public class PerpendicularLinesFX extends JPanel {
        @Override
        protected void paintComponent(Graphics g) {
            super.paintComponent(g);
            Graphics2D g2d = (Graphics2D) g;

            // Turn on antialiasing for smooth lines
            g2d.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            g2d.setStroke(new BasicStroke(3)); // Line thickness

            // 1. Define Main Line Points
            double x1 = 100, y1 = 300;
            double x2 = 400, y2 = 100;

            // Draw Main Line (Blue)
            g2d.setColor(Color.BLUE);
            g2d.drawLine((int) x1, (int) y1, (int) x2, (int) y2);

            // 2. Calculate Perpendicular Line from the Midpoint
            double midX = (x1 + x2) / 2;
            double midY = (y1 + y2) / 2;

            double dx = x2 - x1;
            double dy = y2 - y1;

            // Desired length of perpendicular line (half-length in each direction)
            double perpLength = 80;
            double currentLength = Math.hypot(dx, dy);

            // Normalized perpendicular vector
            double px = -dy / currentLength * perpLength;
            double py =  dx / currentLength * perpLength;

            // Perpendicular line endpoints
            double px1 = midX + px;
            double py1 = midY + py;
            double px2 = midX - px;
            double py2 = midY - py;

            // Draw Perpendicular Line (Red)
            g2d.setColor(Color.RED);
            g2d.drawLine((int) px1, (int) py1, (int) px2, (int) py2);
        }

        public static void main(String[] args) {
            JFrame frame = new JFrame("Perpendicular Lines in Swing");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setSize(500, 500);
            frame.add(new PerpendicularLinesFX());
            frame.setLocationRelativeTo(null);
            frame.setVisible(true);
        }
    }
