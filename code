//#define asciiToAh 11 //13
//#define ahToAscii 11
#define greenLed 10
#define blueLed 11
#define redLed 5
#define orangeLed 6
#define yellowLed 9
#define jack A2
//character arrays to store AH code applicable to each character
char ah_a[] = "*";
char ah_b[] = "!**";
char ah_c[] = "!!@";
char ah_d[] = "*!";
char ah_e[] = "!";
char ah_f[] = "!*!";
char ah_g[] = "**";
char ah_h[] = "!!*";
char ah_i[] = "!!";
char ah_j[] = "*!!";
char ah_k[] = "*@";
char ah_l[] = "!*@";
char ah_m[] = "!*";
char ah_n[] = "!@";
char ah_o[] = "!@*";
char ah_p[] = "!@!";
char ah_q[] = "*!@";
char ah_r[] = "@*";
char ah_s[] = "@!";
char ah_t[] = "@";
char ah_u[] = "@@";
char ah_v[] = "**!";
char ah_w[] = "***";
char ah_x[] = "*@!";
char ah_y[] = "!@@";
char ah_z[] = "**@";
char ah_0[] = "@!!!";
char ah_1[] = "@!!*";
char ah_2[] = "@!!@";
char ah_3[] = "@!*!";
char ah_4[] = "@!**";
char ah_5[] = "@!*@";
char ah_6[] = "@!@!";
char ah_7[] = "@!@*";
char ah_8[] = "@!@@";
char ah_9[] = "@*!!";
char ah_fullStop[] = "@!*";
char ah_comma[] = "@!!";
char ah_apostrope[] = "@*!";
char ah_questionMark[] = "@**";
char ah_exclamationMark[] = "@*@";
char ah_plus[] = "@@!";
char ah_minus[] = "@@*";
char ah_multiply[] = "@@@";
char ah_divide[] = "@!@";
char ah_space[] = " ";


void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  String input;
  String translated;
  String tempInput;
  bool changeLEDFormat;

  while (1) { //to allow the user for input more than once
    input = gettingInput(); //get user input
    translated = ahOrAscii(input); //translate the input
    changeLEDFormat = translated.length() == 13 && translated.charAt(0) == 'l' && isDigit(translated.charAt(1)) && isDigit(translated.charAt(2)) && isDigit(translated.charAt(3))
               && isDigit(translated.charAt(4)) && isDigit(translated.charAt(5)) && isDigit(translated.charAt(6)) && isDigit(translated.charAt(7)) && isDigit(translated.charAt(8))
               && isDigit(translated.charAt(9)) && isDigit(translated.charAt(10)) && isDigit(translated.charAt(11)) && isDigit(translated.charAt(12)); //to check if entered format matches the format
               //required to set the brigtness of LEDs
       
    if (input != "@!/@@!" && input != "@!/@@*" && input != "!@!/!@*/@" && changeLEDFormat == 0) {  //check if input is not a commnad, if not, print the translation out
      Serial.println(translated);
      blueOrGreen(input);
      tempInput = input;  //save input to another variable that won't be changed by input if the input is a command
      input = "";
      translated = "";
    } else if (input.charAt(0) == '!' || input.charAt(0) == '@') { //if it is one of the commands check which
      if (translated == "s+") { //transmit ah code by sound
        if (tempInput.charAt(0) == '!' || tempInput.charAt(0) == '@' || tempInput.charAt(0) == '*') { //if the input was ah code we pass that to the function that produces sound
          sendAnalog(jack, tempInput);
          input = "";
          translated = "";
        } else {
          sendAnalog(jack, ahOrAscii(tempInput)); //if the input was ascii we convert it to AH code and then pass that to the function that produces sound
          input = "";
          translated = "";
        }

      }
      else if (translated == "s-") { //silence sound
        noTone(jack);
        input = "";
      }
      else if (translated == "POT") { //print the value of potentiometer
        Serial.println(analogRead(A0));
        input = "";
        translated = "";
      }
      else if (translated.length() == 13 && translated.charAt(0) == 'l' && changeLEDFormat == 1) {
        //dim the leds 
        ledChange(translated);
        translated = "";
      }
    }


  }


}


