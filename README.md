# GSAP
Workshop : découverte de GSAP (Green Socket Animation Platform)
=======================

[Présentation rapide de GSAP](https://greensock.com/ "Présentation rapide de GSAP")

***

1: Gsap c'est 4 librairies, et des plugins (pas tous gratuits :-(  )
-----------------

1. TweenLite
2. TimelineLite
3. TimelineMax
4. TweenMax
5. Plugins : CSS, Easing, Colors...
⋅⋅* [Liste des plugins](https://greensock.com/plugins/)
⋅⋅* [Liste des liens CDN](https://cdnjs.com/libraries/gsap)

Pour ce workshop, on utilisera le TweenMax : 

  ```
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/2.0.1/TweenMax.min.js"></script>
  ```
  
***
  
2: Les sélecteurs : JQuery ou Javascript (pour les puristes)
-----------------
```
  <div class="box">Boiteuh</div>
  <h1>Titreuh</h1>
  
Jquery
  let box = $('.box');
  let h2 = $('h2');

Pure JS
  let box = document.getElementsByClassName('box');
  let h2 = document.getElementsByTagName(h2);
  
Autre méthode  
  // JavaScript querySelector
    let select = function(s) {
    return document.querySelector(s);
    };
 
  // JavaScript querySelectorAll
    let selectAll = function(s) {
    return document.querySelectorAll(s);
    };
 
  let box = select('.box');
  let allh2 = selectAll('h2');
  
  ```
  
  ***
 3: Copiez/Collez ;-)
 ============
 
 Pour démarrer facilement en GSAP, copiez ceci dans un doc html vide : 
 
 ```
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/2.0.1/TweenMax.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/2.0.1/plugins/TextPlugin.min.js"></script>
  
 <!-- le plugin text (transforme le texte) n'est pas repris dans TweenMax -->
  
  <title>GSAP</title>
 <style>
 *{
   margin: 0;
   padding: 0;
   box-sizing: border-box;
   text-align: center;
 }
 .img img{
   width: 250px;
   margin-bottom: 100px;
 }

 .box{
   width : 250px;
   height : 250px;
   background-color : teal;
   margin: 100px auto;
 }

 </style>
</head>
<body>

 <div class="img">
   <img src="ah.png" alt="">
 </div>
 <div class="text">
   Ceci est mon texte
 </div>
 <div class="box">
   Box
 </div>

  
<script>

window.onload = function() {
  let img = $('.img');
  let text = $('.text');
  let box = $('.box');



}
</script>
</body>
</html>

 
 ```
![alt text](https://i.kym-cdn.com/photos/images/original/001/305/802/660.png "Nommez-moi ah.png plz")
 
***

 4: Mon premier tween :-D
 ============
 
- Créer le Tween :
 ```
   TweenMax.to(img, 1, {x:200});
   
   TweenMax.to(img, 1, {x: -200});
   
   TweenMax.from(img, 1, {x:200});
   
   TweenMax.from(img, 1, {x: -200});
   
   TweenMax.fromTo(img, 1, {x: -200}, {x:200});

   TweenMax.fromTo(text, 1, {x: 200}, {x:-200});
   
   TweenMax.to(box, 1, {y : -50});

   TweenMax.to(box, 1, {backgroundColor: 'teal'});

 ```
- Add some delay :
  
  ```
  
    TweenMax.to(box, 1, {y : -50, delay : 1});

    TweenMax.to(box, 1, {backgroundColor: 'teal', delay : 1.5});
    
    
  ```
- Se mettre à l'ease:
  
  Super utile :  [le visualizer](https://greensock.com/ease-visualizer)
  
  ```
 TweenMax.fromTo(box, 1, {y: -100}, {ease: Elastic. easeOut.config( 1, 0.3), y:100, delay : 0.5});

 TweenMax.to(box, 1, {backgroundColor: 'teal', ease:RoughEase.ease.config({template:Power0.easeNone,strength:1,points:20,taper:"none",randomize: true,clamp: false}), delay : 1.5});
  
  ```
  
  
 5: Call-Backs functions
 ============
 
 OnStart, OnUpdate, OnComplete
 
 6: L'atout n°1 de GSAP : les Timelines
 ============
 
 Permet d'animer facilement plusieurs objets.
 
 Quand on met plusieurs Tweens à la suite, si tout ne doit pas être animé en même temps, il faut calculer le delay.
 Grâce aux TL, plus besoin de delay, chaque tween a lieux à la suite de l'autre (on peut facilement ajuster le timing => overlap).
 
 Changer les Tweens successifs en une TL : 

```
TweenMax.fromTo(img, 1, {x: -200}, {x:200});
TweenMax.fromTo(text, 1, {x: 200}, {x:-200, delay:1});
TweenMax.fromTo(box, 1, {y: -100}, {ease: Elastic. easeOut.config( 1, 0.3), y:100, delay : 2});
TweenMax.to(box, 1, {backgroundColor: 'teal', ease:RoughEase.ease.config({template:Power0.easeNone,strength:1,points:20,taper:"none",randomize: true,clamp: false}), delay : 3});

TweenMax.fromTo(img, 1, {x: -200}, {x:200});
TweenMax.fromTo(text, 1, {x: 200}, {x:-200});
TweenMax.fromTo(box, 1, {y: -100}, {ease: Elastic. easeOut.config( 1, 0.3), y:100});
TweenMax.to(box, 1, {backgroundColor: 'teal', ease:RoughEase.ease.config({template:Power0.easeNone,strength:1,points:20,taper:"none",randomize: true,clamp: false})});


tl = new TimelineLite();

  tl
    .fromTo(img, 1, {x: -200}, {x:200})
    .fromTo(text, 1, {x: 200}, {x:-200})
    .fromTo(box, 1, {y: -100}, {ease: Elastic. easeOut.config( 1, 0.3), y:100})
    .to(box, 1, {backgroundColor: 'teal', ease:RoughEase.ease.config({template:Power0.easeNone,strength:1,points:20,taper:"none",randomize: true,clamp: false})})

    ;
```

Attention, ne pas oublier la variable tl = ... et le fait que les ; ne viennent qu'une fois, à la fin (les retirer dans les autre lignes)

Comment gérer les delays dans une tl : fini les ``` ,delay : 1```   => ``` ,'+=1'``` 
