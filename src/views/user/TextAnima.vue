<template>
   <div class="rotating">
      <p class="first">보육 콘텐츠 큐레이션 플랫폼</p>
      <p class="second">
         <span class="word wisteria">위파위키</span>
         <span class="word belize">With Parents With Kids</span>
         <!-- <span class="word pomegranate">fancy.</span> -->
         <!-- <span class="word green">beautiful.</span> -->
         <!-- <span class="word midnight">cheap.</span> -->
      </p>
   </div>
</template>
<script>
export default {
   name: 'Test1',

   mounted() {
      setTimeout(this.doSome(), 1000);
   },

   methods: {
      doSome() {
         var words = document.getElementsByClassName('word');
         var wordArray = [];
         var currentWord = 0;

         words[currentWord].style.opacity = 1;
         for (var i = 0; i < words.length; i++) {
            splitLetters(words[i]);
         }

         function changeWord() {
            var cw = wordArray[currentWord];
            var nw = currentWord == words.length - 1 ? wordArray[0] : wordArray[currentWord + 1];
            for (var i = 0; i < cw.length; i++) {
               animateLetterOut(cw, i);
            }

            for (var j = 0; j < nw.length; j++) {
               nw[j].className = 'letter behind';
               nw[0].parentElement.style.opacity = 1;
               animateLetterIn(nw, j);
            }

            currentWord = currentWord == wordArray.length - 1 ? 0 : currentWord + 1;
         }

         function animateLetterOut(cw, i) {
            setTimeout(function() {
               cw[i].className = 'letter out';
            }, i * 80);
         }

         function animateLetterIn(nw, i) {
            setTimeout(function() {
               nw[i].className = 'letter in';
            }, 340 + i * 80);
         }

         function splitLetters(word) {
            var content = word.innerHTML;
            word.innerHTML = '';
            var letters = [];
            for (var i = 0; i < content.length; i++) {
               var letter = document.createElement('span');
               letter.className = 'letter';
               letter.innerHTML = content.charAt(i);
               word.appendChild(letter);
               letters.push(letter);
            }

            wordArray.push(letters);
         }

         changeWord();
         setInterval(changeWord, 4000);
      },
   },
};
</script>

<style lang="scss">
.rotating {
   // background-color: red;
   position: absolute;
   width: 450px;
   left: 50%;
   margin-left: -225px;
   height: 40px;
   top: 50%;
   margin-top: -20px;

   p.first {
      font-weight: 500;
      margin-bottom: 0px;
   }

   p.second {
      display: block;
      // vertical-align: top;
      height: 200px;
      margin: 0;
      // background-color: red;
      font-size: 26pt;
   }

   .word {
      position: absolute;
      width: 300px;
      opacity: 0;
   }

   .letter {
      display: inline-block;
      position: relative;
      float: left;
      transform: translateZ(25px);
      transform-origin: 50% 50% 25px;

      font-family: 'Poor Story';
      font-weight: 600;
   }

   .letter.out {
      margin-right: 1px;
      transform: rotateX(90deg);
      transition: transform 0.32s cubic-bezier(0.55, 0.055, 0.675, 0.19);

      font-family: 'Poor Story';
      font-weight: 600;
   }

   .letter.behind {
      transform: rotateX(-90deg);
   }

   .letter.in {
      margin-right: 1px;
      transform: rotateX(0deg);
      transition: transform 0.38s cubic-bezier(0.175, 0.885, 0.32, 1.275);

      font-family: 'Poor Story';
      font-weight: 600;
   }

   .wisteria {
      color: #c0392b;
   }

   .belize {
      color: #16a085;
   }
}

// .pomegranate {
//    color: #c0392b;
// }

// .green {
//    color: #16a085;
// }

// .midnight {
//    color: #2c3e50;
// }
</style>
