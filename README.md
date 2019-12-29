# cp2-fa19-final-project
computational-practices-2__fall-2019__final-project

## Source Code


let video;
let poseNet;
let poses = [];

// DRAWING
var stepSize = 5.0;
var moduleSize = 1;

var nse_x = 0;
var nse_y = 0;
var ear_x = 0;
var ear_y = 0;




function setup() {
  var cnv = createCanvas(windowWidth, windowHeight);
  cnv.style('display', 'block');
  
  createCanvas(displayWidth, displayHeight);
  video = createCapture(VIDEO);
  
  video.size(displayWidth, displayHeight);
  cursor(CROSS);

  let fs = fullscreen(); 
  fullscreen(!fs);
  // Create a new poseNet method with a single detection
  poseNet = ml5.poseNet(video, modelReady);
  // This sets up an event that fills the global variable "poses"
  // with an array every time new poses are detected
  poseNet.on('pose', function(results) {
    poses = results;
  });
  // Hide the video element, and just show the canvas
  video.hide();
  
  //background(245, 245, 245, 120);
  
}

function modelReady() {
  select('#status').html('Model Loaded');
}

function mousePressed(){
  //console.log(JSON.stringify(poses))
  
}

function draw() { 
  colorMode(HSB);
  tint(240, 100, 50, .01);
  
  colorMode(RGB);
  image(video, 0, 0, width, height);
  
  
  // Hides video
  //// background(255);
  
  // Overlay video
   //background(255, 255, 255, 191);

  // For one pose only (use a for loop for multiple poses!)
  if (poses.length > 0) {
    let poseA = poses[0].pose;
    
      // point 1, person 1
    //// color
         stroke(180 ,150, 205, 200);
         strokeWeight(1);
         fill(0);
    //// define point
         let nose = poseA['nose'];
         var nse = dist(nse_x, nse_y, nose.x, nose.y);
    
          if (nse > stepSize) {
             var angle = atan(nose.y - nse_y, nose.x - nse_x);
           push();
           strokeWeight(2);
           translate(nose.x, nose.y);
           rotate(angle, PI);
           line(0, 0, nse, moduleSize);
           pop();
           
           nse_x = nse_x + cos(angle) * stepSize * -1;
           nse_y = nse_y + sin(angle) * stepSize;
         }
    
    // point 2, person 1
    //// color
         stroke(100 ,185, 205, 200);
         strokeWeight(1);
         fill(0);
    //// define point
         let rightEar = poseA['rightEar'];
    //// draw from point
         var rtEar = dist(ear_x, ear_y, rightEar.x, rightEar.y);
         if (rtEar > stepSize) {
         
           var angle = atan(rightEar.y - ear_y, rightEar.x - ear_x);
      
           push();
           strokeWeight(1);
           translate(rightEar.x, rightEar.y);
           rotate(angle, PI);
           line(0, 0, rtEar, moduleSize);
           pop();
           
           ear_x = ear_x + cos(angle) * stepSize;
           ear_y = ear_y + sin(angle) * stepSize;
         }
    // point 3, person 1
    //// color
         noStroke();
         fill(245, 90);
    //// define point
         let leftEye = poseA['leftEye'];
    //// draw from point
         rect(leftEye.x, leftEye.y, 22, 8);
    
    // point 4, person 1
    //// color
         noStroke();
         fill(245);
    //// define point
         let rightWrist = poseA['rightWrist'];
    //// draw from point
         ellipse(rightWrist.x, rightWrist.y, 12, 12);
    
    // point 5, person 1
    //// color
         noStroke();
         fill(0);
    //// define point
         let leftWrist = poseA['leftWrist'];
    //// draw from point
         ellipse(leftWrist.x, leftWrist.y, 12, 12);
   
      if (poses[1]) {
        let poseB = poses[1].pose;
        
        var nseB_x = 0;
        var nseB_y = 0;
        var earB_x = 0;
        var earB_y = 0;
        
        
      // point 1, person 2
    //// color
         stroke(115 ,170, 205, 200);
         strokeWeight(1);
         fill(0);
    //// define point
         let noseB = poseB['nose'];
         var nseB = dist(nseB_x, nseB_y, nose.x, nose.y);
    
          if (nseB > stepSize) {
             var angle = atan(noseB.y - nseB_y, noseB.x - nseB_x);
      
           push();
           strokeWeight(2);
           translate(noseB.x, noseB.y);
           rotate(angle, PI);
           line(0, 0, nse, moduleSize);
           pop();
           
           nseB_x = nseB_x + cos(angle) * stepSize * -1;
           nseB_y = nseB_y + sin(angle) * stepSize;
         }
    
    //// draw from point
         //ellipse(nose.x, nose.y, 12, 12);
    
    // point 2, person 2
    //// color
         stroke(150 ,205, 180, 200);
         strokeWeight(1);
         fill(0);
    //// define point
         let rightEarB = poseB['rightEar'];
    //// draw from point
         var rtEarB = dist(earB_x, earB_y, rightEarB.x, rightEarB.y);
         if (rtEarB > stepSize) {
           var angle = atan(rightEarB.y - ear_y, rightEarB.x - ear_x);
      
           push();
           strokeWeight(1);
           translate(rightEarB.x, rightEarB.y);
           rotate(angle, PI);
           line(0, 0, rtEarB, moduleSize);
           pop();
           
           earB_x = earB_x + cos(angle) * stepSize;
           earB_y = earB_y + sin(angle) * stepSize;
         }
    // point 3, person 2
    //// color
         noStroke();
         fill(245, 90);
    //// define point
         let leftEyeB = poseB['leftEye'];
    //// draw from point
         rect(leftEyeB.x, leftEyeB.y, 22, 8);
    
    // point 4, person 2
    //// color
         noStroke();
         fill(245);
    //// define point
         let rightWristB = poseB['rightWrist'];
    //// draw from point
         ellipse(rightWristB.x, rightWristB.y, 12, 12);
    
    // point 5, person 2
    //// color
         noStroke();
         fill(0);
    //// define point
         let leftWristB = poseB['leftWrist'];
    //// draw from point
         ellipse(leftWristB.x, leftWristB.y, 12, 12);
      }
    
    if (poses[2]) {
        let poseC = poses[2].pose;
        
        var nseC_x = 0;
        var nseC_y = 0;
        var earC_x = 0;
        var earC_y = 0;
        
        
      // point 1, person 3
    //// color
         stroke(150 ,205, 180, 200);
         strokeWeight(1);
         fill(0);
    //// define point
         let noseC = poseC['nose'];
    //// draw from point
         var nseC = dist(nseC_x, nseC_y, nose.x, nose.y);
    
          if (nseB > stepSize) {
             var angle = atan(noseC.y - nseC_y, noseC.x - nseC_x);
      
           push();
           strokeWeight(2);
           translate(noseC.x, noseC.y);
           rotate(angle, PI);
           line(0, 0, nse, moduleSize);
           pop();
           
           nseC_x = nseC_x + cos(angle) * stepSize * -1;
           nseC_y = nseC_y + sin(angle) * stepSize;
         }
    
    //// draw from point
         //ellipse(nose.x, nose.y, 12, 12);
    
    // point 2, person 3
    //// color
         stroke(180 ,150, 205, 200);

         strokeWeight(1);
         fill(0);
    //// define point
         let rightEarC = poseC['rightEar'];
    //// draw from point
         var rtEarC = dist(earC_x, earC_y, rightEarC.x, rightEarC.y);
         if (rtEarB > stepSize) {
           var angle = atan(rightEarC.y - ear_y, rightEarC.x - ear_x);
      
           push();
           strokeWeight(1);
           translate(rightEarC.x, rightEarC.y);
           rotate(angle, PI);
           line(0, 0, rtEarC, moduleSize);
           pop();
           
           earC_x = earC_x + cos(angle) * stepSize;
           earC_y = earC_y + sin(angle) * stepSize;
         }
      
    // point 3, person 3
    //// color
         noStroke();
         fill(245, 90);
    //// define point
         let leftEyeC = poseB['leftEye'];
    //// draw from point
         rect(leftEyeC.x, leftEyeC.y, 22, 8);
    
    // point 4, person 3
    //// color
         noStroke();
         fill(245);
    //// define point
         let rightWristC = poseB['rightWrist'];
    //// draw from point
         ellipse(rightWristC.x, rightWristC.y, 12, 12);
    
    // point 5, person 3
    //// color
         noStroke();
         fill(0);
    //// define point
         let leftWristC = poseB['leftWrist'];
    //// draw from point
         ellipse(leftWristC.x, leftWristC.y, 12, 12);
      }
      
      
    //} 
  }
}
