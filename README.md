<html>
 <head>
  <title> My Melon Falling Game </title>
 </head>

<body>
<canvas id="myCanvas" width=400 height=400 style="background:url('/img/etc/boardwalk.png'); background-size: cover">
  </canvas> 
<script>
    var ctx = myCanvas.getContext("2d");
var bug_x = 0;
 var bug_y = 0;
 var BugImg = new Image();
 BugImg.src = "https://p7.hiclipart.com/preview/456/61/155/cat-sticker-wall-decal-adhesive-stickers.jpg";         
 var melon_x = 0;
 var melon_y = 0;
 var MelonImg = new Image();
 MelonImg.src = "https://images.rawpixel.com/image_png_800/cHJpdmF0ZS9sci9pbWFnZXMvd2Vic2l0ZS8yMDIzLTA0L2pvYjk2Ny0wNTNiLXAucG5n.png";  
 var score = 0;
 var melon_speed = 3;
 var FPS = 40;                        
 var time_remaining = 20;
function restart_game() {
     time_remaining = 20;
     score = 0;
     melon_speed = 3;
     }
function ImagesTouching(x1, y1, img1, x2, y2, img2) {
          if (x1 >= x2+img2.width || x1+img1.width <= x2) return false;   
          if (y1 >= y2+img2.height || y1+img1.height <= y2) return false; 
          return true;                                                       
          }
function Do_a_Frame () {
    ctx.clearRect(0, 0, myCanvas.width, myCanvas.height);                 
    ctx.fillStyle= "purple";
    ctx.font = "20px Arial";
    ctx.fillText("Score: " + score, 0, 20);                               
    bug_y = myCanvas.height - BugImg.height;                              
    ctx.drawImage(BugImg, bug_x, bug_y);                                  
    ctx.fillText("Time Remaining: " + Math.round(time_remaining), 0, 45); }
if (time_remaining <= 0) {                                            
          ctx.fillStyle= "red";
          ctx.font = "bold 50px Arial";                                   
          ctx.textAlign="center";
          ctx.fillText("Game Over", myCanvas.width / 2, myCanvas.height / 2);  
          ctx.font = "bold 20px Arial";
          ctx.fillText("Press S to play again", myCanvas.width / 2, (myCanvas.height / 2)+50);
          ctx.textAlign="left"; }      
else {
          time_remaining = time_remaining - 1/FPS;                        
          melon_y = melon_y + melon_speed;  }                              
          if (melon_y > myCanvas.height)                                 
              melon_y= 0;                                                 
              melon_x= Math.random() * (myCanvas.width - MelonImg.width); 
ctx.drawImage(MelonImg, melon_x, melon_y);                            
    if (ImagesTouching(bug_x, bug_y, BugImg, melon_x, melon_y, MelonImg)) {  
        score= score + 1;                                                    
        melon_speed = melon_speed + 0.5;                                     
        melon_x= -MelonImg.width;                                            
        }
     setInterval(Do_a_Frame, 1000/FPS);                                          
function MyKeyDownHandler (MyEvent) { 
   if (MyEvent.keyCode == 37 && bug_x > 0) {bug_x = bug_x - 10;}                          
   if (MyEvent.keyCode == 39 && bug_x+BugImg.width < myCanvas.width) {bug_x = bug_x+10;}  
   if (MyEvent.keyCode == 83) restart_game();                                             
   MyEvent.preventDefault();
   }
 addEventListener("keydown", MyKeyDownHandler);                      
 myCanvas.width = window.innerWidth - 20;                            
 myCanvas.height = window.innerHeight - 20;                          

</script>
</body>
</html>





<!DOCTYPE html>
<html>
<head>
    <title>My Melon Falling Game</title>
