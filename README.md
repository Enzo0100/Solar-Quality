# SolarQuality

# Grupo

| Nome                          | RA      | Email                    |
| ----------------------------- | ------- | ------------------------ |
| João Vinicius Farah Colombini | 159.501 | jvfcolombini@unifesp.br  |
| Victor Jorge Carvalho Chaves  | 156.740 | victor.chaves@unifesp.br |
| Enzo Soares e Silva Cerávolo  | 159.319 | enzo.ceravolo@unifesp.br |
| David Aaron Medeiro           |         |                          |


# Fundamentos

- ## [Irradiação (SI)](https://en.wikipedia.org/wiki/Irradiance#:~:text=The%20SI%20unit%20of%20irradiance,to%20confusion%20with%20radiant%20intensity)


- ## [Resistencia de Calor da Placa Solar](https://www.eco-greenenergy.com/pt-pt/o-clima-afetara-a-eficiencia-do-painel-solar/#:~:text=Como%20todos%20sabemos%2C%20os%20pain%C3%A9is,durante%20o%20ver%C3%A3o%20e%20inverno.)

- ## [Conversão de Lux para $W/m²$](https://fenix.tecnico.ulisboa.pt/downloadFile/1970719973966843/MasterThesis_70481.pdf)
  
$$R = L \times 8$$
$$L :\text{Luminosidade (lx ou lux)}$$
$$R : \frac{mW}{m²} : \frac{\text{ mili watts}}{\text{metro²}}$$


# Descrição

A partir da ODS 7 foi abstraída a ideia de desenvolver um projeto em circuitos digitais de maneira teórica para obtenção da qualidade de um território para a instalação de painéis solares. Isto é verificar tanto a procedência da área a colocar os painéis e também se existe uma quantidade aceitável luminosidade solar.

