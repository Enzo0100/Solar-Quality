# Mini-ULA

# Grupo

| Nome                          | RA      | Email                    |
| ----------------------------- | ------- | ------------------------ |
| João Vinicius Farah Colombini |         |                          |
| Victor Jorge Carvalho Chaves  | 156.740 | victor.chaves@unifesp.br |
| Enzo Soares e Silva Cerávolo  |         |                          |
| David Aaron Medeiro           |         |                          |


https://circuitdigest.com/microcontroller-projects/solar-irradiance-mesurement-meter-using-arduino

https://www.extrica.com/article/21667

https://fenix.tecnico.ulisboa.pt/downloadFile/1970719973966843/MasterThesis_70481.pdf

https://pdf1.alldatasheet.com/datasheet-pdf/view/338083/ROHM/BH1750FVI.html

# Fundamentos

- ## [Irradiação (SI)](https://en.wikipedia.org/wiki/Irradiance#:~:text=The%20SI%20unit%20of%20irradiance,to%20confusion%20with%20radiant%20intensity)

- ## [Conversão de Lux para $W/m²$](https://fenix.tecnico.ulisboa.pt/downloadFile/1970719973966843/MasterThesis_70481.pdf)

$$R = L \times 8 \times 10^{-5} $$
$$L :\text{Luminosidade (lx ou lux)}$$
$$R : \frac{kW}{m²} : \frac{\text{ kilo watts}}{\text{metro²}}$$


# Descrição

A partir da ODS 7 foi abstraída a ideia de desenvolver um projeto em circuitos digitais de maneira teórica para obtenção da qualidade de um território para a instalação de painéis solares. Isto é verificar tanto a procedência da área a colocar os painéis e também se existe uma quantidade aceitável luminosidade solar.

## **Sensores Utilizados**
- **Sensor de Luminosidade** 
    - Modelo : [BH1750](https://imasters.com.br/desenvolvimento/como-funciona-o-sensor-de-luz-bh1750)
    - Função : Mede a luminosidade em [lux (simbolo lx)](https://en.wikipedia.org/wiki/Lux).
    - Saída : 0 a 65535 (16 bits), que são em lux.
    - Saída Adaptada : 0 a 31 (5 bits), que são em $\frac{lx}{4096}$.

- **Sensor de Vibração** 
  - Modelo : [HEDRO-H1](https://www.hedro.com.br/wp-content/uploads/2020/08/Datasheet-HEDRO-H1-V2.pdf)
  - Função : Medir Velocidade de Vibração ($mm/s$)
  - Saída : 0 a 65535 (16 bits)

- **Sensor de Peso** 
  - Modelo : [Célula de Carga](https://www.robocore.net/tutoriais/celula-de-carga-hx711-com-arduino)
  - Função : Medir o peso sobre ele
  - Saída : 0 até 50kg
  - Saída Adaptada : 0 a 31 kg (5 bits)



# Funcionamento do Sistema

## **Entradas**

- ## Luminosidade Codificada 

$$R = \text{Input} \div 4096$$
$$R = \{0, 1, 2, ..., 31\}$$

## **Processamentos** 

- ## Quantidade de $W/m²$ produzido 

$$R = \text{Luminosidade Codificada} \times 8$$
$$R = \{0, 8, 16, 24\}$$

## **Saídas**


- ## Período de Rendimento em $W/m²$ 

$$R = \text{Energia} \times 210$$
$$R = \{0, 8, 16, 24\}$$


- ## Quantidade de $W/m²$ produzido 

	
Em relação aos sensores de  radiação solar, ao atingirem certo nível de radiação mudam suas entradas de 0 para 1 e assim quando todos os sensores estiverem em 1 (porta AND) passam um sinal de saída X dizendo que aquele lugar recebe uma boa quantidade de radiação (esses sensores medem uma quantidade certa de radiação e somente assim mudam de 0 para 1).


Os sensores de pressão e de vibração emitem saídas de perigo a possíveis danos em relação ao local onde será colocado o painel e sobre a qualidade de preservação do equipamento que mede essas condições (dispositivo criado pelo projeto), no geral apitam 3 leds, são eles:

d- Os sensores de pressão que vão de 1 a 0 pois estavam pressionados ao solo e por algum motivo foi identificado um problema na estabilidade estrutural na área onde o dispositivo está instalado.
- Os de vibrações fortes variam de 0 a 1. Apita outro led onde mostra que estão tendo ventos ou vibrações fortes o suficiente para danificar o aparelho e a futura instalação de painéis solares.
- Os de radiação solar ficam em 0 e vão para 1 quando o sensor atinge um certo nível de radiação solar estimado para que aquele local seja apropriado para a instalação de um painel solar.


OBS: todos os leds nesse caso são considerados alarmes.


Tem-se também a ideia de implementar portas AND e OR para uma melhor acurácia na avaliação de todos os sensores.

Para os sensores de pressão como a ideia é usar de 2 ou 4 a ideia é de que usando uma porta AND quando temos 2 sensores, se 1 falhar o led acende. Ao terem 4 portas são necessários 2 sensores falharem pelo menos, para isso será necessário utilizar simplificações algébricas e mapas de karnaugh para realizar um circuito que apite apenas quando 2 falharem.
Fora isso essa lógica dos sensores de pressão funcionam igualmente para os de vibrações, sendo assim possível montar um dispositivo simples e barato com uma boa eficácia em medir o potencial de uma área para instalação de painéis solares.

(Uma outra opção viável seria utilizar outros tipos de sensores para medir áreas propícias para aplicação de “moinhos” de geração de energia eólica, apenas uma ideia).


```mermaid

graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

# Referências

**Conversão de Lux para $W/m²$** : [Tese de Mestrado](https://fenix.tecnico.ulisboa.pt/downloadFile/1970719973966843/MasterThesis_70481.pdf)

