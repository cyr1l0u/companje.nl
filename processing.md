---
title: Processing
---

=====PVector 3D rotation=====
<code javascript>
void applyRotation(PVector src, PVector axis, float angle) {
  PMatrix3D rMat = new PMatrix3D();
  PVector tmp = new PVector();
  rMat.rotate(radians(angle), axis.x, axis.y, axis.z);
  rMat.mult(src, tmp);
  src.set(tmp);
}
</code>

=====convert 16bit gray RAW image to 8 bit RGB png=====
<code javascript>
byte gray[] = loadBytes("/Users/rick/Documents/openFrameworks/of0093/apps/Globe4D/Globe4D/bin/data/maps/hull/terra8M.raw"); 

PImage img = createImage(4096, 2048, RGB);
img.loadPixels();

int j=0;
for (int i = 0; i < gray.length; i+=2) {
  img.pixels[j++] = color(gray[i],gray[i+1],0);
}

img.updatePixels();
img.save("rgb.png");

println("done");
</code>

===== Globe intro in ProcessingJS for Khan Academy =====
<code javascript>
var planet = getImage("space/planet");
var logoY,sloganX,globeY,webY;

var resetAnimation = function() {
    logoY=-50;
    sloganX=-1000;
    webY=1000;
    globeY=300;
};

resetAnimation();

var draw = function() {
    //drawing a semi transparent rect instead of
    //using background() creates the nice fading effect.
    noStroke();
    fill(128,128,128,50);
    rect(0,0,width,height);
    
    //restart the aimation every 300 frames
    if ((frameCount % 300)===0) {
        resetAnimation();
    }
    
    //animate
    if (logoY<50)        { logoY+=3;    }
    if (sloganX<width/2) { sloganX+=20; }
    if (webY>120)        { webY-=10;    }
    if (globeY>120)      { globeY-=10;  }
    
    //text
    fill(255);
    textAlign(CENTER);
    textFont(createFont("sans-serif",50));
    text("Globe4D",width/2,logoY);
    textFont(createFont("serif",20));
    text("interactive four-dimensional globes",sloganX,90);
    textFont(createFont("sans-serif",15));
    text("www.globe4d.com",width/2,webY);
    
    //draw globe
    fill(255);
    ellipse(200,250,300,140);
    image(planet,100,globeY,220,220);

    //draw pedestal
    stroke(255);
    fill(0);
    rect(95,260,220,190);
    
    //mask ring
    strokeWeight(70); //for a very thick arc
    stroke(255); //make red to see mask
    noFill();
    arc(200,223,260,130,30,150);
    
    //draw thin gray arc for table
    strokeWeight(1);
    stroke(0,0,0,50);
    arc(201,240,299,140,0,180);
};
</code>

===== Monstertje in ProcessingJS voor Khan Academy=====
<code javascript>
var eye = function(cx,cy,eyeX,eyeY) {
    fill(126, 242, 149);
    triangle(eyeX-10,eyeY,eyeX+10,eyeY,cx,cy);
    ellipse(eyeX,eyeY,35,35);
    fill(255);
    stroke(0);
    ellipse(eyeX,eyeY,24,24);
    fill(0);
    ellipse(eyeX,eyeY+2,12,12);
    fill(255);
    noStroke();
    ellipse(eyeX,eyeY+4,4,4);
};

var animate = function(f) {
    return sin(millis()*f); //use sine function for smooth animation
};

