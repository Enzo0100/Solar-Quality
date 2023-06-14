# Mini-ULA

## Integrantes:
- João Vinicius Farah Colombini
- Victor Jorge Carvalho Chaves
- Enzo Soares e Silva Cerávolo
- David Aaron Medeiro

<br>

## Descrição Básica:

A partir da ODS 7 foi abstraída a ideia de desenvolver um projeto em circuitos digitais de maneira teórica para obtenção da qualidade de um território para a instalação de painéis solares. Isto é verificar tanto a procedência da área a colocar os painéis e também se existe uma quantidade aceitável em relação a radiação solar.

### Sensores utilizados serão (descrição básica):
- **Sensor Solar** que mede radiação (existe tanto para arduino quanto um piranômetro, a ideia é usar uma quantidade razoável para arduino, assim medindo a quantidade de radiação solar na área para instalar um futuro painel solar);
- **Sensor de Vibração** (existe tanto um sobre vibrações no solo quando para vibração do ar no caso  para medir ventos fortes, o motivo deste é ver se o vento forte é forte o suficiente para danificar o aparelho a ser instalado para verificação e também sobre o futuro painel solar a ser instalado);
- **Sensor de Pressão** (utilizado em arduinos para medir a pressão em relação a objetos, assim a ideia é colocar 4 desses um em cada ponto médio de cada lado do dispositivo para medir a quantidade de pressão entre o dispositivo e o local onde o painel será instalado.

### Entrada, Processamento e Saida
	
Em relação aos sensores de  radiação solar, ao atingirem certo nível de radiação mudam suas entradas de 0 para 1 e assim quando todos os sensores estiverem em 1 (porta AND) passam um sinal de saída X dizendo que aquele lugar recebe uma boa quantidade de radiação (esses sensores medem uma quantidade certa de radiação e somente assim mudam de 0 para 1).


Os sensores de pressão e de vibração emitem saídas de perigo a possíveis danos em relação ao local onde será colocado o painel e sobre a qualidade de preservação do equipamento que mede essas condições (dispositivo criado pelo projeto), no geral apitam 3 leds, são eles:

- Os sensores de pressão que vão de 1 a 0 pois estavam pressionados ao solo e por algum motivo foi identificado um problema na estabilidade estrutural na área onde o dispositivo está instalado.
- Os de vibrações fortes variam de 0 a 1. Apita outro led onde mostra que estão tendo ventos ou vibrações fortes o suficiente para danificar o aparelho e a futura instalação de painéis solares.
- Os de radiação solar ficam em 0 e vão para 1 quando o sensor atinge um certo nível de radiação solar estimado para que aquele local seja apropriado para a instalação de um painel solar.


OBS: todos os leds nesse caso são considerados alarmes.


Tem-se também a ideia de implementar portas AND e OR para uma melhor acurácia na avaliação de todos os sensores.

Para os sensores de pressão como a ideia é usar de 2 ou 4 a ideia é de que usando uma porta AND quando temos 2 sensores, se 1 falhar o led acende. Ao terem 4 portas são necessários 2 sensores falharem pelo menos, para isso será necessário utilizar simplificações algébricas e mapas de karnaugh para realizar um circuito que apite apenas quando 2 falharem.
Fora isso essa lógica dos sensores de pressão funcionam igualmente para os de vibrações, sendo assim possível montar um dispositivo simples e barato com uma boa eficácia em medir o potencial de uma área para instalação de painéis solares.

(Uma outra opção viável seria utilizar outros tipos de sensores para medir áreas propícias para aplicação de “moinhos” de geração de energia eólica, apenas uma ideia).
