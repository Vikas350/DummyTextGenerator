
<script>
  import { HtmlTag, prevent_default } from "svelte/internal";

  const genForm = document.getElementById('gen-form');
  const genBtn = document.getElementById('gen-btn');
  const copyBtn = document.getElementById('copy-btn');
  const genContent = document.getElementById('text-content');
  // const genValue = document.getElementById('gen_count');

  //initialize variables--> count,type
  let count = 0;
  let optionSelected = "type";
  let tempOption = "";
  let tempCount = 0;

  // on click generate text 
  function onClick(e){
    // console.log(count,optionSelected);

    // validate values
    validateValues();

    // api for dummy text generation
    let url = `https://baconipsum.com/api/?type=meat-and-filler&${optionSelected}=${count}&start-with-lorem=1`;
    fetchContent(url); // fetch this url 
  }

  // function for validating the count and option
  function validateValues(){
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
        <!-- icon666.com - MILLIONS vector ICONS FREE --><svg version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 512.001 512.001" style="enable-background:new 0 0 512.001 512.001;" xml:space="preserve"><g><g><path d="M0.849,448.713v62.936h287.043v-62.936H0.849z M272.98,496.737H15.761v-33.111H272.98V496.737z" fill="#000000" style="fill: rgb(254, 204, 135);"></path></g></g><g><g><rect x="56.6" y="472.8" width="15.906" height="14.912" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g><g><g><rect x="216.656" y="472.8" width="15.906" height="14.912" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g><g><g><rect x="136.129" y="472.8" width="15.906" height="14.912" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g><g><g><path d="M231.865,393.698l56.876-130.003L164.118,37.815c6.89-2.999,11.721-9.874,11.721-17.856 c0-10.731-8.731-19.462-19.463-19.462h-24.012c-10.731,0-19.462,8.731-19.462,19.462c0,7.982,4.831,14.857,11.721,17.856 L0,263.695l56.876,130.003v31.38H32.74v14.912h223.685v-14.912h-24.56V393.698z M132.365,15.409h24.012 c2.508,0,4.55,2.041,4.55,4.549s-2.041,4.549-4.55,4.549h-16.631h-7.381c-2.508,0-4.549-2.041-4.549-4.549 S129.856,15.409,132.365,15.409z M216.954,425.078H71.788v-34.5L16.61,264.458L136.132,47.825v160.528h14.912V44.988 l121.087,219.469l-55.178,126.12V425.078z" fill="#000000" style="fill: rgb(254, 204, 135);"></path></g></g><g><g><rect x="136.129" y="224.261" width="14.912" height="15.906" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g><g><g><rect x="136.129" y="256.074" width="14.912" height="15.906" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g><g><g><path d="M151.045,297.612v-9.727h-14.912v10.251c-8.886,3.343-15.225,11.927-15.225,21.967c0,12.939,10.526,23.465,23.464,23.465 s23.464-10.526,23.464-23.464C167.835,309.484,160.742,300.495,151.045,297.612z M144.371,328.655 c-4.715,0-8.552-3.836-8.552-8.552s3.836-8.552,8.552-8.552s8.552,3.836,8.552,8.552S149.086,328.655,144.371,328.655z" fill="#000000" style="fill: rgb(254, 204, 135);"></path></g></g><g><g><path d="M484.535,376.677h-32.017c-6.921,0-12.553-5.632-12.553-12.553c0-6.92,5.632-12.552,12.553-12.552h12.006 c26.178,0,47.475-21.298,47.475-47.476V47.973c0-26.168-20.853-46.666-47.441-46.666L319.652,0.641l0.576-0.289L299.826,0.55 L288.88,0.499c-12.208-0.111-23.814,4.366-32.788,12.724c-9.412,8.765-14.778,20.662-15.11,33.501 c-0.241,9.317-6.938,17.115-15.247,17.753c-4.685,0.36-9.15-1.187-12.57-4.354c-3.424-3.171-5.31-7.487-5.31-12.15V31.417h32.563 V16.505h-47.475v31.468c0,8.736,3.677,17.152,10.089,23.09c5.943,5.505,13.528,8.424,21.567,8.368v0.008l87.486,0.172 l0.029-14.912l-61.537-0.121c3.207-5.061,5.149-11.068,5.315-17.467c0.228-8.802,3.909-16.96,10.366-22.974 c5.328-4.962,12-7.93,19.143-8.587l0.006,0.178l4.128,0.019l0.58-0.291c17.047,0.858,30.89,16.182,30.89,34.239v266.426 c0,11.325-9.222,20.539-20.557,20.539c-15.145,0-27.466,12.322-27.466,27.465c0,15.145,12.322,27.466,27.466,27.466h8 l33.122,0.056c6.406,0.562,11.451,5.948,11.451,12.497c0,6.922-5.632,12.553-12.553,12.553h-28.013v14.912h172.083 c15.144,0,27.466-12.322,27.466-27.466C512.001,388.997,499.679,376.677,484.535,376.677z M484.535,416.697H364.891 c1.943-3.765,3.04-8.034,3.04-12.553c0-4.484-1.087-8.716-3-12.458l52.534,0.088l0.025-14.912l-75.338-0.127 c-0.559-0.034-1.12-0.057-1.687-0.057h-40.019c-6.922,0-12.553-5.632-12.553-12.553c0-6.922,5.632-12.553,12.553-12.553 c0.305,0,0.607-0.016,0.912-0.023v0.005l43.469,0.454l0.156-14.911l-15.848-0.166c4.259-5.85,6.78-13.039,6.78-20.811V49.694 c0-12.451-4.569-24.385-12.866-33.604c-0.158-0.176-0.317-0.35-0.477-0.523l141.953,0.652c18.26,0,32.563,13.948,32.563,31.753 v256.124c0,17.955-14.607,32.564-32.563,32.564h-12.006c-15.144,0-27.465,12.322-27.465,27.466 c0,15.145,12.322,27.466,27.465,27.466h32.016c6.921,0,12.553,5.632,12.553,12.553 C497.088,411.067,491.456,416.697,484.535,416.697z" fill="#000000" style="fill: rgb(254, 204, 135);"></path></g></g><g><g><rect x="360.808" y="41.336" width="63.626" height="14.912" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g><g><g><rect x="360.808" y="73.15" width="31.813" height="14.912" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g><g><g><rect x="408.528" y="73.15" width="63.626" height="14.912" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g><g><g><rect x="360.808" y="104.963" width="55.673" height="14.912" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g><g><g><rect x="432.387" y="104.963" width="39.766" height="14.912" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g><g><g><rect x="360.808" y="136.776" width="39.766" height="14.912" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g><g><g><rect x="360.808" y="168.589" width="15.906" height="14.912" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g><g><g><rect x="360.808" y="201.396" width="63.626" height="14.912" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g><g><g><rect x="360.808" y="233.209" width="23.86" height="14.912" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g><g><g><rect x="400.574" y="233.209" width="71.579" height="14.912" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g><g><g><rect x="360.808" y="265.021" width="55.673" height="14.912" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g><g><g><rect x="432.387" y="265.021" width="23.86" height="14.912" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g><g><g><rect x="360.808" y="296.834" width="15.906" height="14.912" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g><g><g><rect x="352.855" y="337.595" width="31.813" height="14.912" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g><g><g><rect x="392.621" y="337.595" width="15.906" height="14.912" fill="#000000" style="fill: rgb(254, 204, 135);"></rect></g></g></svg>
      </div>
      <span>
        <!-- <img src="src/Images/logo.png" alt=""> -->
        
        <h1 class="logo-text"><span class="gradient-text">Lorem Ipsum</span></h1>
        <p>A Dummy Text Generator</p>
      </span>
    </nav>
    <div class="gradient">
      <section class="section1" style="border: 20px;">
        <div class="home-body"></div>
        <div class="side-text">
          <h1>Lorem ipsum</h1><h4>is placeholder text commonly used in the graphic, print, and publishing industries for previewing layouts and visual mockups.</h4>
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
  width: 42px;
  height: 42px;
  margin: 1rem;
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
  background-image: url(src/Images/20827476_Tiny\ characters\ sitting\ on\ laptop\ with\ lorem\ ipsum\ title.jpg);
  height: 80vh;
  background-color: white;
  background-size:contain;
  background-repeat: no-repeat;
  border: 20px;
  margin: auto;
  border-radius: 20px;
  box-shadow: 2px 5px 5px rgba(16, 24, 40, 0.05);

}

.side-text{
  /* border: 4px solid red; */
  position:absolute;
  height: 246px;
  width: 579px;
  top: 200px;
  right: 150px;

}

.side-text h1{
  font-size: 100px;
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
  position: absolute;
  top: 400px;
  right: 500px;
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
  justify-content: space-around;
  align-items: center;
  margin: 1em auto;
  width: 60%;
  /* margin-bottom: 50px; */
  /* padding: 2.5em; */

/* issues are here */
}

.input-div form{
  display: flex;
  flex-direction: row;
  
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
  justify-content: end;
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
   line-height: 3;
   background: #5c6664;
   overflow: hidden;
   border-radius: .25em;
}
.input2::after {
   content: '\25BC';
   position: absolute;
   top: 0;
   right: 0;
   padding: 0 1em;
   padding-bottom: 2em;
   background: #2b2e2e;
   cursor:pointer;
   pointer-events:none;
   transition:.25s all ease;
}
.input2:hover::after {
  color: rgb(252, 166, 170);
}

</style>
