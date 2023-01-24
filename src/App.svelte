
<script>
  import { HtmlTag, prevent_default } from "svelte/internal";

  const genForm = document.getElementById('gen-form');
  const genBtn = document.getElementById('gen-btn');
  const copyBtn = document.getElementById('copy-btn');
  const genContent = document.getElementById('text-content');
  // const genValue = document.getElementById('gen_count');

  //initialize variables--> count,type
  let count;
  let optionSelected;
  let tempOption = "";
  let tempCount = 0;

  // on click generate text 
  function onClick(){
    // console.log(count,optionSelected);

    // validate values
    validateValues();

    // api for dummy text generation
    let url = `https://baconipsum.com/api/?type=meat-and-filler&${optionSelected}=${count}&start-with-lorem=1`;
    fetchContent(url); // fetch this url 
  }

  // function for validating the count and option
  function validateValues(e){
    // if select word
    if(optionSelected === "words"){
      tempCount = count; // store count and option in temp value
      tempOption = optionSelected;
      // optionSelected = "paras";
      // count = 100;

      // if word count is more than 2000 --> we can access only 200 words
      if(tempCount > 2000){
        invalidInput();
        tempCount = 2000;  // print only 2000 words
      }
      else if(tempCount<1 || isNaN(tempCount)){
        invalidInput();
        tempCount = 1;  // if text box is empty or count < 1---> set count to 1
      }
    }
    else{ // if option is sentences or paras
      tempCount = 0;  
      if(count > 100){  // we can generate only 100 sentences or paras
        invalidInput();
        count = 100;  // print only 100 paras or sentences
        
      }
      else if(count < 1 || isNaN(count)){
        invalidInput();
        count = 1;  // if text box empty or count < 1 --> then print only one sentence or paragraph
      }
    }
  }

  // function --> if invalid value detected
  function invalidInput(){
    // genForm.gen_count.style.borderColor = "red";
    setTimeout(()=>{
      //---------------
    },2000);
  }

  // fetch the displayed dummy text
  async function fetchContent(url){
    let response = await fetch(url);
    if(response.status === 200){
      let data = await response.json();
      // console.log(data);
      displayGenContent(data);
    }
    else{
      alert("An error Occured");
    }
  }

  // this is the dummy text which we change using count and option selected...
  let texts = "";

  // display the generated random text
  function displayGenContent(data){
    // console.log(data);
    
    //if word is selected 
    if(tempOption === "words"){
      // console.log();
      // tempOption = "";
      texts = data.join();  // join all paragraphs 
      // console.log(texts); ---> provide full 100 paras text
      if(tempCount <= texts.length){
        let textArray = texts.split(" "); // split this text with space 
        // console.log(textArray);
        let selectedText = textArray.splice(0,tempCount).join(" "); // select text according to count 
        // textContent.innerHTML = selectedText + ".";
        // console.log(selectedText);
        texts = selectedText;  // reset this selected text value to text
      }
      return ;

    }
    else{ // if sentence or para selected
      
      texts = data.join("<br><br>");  // gives a line break between paras
      // console.log(texts);
      
    }
  }

  // function for copy button --> to copy the text
  function copyToClipboard(){

    navigator.clipboard.writeText(texts);
  }




</script>

