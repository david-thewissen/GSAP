# GSAP
Workshop : découverte de GSAP (Green Socket Animation Platform)
=======================



[Présentation rapide de GSAP](https://greensock.com/ "Présentation rapide de GSAP")




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
  
  
