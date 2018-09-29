# AlarmaAlerta#include <LowPower.h>; //Libreria lowpoer para utilizar el Sleep

int Led = 8;
int Reed_switch = 2;
int Buzzer = 9;
int Valor = 0;

void setup() {
  pinMode(Led, OUTPUT);                 // el led lo mandara como salidas
  pinMode(Reed_switch, INPUT);          // el reed sweetch permanecera como entrada
  pinMode(Buzzer, OUTPUT);              // buzzer lo mandara como salidas

}
void loop() { 
  
  //Lee sl ReedSwitch si se encuentra en alto logico o bajo logico
  Valor = digitalRead(Reed_switch);

  //si se aleja el iman, el led se enciende junto con
  //el sonido(buzzer) de la alarma

  if (Valor == LOW) {
    digitalWrite(Led, HIGH);
    digitalWrite(Buzzer, HIGH);
    delay(200);
    // despues terminara su tiempo y se apagara los mismos 2000 y asi el ciclo
    digitalWrite(Led, LOW);
    digitalWrite(Buzzer, LOW);
    delay(200);
    
    LowPower.powerDown(SLEEP_4S, ADC_OFF, BOD_OFF);           // poner a dormir 4 segundo es lo recomendado segun las fuentes, 
                                                              //para que vuelva a ser lo mismo nuevamente cuando despierta 
  } else {//si el iman no se aleja permanecera apagado
    digitalWrite(Led, LOW);
    digitalWrite(Buzzer, LOW);
  }
}