<main>
  <body class="body-class">
    <nav class="nav-bar">
      <div class="image">
        <!-- icon666.com - MILLIONS vector ICONS FREE --><svg version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 512.001 512.001" style="enable-background:new 0 0 512.001 512.001;" xml:space="preserve"><circle style="fill:#005C83;" cx="256" cy="256" r="256"/><path style="fill:#00263F;" d="M509.16,294.202L275.85,60.892l-2.783,28.041l-28.041-28.041L207,227.667l88.232,281.343 C405.546,492.044,492.632,404.659,509.16,294.202z"/><path style="fill:#FF6838;" d="M324.866,502.618v-136.33H187.134v136.33C209.047,508.724,232.14,512,256,512 S302.953,508.724,324.866,502.618z"/><path style="fill:#AE4E32;" d="M324.866,502.618v-136.33H255v145.704c0.334,0.001,0.666,0.009,1,0.009 C279.86,512,302.953,508.724,324.866,502.618z"/><path style="fill:#FFFFFF;" d="M275.85,60.892h-8.875v162.555c11.55,4.419,19.754,15.6,19.754,28.703 c0,16.971-13.758,30.729-30.729,30.729s-30.729-13.758-30.729-30.729c0-13.103,8.205-24.284,19.754-28.703V60.892h-8.875 l-96.767,179.61v42.453l61.975,100.892h109.282l61.975-100.892v-42.453L275.85,60.892z"/><path style="fill:#E6E6E6;" d="M372.617,282.955v-42.453L275.85,60.892h-8.875v162.555c11.55,4.419,19.754,15.6,19.754,28.703 c0,16.971-13.758,30.729-30.729,30.729c-0.335,0-0.667-0.015-1-0.025v100.992h55.641L372.617,282.955z"/><rect x="171.67" y="357.19" style="fill:#FFDC00;" width="168.67" height="55.19"/><rect x="255" y="357.19" style="fill:#FFC000;" width="85.33" height="55.19"/></svg>
      </div>
      <span>
        <!-- <img src="src/Images/logo.png" alt=""> -->
        
        <h1 class="logo-text"><span class="gradient-text">Lorem Ipsum</span></h1>
        <p>A Dummy Text Generator</p>
      </span>
    </nav>
    <div class="gradient">
      <section class="section1" style="border: 20px;">
        <div class="home-body">
          <div class="side-text">
            <h1>Lorem ipsum</h1><h4>is placeholder text commonly used in the graphic, print, and publishing industries for previewing layouts and visual mockups.</h4><br><hr><br>
            <h4 style="color:red">“Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.”</h4>
          </div>
        </div>
        <div class="side-below">
          <h2><span class="auto-type"></span></h2>
        </div>
      </section>
    </div>
    

    <script src="https://cdn.jsdelivr.net/npm/typed.js@2.0.12"></script>
    <script>
      var typed = new Typed(".auto-type",{
        strings:["Create!","Copy!","Paste!!!"],
        typeSpeed:150,
        backSpeed:150,
        loop:true
      })
    </script>
    <section class="section2">
      <!-- <div class="head-section">
        <h1 style="color: #0066ff">Try our Dummy Text Generator</h1>
        <hr>
        <p>
          The classic latin passage that just never gets old, enjoy as much (or
          as little) lorem ipsum as you can handle with our easy to use filler
          text generator.
        </p>
      </div> -->

      <div class="input-div">
      <form id="gen-form" on:submit|preventDefault={onClick}>
        
        <div class="input-nav">
          <div class="input1">
            <!-- <label for="gen_count">Enter Value</label> -->
            <input name="gen_count" type="number" class="form-control" placeholder="Enter Value" min="1" max="100" bind:value={count}>
          </div>

  
          <div class="input2">
            <!-- <label for="gen_option">Select Type</label> -->
            <select name="gen_option" class="form-control" placeholder="Select Type" bind:value={optionSelected}>
              <option value="" disabled selected>Select Type</option>
              <option value="words">Words</option>
              <option value="sentences">Sentences</option>
              <option value="paras">Paragraphs</option>
            </select>
          </div>
          <button type="submit" id="gen-btn" class="btn">Generate</button>
        </div>
          
      </form>
      </div>
      <div class="text-body">
        <div id="text-content">{@html texts}</div>
      </div>
      <div class="button-bar">
        <button type="button" id="copy-btn" class="btn" on:click={copyToClipboard}>Copy Text</button>
      </div>

    </section>
  </body>
</main>

<style>
@import url("https://fonts.googleapis.com/css2?family=Scada:wght@400;700&display=swap");
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans:wght@200&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Poiret+One&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Lobster+Two:ital,wght@1,700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Comfortaa:wght@300&display=swap');
/* logo font */
@import url('https://fonts.googleapis.com/css2?family=Roboto+Flex:opsz@8..144&display=swap');


*{
  padding: 0;
  margin: 0;
}

.body-class{
  padding: 0px;
  margin:0px;
}

