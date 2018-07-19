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
  
  //le plugin text (transforme le texte) n'est pas repris dans TweenMax
  
  <title>GSAP</title>

  <style>
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  .box{
    width : 250px;
    height : 250px;
    background-color : teal;
    margin-left : auto;
    margin-right : auto;
  }
 
  </style>
</head>
<body>

  <div class="img">
    <img src="ah.jpg" alt="">
  </div>
  <div class="text">
    Ceci est mon texte
  </div>
  <div class="box">
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
![alt text](https://i.kym-cdn.com/photos/images/original/001/305/802/660.png "Image Ah")
 
