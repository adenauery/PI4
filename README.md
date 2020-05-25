### Apresentação
Este é o repositório de trabalho da Disciplina de Projeto Integrador IV realizada no primeiro semestre de 2020.

### Equipe


|   |   |   |
|---|--:|:--|
| **Nome** |  **Primeira Avaliação**|**Segunda Avaliação** |
|Guilherme Carvalho |  [Repositório](https://github.com/carvalhoGuilherme/PI5)  | |
|   |   |   |


### Encontro em 18/02/2020

* Discussão dos objetivos
* Explorando as funções web do GitHub 
* Python & Arduino

**Metas até o próximo encontro:**
* Criar conta no GitHub - [existem outras opções](https://pt.wikiversity.org/wiki/Github_x_Gitlab_x_Bitbucket)
* Exercitar a sintaxe do Markdown (https://docs.pipz.com/central-de-ajuda/learning-center/guia-basico-de-markdown)
* Exercitar pequenos códigos em Python

### Encontro em 25/02/2020 - Recesso de Carnaval

### Encontro em 03/03/2020
* Atualização dos Sistemas Linux
* Instalação do Git para operação console
* Testes iniciais com o Git, explorando a plataforma GitHub

### Encontro em 10/03/2020
* Revisando as operações com o Git
* Programando com Python - Etapa 1

### Encontro em 17/03/2020
* Operações com o Git
* Programando com Python - Etapa 2

### Quinto Encontro - 24/03/2020
* Programando com Python - Etapa 3 
  * Explorando laços: While

### Encontro em 31/03/2020
* Avaliando a comunicação Arduino --> Desktop - Etapa 1
  * Arduino: fazer um programa que fique em um laço infinito lendo uma porta analógica e escrevendo na saída serial. Empregar um potenciômetro para variar a tensão na porta analógica.
  * Desktop: elaborar um programa que leia uma porta serial e escreva na tela. Executar o programa como root para ter direito a leitura e/ou escrita nas portas seriais.
  * Como exemplo, considerar o que foi desenvolvido no [Projeto Integrador II](http://olaria.ucpel.edu.br/pi2/)
  * [Características Técnicas do Arduino UNO](https://www.embarcados.com.br/arduino-uno/)
  
### Encontro em 07/04/2020
* Continuidade dos testes envolvendo a comunicação Arduino <-> Desktop

### Encontro em 14/04/2020
* Finalização do programa necessário para controle do Arduíno pelo Desktop
* A seguir códidos desenvolvidos pelo acadêmico Matheus Gonçalves Stigger. O objetivo destes códigos é controle de acendimento de três leds por parte do Desktop. Os leds tem seu acionamento feito pela plataforma Arduino.
``` 
#Programa Arduino
const int led=12;
const int led2=10;
const int led3=8;
int value=0;

void setup() 
   { 
      Serial.begin(9600); 
      pinMode(led, OUTPUT);
      pinMode(led2, OUTPUT);
      pinMode(led3, OUTPUT);
      digitalWrite (led, LOW);
      digitalWrite (led2, LOW);
      digitalWrite (led3, LOW);
      Serial.println("Connection established...");
   }
 
void loop(){
  
     while (Serial.available()){
       
           value = Serial.read();
     }
     
     if (value == 'a'){
        digitalWrite (led, HIGH);
     }
     
     else if (value == 'b'){
        digitalWrite (led, LOW);
     }
        
     else if (value == 'c'){
       digitalWrite (led2, HIGH);
     }
       
     else if (value == 'd'){
       digitalWrite (led2, LOW);
     }
       
     else if (value == 'e'){
       digitalWrite (led3, HIGH);
     }
       
     else if (value == 'f'){
       digitalWrite (led3, LOW);
     }
       
     else if (value == 'g'){
       digitalWrite (led, HIGH);
       digitalWrite (led2, HIGH);
       digitalWrite (led3, HIGH);
     }
       
     else if (value == 'h'){
       digitalWrite (led, LOW);
       digitalWrite (led2, LOW);
       digitalWrite (led3, LOW);
     }
}
``` 


``` 
#Programa Python - Desktop
import serial                                 # add Serial library for Serial c$

Arduino_Serial = serial.Serial('/dev/ttyACM0',9600)  #Create Serial port object$
print Arduino_Serial.readline()               #read the serial data and print i$
print ("Enter 1 to ON LED and 0 to OFF LED")

while 1:                                      #infinite loop
    input_data = raw_input()                  #waits until user enters data
    print "you entered", input_data           #prints the data for confirmation

    if (input_data == 'a'):                   #if the entered data is 1 
        Arduino_Serial.write('a')             #send 1 to arduino
        print ("LED ON")


    if (input_data == 'b'):                   #if the entered data is 0
        Arduino_Serial.write('b')             #send 0 to arduino 
        print ("LED OFF")
    
    if (input_data == 'c'):                   #if the entered data is 1 
        Arduino_Serial.write('c')             #send 1 to arduino
        print ("LED ON")


    if (input_data == 'd'):                   #if the entered data is 0
        Arduino_Serial.write('d')             #send 0 to arduino 
        print ("LED OFF")

    if (input_data == 'e'):
        Arduino_Serial.write('e')             #send 1 to arduino
        print ("LED ON")


    if (input_data == 'f'):                   #if the entered data is 0
        Arduino_Serial.write('f')             #send 0 to arduino 
        print ("LED OFF")

    if (input_data == 'g'):                   #if the entered data is 1 
        Arduino_Serial.write('g')
        print ("LED ON")


    if (input_data == 'h'):                   #if the entered data is 0
        Arduino_Serial.write('h')             #send 0 to arduino 
        print ("LED OFF")
``` 


### Encontro em 21/04/2020
#### Gerando gráficos no Desktop a partir de informações coletas pelo Arduino

``` 
from random import randint
import matplotlib.pyplot as plt #sudo apt install python3-matplotlib
import matplotlib.animation as animation #sudo apt install python3-tk

fig = plt.figure()
ax = fig.add_subplot(1, 1, 1)

xs = [1, 2, 3, 4, 5, 6, 7, 8]
ys = [10, 20, 30 ,40 , 50 ,60 , 70, 80]

#incremento partindo dos ultimos valores de cada lista
temperatura=80
tempo=8;

#funcao para animar
def animate(i, xs, ys):
    global temperatura
    global tempo

    #incremento
    #temperatura= temperatura+10
    temperatura= randint(0, 100)
    tempo = tempo + 1

    #append índice do tempo e temperatura
    xs.append(tempo)
    ys.append(temperatura)

    # desenhar x e y
    ax.clear()
    ax.plot(xs, ys)

    plt.title('Temperatura Atual e Tempo')
    plt.ylabel('Temperatura')

# altere o valor do interval para que que o frame seja atualizado de maneira mais rápida ou não
ani = animation.FuncAnimation(fig, animate, fargs=(xs, ys), interval=1000)
plt.show()
``` 


### Encontro em 28/04/2020
#### Gerando gráficos no Desktop a partir de informações coletas pelo Arduino (continuação)

Abaixo código desenvolvido pelo colega Miguel Gut Seara a partir dos exemplos disponíveis na página da bilbioteca Matplotlib. As URL para acesso a versão da bilbioteca instalada nos equipamentos dos laboratórios estão comentadas no início do código.

Este código gera dois gráficos: (1) potência de dois e (ii) seno

``` 
# Pagina de exemplos
# https://matplotlib.org/1.3.1/examples/index.html
# Exemplo do base do programa
# https://matplotlib.org/1.3.1/examples/lines_bars_and_markers/line_demo_dash_control.html

import numpy as np
import matplotlib.pyplot as plt


x0 = np.linspace(0, 10)
y0 = np.sin(x0)
y0 = np.multiply(y0,100);
line0, = plt.plot(x0, y0, '-', linewidth=2)

x1 = np.linspace(0,10)
y1 = np.power(x1,2)
line1, = plt.plot(x1, y1, '-', linewidth=2)

plt.show()
``` 

### Encontro em 05/05/2020
#### Gerando gráficos animados no Desktop a partir de informações coletas pelo Arduino (Osciloscópio)

Abaixo código desenvolvido pelo colega Ícaro Gonçalves Siqueira que permite o desenvolvimento de um osciloscópio. As bibliotecas necessárias para desenvolvimento do código estão comentadas no fonte do programa.

No [repositório do Miguel Gut Seara](https://github.com/miguelgut/teste-repositorio/tree/master/aula12) estão em construção códigos para o Desktop (Python) e Arduino (C Wiring) para troca de dados entre as plataformas.

``` 
import matplotlib.pyplot as plt #sudo apt install python3-matplotlib
import matplotlib.animation as animation #sudo apt install python3-tk
import numpy as np

#fig = plt.figure()
#ax = fig.add_subplot(1,1,1)
fig, ax = plt.subplots()

#valores iniciais
xs = [0]
ys = [0]
tempo=0

#funcao para animar
def animate(i, xs, ys):
     global tempo
     tempo = tempo + 1

     #recebe o valor da serial
     volt= np.sin(tempo)

     #incremento do novo valor
     xs.append(tempo)
     ys.append(volt)

     #mantem grafico dentro do intervalo de 100 plots
     if tempo > 100:
         xs = xs[tempo-99:tempo]
         ys = ys[tempo-99:tempo]

     ax.clear()
     # desenhar x e y
     ax.plot(xs, ys)

     plt.title('Medidor de Tensao')
     plt.ylabel('Volts')
     plt.xlabel('Tempo')

# altere o valor do interval para que que o frame seja atualizado de maneira mais rapida ou nao
ani = animation.FuncAnimation(fig, animate, fargs=(xs, ys), interval=100)
plt.show()
``` 

### Encontro em 12/05/2020
Avanço dos cógidos para Desktop e Arduino organizado pelo acadêmico Ícaro Gonçalves Siqueira. Estes códigos podem ser acessados neste link: http://olaria.ucpel.edu.br/materiais/lib/exe/fetch.php?media=codigos_arduino_e_python_projeto_osciloscopio.zip


### Encontro em 19/05/2020

* Conclusão da Primeira Avaliação