/* .body-class {
  height: 100vh;
  width: 100vw;
  font-family: "Scada", sans-serif !important;
} */

.image{
  width: 45px;
  height: 45px;
  margin: 0.7rem;
  margin-left: 0.2rem;
}

.nav-bar {
  width: 100%;
  padding: 1em 1.5em;
  box-sizing: border-box;
  margin:0;
  display: flex;
  
  /* display:block; */
}

/* .nav-bar img{
  height: 60px;
  border-radius: 10px;
  
} */

.nav-bar p{
  font-size: 15px;
  padding-left: 40px;
  font-family: 'Comfortaa', cursive;
  color: #161616;
  
}


.logo-text{
  display: inline; /* move this text to right siide of logo*/
  font-family:serif;
  font-size: 48px;
  background-color: #ffffff;
  font-family: 'Lobster Two', cursive;


  /* font-style: italic; */
  /* font-weight: 100px; */
  /* line-height: 60px; */
}

.gradient-text{
  background-color: rgb(253,232,192);
  background: linear-gradient(164deg, rgba(253,232,192,1) 0%, rgba(255,222,225,1) 51%, rgba(254,204,135,1) 100%); 
  background-size: 100%;
  background-image: linear-gradient(45deg, #f3ec78, #af4261);
  background-clip: text;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent; 
  -moz-text-fill-color: transparent;
}


section {
  margin: 1em;
  border-radius: 10px;
}

input {
  border:none;
  /* border: 1px solid #d0d5dd; */
  background-color: #191a19e8;
  box-shadow: 0px 1px 2px rgba(16, 24, 40, 0.05);
  border-radius: 8px;
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 10px 14px;
  width: 220px;
  color: #d0d5dd;
}

.input1 input:focus, 
.input1:hover input{
  color: #090c0f;
  background-color: rgba(255, 255, 255, 0.638);
  outline: none !important;
  border-color: #719ECE;
}

#gen-btn{
  margin-left:2rem;
  margin-right: 2rem;
}


.home-body {
  /* background-image: url(src/Images/20827476_Tiny\ characters\ sitting\ on\ laptop\ with\ lorem\ ipsum\ title.jpg); */
  height: 45vh;
  background-color: rgb(255, 255, 255);
  border: 20px;
  margin: auto;
  border-radius: 15px;
  box-shadow: 2px 5px 5px rgba(16, 24, 40, 0.05);
  display: flex;
  flex-wrap: wrap;
  text-align: center;
  align-items: center;
  justify-content: center;

}

.side-text{
  /* border: 4px solid red; */
  position:absolute;
  height: 40%;
  width: 40%;
  margin:auto;
  align-items: center;
  justify-content: center;

}

.side-text h1{
  font-size: 80px;
  color: rgb(27, 26, 26);
  /* bottom right color  */
  text-shadow: 2px 2px #72afec; 
}

.side-text h4{
  font-size: 20px;
  font-family:monospace;
  color: rgb(69, 67, 67);
}

.side-below{
  display: flex;
  margin: auto;
  align-items: center;
  justify-content: center;
}

.side-below h2{
  font-size: 70px;
  color: rgb(249, 169, 20);
  font-family: 'Poiret One', cursive;
  
}

.input-div {
  padding: 2rem;

}

.input-nav{
  font-family: 'Noto Sans', sans-serif;
  margin-top: 15rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 1em auto;
  width: 60%;
  /* margin-bottom: 50px; */
  /* padding: 2.5em; */

/* issues are here */
}

.input-div form{
  display: flex;
  flex-direction:row;
  /* overflow:hidden; */
}

#gen-form{
  margin:2rem;
}


.input-nav{
  padding:2rem 2rem;
  background: rgb(253,232,192);
  background: linear-gradient(164deg, rgba(253,232,192,1) 0%, rgba(255,222,225,1) 51%, rgba(254,204,135,1) 100%); 
  /* background-color: #29354896; */
  border-radius: 1rem;
  box-shadow: 0 0 13px 0 rgb(133, 131, 107);
  /* background-color: #36312d; */
}

.input-nav>div{
  margin:1rem;
  display: flex;
}

