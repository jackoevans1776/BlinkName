# BlinkName
int led1 = D0; // Instead of writing D0 over and over again, we'll write led1
// You'll need to wire an LED to this one to see it blink.

int led2 = D6; // Instead of writing D7 over and over again, we'll write led2
// This one is the little blue LED on your board. On the Photon it is next to D7, and on the Core it is next to the USB jack.

// Having declared these variables, let's move on to the setup function.
// The setup function is a standard part of any microcontroller program.
// It runs only once when the device boots up or is reset.

void setup() {

  // We are going to tell our device that D0 and D7 (which we named led1 and led2 respectively) are going to be output
  // (That means that we will be sending voltage to them, rather than monitoring voltage that comes from them)

  // It's important you do this here, inside the setup() function rather than outside it or in the loop function.

  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
  
}

// Next we have the loop function, the other essential part of a microcontroller program.
// This routine gets repeated over and over, as quickly as possible and as many times as possible, after the setup function is called.
// Note: Code that blocks for too long (like more than 5 seconds), can make weird things happen (like dropping the network connection).  The built-in delay function shown below safely interleaves required background activity, so arbitrarily long delays can safely be done if you need them.

void loop() {
  // To blink the LED, first we'll turn it on...
  
  char* morseCode[26] = {".-", "-...", "-.-.", "-..",".", "..-.", "--.", "....", "..", ".---", 
    "-.-", ".-..", "--", "-.", "---", ".--.", "--.-", ".-.", "...", "-", 
    "..-", "...-", ".--", "-..-", "-.--", "--.."};
                   
    char* alphabet[26] = {"A", "B", "C", "D", "E", "F", "G", "H", "I", "J", 
    "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T",
    "U", "V", "W", "X", "Y", "Z"};
    
    char* name[5] = {"J", "A", "C", "K", "O"};
    
  for (int i = 0; i < 5; i++)
    {

        //For letter in alphabet
        for (int j = 0; j < 26; j++)
        {
            if (name[i] == alphabet[j])
            {
                //For char in morseCode letter LENGTH equivelant
                for (int k = 0; k < strlen(morseCode[j]); k++)
                {
                    if (morseCode[j][k] == '.')
                    {
                        digitalWrite(led1, HIGH);
                        delay(200);
                        digitalWrite(led2, LOW);
                        delay(200);
                    }
                    else if (morseCode[j][k] == '-')
                    {
                        digitalWrite(led1, HIGH);
                        delay(400);
                        digitalWrite(led2, LOW);
                        delay(200);
                    }
                }
                delay(1000);
            }
        }
    }
