---
title: A game from the past

date: 2019-11-28
updated: 2022-07-23
taxonomies:
    tags: [blog,]
---
I've ported an old game I made in inform7 to javascript. It is filled with teenager angst, because I made the game in order to deal with some problems I was having back them.

**Alone in the darkness**

by Ivan Tadeu "This is a Interactive Narrative  by Ivan Tadeu Ferreira Antunes Filho. It talks about a night in the life of a sad boy. The changes that happens after writing one word may or may not depend upon the words that are already in the narrative."

Click a word of significance from the text to revise the story. 

---

 <br><br>
 <style> 

 
</p>
 
</p>
 
@keyframes colorize {
    0% {
        -webkit-filter: grayscale(100%);
        filter: grayscale(100%);
    }
    100% {
        -webkit-filter: grayscale(0%);
        filter: grayscale(0%);
    }
}
.clickable-word {
  cursor: default;
   /*! border-bottom: 1px dotted; */
   border-bottom: 0px dotted; 
  transition: cursor 3s linear ;

}

.clickable-word:hover {
  animation: delay-clickable-change 0.4s steps(10, end);
  cursor: pointer;
  border-bottom: 1px ridge; 
    /*! color:brown; */
    /*! border-bottom: 1px dotted; */
}


@keyframes delay-clickable-change {
    0% {
      cursor: default;
      border-bottom: 0px dotted; 
    }
    50% {
        cursor: : default;
      border-bottom: 0px ridge; 
    }
    100% {
        cursor: pointer;
        border-bottom: 1px ridge; 
    }
}

.story{
  line-height: 1.7em;
  overflow: hidden; /* Ensures the content is not revealed until the animation */
  white-space: wrap; /* Keeps the content on a single line */
  margin: 0 auto; /* Gives that scrolling effect as the typing happens */
  letter-spacing: .03em; /* Adjust as needed */
  vertical-align: text-bottom;
    
}
.new-text {
  display: inline;
  overflow: hidden; /* Ensures the content is not revealed until the animation */
  white-space: wrap; /* Keeps the content on a single line */
  margin: 0 auto; /* Gives that scrolling effect as the typing happens */
  vertical-align: bottom;
  animation: 
    typing 0.85s steps(50, end);
}

.substituted-text {
  display: inline;
  pointer-events: none;
  overflow: hidden; /* Ensures the content is not revealed until the animation */
  white-space: wrap; /* Keeps the content on a single line */
  margin: 0 auto; /* Gives that scrolling effect as the typing happens */
  vertical-align: bottom;
  max-width: 0;
  animation: 
    deleting 0.5s steps(40, end)
}

.substituting-text {
  display: inline;
  overflow: hidden; /* Ensures the content is not revealed until the animation */
  white-space: wrap; /* Keeps the content on a single line */
  margin: 0 auto; /* Gives that scrolling effect as the typing happens */
  vertical-align: bottom;
  -webkit-animation-delay: 0.5s; /* Safari 4.0 - 8.0 */
  animation-delay: 0.5s;
  animation: 
    typing 0.85s steps(50, end)
}

.old-text {
  display: inline;
  overflow: hidden; /* Ensures the content is not revealed until the animation */
  white-space: wrap; /* Keeps the content on a single line */
  margin: 0 auto; /* Gives that scrolling effect as the typing happens */
  vertical-align: bottom;
}



/* The deleting effect */
@keyframes deleting {
  from { max-width: 100% }
  to { max-width: 0% }
}


/* For editting */
pre {
    white-space: pre-wrap;       /* Since CSS 2.1 */
    white-space: -moz-pre-wrap;  /* Mozilla, since 1999 */
    white-space: -pre-wrap;      /* Opera 4-6 */
    white-space: -o-pre-wrap;    /* Opera 7 */
    word-wrap: break-word;       /* Internet Explorer 5.5+ */
}

.flash-dark {
    animation: 
       flashDark 1.0s steps(40, end)
}