char * char2AH(char c) {
  //function to convert ascii characters to AH code characters

  switch (c)
  {
    case 'a':
      return ah_a;

    case 'b':
      return ah_b;

    case 'c':
      return ah_c;

    case 'd':
      return ah_d;

    case 'e':
      return ah_e;

    case 'f':
      return ah_f;

    case 'g':
      return ah_g;

    case 'h':
      return ah_h;

    case 'i':
      return ah_i;

    case 'j':
      return ah_j;

    case 'k':
      return ah_k;

    case 'l':
      return ah_l;

    case 'm':
      return ah_m;

    case 'n':
      return ah_n;

    case 'o':
      return ah_o;

    case 'p':
      return ah_p;

    case 'q':
      return ah_q;

    case 'r':
      return ah_r;

    case 's':
      return ah_s;

    case 't':
      return ah_t;

    case 'u':
      return ah_u;

    case 'v':
      return ah_v;

    case 'w':
      return ah_w;

    case 'x':
      return ah_x;

    case 'y':
      return ah_y;

    case 'z':
      return ah_z;


    case '0':
      return ah_0;


    case '1':
      return ah_1;


    case '2':
      return ah_2;

    case '3':
      return ah_3;

    case '4':
      return ah_4;

    case '5':
      return ah_5;

    case '6':
      return ah_6;

    case '7':
      return ah_7;

    case '8':
      return ah_8;

    case '9':
      return ah_9;

    case '.':
      return ah_fullStop;

    case ',':
      return ah_comma;


    case '\'':
      return ah_apostrope;


    case '?':
      return ah_questionMark;


    case '!':
      return ah_exclamationMark;


    case '+':
      return ah_plus;

    case '-':
      return ah_minus;


    case '*':
      return ah_multiply;


    case '/':
      return ah_divide;

    case ' ':
      return ah_space;
      //    default:
      //      return  morse_unknown;
  }
}




char ah2char(String m) {
  //function to translate AH code into ascii characters

  if (m.equals("*")) {
    return 'a';
  }
  else if (m.equals("!**")) {
    return 'b';
  }

  else if (m.equals("!!@")) {
    return 'c';
  }
  else if (m.equals("*!")) {
    return 'd';
  }
  else if (m.equals("!")) {
    return 'e';
  }
  else if (m.equals("!*!")) {
    return 'f';
  }
  else if (m.equals("**")) {
    return 'g';
  }
  else if (m.equals("!!*")) {
    return 'h';
  }
  else if (m.equals("!!")) {
    return 'i';
  }
  else if (m.equals("*!!")) {
    return 'j';
  }
  else if (m.equals("*@")) {
    return 'k';
  }
  else if (m.equals("!*@")) {
    return 'l';
  }
  else if (m.equals("!*")) {
    return 'm';
  }
  else if (m.equals("!@")) {
    return 'n';
  }
  else if (m.equals("!@*")) {
    return 'o';
  }
  else if (m.equals("!@!")) {
    return 'p';
  }
  else if (m.equals("*!@")) {
    return 'q';
  }
  else if (m.equals("@*")) {
    return 'r';
  }
  else if (m.equals("@!")) {
    return 's';
  }
  else if (m.equals("@")) {
    return 't';
  }
  else if (m.equals("@@")) {
    return 'u';
  }
  else if (m.equals("**!")) {
    return 'v';
  }
  else if (m.equals("***")) {
    return 'w';
  }
  else if (m.equals("*@!")) {
    return 'x';
  }
  else if (m.equals("!@@")) {
    return 'y';
  }
  else if (m.equals("**@")) {
    return 'z';
  }
  else if (m.equals(" ")) {
    return ' ';
  }
  else if (m.equals("@!!*")) {
    return '1';
  }
  else if (m.equals("@!!@")) {
    return '2';
  }
  else if (m.equals("@!*!")) {
    return '3';
  }
  else if (m.equals("@!**")) {
    return '4';
  }
  else if (m.equals("@!*@")) {
    return '5';
  }
  else if (m.equals("@!@!")) {
    return '6';
  }
  else if (m.equals("@!@*")) {
    return '7';
  }
  else if (m.equals("@!@@")) {
    return '8';
  }
  else if (m.equals("@*!!")) {
    return '9';
  }
  else if (m.equals("@!!!")) {
    return '0';
  }
  else if (m.equals("@!*")) {
    return '.';
  }
  else if (m.equals("@!!")) {
    return ',';
  }
  else if (m.equals("@*!")) {
    return '\'';
  }
  else if (m.equals("@**")) {
    return '?';
  }
  else if (m.equals("@*@")) {
    return '!';
  }
  else if (m.equals("@@!")) {
    return '+';
  }
  else if (m.equals("@@*")) {
    return '-';
  }
  else if (m.equals("@@@")) {
    return '*';
  }
  else if (m.equals("@!@")) {
    return '/';
  }
  else if (m.equals(" ")) {
    return ' ';
  }
  else {
    return 'E';
  }
}


