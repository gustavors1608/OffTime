## OffTime: Uma solução para tempo em projetos Arduino offline e sem RTC externo

**OffTime** é uma biblioteca para Arduino que fornece uma solução simples e eficiente para gerenciar o tempo em projetos que não possuem acesso a um RTC externo ou a uma conexão de rede constante ou estável para sincronizar o tempo com um servidor NTP. 

**Situações ideais para usar OffTime:**

* **Projetos offline:** Ideal para dispositivos que não possuem conexão constante com a internet, como sensores remotos, dispositivos embarcados em veículos ou equipamentos industriais.
* **Redução de custos:** Elimina a necessidade de um RTC externo, reduzindo o custo e tamanho fisico do projeto.
* **Diminuição do tamanho de memória:** A biblioteca é compacta e não depende de bibliotecas externas, minimizando o espaço de memória necessário.

**Como funciona:**

OffTime utiliza um contador interno para rastrear o tempo em segundos desde um ponto de referência inicial. A função `set()` permite definir o tempo inicial manualmente(usado valor unix timestamp), permitindo a sincronização com um RTC externo ou um servidor NTP em momentos específicos com conexão.

**Funcionalidades:**

* **`now()`:** Retorna o tempo atual em segundos desde o ponto de referência inicial.
* **`set()`:** Define o tempo atual em segundos, sendo usado o valor unix timestamp atual.
* **`get_hour()`, `get_minute()`, `get_second()`:** Retorna a hora, minuto e segundo atuais.
* **`get_day()`, `get_month()`, `get_year()`:** Retorna o dia, mês e ano atuais.

**Exemplo de uso:**

```cpp
#include <OffTime.h>

OffTime time;

void setup() {
  // Inicializar o tempo com o valor atual do RTC externo ou servidor NTP
  unsigned long unix_timestamp = 1678886400;// Exemplo: 1 de março de 2023 às 00:00:00 UTC
  time.set(unix_timestamp); 
  Serial.begin(9600);
}

void loop() {
  // Imprimir a hora atual
  Serial.print("Hora atual: ");
  Serial.print(time.get_hour());
  Serial.print(":");
  Serial.print(time.get_minute());
  Serial.print(":");
  Serial.println(time.get_second());

  delay(1000);
}
```

**Observações:**

* A precisão do tempo é limitada pela resolução do `millis()` da biblioteca Arduino.
* A biblioteca assume que o ano tem 365 dias, ignorando anos bissextos.


**Contribuições:**

Contribuições para a biblioteca são bem-vindas! Se você encontrar bugs, tiver sugestões de melhorias ou quiser adicionar novas funcionalidades, por favor, envie um pull request.

Alguma das futuras melhorias planejas são:
- função que retorna o dia da semana de 0 a 6 sendo 0 (para domingo) até 6 (para sábado) por exemplo ->(mesmo padrão do php)
- função que retorna data completa formatada contando data e hora
- entre outras melhorias não imaginadas ainda...

**Licença:**

Este projeto é licenciado sob a licença MIT.