</head>
<body>
<canvas id="myCanvas" width="400" height="400" style="background:url('/img/etc/boardwalk.png'); background-size: cover">
</canvas>
<script>
    var ctx = myCanvas.getContext("2d");
    var bug_x1 = 0, bug_y1 = 0, bug_x2 = 300, bug_y2 = 300;
    var BugImg1 = new Image(), BugImg2 = new Image();
    BugImg1.src = "https://p7.hiclipart.com/preview/456/61/155/cat-sticker-wall-decal-adhesive-stickers.jpg";
    BugImg2.src = "https://p7.hiclipart.com/preview/456/61/155/cat-sticker-wall-decal-adhesive-stickers.jpg";
    var melon_x = 0, melon_y = 0, bomb_x = 100, bomb_y = 0;
    var MelonImg = new Image(), BombImg = new Image();
    MelonImg.src = "https://images.rawpixel.com/image_png_800/cHJpdmF0ZS9sci9pbWFnZXMvd2Vic2l0ZS8yMDIzLTA0L2pvYjk2Ny0wNTNiLXAucG5n.png";
    BombImg.src = "https://p7.hiclipart.com/preview/922/23/322/hand-grenade-bomb-computer-icons-missile.jpg";
    var score1 = 0, score2 = 0, melon_speed_x = 3, melon_speed_y = 3, bomb_speed_x = 3, bomb_speed_y = 3;
    var FPS = 40, time_remaining = 180;
    var speed_increase_interval = 10 * FPS;
    var frame_count = 0;
    function restart_game() {
        time_remaining = 180;
        score1 = 0, score2 = 0;
        melon_speed_x = 3, melon_speed_y = 3;
        bomb_speed_x = 3, bomb_speed_y = 3;
        frame_count = 0;
    }
    function ImagesTouching(x1, y1, img1, x2, y2, img2) {
        if (x1 >= x2 + img2.width || x1 + img1.width <= x2) return false;
        if (y1 >= y2 + img2.height || y1 + img1.height <= x2) return false;
        return true;
    }
    function Do_a_Frame() {
        ctx.clearRect(0, 0, myCanvas.width, myCanvas.height);
        ctx.fillStyle = "purple";
        ctx.font = "20px Arial";
        ctx.fillText("Score 1: " + score1, 0, 20);
        ctx.fillText("Score 2: " + score2, 0, 40);
        ctx.fillText("Time Remaining: " + Math.round(time_remaining), 0, 60);
        bug_y1 = Math.min(myCanvas.height - BugImg1.height, Math.max(0, bug_y1));
        bug_y2 = Math.min(myCanvas.height - BugImg2.height, Math.max(0, bug_y2));
        ctx.drawImage(BugImg1, bug_x1, bug_y1);
        ctx.drawImage(BugImg2, bug_x2, bug_y2);
        if (time_remaining <= 0) {
            ctx.fillStyle = "red";
            ctx.font = "bold 50px Arial";
            ctx.textAlign = "center";
            ctx.fillText("Game Over", myCanvas.width / 2, myCanvas.height / 2);
            ctx.font = "bold 20px Arial";
            ctx.fillText("Press S to play again", myCanvas.width / 2, (myCanvas.height / 2) + 50);
            ctx.textAlign = "left";
            return;
        } else {
            time_remaining -= 1 / FPS;
            melon_x += melon_speed_x;
            melon_y += melon_speed_y;
            bomb_x += bomb_speed_x;
            bomb_y += bomb_speed_y;
            if (melon_x > myCanvas.width || melon_x < 0) melon_speed_x *= -1;
            if (melon_y > myCanvas.height || melon_y < 0) melon_speed_y *= -1;
            if (bomb_x > myCanvas.width || bomb_x < 0) bomb_speed_x *= -1;
            if (bomb_y > myCanvas.height || bomb_y < 0) bomb_speed_y *= -1;
            ctx.drawImage(MelonImg, melon_x, melon_y);
            ctx.drawImage(BombImg, bomb_x, bomb_y);
            if (ImagesTouching(bug_x1, bug_y1, BugImg1, melon_x, melon_y, MelonImg)) {
                score1 += 1;
                reset_melon();
            } else if (melon_y > myCanvas.height) {
                score1 -= 1;
                reset_melon();
            }
            if (ImagesTouching(bug_x2, bug_y2, BugImg2, melon_x, melon_y, MelonImg)) {
                score2 += 1;
                reset_melon();
            } else if (melon_y > myCanvas.height) {
                score2 -= 1;
                reset_melon();
            }
            if (ImagesTouching(bug_x1, bug_y1, BugImg1, bomb_x, bomb_y, BombImg)) {
                score1 -= 1;
                reset_bomb();
            }
            if (ImagesTouching(bug_x2, bug_y2, BugImg2, bomb_x, bomb_y, BombImg)) {
                score2 -= 1;
                reset_bomb();
            }
        }
        frame_count++;
        if (frame_count % speed_increase_interval == 0) {
            melon_speed_x *= 1.1;
            melon_speed_y *= 1.1;
            bomb_speed_x *= 1.1;
            bomb_speed_y *= 1.1;
        }
    }
    function reset_melon() {
        melon_x = Math.random() * (myCanvas.width - MelonImg.width);
        melon_y = 0;
    }
    function reset_bomb() {
        bomb_x = Math.random() * (myCanvas.width - BombImg.width);
        bomb_y = 0;
    }
    function MyKeyDownHandler(MyEvent) {
        switch (MyEvent.keyCode) {
            case 37: 
                if (bug_x1 > 0) bug_x1 -= 10;
                break;
            case 38: 
                if (bug_y1 > 0) bug_y1 -= 10;
                break;
            case 39: 
                if (bug_x1 + BugImg1.width < myCanvas.width) bug_x1 += 10;
                break;
            case 40: 
                if (bug_y1 + BugImg1.height < myCanvas.height) bug_y1 += 10;
                break;
            case 65: 
                if (bug_x2 > 0) bug_x2 -= 10;
                break;
            case 87: 
                if (bug_y2 > 0) bug_y2 -= 10;
                break;
            case 68: 
                if (bug_x2 + BugImg2.width < myCanvas.width) bug_x2 += 10;
                break;
            case 83: 
                if (bug_y2 + BugImg2.height < myCanvas.height) bug_y2 += 10;
                break;
            case 82: 
                restart_game();
                break;
        }
        MyEvent.preventDefault();
    }
    addEventListener("keydown", MyKeyDownHandler);
    myCanvas.width = window.innerWidth - 20;
    myCanvas.height = window.innerHeight - 20;
    setInterval(Do_a_Frame, 1000 / FPS);
</script>
</body>
</html>