String ah2ascii(String input) {
  //translates AH code string into ascii string
  int stringLength = input.length(); //used for looping
  String ah = ""; //to store AH code symbol for translation to ascii
  char letter; //to store an ascii character
  String fullTranslation = ""; //to store the full translation


  for (int i = 0; i < stringLength + 1; i++) {

    if (input.charAt(i) == ' ') {
      fullTranslation = fullTranslation + " "; //add an empty space since that's the input
    }
    else if (input.charAt(i) == '/') {
      //if backslash is reached we translate the AH symbols that were added  to ah variable string
      letter = ah2char(ah); //translate the current AH symbols into an ascii char
      ah = ""; //clear the variable
      fullTranslation = fullTranslation + String(letter); //add the translation to make a full word or sentence
    }
    else if (i == stringLength) {
      //if end was reached translate what is stored into an ah variable string and add it to the rest of translation
      letter = ah2char(ah);
      fullTranslation = fullTranslation + String(letter);
    }
    else if (input.charAt(i + 1) == ' ') {
      //if the next character is an empty space we add the last symbol to ah variable and translate it to ascii char
      ah = ah + String(input.charAt(i));
      letter = ah2char(ah); //translate the current AH symbols into an ascii char
      fullTranslation = fullTranslation + String(letter); //add the translation to make a full word or sentence
      ah = "";
    }
    else if (input.charAt(i) != '/') {
      //collecting the AH code symnols to make a full symbol
      ah = ah + String(input.charAt(i));
    }


  }
  return fullTranslation;
}


String ascii2AH(String input) {
  //takes ascii input and converts it into AH code

  int stringLength = input.length();//used for looping
  char c; //to store one character at the time to pass it to a char2AH function that will translate it to AH code
  String ah; //to store AH characters
  String fullTranslation = ""; //to concatinate all the AH characters together
  String fullTNS;
  String symbol = "";//to store dash between AH code characters if it's needed

  for (int i = 0; i < stringLength; i++) { //looping through the string one character at a time
    symbol = "";
    c = tolower(input.charAt(i));
    ah = char2AH(c);

    if (i != stringLength - 1 && (c != ' ') && (input.charAt(i + 1) != ' ')) {
      symbol = "/";
    }
    fullTranslation = fullTranslation + ah + symbol;

  }

  return fullTranslation;
}

