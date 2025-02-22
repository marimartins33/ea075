# `<Aquário Inteligente >`
# `<Smart Aquarium>`

## Apresentação

O presente projeto foi originado no contexto das atividades da disciplina de graduação *EA075 - Sistemas Embarcados*, 
oferecida no segundo semestre de 2022, na Unicamp, sob supervisão da Profa. Dra. Paula Dornhofer Paro Costa, do Departamento de Engenharia de Computação e Automação (DCA) da Faculdade de Engenharia Elétrica e de Computação (FEEC).

> |Nome  | RA | Curso|
> |--|--|--|
> | Mariane Martins | 221919  | Eng. Elétrica|
> | Luis Felipe da Silva Teruel  | 202245  | Eng. Elétrica|


## Descrição do Projeto
O projeto Aquário Inteligente visa, que os amantes de aquário que tenham uma rotina que exija muitas horas longe de casa, possam garantir que o ambiente de seus animais de estimação esteja em perfeitas condições. Muitas espécies de animais aquáticos precisam de certas características especificas para ter uma qualidade de vida, tais como determinada temperaturas da água, determinado Ph, salinidade da água, entre outros. Esses parâmetros precisam ser verificados periodicamente, o torna muitas vezes inviável a aquisição dessas espécies. O Aquário inteligente tornará viável essa prática, pois irá checar tais parâmetros e enviar um relatório regularmente para o tutor, além de automatizar algumas das ações, como por exemplo dar comida e fazer a regulação da temperatura da água.


## Descrição Funcional
O projeto tem como objetivo desenvolver um aquário com um sistema de controle e gerenciamento das condições da água, que atua por meio da coleta de parâmetros físicos e químicos através de sensores, que acionarão circuitos externos para tomadas de decisões e emissão de alertas. Os dados coletados serão armazenados na nuvem, no qual podem ser gerados relatórios periódicos da qualidade do aquário. 

### Funcionalidades
- Sensor de Temperatura e atuador 
- Sensor de nível de água
- Temporizador para alimentação e atuador 
- Sensor de Ph e atuador 
- Medidor de oxigênio e atuador
- Medidor de luminosidade e atuador 
- Sensor de turbidez
- Conexão com a internet (wi-fi)


### Configurabilidade
O usuário poderá configurar:
- Horário de alimentação
- Periodicidade do envio do relatório


### Eventos
- Emitir alerta ao atingir determinada temperatura e acionar o termostato 
- Emitir alerta ao atingir nível máximo ou mínimo de água
- Ao definir um horário(s), um motor de passo será acionado para dosar a ração (evento períodico determinado pelo usuário)
- Emitir alerta ao atingir determinado pH e acionar dosador da solução corretora
- Emitir alerta e ligar bomba caso oxigênio atinja determinado valor
- Ligar luz durante o dia caso fique escuro
- Emitir alerta caso aquário esteja muito turvo 
- Envio de um relatório com os dados medidos em um determinado intervalo (evento periódico determinado pelo usuário

### Tratamento de Eventos
- Um sensor de temperatura deverá aferir a temperatura. Enquanto o valor não atingir o máximo estipulado, o valor deverá ser armazenado. Se o valor atingir o máximo, além de armazenar, deverá acionar o circuito de comando do termostato e enviar um alerta ao aplicativo do aquário
- Um sensor de nível deverá verificar se a água do aquário ultrapassou os limites máximo e mínimo de altura. Caso seja ultrapassado, deverá enviar um alerta para o aplicativo.
- O usuário poderá configurar um ou mais horários para ocorrer a alimentação dos peixes. Quando esse(s) horários definidos chegam, um circuito de comando é acionado, e um motor de passo irá ligar e permitir que um determinado volume de comida, também definido pelo usuário, caia no aquário
- Um sensor de pH deverá aferir o valor do pH e armazená-lo. Caso o valor seja superior ao desejado, um circuito de comando será acionado e um dosador eletrônico irá despejar uma determinada quantidade da solução corretora, que será calculado a partir do valor medido e um alerta será enviado ao aplicativo
- Um sensor de oxigênio irá verificar se a concentração de oxigênio e armazená-lo. Caso esteja abaixo do ideal, o circuito de comando da bomba será acionado e um alerta será enviado ao aplicativo
- Um sensor de luminosidade irá verificar se o local está escuro, e caso esteja e seja ainda de dia, o circuito de comando do led deverá ser acionado 
- Um sensor de turbidez irá verificar caso a água esteja muito turva, e caso esteja, enviará um alerta ao aplicativo
- Os dados armazenados irão gerar gráficos periódicos, com período definido pelo usuário


## Descrição Estrutural do Sistema
O Aquário Inteligente é dividido basicamente no nível dos sensores, atuadores e a nuvem. Os sensores fazem a leitura dos valores estipulados ou a condição desejada. Esses dados que foram aferidos, serão enviados para nuvem periodicamente, e se caso estejam fora do valor desejado ou condição, deverão acionar os atuadores. 
![Diagrama blocos Aquário inteligente](https://github.com/marimartins33/ea075/blob/main/2022.2/Aquario_Inteligente/images/diagrama_aquario.jpg)

## Especificações 

### Especificação Estrutural dos componentes
Os componentes utilizados no projeto serão os seguintes:
 - Microcontrolador ESP32
 - Sensor de temperatura DS18B20
 - Sensor de nível LA16M-40
 - Sensor de pH PH4502C + PH Eletrodo
 - Sensor de luminosidade GL5528
 - Sensor de turbidez CUS52D
 - Micro Servo Motor 9g Tower Pro SG90
 - Regulador de Tensão AMS1117 5V 1A
 - Mini Fonte 5V HLK-PM01 100-240V

O datasheet dos componentes e a justificativa do uso pode ser acessada [aqui](https://github.com/marimartins33/ea075/blob/main/2022.2/Aquario_Inteligente/components.md).
 ### Especificação do microcontrolador ESP32
- ROM interna de 448kB
- RAM estática 520kB
- Memória externa: suporte até 16MB (Flash e SRAM)
- Interface WiFi e Bluetooth
- Dois grupos de timers – 4 timers de 64 bits
- Alimentação VCC de 2,3V a 3,6V

### Periféricos do chip ESP32
- 34 portas GPIO’s
- 2 conversores ADC 12-bits (18 canais)
- 2 Conversores DAC 8-Bits
- 4 Interfaces SPI – Clock até 40MHz
- 4 Interfaces I2S – Clock até 40MHz
- 4 Interfaces I2C– Clock até 5Mbps
- Controle de motor PWM
- Controle de Motor Led PWM até 16 canais

### Periféricos
- Sistema de Purificação
Filtro Externo Sunsun HBL-302 350 L/h 127v
- Sistema de ar comprimido
Compressor de ar 2,5W 110V Maxxi Power
-Sistema de aquecimento
Aquecedor com termostato integrado Roxin HT1300 25W
-Sistema de alimentação
Micro servo 9G SG90 TowerPro
-Display Oled
LILYGO®Ttgo t-display 1.14 Polegadas 

### Demais itens
- Ração para peixes
- Anti-Cloro
- Amonia
- Anti-algas
- Tanque de vidro
- Caixa de componentes
- Tanque de alimentação
- Kit Air Plus 02 Peças

### Especificação de Algoritmos 

## Referências
- [1] https://maua.br/files/artigos/aquario-automatizado.pdf - Acessado em 18/09/2022
- [2] https://periodicos.unis.edu.br/index.php/interacao/article/view/144 - Acessado em 18/09/2022

