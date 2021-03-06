/\*  \*/

/\* <noinclude>

Fonctions standards pour gérer des éléments en position absolute :

  - fonction "move",
  - fonction "resize"

Voir page de discussion.</noinclude>

## CODES SOURCE

### FONCTION : navigateur

  - Renvoie true si le navigateur est Internet Explorer

<div style="border:1px dashed green;margin:1em;padding:1em;">

``` javascript
//<pre><nowiki>

function MoveResizeAbsolute_NavIsIE(){
     var agt=navigator.userAgent.toLowerCase();
     var is_ie = ((agt.indexOf("msie") != -1) && (agt.indexOf("opera") == -1));
     return is_ie;
}

//</nowiki></pre>
```

</div>

### FONCTION : largeur de l'écran

  - Renvoie la largeur de l'écran (en pixels)

<div style="border:1px dashed green;margin:1em;padding:1em;">

``` javascript
//<pre><nowiki>

function MoveResizeAbsolute_GetScreenWidth(){
     if(MoveResizeAbsolute_NavIsIE()){
          var ScreenWidth = parseInt(screen.width);
     }else{
          var ScreenWidth = parseInt(window.innerWidth);
     }
     return ScreenWidth;
}

//</nowiki></pre>
```

</div>

### FONCTION : hauteur de l'écran

  - Renvoie la hauteur de l'écran (en pixels)

<div style="border:1px dashed green;margin:1em;padding:1em;">

``` javascript
//<pre><nowiki>

function MoveResizeAbsolute_GetScreenHeight(){
     if(MoveResizeAbsolute_NavIsIE()){
          var ScreenHeight = parseInt(screen.height);
     }else{
          var ScreenHeight = parseInt(window.innerHeight);
     }
     return ScreenHeight;
}

//</nowiki></pre>
```

</div>

### FONCTION : MOVE

Transforme un élément en ancre pour bouger un autre élément (en position
fixed)

  - elementArea = élément ancre (obligatoire)
  - elementsToMove = éléments à bouger (obligatoire)
  - LeftLimit = limite gauche, en pixel (facultatif)
  - TopLimit = limite haut, en pixel (facultatif)

<div style="border:1px dashed green;margin:1em;padding:1em;">

``` javascript
//<pre><nowiki>

function MoveResizeAbsolute_AddMoveArea(elementArea, elementsToMove, LeftLimit, TopLimit){
     if((!elementArea)||(!elementsToMove)) return;
     elementArea.onmousedown=function(event) {
          var monbody = document.body;
          if(!event) { event = window.event; }
          if(MoveResizeAbsolute_NavIsIE()){
               positionSouris_X = parseInt( event.clientX + monbody.scrollLeft );
               positionSouris_Y = parseInt( event.clientY + monbody.scrollTop );
          }else{
               positionSouris_X = parseInt( event.pageX );
               positionSouris_Y = parseInt( event.pageY );
          }
          for(var a=0;a<elementsToMove.length;a++){
               elementsToMove[a].initialX = parseInt( positionSouris_X - elementsToMove[a].offsetLeft);
               elementsToMove[a].initialY = parseInt( positionSouris_Y - elementsToMove[a].offsetTop);
               elementsToMove[a].style.opacity = '.8';
          }
          monbody.onmousemove = function(event) {
               if(!event) { event = window.event; }
               if(MoveResizeAbsolute_NavIsIE()){
                    positionSouris_X = parseInt( event.clientX + monbody.scrollLeft );
                    positionSouris_Y = parseInt( event.clientY + monbody.scrollTop );
               }else{
                    positionSouris_X = parseInt( event.pageX );
                    positionSouris_Y = parseInt( event.pageY );
               }
               var LeftLimitDone = false;
               var TopLimitDone = false;
               for(var a=0;a<elementsToMove.length;a++){
                    PositionGauche = parseInt( positionSouris_X ) - elementsToMove[a].initialX;
                    PositionHaut = parseInt(positionSouris_Y ) - elementsToMove[a].initialY;
                    if(LeftLimit){
                         if(LeftLimit[a]|| LeftLimit[a]==0){
                              if( PositionGauche < parseInt(LeftLimit[a])){
                                   PositionGauche = LeftLimit[a];
                                   LeftLimitDone = true;
                              }
                         }
                    }
                    if(TopLimit){
                         if(TopLimit[a]||TopLimit[a]==0){
                              if( PositionHaut < parseInt(TopLimit[a])){
                                   PositionHaut = parseInt(TopLimit[a]);
                                   TopLimitDone = true;
                              }
                         }
                    }
                    elementsToMove[a].style.left = PositionGauche + 'px';
                    elementsToMove[a].style.top = PositionHaut + 'px';
               }
               if(LeftLimitDone){
                    for(var a=0;a<elementsToMove.length;a++){
                         if(LeftLimit[a]) elementsToMove[a].style.left = LeftLimit[a] + 'px';
                    }
                    LeftLimitDone = false;
               }
               if(TopLimitDone){
                    for(var a=0;a<elementsToMove.length;a++){
                         if(TopLimit[a]) elementsToMove[a].style.top = TopLimit[a] + 'px';
                    }
                    TopLimitDone = false;
               }
          }
          monbody.onmouseup=function(event) {
               for(var a=0;a<elementsToMove.length;a++){
                    elementsToMove[a].style.opacity = '';
               }
               monbody.onmousemove = null;
               monbody.onmouseup = null;
          }
     }
     elementArea.style.cursor = "move";
}

//</nowiki></pre>
```