String ahOrAscii(String input) {
  //checks if the input is ascii or HA! code and accordingly calls functions to tanslate the input
  //calls a function to flash the LED passing the appropriate LED port to a function depending on if the input is ascii or AH! code
  int i = 0;
  String translate;
  while (input.charAt(i) == ' ') { //counting how many first characters if any are spaces so we know what not to take into consideration
    i++;
  }
  if (input.charAt(i) == '@' || input.charAt(i) == '!' || input.charAt(i) == '*') { //we use number i to set the first symbol. checks if the first symbol is ah code
    translate = ah2ascii(input);
    //return translate;
    //delay(20);
    //sendDigital(ahToAscii, input); //passes the unmodified ah code and blue LED port
  } else {
    translate = ascii2AH(input);
    //return translate;
    //delay(20);
    //sendDigital(asciiToAh, translate); //passes the translation and green LED port
  }
  return translate;
}


void blueOrGreen(String input) {
  //calls a function to flash the LED passing the appropriate LED port to a function depending on if the input is ascii or AH! code
  //takes the value of input
  int i = 0;
  String translate;
  while (input.charAt(i) == ' ') { //counting how many first characters if any are spaces so we know what not to take into consideration
    i++;
  }
  if (input.charAt(i) == '@' || input.charAt(i) == '!' || input.charAt(i) == '*') { //we use number i to set the first symbol. checks if the first symbol is ah code
    translate = ah2ascii(input);
    sendDigital(blueLed, input); //passes the unmodified ah code and blue LED port
  } else {
    translate = ascii2AH(input);
    sendDigital(greenLed, translate); //passes the translation and green LED port
  }
}

String gettingInput() {
  //function that gets input from serial port
  char inputChar = 0; //to store characters of our input one by onw
  String input = ""; //to add those characters to make a complete string


  while (Serial.available() <= 0) {} //if there's no input do nothing

  while (1) {
    if (Serial.available() > 0) {
      inputChar = Serial.read();
      if (inputChar != '\n') {
        input = input + inputChar;
      } else if (inputChar == '\n') {
        return input;
      }
    }
  }
}


void sendDigital(int p, String message) {
  //flashes the LED with appropriate delays
  //takes in the LED pin (p) and the message to be desplayed as LED flashes
  int i;
  int time;
  time = millis();
  char c; //to store one symbol at a time
  for (i = 0; i < message.length(); i++) {
    c = message.charAt(i);

    //checks the current character to determine the period of time the LED needs to stay on for
    switch (c)
    {
      case '!':
        digitalWrite(p, HIGH);
        delay((0.3715 * analogRead(A0)) + 20); //stay on for this time
        digitalWrite(p, LOW);
        //checking what the next character is to determine the period of time the LED needs to stay off for
        if (message.charAt(i + 1) == ' ') {
          delay(((0.3715 * analogRead(A0)) + 20) * 8);
        }
        else if (message.charAt(i + 1) == '!' || message.charAt(i + 1) == '@' || message.charAt(i + 1) == '*') {
          delay((0.3715 * analogRead(A0)) + 20);
        }
        else if (message.charAt(i + 1) == '/') {
          delay(((0.3715 * analogRead(A0)) + 20) * 3);
        }
        break;
      case '*':
        digitalWrite(p, HIGH);
        delay(((0.3715 * analogRead(A0)) + 20) * 2);
        digitalWrite(p, LOW);
        if (message.charAt(i + 1) == ' ') {
          delay(((0.3715 * analogRead(A0)) + 20) * 8);
        }
        else if (message.charAt(i + 1) == '!' || message.charAt(i + 1) == '@' || message.charAt(i + 1) == '*') {
          delay((0.3715 * analogRead(A0)) + 20);
        }
        else if (message.charAt(i + 1) == '/') {
          delay(((0.3715 * analogRead(A0)) + 20) * 3);
        }
        break;

      case '@':
        digitalWrite(p, HIGH);
        delay(((0.3715 * analogRead(A0)) + 20) * 4);
        digitalWrite(p, LOW);
        if (message.charAt(i + 1) == ' ') {
          delay(((0.3715 * analogRead(A0)) + 20) * 8);
        }
        else if (message.charAt(i + 1) == '!' || message.charAt(i + 1) == '@' || message.charAt(i + 1) == '*') {
          delay((0.3715 * analogRead(A0)) + 20);
        }
        else if (message.charAt(i + 1) == '/') {
          delay(((0.3715 * analogRead(A0)) + 20) * 3);
        }
        break;

    }

  }

}

