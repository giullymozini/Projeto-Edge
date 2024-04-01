# Projeto cp1 de EDGE 

Integrantes: 

Artur Alves Tenca RM: 555171
Igor Brunelli RM: 555035
Ian Monteiro RM: 558652
Giuliana RM:557597

Turma: 1ESPH 
Professor Cabrini 


Lista de material: 

U1
1
 Arduino Uno R3
D1
1
Red LED


R2
1
10 kΩ Resistor
R3, R4, R5
3
220 kΩ Resistor
D2
1
Yellow LED
D3
1
Green LED
R1
1
 Photoresistor
PIEZO1
1
 Piezo






Descrição do case:


  O caso é sobre uma vinheria tradicional, que antes da pandemia estava operando como loja física, no período pandêmico, a mudança para um portal de e-commerce foi necessária, porém a única exigência, era   que a loja virtual conseguisse criar uma experiência similar à do atendimento presencial. 

  Outras exigências são sobre, a luminosidade que influencia o gosto dos vinhos, principalmente os brancos e os espumantes, então a pedido da Vinheria, a luz deveria ser muito suave; a temperatura, o calor excessivo termina com a vida do vinho rapidamente, a melhor temperatura constante seria de 13 graus; e a umidade, a falta dela pode levar ao ressecamento do vedame ou estragar o rótulo, o ideal seria 70% (com variações entre 60% a 80%).

  
Descrição do projeto:


  Nós da DataSphere sugerimos que o projeto seja um sistema de monitoramento a ser instalado no ambiente em que os vinhos são armazenados, sugerimos que o projeto seja feito em partes, a primeira seria elaborar um sistema usando Arduino que terá como objetivo capturar as informações da luminosidade do ambiente.

  
Descrição do objetivo: 

   O sistema Arduino terá um led verde, que significará que a luminosidade do ambiente está OK, um led amarelo para indicar um alerta e um led vermelho para indicar problema e junto instalado uma buzina que se acionará a cada 3 segundos e ficará ativa até o nível normalizar. 
   No software foi utilizado o seguinte código e o nosso protótipo foi usado no Tinkercad: 




(projeto no Tinkercad)






(Circuito eletrônico)

 Código Comentado: 

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