.text-body {
  background-color: #17171778;
  border-radius: 0.3rem;
  /* height: 60vh; */
  width: 70%;
  /* border-radius: 20px; */
  margin: auto;
  margin-bottom: 2rem;
  height: 500px;
  box-shadow: 0 0 13px 0 rgb(133, 131, 107);

}

.text-body #text-content{
  /* width:100%; */
  height: 500px;
  overflow-y:scroll;  /** if text over flow in line then it takes to next line */
  font-size: 1.2rem;
  color: #2b2e2e;
  background: rgb(253,232,192);
  background: linear-gradient(164deg, rgba(253,232,192,1) 0%, rgba(255,222,225,1) 51%, rgba(254,204,135,1) 100%); 
  line-height: 1.5;
  font-family: 'Roboto Flex', sans-serif;
  
}

#text-content{
  padding-left: 3.5rem;
  
  padding-right: 3rem;

  padding-top: 1rem;

  padding-bottom: 1rem;
  
}

#copy-btn:hover{
  background-color: #fd7580; /* Green */
  color: rgb(255, 255, 255);
  cursor: pointer;
}


button {
  width: 126px;
  height: 46px;
  font-weight: 400;
  font-size: 20px;
  line-height: 25px;
  background: #2b323e;
  color: white;
  border-radius: 0.2rem;
  border: none;
  transition-duration: 0.5s;
}

button:hover {
  background-color: #fcfffc; /* Green */
  color: rgb(8, 8, 8);
  cursor: pointer;
}

.button-bar {
  width: 70%;
  margin: auto;
  display: flex;
  justify-content:center;
}

.button-bar button {
  margin: 1em;
}


::placeholder { /* Chrome, Firefox, Opera, Safari 10.1+ */
  color: rgb(252, 166, 170);
  opacity: 1; /* Firefox */
}

select { 
  box-shadow: 0px 1px 2px rgba(16, 24, 40, 0.05);
  border-radius: 8px;
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 10px 14px;
  width: 220px;
}

select {
   border:0!important;
   background: #191a19c1;
   flex: 1;
   padding: 0.5em;
   color:#fff;
   cursor:pointer;
   font-size: 1em;
   font-family: 'Open Sans', sans-serif;
}


.input2 {
   position: relative;
   display: flex;
   width: 220px;
   height: 2.2em;
   /* line-height: 3; */
   background: #5c6664;
   /* overflow: hidden; */
   border-radius: 8px;
}
.input2::after {
   /* content: '\25BC'; */
   position: absolute;
   /* top: 0; */
   /* right: 0; */
   padding: 0 1em;
   padding-bottom: 2em;
   background: #2b2e2e;
   cursor:pointer;
   pointer-events:none;
   transition:.25s all ease;
}
.input2:hover{
  color: rgb(252, 166, 170);
}

@media screen and (max-width: 768px){
    .input1{
      width:120px;
    }
    .input2{
      width:120px;

    }
    .input-nav{
        /* -ms-flex-wrap: wrap; */
            flex-wrap: wrap;
            margin: auto;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            width: 80%;
    }
    #copy-btn{
        margin-top: 2rem;
    }
    #gen-btn{
      font-size: 20px;
      margin:auto;

    }
    .text-body{
      width: 90%;
    }
    .text-body #text-content{
     font-size: 0.7rem;
  
    }
    #text-content{
      padding-left: 1rem;
      padding-right: 1rem;
    }
    .nav-bar span{
      font-size:35px;
    }
    .nav-bar span p{
      font-size: 12px;
    }
    .nav-bar .image{
      height:40px;
      width:40px;
      margin-top: 1rem;
      margin-left: 0.1rem;
    }
    .side-text{
      height: 35%;
      width:60%;
      line-height: 1.5;
    }
    .side-text h1{
      font-size: 25px;
    }
    .side-text h4{
      font-size: 8px;
    }
    .home-body{
      box-shadow: 2px 3px 5px 5px rgba(16, 24, 40, 0.05);
      margin:auto;
      align-items: center;
      justify-content: center;
    }
    
}

</style>