void sendAnalog(int p, String message) {
  //creates sound signal in AH code with appropriate delays
  //takes in the value of earphone jack pin (p) and a message to be displayed as a sound signal
  int i;
  int freq = 440;
  char c; //to store one symbol at a time
  for (i = 0; i < message.length(); i++) {
    c = message.charAt(i);
    //checks the current character to determine the period of time the sound needs to stay on for
    switch (c)
    {
      case '!':
        tone(p, freq);
        delay((0.3715 * analogRead(A0)) + 20); //stay on for this time
        noTone(p);
        //checking what the next character is to determine the period of time the sound needs to stay off for
        if (message.charAt(i + 1) == ' ') {
          delay(((0.3715 * analogRead(A0)) + 20) * 8);
        }
        else if (message.charAt(i + 1) == '!' || message.charAt(i + 1) == '@' || message.charAt(i + 1) == '*') {
          delay((0.3715 * analogRead(A0)) + 20);
        }
        else if (message.charAt(i + 1) == '/') {
          delay(((0.3715 * analogRead(A0)) + 20) * 3);
        }
        break;
      case '*':
        tone(p, freq);
        delay(((0.3715 * analogRead(A0)) + 20) * 2);
        noTone(p);
        if (message.charAt(i + 1) == ' ') {
          delay(((0.3715 * analogRead(A0)) + 20) * 8);
        }
        else if (message.charAt(i + 1) == '!' || message.charAt(i + 1) == '@' || message.charAt(i + 1) == '*') {
          delay((0.3715 * analogRead(A0)) + 20);
        }
        else if (message.charAt(i + 1) == '/') {
          delay(((0.3715 * analogRead(A0)) + 20) * 3);
        }
        break;

      case '@':
        tone(p, freq);
        delay(((0.3715 * analogRead(A0)) + 20) * 4);
        noTone(p);
        if (message.charAt(i + 1) == ' ') {
          delay(((0.3715 * analogRead(A0)) + 20) * 8);
        }
        else if (message.charAt(i + 1) == '!' || message.charAt(i + 1) == '@' || message.charAt(i + 1) == '*') {
          delay((0.3715 * analogRead(A0)) + 20);
        }
        else if (message.charAt(i + 1) == '/') {
          delay(((0.3715 * analogRead(A0)) + 20) * 3);
        }
        break;

    }

  }
}

void ledChange(String values) {
  String red = String(values.charAt(1)) + String(values.charAt(2)) + String(values.charAt(3));
  String orange = String(values.charAt(4)) + String(values.charAt(5)) + String(values.charAt(6));
  String yellow = String(values.charAt(7)) + String(values.charAt(8)) + String(values.charAt(9));
  String green = String(values.charAt(10)) + String(values.charAt(11)) + String(values.charAt(12));

  int brightRed = red.toInt();
  int brightOrange = orange.toInt();
  int brightYellow = yellow.toInt();
  int brightGreen = green.toInt();

  pinMode(redLed, OUTPUT);
  pinMode(orangeLed, OUTPUT);
  pinMode(yellowLed, OUTPUT);
  pinMode(greenLed, OUTPUT);

  if (brightRed <= 255 && orangeLed <= 255 && brightYellow <= 255 && brightGreen <= 255) {
    analogWrite(redLed, brightRed);
    analogWrite(orangeLed, brightOrange);
    analogWrite(greenLed, greenLed);
    analogWrite(yellowLed, brightYellow);

  }

}

void loop() {
  // put your main code here, to run repeatedly:
}
