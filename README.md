# INTRODUÇÃO

Muitas vezes, em semáforos convencionais há desperdício de energia ao deixar a iluminação muito forte à noite, além de produzir ofuscamento em dias chuvosos ou nublados, ao mesmo tempo pode haver falta de iluminação em dias ensolarados. Para isso, foi implementado um controle inteligente de iluminação, baseado nos dados obtidos em experimentos práticos que realizei com LDR foi especificada a tabela proposta no trabalho, e foram estabelecidos nove níveis de iluminação, variando o brilho de 10% a 100%, visto que o semáforo nunca pode ficar desligado, e também na execução do código abaixo, onde pode-se observar que o brilho do semáforo é ajustado automaticamente, dependendo da medição do LDR, o que faz com que o semáforo tenha seu brilho controlado digitalmente de forma autônoma. O semáforo inteligente trabalha coletando dados de sensores como sensor de luminosidade e sensor contador de tráfego. O semáforo periodicamente realiza as tarefas de leitura dos sensores, preparação e envio dos dados pela rede, e esses dados são recebidos numa central de controle, onde o usuário pode controlar alguns parâmetros como o tempo de abertura do semáforo, assim como encerrar a conexão.

# SENSORES

Para o projeto de sinaleira inteligente utilizarei essencialmente dois sensores, um de luminosidade, que pode ser um LDR, por exemplo. Para o sensor de tráfego podem ser feitas diversas soluções, por exemplo utilizar um sensor de distância a laser, ultrassom, e quando um veículo passa embaixo do semáforo, quando houver alteração de distância medida relevante será contabilizado como um veículo.

● Sensor de luminosidade
● Sensor contador de tráfego

Para o contador de tráfego utilizei uma contagem direta de veículos. Já no sensor LDR, utilizei uma tabela de valores que desenvolvi utilizado um LDR e um Arduino UNO, utilizando um divisor de tensão com um resistor de 10K Ohms. Segue abaixo a tabela de valores do LDR:

Nível Valor Condição da medição
- 0 Escuro absoluto
1 100 Ambiente com Iluminação fraca à noite
2 300 Ambiente Interior pouco iluminado diurno
3 350 Ambiente interno indiretamente iluminado 45W
4 550 Ambiente interno diretamente iluminado 45W
5 770 Ambiente interno com iluminação natural
6 940 Ambiente Interno com ótima iluminação natural
7 960 Ambiente externo coberto
8 990 Ambiente externo com incidência solar indireta
9 1015 Ambiente externo com incidência solar direta


# COMANDOS

O projeto permite que sejam enviados comandos da interface de controle para o cliente, esses comandos permitem com que os parâmetros do semáforo sejam alterados manualmente, como tempo de abertura do semáforo, e a opção de encerrar a comunicação.

● Alterar tempo de abertura do semáforo
● Encerrar a comunicação

Inicialmente, os comandos serão enviados na forma de uma palavra (comando)
seguido de um espaço e o valor a ser modificado, conforme foi definido na tabela abaixo:

Comando Valor
T+ Aumenta em 1 minuto o tempo de abertura do sinal
T- Diminui em 1 minuto o tempo de abertura do sinal
SAIR Encerra a comunicação com o servidor/simulador


# FUNÇÕES

O cliente irá executar quatro tarefas periódicas, sendo a leitura dos sensores de luminosidade e tráfego, ajuste do brilho do semáforo com base na incidência de luz recebida pelo sensor, ajuste da abertura do semáforo de acordo com o tempo escolhido manualmente ou definido de acordo com o fluxo de tráfego no momento recebido pelo sensor, e exibição do status dos dados na tela no período definido.

Abaixo encontram-se as funções do servidor e suas finalidades:

● static void *le_sensor(void *arg)
Função que efetua a leitura dos sensores de luminosidade e tráfego
O sensor de luminosidade e tráfego
fazem a leitura de dados randômicos
definidos pelas funções:
Luminosidade_atual=0+rand()%1024;
Trafego_atual = 0+rand()%100;
● static void *le_luminosidade(void *arg)
Função que seta o brilho do semáforo a partir da luminosidade recebida pelo sensor.
● static void *le_trafego(void *arg)
Função que seta o tempo de abertura do semáforo a partir da quantidade de tráfego
recebida pelo sensor.
● static void *le_status(void *arg)
Função que reúne os dados das threads e exibe na tela.
ESCOPO DO SERVIDOR/SIMULADOR:
ESCOPO DO CLIENTE / MONITOR:
Código baseado no exemplo disponibilizado em aula
