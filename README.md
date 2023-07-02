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

- **Sensor de Temperatura** 
  - Modelo : [LM35](https://blogmasterwalkershop.com.br/arduino/como-usar-com-arduino-sensor-de-temperatura-lm35)
  - Função : Medir Temperatura
  - Saída : 0 a 100 ºC
  - Saída Adaptada : 0 a 63 ºC

- **Sensor de Peso** 
  - Modelo : [Célula de Carga](https://www.robocore.net/tutoriais/celula-de-carga-hx711-com-arduino)
  - Função : Medir o peso sobre ele
  - Saída : 0 até 50kg
  - Saída Adaptada : 0 a 31 kg (5 bits)



# Funcionamento do Sistema

## Processamento


## Saídas

- ### Qualidade da Luminosidade 
  - Ruim : 0 a 25% do máximo
  - Fraco : 25% a 50% do máximo
  - Moderado : 50% a 75% do máximo
  - Bom : 75% a 100% do máximo

- ### Qualidade de Instalação
  - Acender cada led referente ao pé, se ele estiver ruim.
  - Se 2 ou mais estiverem ruins, alerta.

- ### Situação da Temperatura
  - Boa : 15ºC < Temperatura < 35ºC
  - Ruim : (Temperatura < 15ºC) ou (35ºC < Temperatura)

	
```mermaid

graph LR;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

# Referências

**Conversão de Lux para $W/m²$** : [Tese de Mestrado](https://fenix.tecnico.ulisboa.pt/downloadFile/1970719973966843/MasterThesis_70481.pdf)

