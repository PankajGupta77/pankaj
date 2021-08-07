//html code for keypad
<html>
 <head>
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.2.3/jquery.min.js"></script> 
 </head>
 <body>
  <table id="phone"> 
   <tbody>
    <tr> 
     <td colspan="3"> <input type="text" id="result"> </td> 
    </tr> 
    <tr> 
     <td> <button data-value="1" class="key">1 <span>. , !</span> </button> </td> 
     <td> <button data-value="2" class="key">2 <span>a b c</span> </button> </td> 
     <td> <button data-value="3" class="key">3 <span>d e f</span> </button> </td> 
    </tr> 
    <tr> 
     <td> <button data-value="4" class="key">4 <span>g h i</span> </button> </td> 
     <td> <button data-value="5" class="key">5 <span>j k l</span> </button> </td> 
     <td> <button data-value="6" class="key">6 <span>m n o</span> </button> </td> 
    </tr> 
    <tr> 
     <td><button data-value="7" class="key">7 <span>p q r s</span> </button> </td> 
     <td> <button data-value="8" class="key">8 <span>t u v</span> </button> </td> 
     <td> <button data-value="9" class="key">9 <span>w x y z</span> </button> </td> 
    </tr> 
    <tr> 
     <td><button data-value="*" class="key">*</button></td> 
     <td><button data-value="0" class="key">0</button></td> 
     <td><button data-value="#" class="key">#</button></td> 
    </tr> 
   </tbody>
  </table>
 </body>
</html>







// CSS code For keypad


#phone button {

  height: 50px;

  width: 75px;

}

#phone button span  {

  display: block;

  margin-top: 5px;

  font-size: 10px;

}

#result{

  width: 225px;

  height: 25px;

  margin-left:2px;

}






// javascript for keypad

var to = 1000, timeout, counter = 0, lastKey, keyPressTimeout, keyPressTO = 1000;

$("#phone button").bind("mousedown", function() {

  var $this = $(this),

      $result = $('#result'),

      val = $result.val(),

      button_pressed = $this.attr("data-value");

  keyPressTimeout = setTimeout(function() {

    // if the click is long add the value of the button to the textxbox

    val += button_pressed;

    $result.val(val);

    keyPressTimeout = null;

  }, keyPressTO);



}).bind("mouseup", function(event) {

  clearTimeout(keyPressTimeout);



  if (!keyPressTimeout) {

    return false;

  }

  var $this = $(this),

      $result = $('#result'),

      val = $result.val(),

      button_pressed = $this.attr("data-value");

  // if the user clicks on a new key reset all

  if (lastKey !== button_pressed) {

    reset();  

  }

  // if the user click fast on the same key, remove the last charchter to replace it with the new

  if (counter !== 0 && lastKey === button_pressed) {

    val = val.substring(0, val.length-1);

  }

  val += t9(button_pressed);

  $result.val(val);

  // restart the timeout

  clearTimeout(timeout);

  counter++;

  // save the last key pressed so we can compare it in the next click

  lastKey = button_pressed;

  // if the user not clicked on anything within the timeout delay (to variable) reset all.

  timeout = setTimeout(reset, to);

});

function t9(button_pressed) {

  return keys[button_pressed][counter % keys[button_pressed].length];

}

function reset() {

  counter = 0;

  lastKey = null;

}

var keys = {

  '1': ['.', ',', '!'],

  '2': ['a', 'b', 'c'], 

  '3': ['d', 'e', 'f'], 

  '4': ['g', 'h', 'i'], 

  '5': ['j', 'k', 'l'], 

  '6': ['m', 'n', 'o'], 

  '7': ['p', 'q', 'r', 's'], 

  '8': ['t', 'u', 'v'], 

  '9': ['w', 'x', 'y', 'z'], 

  '*': ['*'], 

  '0': ['0']

};