</div>

### FONCTION : RESIZE

Transforme un élément en ancre pour redimensionner un autre élément (en
position fixed)

  - elementArea = élément ancre (obligatoire)
  - elementsToResize = éléments à redimensionner (obligatoire, dans une
    Array)
  - MinWidth = largeur minimum, en pixel (facultatif)
  - MinHeight = hauteur minimum, en pixel (facultatif)

<div style="border:1px dashed green;margin:1em;padding:1em;">

``` javascript
//<pre><nowiki>

function MoveResizeAbsolute_AddResizeArea(elementArea, elementsToResize, MinWidth, MinHeight){
     if((!elementArea)||(!elementsToResize)) return;
     elementArea.onmousedown = function(event){
          var monbody = document.body;
          if(!event) { event = window.event; }
          if(MoveResizeAbsolute_NavIsIE()){
               positionSouris_X = parseInt( event.clientX + monbody.scrollLeft );
               positionSouris_Y = parseInt( event.clientY + monbody.scrollTop );
          }else{
               positionSouris_X = parseInt( event.pageX );
               positionSouris_Y = parseInt( event.pageY );
          }
          for(var a=0;a<elementsToResize.length;a++){
               elementsToResize[a].initialWidth = parseInt( positionSouris_X - elementsToResize[a].offsetWidth );
               elementsToResize[a].initialHeight = parseInt( positionSouris_Y - elementsToResize[a].offsetHeight );
               elementsToResize[a].style.opacity = '.8';
          }
          monbody.onmousemove=function(event) {
               if(!event) { event = window.event; }
               if(MoveResizeAbsolute_NavIsIE()){
                    positionSouris_X = parseInt( event.clientX + monbody.scrollLeft );
                    positionSouris_Y = parseInt( event.clientY + monbody.scrollTop );
               }else{
                    positionSouris_X = parseInt( event.pageX );
                    positionSouris_Y = parseInt( event.pageY );
               }
               var MinWidthDone = false;
               var MinHeightDone = false;
               for(var a=0;a<elementsToResize.length;a++){
                    var NewWidth = parseInt( positionSouris_X - elementsToResize[a].initialWidth  );
                    var NewHeight = parseInt( positionSouris_Y - elementsToResize[a].initialHeight );
                    if(MinWidth){
                         if(MinWidth[a] || MinWidth[a]==0){
                              if(NewWidth<parseInt(MinWidth[a])){
                                   NewWidth = MinWidth[a];
                                   MinWidthDone = true;
                              }
                         }
                    }
                    if(MinHeight){
                         if(MinHeight[a] || MinHeight[a]==0){
                              if(NewHeight<parseInt(MinHeight[a])){
                                   NewHeight = MinHeight[a];
                                   MinHeightDone = true;
                              }
                         }
                    }
                    elementsToResize[a].style.width  = NewWidth + 'px';
                    elementsToResize[a].style.height = NewHeight + 'px';
               }
               if(MinWidthDone){
                    for(var a=0;a<elementsToResize.length;a++){
                         if(MinWidth[a]) elementsToResize[a].style.width  = MinWidth[a] + 'px';
                    }
               }
               if(MinHeightDone){
                    for(var a=0;a<elementsToResize.length;a++){
                         if(MinHeight[a]) elementsToResize[a].style.height  = MinHeight[a] + 'px';
                    }
               }

          }
          monbody.onmouseup=function(event) {
               for(var a=0;a<elementsToResize.length;a++){
                    elementsToResize[a].style.opacity = '';
               }
               monbody.onmousemove = null;
               monbody.onmouseup = null;
          }
     }
     elementArea.style.cursor = "se-resize";
}
//</nowiki></pre>
```

</div>

window.MoveResizeAbsolute_GetScreenWidth =
MoveResizeAbsolute_GetScreenWidth;
window.MoveResizeAbsolute_GetScreenHeight =
MoveResizeAbsolute_GetScreenHeight;
window.MoveResizeAbsolute_AddMoveArea =
MoveResizeAbsolute_AddMoveArea;
window.MoveResizeAbsolute_AddResizeArea =
MoveResizeAbsolute_AddResizeArea;