## **Sensores Utilizados**
- **Sensor de Luminosidade** 
    - Modelo : [BH1750](https://imasters.com.br/desenvolvimento/como-funciona-o-sensor-de-luz-bh1750)
    - Função : Mede a luminosidade em [lux (simbolo lx)](https://en.wikipedia.org/wiki/Lux).
    - Saída : 0 a 65535 (16 bits), que são em lux.
    - Saída Adaptada : 0 a 31 (5 bits), que são em $\frac{lx}{4096}$.

- **Sensor de Temperatura** 
  - Modelo : [LM35](https://blogmasterwalkershop.com.br/arduino/como-usar-com-arduino-sensor-de-temperatura-lm35)
  - Função : Medir Temperatura
  - Saída : 0 a 100 ºC
  - Saída Adaptada : 0 a 63 ºC (6 bits)

- **Sensor de Peso** 
  - Modelo : [Célula de Carga](https://www.robocore.net/tutoriais/celula-de-carga-hx711-com-arduino)
  - Função : Medir o peso sobre ele
  - Saída : 0 até 50kg
  - Saída Adaptada : 0 a 31 kg (5 bits)



# Funcionamento do Sistema
## Circuitos 

- ### Codificador 3

$$ A_{16} A_{15} \dots A_1 \Rightarrow A_{16} A_{15} \dots A_1 000$$

- ### Codificador -11

$$ A_{16} A_{15} \dots A_1 \Rightarrow A_{16} A_{15} A_{14} A_{13} A_{12}$$

- ### Codificador Par 2

|                       | $A_3 A_4$ | $A_3 \bar{A_4}$ | $\bar{A_3} \bar{A_4}$ | $\bar{A_3} A_4$ |
| --------------------- | --------- | --------------- | --------------------- | --------------- |
| $A_1 A_2$             | 1         | 1               | 1                     | 1               |
| $A_1 \bar{A_2}$       | 1         | 1               | 0                     | 1               |
| $\bar{A_1} \bar{A_2}$ | 1         | 0               | 0                     | 0               |
| $\bar{A_1} A_2$       | 1         | 1               | 0                     | 1               |


Formula Final: $A_1 A_2 + A_1 A_3 + A_1 A_4 + A_2 A_3 + A_2 A_4 + A_3 A_4$

- ### Codificador

$$R_1 R_2 + R_1 R_3 + R_1 R_4 + R_2 R_3 + R_2 R_4 + R_3 R_4$$
$$+$$
$$(R_1 + R_2 + R_3 + R_4) \times (R_5 + R_6 + R_7 + R_8)$$
$$+$$
$$R_5 R_6 + R_5 R_7 + R_5 R_8 + R_6 R_7 + R_6 R_8 + R_7 R_8$$

## Processamento


- ### Calculo da Qualidade de Luminosidade

```mermaid
graph LR; 
    sensor(Sensor de Luminosidade)-->|0...65535|cod2(Codificador -11);
    sensor(Sensor de Luminosidade)-->|0...65535|cod(Codificador 3)
    cod(Codificador 3)-->|x * 8|Output
    cod2(Codificador -11)-->|0...31|mini-ULA-1
    cod2(Codificador -11)-->|0...31|mini-ULA-2
    cod2(Codificador -11)-->|0...31|mini-ULA-3
    mini-ULA-1-->|x < 8|R1
    mini-ULA-2-->|x < 16|R2
    mini-ULA-3-->|x < 23|R3
    R1-->Decodificador
    R2-->Decodificador
    R3-->Decodificador
    Decodificador-->Ruim(Ruim : R1 * R2 * R3)
    Decodificador-->Fraco(Fraco : R1' * R2 * R3)
    Decodificador-->Moderado(Moderado : R1' * R2' * R3)
    Decodificador-->Bom(Bom : R1' * R2' * R3')
```


- ### Verificação da Instalação

```mermaid
graph LR; 
sensorA(Célula de Carga A)-->Comparador-1
sensorB(Célula de Carga B)-->Comparador-2
sensorC(Célula de Carga C)-->Comparador-3
sensorD(Célula de Carga D)-->Comparador-4
Comparador-1-->|x < 2|Comparador-5
Comparador-2-->|x < 2|Comparador-6
Comparador-3-->|x < 2|Comparador-7
Comparador-4-->|x < 2|Comparador-8
Comparador-1-->|x < 2|R1
Comparador-2-->|x < 2|R2
Comparador-3-->|x < 2|R3
Comparador-4-->|x < 2|R4
Comparador-5-->|x < 1|R5
Comparador-6-->|x < 1|R6
Comparador-7-->|x < 1|R7
Comparador-8-->|x < 1|R8
R1-->LED-1
R2-->LED-2
R3-->LED-3
R4-->LED-4
R1-->Codificador
R2-->Codificador
R3-->Codificador
R4-->Codificador
R5-->Codificador
R6-->Codificador
R7-->Codificador
R8-->Codificador
Codificador-->LED-W
LED-W---led(2 ou Mais R de 1 a 4.\nOU\n Um R 5 a 8 e mais Qualquer R de 1 a 4.\nOU\n Dois ou mais de R 5 a 8.)
```

- ### Verificação da Temperatura

```mermaid
graph LR; 
sensorA(Sensor 1)-->Comparador-1
sensorA(Sensor 1)-->Comparador-2
Comparador-1-->|x < 15|cod(Codificador Ava)
Comparador-2-->|x > 35|cod(Codificador Ava)
cod(Codificador Ava) --> LED-B
LED-B --- text(Está Ruim)
```


## Saídas

- ### Qualidade da Luminosidade 
  - Ruim : 0 a 25% do máximo de luminosidade 
  - Fraco : 25% a 50% do máximo de luminosidade 
  - Moderado : 50% a 75% do máximo de luminosidade
  - Bom : 75% a 100% do máximo de luminosidade

- ### Qualidade de Instalação
  - Acender cada led referente ao pé, se ele estiver ruim.
  - Se 2 ou mais estiverem ruins, alerta.

- ### Situação da Temperatura
  - Boa : 15ºC < Temperatura < 35ºC
  - Ruim : (Temperatura < 15ºC) ou (35ºC < Temperatura)
