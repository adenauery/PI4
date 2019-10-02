## Equipe

* Gabriel Härter Zoppo
* Guilherme Corrêa Carvalho
* Helena Garcia Tavares
* Ícaro Gonçalves Siqueira
* Miguel Gut Seara
* Matheus Gonçalves Stigger
* Pedro Rosado Julio

## Primeiro Encontro - 07/08/2019

* Discussão dos objetivos
* Explorando as funções web do GitHub 
* Python & Arduino

**Metas até o próximo encontro:**
* Criar conta no GitHub - [existem outras opções](https://pt.wikiversity.org/wiki/Github_x_Gitlab_x_Bitbucket)
* Exercitar a sintaxe do Markdown (https://docs.pipz.com/central-de-ajuda/learning-center/guia-basico-de-markdown)
* Exercitar pequenos códigos em Python

## Segundo Encontro - 14/08/2019
* Atualização dos Sistemas Linux
* Instalação do Git para operação console
* Testes iniciais com o Git, explorando a plataforma GitHub

## Terceiro Encontro - 21/08/2019
* Revisando as operações com o Git
* Programando com Python - Etapa 1

## Quarto Encontro - 28/08/2019
* Operações com o Git
* Programando com Python - Etapa 2

## Quinto Encontro - 04/09/2019
* Programando com Python - Etapa 3 
  * Explorando laços: While

## Sexto Encontro - 11/09/2019
* Avaliando a comunicação Arduino --> Desktop - Etapa 1
  * Arduino: fazer um programa que fique em um laço infinito lendo uma porta analógica e escrevendo na saída serial. Empregar um potenciômetro para variar a tensão na porta serial.
  * Desktop: elaborar um programa que leia uma porta serial e escreva na tela. Executar o programa como root para ter direito a leitura e/ou escrita nas portas seriais.
  * Como exemplo, considerar o que foi desenvolvido no [Projeto Integrador II](http://olaria.ucpel.edu.br/pi2/)
  * [Características Técnicas do Arduino UNO](https://www.embarcados.com.br/arduino-uno/)

## Sétimo Encontro - 18/09/2019
* Continuidade dos testes envolvendo a comunicação Arduino <-> Desktop

## Oitavo Encontro - 18/09/2019
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
## Nono Encontro - 02/10/2019

* Gerando gráficos no Desktop a partir de informações coletas pelo Arduino


``` 
from random import randint
import matplotlib.pyplot as plt
import matplotlib.animation as animation



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

## Informações Refentes à Disciplina

**Professores do Segundo Semestre de 2019:**
* Matemática Aplicada - Marilia
* Análise de Circuitos II - Lizandro
* Matemática Discreta - Mateus
* Classificação e Pesquisa de Dados - Mateus
* Física Moderna - Chiara

**Python & Arduino:**
* Exemplo básico de comunicação entre Python e Arduino
  * https://medium.com/grupy-rn/python-e-arduino-ganhando-produtividade-em-seus-projetos-de-internet-das-coisas-37781e21b9ee

* Exemplo de integração de Python com Arduino:
  * http://www.toptechboy.com/using-python-with-arduino-lessons/

* IUP - Introdução ao Universo da Programação com Python. Wendel Melo. 2019
  * [Download](http://www.facom.ufu.br/~wendelmelo/meu_material/introducao_programacao_python_wendel_melo.pdf)

**Simulink**
  * https://www.mathworks.com/products/simulink.html (opção Mathlab)
  * https://www.scilab.org/software/xcos (opção Scilab)

**Draw**
  * https://www.draw.io

**6 compiladores online para estudantes e profissionais de programação**
  * https://elias.praciano.com/2016/12/6-compiladores-online-para-estudantes-de-programacao/

**Tutoriais sobre o git**
  * https://rogerdudler.github.io/git-guide/index.pt_BR.html
    * Para criar um repositório:
      * git clone \<URL do Repositório disponibilizada pelo Git Hub\> (somente se executa uma vez)
    * Para adicionar arquivo(s) criado(s) no repositório local:
      * git add \<nome do arquivo\> ou git add *
    * Para enviar os arquivos alterados ou criados localmente para o repositório remoto:
      * git commit -m "comentários das alterações" \<nome do arquivo\>
      * git push origin master
    * Para atualizar seu repositório local com a mais nova versão
      * git pull
  * https://www.hostinger.com.br/tutoriais/comandos-basicos-de-git/

**Atualizando o sistema operacional (Ubuntu)**
* sudo su
* apt-get update
* apt-get upgrade
* apt-get dist-upgrade (se necessário)
* apt-get autoremove (se necessário)

**Instalando um software por apt-get**
* Atualizar o sistema operacional
* Como root:
  * apt-cache search \<parte do nome do possível pacote\>
  * apt-get install \<nome do pacote\>

**Editor leve para Python**
* apt-get install idle3

**Gerenciando Múltiplas versões de Python**
* https://gist.github.com/luzfcb/ef29561ff81e81e348ab7d6824e14404
