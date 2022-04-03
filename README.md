void setup()
{
  size(600, 600);
  DrawCircle();
}
void draw(){}
void DrawCircle()
{
  colorMode(HSB, 1);
  background(1);
  strokeWeight(4);
  for(int i=0; i<500; i++)
  {
    for(int j=0; j<100; j++)
    {
      stroke((float)i/500, (float)j/100, 1);
      point(300+(50+2*j)*sin(i/250.0*PI), 300-(50+2*j)*cos(i/250.0*PI));
    }
  }
  stroke(0);
  fill(1);
  strokeWeight(3);
  ellipseMode(CENTER);
  ellipse(300, 300, 100, 100);
}
int X, Y;
float I, J, theta;
float H, S, R, G, B;
void mousePressed()
{
  DrawCircle();
  colorMode(RGB, 1);
  
  X = mouseX;
  Y = mouseY;
  J = sqrt((X-300)*(X-300) + (Y-300)*(Y-300)) - 50;
  J /= 2;
  if(J < 0 || J > 100) return;
  
  if(X >= 300 && Y <= 300) theta = asin((X-300)/(50+2*J));
  else if(Y >= 300) theta = PI - asin((X-300)/(50+2*J));
  else theta = 2*PI + asin((X-300)/(50+2*J));
  I = theta * 250 / PI;
  H = I/500;
  S = J/100;
  
  if(H < 1/6.)
  {
    R = 1;
    G = 6*H;
    B = 0;
  }
  else if(H < 2/6.)
  {
    R = 2 - 6*H;
    G = 1;
    B = 0;
  }
  else if(H < 3/6.)
  {
    R = 0;
    G = 1;
    B = 6*H - 2;
  }
  else if(H < 4/6.)
  {
    R = 0;
    G = 4 - 6*H;
    B = 1;
  }
  else if(H < 5/6.)
  {
    R = 6*H - 4;
    G = 0;
    B = 1;
  }
  else
  {
    R = 1;
    G = 0;
    B = 6 - 6*H;
  }
  R += (1-R)*(1-S);
  G += (1-G)*(1-S);
  B += (1-B)*(1-S);
  
  fill(R, G, B);
  ellipse(300, 300, 100, 100);
  String s = str(int(R*255)) + ", " + str(int(G*255)) + ", " + str(int(B*255));
  textSize(30); fill(0); text(s, 20, 20);
}
