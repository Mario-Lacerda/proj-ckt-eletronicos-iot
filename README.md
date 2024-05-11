# Desafio Dio - **Projeto de Circuitos Eletrônicos** 
Projeto de Circuitos Eletrônicos - IOT Seecialist

## **Sistema de Monitoramento de Temperatura e Umidade usando Arduino e IoT**

O objetivo deste projeto é criar um sistema de monitoramento de temperatura e umidade usando um Arduino e a Internet das Coisas (IoT). O sistema permitirá aos usuários monitorar remotamente a temperatura e a umidade de um ambiente e receber alertas quando certos limites forem atingidos.

### **Estruturando o Projeto**

O projeto será estruturado em vários módulos, cada um responsável por uma tarefa específica. Os módulos serão organizados de forma lógica e reutilizável.

### **Documentando**

O projeto será extensivamente documentado usando comentários e diagramas. A documentação incluirá exemplos de código e explicações claras de como usar cada função.

### **Definindo Modelos**

O projeto usará um modelo orientado a objetos para representar sensores, dados de medição e outras entidades. Os modelos fornecerão uma interface consistente para trabalhar com esses dados.

### **Definindo Serviços**

O projeto definirá uma série de serviços que executarão tarefas comuns de monitoramento de temperatura e umidade. Os serviços serão projetados para serem eficientes e fáceis de usar.

## **Definindo Regras de Negócio**

O projeto definirá um conjunto de regras de negócios que governarão como o sistema monitora a temperatura e a umidade. As regras de negócio serão documentadas e testadas para garantir sua precisão.

### **Integrando**

O projeto será integrado com um sensor de temperatura e umidade e com uma plataforma IoT para enviar dados de medição. O sistema também será integrado com um serviço de notificação para enviar alertas aos usuários.

### **Testando**

O projeto será extensivamente testado para garantir sua funcionalidade e precisão. Os testes serão automatizados para garantir a consistência.

## **Descrição**

O sistema de monitoramento de temperatura e umidade será um dispositivo autônomo que pode ser instalado em qualquer ambiente. O sistema incluirá um sensor de temperatura e umidade, um Arduino e um módulo IoT. O sistema enviará dados de medição para uma plataforma IoT em nuvem, onde os usuários poderão monitorar remotamente a temperatura e a umidade do ambiente. O sistema também enviará alertas aos usuários quando certos limites de temperatura e umidade forem atingidos.

### **Circuito**

O circuito do sistema de monitoramento de temperatura e umidade é relativamente simples. Os componentes necessários incluem:

- Arduino Uno
- Sensor de temperatura e umidade DHT11
- Módulo IoT ESP8266
- Resistor de 10kΩ
- Protoboard
- Cabos jumper

O circuito pode ser montado conforme o seguinte diagrama:

[Diagrama do circuito]

### **Programas e Códigos**

**Programa Arduino**

```cpp
#include <DHT.h>
#include <ESP8266WiFi.h>
#include <PubSubClient.h>

const char* ssid = "SEU_SSID";
const char* password = "SUA_SENHA";
const char* mqtt_server = "SEU_SERVIDOR_MQTT";
const int mqtt_port = 1883;
const char* mqtt_user = "SEU_USUARIO_MQTT";
const char* mqtt_pass = "SUA_SENHA_MQTT";
const char* mqtt_topic = "SEU_TOPICO_MQTT";

DHT dht(2, DHT11);
WiFiClient espClient;
PubSubClient client(espClient);

void setup() {
  Serial.begin(9600);
  dht.begin();
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
  }
  client.setServer(mqtt_server, mqtt_port);
  client.connect(mqtt_user, mqtt_pass);
}

void loop() {
  client.loop();
  float temperature = dht.readTemperature();
  float humidity = dht.readHumidity();
  if (!isnan(temperature) && !isnan(humidity)) {
    String message = String(temperature) + "," + String(humidity);
    client.publish(mqtt_topic, message.c_str());
  }
  delay(2000);
}
```

**Configuração do Módulo ESP8266**

As etapas específicas de configuração do módulo ESP8266 variam dependendo da plataforma IoT que você está usando. No entanto, as etapas gerais são as seguintes:

1. Conecte o módulo ESP8266 ao seu computador usando um cabo USB.

2. Abra um terminal serial em seu computador.

3. Envie o seguinte comando para o módulo ESP8266:

   

```plaintext
AT+RST
```

1. Isso redefinirá o módulo ESP8266.
2. Envie o seguinte comando para o módulo ESP8266:



```plaintext
AT+CWMODE=1
```

1. Isso colocará o módulo ESP8266 no modo de estação.
2. Envie o seguinte comando para o módulo ESP8266:

```plaintext
AT+CWJAP="SEU_SSID","SUA_SENHA"
```

1. Isso conectará o módulo ESP8266 à sua rede Wi-Fi.
2. Envie o seguinte comando para o módulo ESP8266:

```plaintext
AT+CIPMUX=1
```

1. Isso habilitará o modo de conexão múltipla no módulo ESP8266.
2. Envie o seguinte comando para o módulo ESP8266:

```plaintext
AT+CIPSERVER=1,80
```

1. Isso iniciará um servidor TCP na porta 80 no módulo ESP8266.

Agora o módulo ESP8266 está configurado e pronto para se conectar à plataforma IoT em nuvem.



## **Conclusão**

Este projeto resultará em um sistema de monitoramento de temperatura e umidade abrangente, fácil de usar e eficiente. O sistema será valioso para indivíduos e empresas que precisam monitorar remotamente a temperatura e a umidade de um ambiente.

## **Aprendizado**

Este projeto proporcionará uma oportunidade de aprender sobre os seguintes tópicos:

- Monitoramento de temperatura e umidade
- Arduino
- Internet das Coisas (IoT)
- Desenvolvimento de software
- Documentação de software
- Teste de software

## **Aplicabilidade Prática**

Este projeto pode ser usado em uma variedade de aplicações práticas, tais como:

- Monitoramento de temperatura e umidade em residências e empresas
- Monitoramento de temperatura e umidade em estufas e armazéns
- Monitoramento de temperatura e umidade em museus e arquivos