@keyframes flashDark {
  from { background: #000 }
  to { background: ##fff }
}

.flash-red {
	color: #ddcdcd;
    animation: 
       flashRed 1.0s steps(40, end);
    background: #000;
}

.flash-blood {
	color: #ddcdcd;
    animation: 
       flashRed 1.0s steps(40, end);
    background: #000;
      background-image: linear-gradient(182deg, rgb(000, 000, 000) 89%, rgb(90, 7, 20) 100%);
}


@keyframes flashRed {
  from { background: #8A0707;
  		 color: #555; }
  to { background: #000;
  	   color: #ddd;}
}

.get-dark {
	color: #ddcdcd;
    animation: 
       getDark 1.0s steps(40, end);
    background: #000;
}

@keyframes getDark {
  from { background: #ffffff;
  		 color: #555; }
  to { background: #000;
  	   color: #ddd;}
}

.hidden{
    display: none;
}

.cycle3{
	width: auto;

}
.cycle3>span{
	-webkit-animation: topToBottom 7.5s linear infinite 0s;
	opacity: 0;
	overflow: hidden;
		position: absolute;
	vertical-align: bottom;
}
.cycle3>span:nth-child(2){
	position: absolute;
	-webkit-animation-delay: 2.5s;

}
.cycle3>span:nth-child(3){
	position: static;
	-webkit-animation-delay: 5s;
}
@-webkit-keyframes topToBottom{
	0% { opacity: 0; }
	0% { opacity: 0; -webkit-transform: translateY(-60%); }
	5% { opacity: 1; -webkit-transform: translateY(0px); }
	25% { opacity: 1; -webkit-transform: translateY(0px); }
	33% { opacity: 0; -webkit-transform: translateY(60%); }
	80% { opacity: 0; }
	100% { opacity: 0; }
}


.dark_word {
  -webkit-animation: dark_word 2s steps(10) alternate infinite;
          animation: dark_word 2s steps(10) alternate infinite;
   text-shadow: -1px 0px 0px transparent;
}

@-webkit-keyframes dark_word {
  to {
    text-shadow: 1px 0px 3px black;
  }
}

.moving_word {
	position:relative;
  -webkit-animation: moving_word 2s steps(10) alternate infinite;
          animation: moving_word 2s steps(10) alternate infinite;
   left: -1px;
}

@-webkit-keyframes moving_word {
  to {
    left: 1px;;
  }
}
#editor { 
        position: relative;
        height: 80vh;
    }


/* The typing effect */
@keyframes typing {
  from { -webkit-clip-path: polygon(0% 0%, 0% 100vh, 0% 100vh, 0% 0%);
    clip-path:  polygon(0% 0%, 0% 100vh, 0% 100vh, 0% 0%); }
  to { -webkit-clip-path: polygon(0% 0%, 0% 100vh, 100% 100vh, 100% 0%);
    clip-path:  polygon(0% 0%, 0% 100vh, 100vw 100vh, 100vw 0%);}
}

@media (min-device-width: 1224px) {
  	.story {
  	max-width: 40vw;
      margin-left: 0;
      font-size: large;
  }
    /* The typing effect */
@keyframes typing {
  from { -webkit-clip-path: polygon(0% 0%, 0% 100vh, 0% 100vh, 0% 0%);
    clip-path:  polygon(0% 0%, 0% 100vh, 0% 100vh, 0% 0%); }
  to { -webkit-clip-path: polygon(0% 0%, 0% 100vh, 40vw 100vh, 40vw 0%);
    clip-path:  polygon(0% 0%, 0% 100vh, 40vw 100vh, 40vw 0%);}
}

	#editing-1{
		color: #444;
		position:absolute;
		right: 5%;
		top: 1%;
		padding-left: 1%;
		width: 20%;
		background :white;
	}

	#editing-2{
		color: #444;
		position:absolute;
		left: 5%;
		top: 5%;
		padding-left: 1%;
		width: 20%;
		background :white;
	}
  }

<p>

<p>

<p>

<p>

 </style>
 <script src="./js/js-yaml.js"></script>  
 <script src="./js/ace.js" type="text/javascript" charset="utf-8"></script>  
 <script src="./js/interactivenarrative.js"></script>  
 <script> run_from_yaml_file("./yaml/alone.yaml",  {"v": "$1$", "1":"/Sad/ and /lonely/", "END": "END"}); </script>

 <div id = "text-background">
    <p class = "story" id="story"></p>
    <br>
    <p class = "story" id="timed_words"></p>
    <div  id = "editing" class="hidden">
    <br><br>
        <div  id = "editing-1" >
        <p class = "story" id="subs"></p>
                <br><br>
        <p class = "story" id="subs2"></p>
            <br><br>
        </div>
        <div  id = "editing-2" >
        <p class = "story" id="flags"></p>
                <br><br>
        </div>
        <button id="reload_yaml1">RELOAD YAML editor</button>
        <button id="reload_yaml2">RELOAD YAML area</button>
        <button id="restart">RESTART</button>
        <button id="undo_button">UNDO</button>
        <div id="editor"></div>
        <pre > <textarea id="story_yaml" style = "width:100%; height:50vh;"></textarea></pre>
    </div>
    <br><br>
    <button id="toggle_editing" class="hidden">Toggle editing</button>
</div>
