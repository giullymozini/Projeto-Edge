# Projeto cp1 de EDGE 

Descrição do case:
  O case é sobre uma vinheria tradicional, que antes da pandemia estava operando como loja física, no periodo pandemico, a mudança para um portal de e-commerce foi necessaria, porém a unica exigência, era   que a loja virtual conseguisse criar uma expriencia similar á do atendimento presencial. 
  Outras exigêcias são sobre, a luminosidade que influência o gosto dos vinhos, principalmente os brancos e os espumantes, então a pedido da Vinheria, a luz deveria ser muito suave; a temperatura, o calor excessivo termina com a vida do vinho rapidamente, a melhor temperatura constante seria de 13 graus; e a umidade, a falta dela pode levar ao ressecamento do vedame ou estragar o rotulo, o ideal seria 70% (com variações entre 60% a 80%).

  
Descrição do projeto:
  Nos da DataSphere sugerimos que o projeto seja um sistema de monitoramento a ser instalado no ambiente em que os vinhos são armazenados, sugerimos que o projeto seja feito em partes, a primeira seria elaborar um sistema usando Arduino que terá como objetivo capturar as informações da luminosidade do ambiente.

  
Descrição do objetivo: 
   O sistema Arduino tera um led verde, que significará que a luminosidade do ambiente esta OK, um led amarelo para indicar um alerta e um led vermelho para indicar problema e junto instalado uma buzina que se acionará a cada 3 segundos e ficará ativa ate o nivel normalizar. 
   No software foi utilizado o seguinte codigo e o nosso prototipo foi usado no Tinkercad: 


 Codigo Comentado: 

 int LEDV = 8;   // Define o pino digital 8 para o LED vermelho
int LEDA = 12;  // Define o pino digital 12 para o LED amarelo
int LEDG = 13;  // Define o pino digital 13 para o LED verde
int BUZZER = 7; // Define o pino digital 7 para a buzina


void setup() {
  Serial.begin(9600);      // Inicia a comunicação serial com uma taxa de transmissão de 9600 bits por segundo
  pinMode(LEDV, OUTPUT);   // Define o pino LEDV como saída
  pinMode(LEDA, OUTPUT);   // Define o pino LEDA como saída
  pinMode(LEDG, OUTPUT);   // Define o pino LEDG como saída
  pinMode(BUZZER, OUTPUT); // Define o pino BUZZER como saída
}


void loop() {
   int LDR = analogRead(A0); // Lê o valor do sensor LDR conectado ao pino analógico A0
   int i = map(LDR, 0, 1023, 0, 100);//mapeia o LDR e muda seus valores para irem de 0 a 100  
     Serial.println(i); 
  if(i < 80){              // Se o LDR estiver menor que 890
    digitalWrite(LEDG, HIGH); // Liga o LED verde
    digitalWrite(LEDA, LOW);  // Desliga o LED amarelo
    digitalWrite(LEDV, LOW);  // Desliga o LED vermelho
  }
  else if (92 > i) {       // Se o LDR estiver menor que 957
    digitalWrite(LEDA, HIGH); // Liga o LED amarelo
    digitalWrite(LEDG, LOW);  // Desliga o LED verde
    digitalWrite(LEDV, LOW);  // Desliga o LED vermelho
  }
  else {                       // Se o LDR estiver maior que 957
    digitalWrite(LEDA, LOW);   // Desliga o LED amarelo
    digitalWrite(LEDV, HIGH);  // Liga o LED vermelho
    digitalWrite(LEDG, LOW);   // Desliga o LED verde
    tone(BUZZER, 2000, 2000);  // Emite um som com frequência de 1000Hz por 1 segundo
    delay(1000);               // Espera por 1 segundo
  }
  delay(500); // Aguarda 500 milissegundos antes de ler o sensor novamente
}

