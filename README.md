import processing.video.*;
PImage prev;
Capture video;

void captureEvent(Capture video){
  prev.copy(video,0,0,video.width,video.height,0,0,prev.width,prev.height);
prev.updatePixels();
video.read();
}


void setup(){
  size(640,360);
  video=new Capture(this,Capture.list()[3]);
  video.start();
  prev= createImage(video.width,video.height,RGB );
  
}

void draw(){
  prev.loadPixels();
video.loadPixels();
//int count=0;
for(int x=0;x<video.width;x++){
  for(int y=0;y<video.height;y++){
    int loc=x+y*video.width;
    color currentColor=video.pixels[loc];
float r1=red(currentColor);
float b1=blue(currentColor);
float g1=green(currentColor);
    color prevColor=prev.pixels[loc];
float r2=red(prevColor);
float b2=blue(prevColor);
float g2=green(prevColor);

float d=dist(r1,b1,g1,r2,b2,g2);
if(d<625){
//stroke(255);
pixels[loc]=color(255);
}
else{
pixels[loc]=color(0);
}
  }
}
updatePixels();
}
