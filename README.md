# GSAP
Workshop : découverte de GSAP (Green Socket Animation Platform)
=======================

[Présentation rapide de GSAP](https://greensock.com/ "Présentation rapide de GSAP")

***

1: Gsap c'est 4 librairies, et des plugins (pas tous gratuits :-( ... )
-----------------

1. TweenLite
2. TimelineLite
3. TimelineMax
4. TweenMax
5. Plugins : CSS, Easing, Colors...
- [Liste des plugins](https://greensock.com/plugins/)
- [Liste des liens CDN](https://cdnjs.com/libraries/gsap)

Pour ce workshop, on utilisera le TweenMax : 

  ```
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/2.0.1/TweenMax.min.js"></script>
  ```
  
***
  
2: Les sélecteurs : JQuery ou Javascript (pour les puristes)
-----------------
```
  <div class="box">Boite</div>
  <h1>Titre</h1>
  
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
 
 Petit tuto pour démarrer facilement en GSAP, copiez ceci dans un doc html vide : 
 
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
  
  <title>GSAP Tuto</title>
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
   background-color : red;
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
<!-- <button type="button" name="button" class="btn">Bouton</button>
<button type="button" name="button" class="btn">Bouton</button>
<button type="button" name="button" class="btn">Bouton</button>
<button type="button" name="button" class="btn">Bouton</button>
<button type="button" name="button" class="btn">Bouton</button>
<button type="button" name="button" class="btn">Bouton</button>
<button type="button" name="button" class="btn">Bouton</button>
<button type="button" name="button" class="btn">Bouton</button>
<button type="button" name="button" class="btn">Bouton</button> -->
  
<script>

window.onload = function() {
  let img = $('.img');
  let text = $('.text');
  let box = $('.box');
  let btn = $('.btn');


}
</script>
</body>
</html>

 
 ```
 Téléchargez cette image, ajoutez la dans le même dossier (ah.png)
![alt text](https://i.kym-cdn.com/photos/images/original/001/305/802/660.png "Nommez-moi ah.png plz")
 
***

 4: Mon premier tween :-D
 ============
 
- Créer le Tween (différence entre from, to, fromTo):
 ```
   TweenMax.to(img, 1, {x:200});
   
   TweenMax.to(img, 1, {x: -200});
   
   TweenMax.from(img, 1, {x:200});
   
   TweenMax.from(img, 1, {x: -200});
   
   TweenMax.fromTo(img, 1, {x: -200}, {x:200});

   TweenMax.fromTo(text, 1, {x: 200}, {x:-200});
   
   TweenMax.fromTo(box, 1, {y: -100}, {y:100, color:"white"});
   
   TweenMax.to(text, 1,{scale:0.2, opacity:0.3});

   TweenMax.to(box, 1, {backgroundColor: 'teal'});
   
   // !! pas de - entre 2 mots, on utilise le camelCase (backrgound-color => backgroundColor) !!

 ```
- Add some delay :
  
 ```
  
   TweenMax.fromTo(box, 1, {y: -100}, {y:100, color:"white", delay : 0.5});

   TweenMax.to(box, 1, {backgroundColor: 'teal', delay : 1.5});
    
    
 ```
- Se mettre à l'ease:
  
  Super utile :  [le visualizer](https://greensock.com/ease-visualizer)
  
 ```
  TweenMax.fromTo(box, 1, {y: -100}, {ease: Elastic. easeOut.config( 1, 0.3), y:100, color:"white", delay : 0.5});

  TweenMax.to(box, 1, {backgroundColor: 'teal', ease:RoughEase.ease.config({template:Power0.easeNone,strength:1,points:20,taper:"none",randomize: true,clamp: false}), delay : 1.5});
  
  ```
  
  
 5: Call-Backs functions
 ============
 
 OnStart, OnUpdate et OnComplet
 
 [Testez les events call-backs ici](https://greensock.com/jump-start-js#event-callbacks)
 
 6: L'atout n°1 de GSAP : les Timelines
 ============
 
 Permet d'animer facilement plusieurs objets.
 
 Quand on met plusieurs Tweens à la suite, si tout ne doit pas être animé en même temps, il faut calculer le delay.
 Grâce aux TL, plus besoin de delay, chaque tween a lieux à la suite de l'autre (on peut facilement ajuster le timing => overlap).
 
 Changer les Tweens successifs en une TL : 

```
// sans delay, tout se lance en même temps:
TweenMax.fromTo(img, 1, {x: -200}, {x:200});
TweenMax.fromTo(text, 1, {x: 200}, {x:-200});
TweenMax.fromTo(box, 1, {y: -100}, {ease: Elastic. easeOut.config( 1, 0.3), y:100, color:"white"});
TweenMax.to(box, 1, {backgroundColor: 'teal', ease:RoughEase.ease.config({template:Power0.easeNone,strength:1,points:20,taper:"none",randomize: true,clamp: false})});

// on calcule le delay pour que tout se lance à la suite l'un de l'autre
TweenMax.fromTo(img, 1, {x: -200}, {x:200});
TweenMax.fromTo(text, 1, {x: 200}, {x:-200, delay:1});
TweenMax.fromTo(box, 1, {y: -100}, {ease: Elastic. easeOut.config( 1, 0.3), y:100, color:"white", delay : 2});
TweenMax.to(box, 1, {backgroundColor: 'teal', ease:RoughEase.ease.config({template:Power0.easeNone,strength:1,points:20,taper:"none",randomize: true,clamp: false}), delay : 3});


// pour créer une timeline, créer une variable = new TimelineLite(); (ou max) :
tl = new TimelineLite();

// ceci équivaut au tweens précédents
  tl
    .fromTo(img, 1, {x: -200}, {x:200})
    .fromTo(text, 1, {x: 200}, {x:-200})
    .fromTo(box, 1, {y: -100}, {ease: Elastic. easeOut.config( 1, 0.3), y:100, color:"white"})
    .to(box, 1, {backgroundColor: 'teal', ease:RoughEase.ease.config({template:Power0.easeNone,strength:1,points:20,taper:"none",randomize: true,clamp: false})})

    ;
```

- Attention, ne pas oublier la variable tl = ... et le fait que les  ";"  ne viennent qu'une fois, à la fin (les retirer dans les autres lignes)
- Comment gérer les delays dans une tl : fini les ``` ,delay : 1```   => ``` ,'+=1'``` 
- On peut aussi donner un label à un des éléments de la TL (ex : ```.add('intro') ``` ) et le réutiliser plus loin (ex:``` , 'intro +=0.5' ```)

***
 7: Quelques autres fonctionnalités de la TL :
 ============
 
- Controler la timeline 
  - Play
  - Pause
  - Resume
  - Reverse
  - Speed up
  - Slow down
  - Seek (label)
  [Tester ces controles ici](https://greensock.com/jump-start-js#control-playback) 
 
- Stagger
  - S'utilise aussi avec from, to, fromTo
  - Permet de créer un cycle (effet boule de neige)
  
Décommentez les buttons et ajouter ceci à la tl :
```
.staggerTo(btn, 0.5, {opacity:0, y:-100, ease:Back.easeIn}, 0.1)
```
- Repeat
  - [Tester le repeat ici](https://greensock.com/jump-start-js#repeat)
  - Avec TweenMax
  - -1 = à l'infini
  

- Compatible avec SVG, canvas, adobe animate CC, Action Script 3. Fort répendu.


***

 8: Exemples et liens
 ============
 - Exemples
   - Mes anims de ouf (Chouette plugin : textPlugin)
   
   ex de code : ``` .to(text2_1, 1.5, {text:"C'est jusque quel âge ?", ease:Linear.easeNone}, '+=0.5') ```
   - [La demande de Ludo pour Cherry Pulp (anim du texte)](https://www.patholudovic.be/cherrypulp/) 
   - [Exemples sur le site de GS](https://greensock.com/examples-showcases)
 - Liens :
    - [Tuto video (1h10, gratuit, faut juste s'inscrire, anglais australien)](https://ihatetomatoes.net/g101/)
    - [Tuto wiki fr](http://edutechwiki.unige.ch/fr/Tutoriel_GreenSock_GSAP)
    - [Jump Start officiel ](https://greensock.com/jump-start-js#control-playback)
    - [Getting started with GSAP officiel ](https://greensock.com/get-started-js)
    - [Cheatsheet](https://ihatetomatoes.net/wp-content/uploads/2016/07/GreenSock-Cheatsheet-4.pdf) 
 
 ***
 
 Last: Do it yourself ;-)
 ============
 
 Crée un nouveau doc html, reprends la structure suivante, et amuse toi (ou pas, #jemenbatslescouilles) :
 
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
  
  <title>Ma 1ère anim GSAP</title>
 <style>
 *{
   margin: 0;
   padding: 0;
   box-sizing: border-box;
 }


 </style>
</head>
<body>
// insère ici les éléments à animer (div, textes, images, bg...)

  
<script>

window.onload = function() {
// insère ici tes variables, pas oublier la variable timeline si tu l'utilises


// insère ici tes tweens ou timeline


}

</script>
</body>
</html>

 
 ```
 
MERCI bisous
