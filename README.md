Circle[] circles;
int numCircles = 3;
int circleRadius = 30;
int circleDistance = 150;
void setup() {
  size(600, 400);
  circles = new Circle[numCircles];
  for (int i = 0; i < numCircles; i++) {
    float x = (i + 1) * circleDistance;
    float y = height / 2;
    circles[i] = new Circle(x, y, circleRadius);
  }
}
void draw() {
  background(100);
  for (Circle circle : circles) {           //for movement
    circle.move();
    circle.display();
  }
}
void mousePressed() {
  for (Circle circle : circles) {   //when cursor is on circle 
    if (circle.contains(mouseX, mouseY)) {
      circle.pick();       // pick a circle
    }
  }
}
void mouseReleased() {
  for (Circle circle : circles) {         //releasing all the circle
    circle.release();
  }
}
class Circle {
  float x, y;      // Position of the circle
  float radius;    // Radius of the circle
  boolean picked;  // Flag to indicate if the circle is picked
  color defaultColor;  // Default color of the circle
  color pickedColor;    // Color when the cursor is on the circle
  Circle(float x, float y, float radius) {
    this.x = x;
    this.y = y;
    this.radius = radius;
    picked = false;
    defaultColor = color(255, 0, 0);
    pickedColor = color(0, 255, 0);
  } 
  void move() {
    // Move the circle if it is picked
    if (picked) {
      x = mouseX;
      y = mouseY;
    }
  }
  void display() {
    if (contains(mouseX, mouseY)) {         // Change the fill color based on cursor position
      fill(pickedColor);
    } else {
      fill(defaultColor);
    }
    ellipse(x, y, radius * 2, radius * 2);            // Draw the circle
  }
  boolean contains(float px, float py) {
    float d = dist(px, py, x, y);
    return d <= radius;
  }
  void pick() {
    picked = true;
  }
  void release() {
    picked = false;
  }
}