var draw = function() {
    background(0);
    
    //cx,cy = center of body
    var cx = width/2+50*animate(0.1);
    var cy = height/2+10*animate(1);

    //feet
    var footY = 10*animate(0.5);
    fill(126, 242, 149);
    triangle(cx,cy,cx+10,cy+100+footY,cx+20,cy+100+footY);
    triangle(cx,cy,cx-10,cy+100-footY,cx-20,cy+100-footY);
    rect(cx+10,cy+90+footY,30,10,20);
    rect(cx-40,cy+90-footY,30,10,20);
   
    //body
    ellipse(cx,cy,100,70);
    ellipse(cx,cy+0,90,90);
    ellipse(cx,cy+10,80,70);
    ellipse(cx,cy+20,70,60);
    ellipse(cx,cy+30,60,50);
    ellipse(cx,cy+40,50,40);
    
    //eyes
    eye(cx,cy,cx-30,cy-70+10*animate(1));
    eye(cx,cy,cx+30,cy-90+20*animate(0.5));
    
    //mouth
    strokeWeight(3);
    stroke(0);
    noFill();
    fill(255);
    var mouthW = 15*abs(animate(0.3))+5;
    var mouthH = 10*abs(animate(0.3))+5;
    ellipse(cx,cy+25,mouthW,mouthH);
    strokeWeight(2);
    noStroke();
    
    //freckles
    fill(0);
    ellipse(cx-2,cy-16,4,4);
    ellipse(cx-8,cy-25,3,3);
    ellipse(cx+8,cy-21,4,4);
    ellipse(cx+18,cy-19,3,3);
    ellipse(cx-19,cy-22,3,3);
    ellipse(cx+13,cy-7,3,4);
    ellipse(cx-16,cy-9,4,4);
};
</code>

===== Starfield 2D perspective =====
<code java>
class Star extends PVector {
  float speed;
  
  Star(float x, float y, float z) {
    super(x, y, z);
    speed = random(.1,5);
  }
}

ArrayList<Star> stars = new ArrayList();

void setup() {
  size(1280, 800); 
  noStroke();
  for (int i=0; i<300; i++) {
    float x = random(-width*2,width*2);
    float y = random(-height*2,height*2);
    float z = random(-1000,0);
    stars.add(new Star(x,y,z));  
  }
}

void draw() {
  background(0);
  
  translate(width/2, height/2);
  for (Star s : stars) {
    float x = s.x * 100/s.z;
    float y = s.y * 100/s.z;
    float d = 1000. / -s.z;
    ellipse(x, y, d, d);
    
    s.z+=s.speed;
    if (s.z>0) s.z=-1000;
  }
}
</code>

===== Mandelbrot set =====
<code java>
// Interactive Mandelbrot Set
// Inspired by Daniel Shiffman's Processing example.
// by Rick Companje - www.companje.nl - 6 december 2009
 
double xmin = -2.5;
double ymin = -2;
double wh = 4;
double downX, downY, startX, startY, startWH;
int maxiterations = 200;
boolean shift=false;
 
void setup() {
  size(300, 300);
  colorMode(HSB, 255);
  loadPixels();
}
 
void mousePressed() {
  downX=mouseX;
  downY=mouseY;
  startX=xmin;
  startY=ymin;
  startWH=wh;
}
 
void keyPressed() {
  if (keyCode==SHIFT) shift=true;
}
 
void keyReleased() {
  if (keyCode==SHIFT) shift=false;
}
 
void mouseDragged() {
  double deltaX=(mouseX-downX)/width;
  double deltaY=(mouseY-downY)/height;
 
  if (!shift) {
    xmin = startX-deltaX*wh;
    ymin = startY-deltaY*wh;
  } 
  else {
    if (wh>10) wh=10;
    if (deltaX>1) deltaX=1;
    wh = startWH-deltaX*wh;
    xmin = startX+deltaX*wh/2;
    ymin = startY+deltaX*wh/2;
  }
}
 
void draw() {
  double xmax = xmin + wh;
  double ymax = ymin + wh;
 
  // Calculate amount we increment x,y for each pixel
  double dx = (xmax-xmin) / width;
  double dy = (ymax-ymin) / height;
 
  double y = ymin;
  for (int j = 0; j < height; j++) {
    double x = xmin;
    for (int i = 0; i < width; i++) {
      double a = x;
      double b = y;
      int n = 0;
      while (n < maxiterations) { 
        double aa = a * a; 
        double bb = b * b; 
        b = 2.0 * a * b + y; 
        a = aa - bb + x; 
        if (aa + bb > 16.0) break;
        n++;
      }
 
      pixels[i+j*width] = (n==maxiterations) ? color(0) : color(n*16 % 255, 255, 255);
 
      x += dx;
    }
    y += dy;
  }
  updatePixels();
}
</code>