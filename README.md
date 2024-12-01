# dispositivo-indicador-de-chuva
Esse é um projeto para montar um dispositivo indicador de chuva

Descrição do Hardware Utilizado
Plataformas de Desenvolvimento
O projeto utilizou a placa de desenvolvimento ESP8266 como unidade central de controle e comunicação. Esta escolha foi baseada na necessidade de uma conexão confiável com a internet para enviar os dados coletados pelo sensor via protocolo MQTT. A ESP8266 possui recursos integrados de Wi-Fi e é amplamente utilizada para projetos IoT devido à sua eficiência e custo acessível.

Sensores
Foi empregado um sensor de chuva analógico que detecta a presença de água em sua superfície. Este sensor converte o sinal de detecção de chuva em uma leitura analógica (valores de 0 a 1023), que é interpretada pelo ESP8266. O sensor foi escolhido pela sua simplicidade, confiabilidade e custo reduzido, sendo ideal para protótipos de detecção de condições climáticas.

Atuadores
O atuador utilizado foi um servo motor modelo SG90, que possui torque e precisão suficientes para movimentar pequenos objetos. O servo foi programado para realizar movimentos específicos em resposta às leituras do sensor, demonstrando visualmente as condições climáticas detectadas. Este componente é compacto, leve e oferece excelente compatibilidade com projetos baseados no ESP8266.

Peças Fabricadas e Encaixes
Para acomodar os componentes do projeto, foram utilizadas peças projetadas e impressas em impressoras 3D. Estas peças incluem:

Suporte do sensor de chuva: Dimensões aproximadas de 50x50x20 mm, garantindo estabilidade e exposição ideal do sensor à água.
Caixa de proteção para a placa ESP8266 e o servo motor: Dimensões de 100x100x50 mm, projetada para proteger os componentes contra poeira e umidade, além de permitir fácil acesso para manutenção.
Base para fixação: Incluindo aberturas para cabos e ventilação, com medidas de 120x120x10 mm.
As peças foram projetadas no software Tinkercad e impressas com material PLA, garantindo resistência e durabilidade. As dimensões foram ajustadas para facilitar o transporte e a instalação.

Cabos e Conexões
Conexões entre os componentes foram feitas com cabos jumper e conectores do tipo Dupont, assegurando a modularidade e a simplicidade de montagem. Todas as conexões elétricas foram organizadas dentro da caixa impressa para evitar curtos-circuitos.

Energia
O projeto foi alimentado por uma fonte USB de 5V, capaz de suprir tanto o ESP8266 quanto o servo motor. Essa escolha garante flexibilidade, permitindo o uso de carregadores portáteis ou adaptadores comuns.

Conclusão
O projeto foi desenvolvido com foco em simplicidade e funcionalidade, utilizando uma combinação de componentes acessíveis e personalizados. A integração dos sensores, atuadores e peças impressas em 3D resultou em um dispositivo compacto e eficaz para detecção de chuva, com potencial para aplicações em automação residencial e monitoramento ambiental.

Documentação das Interfaces, Protocolos e Módulos de Comunicação
Interface de Comunicação
O projeto utiliza o protocolo MQTT (Message Queuing Telemetry Transport) para a comunicação entre o dispositivo ESP8266 e um servidor na nuvem, onde os dados de detecção de chuva são processados e armazenados. O MQTT foi escolhido devido à sua leveza e eficiência, sendo ideal para dispositivos IoT que operam em redes com largura de banda limitada.

Estrutura do Sistema de Comunicação:
Publicador (ESP8266): Envia leituras do sensor de chuva para um servidor MQTT.
Broker MQTT (exemplo: Thingspeak): Gerencia as mensagens publicadas e distribui para os subscritores.
Subscritor (Aplicações ou Dashboards): Recebe e exibe os dados em tempo real.
Protocolo de Comunicação
MQTT 3.1.1:
Funciona sobre o protocolo TCP/IP.
Utiliza tópicos hierárquicos para organizar mensagens.
Mensagens são publicadas no tópico configurado, por exemplo, /detector/chuva/leituras.
Qualidade de Serviço (QoS): Configurado para QoS 0 (entrega de mensagens sem confirmação) para otimizar a velocidade da transmissão.
Detalhes do Payload:
Formato: JSON
Exemplo de mensagem publicada:
{
  "timestamp": "2024-11-30T10:15:00Z",
  "chuva_detectada": true,
  "valor_sensor": 275
}
Módulos de Comunicação
ESP8266 Wi-Fi:

Protocolo: IEEE 802.11 b/g/n
Frequência de operação: 2.4 GHz
Segurança: WPA2 para criptografia de dados na rede.
MQTT Client:

Biblioteca usada: PubSubClient.
Configuração básica:
Broker: mqtt.thingspeak.com
Porta: 1883 (não segura) ou 8883 (com TLS).
Credenciais: API_KEY fornecida pelo serviço.
Sensor de Dados:

Dados do sensor analógico são convertidos em valores digitais pelo ESP8266.
Periodicidade: Dados são enviados a cada 5 segundos para o broker MQTT.
Plataformas de Visualização:

ThingSpeak:
Interface gráfica que exibe gráficos em tempo real com os dados do sensor.
Configurado para interpretar os tópicos e processar os valores recebidos.
Fluxo de Comunicação
O ESP8266 se conecta à rede Wi-Fi configurada.
Ao estabelecer a conexão, o ESP8266 autentica-se com o broker MQTT usando a chave de API.
O ESP8266 publica os dados do sensor no tópico MQTT.
O broker redistribui as mensagens para os clientes conectados (subscritores).
A interface do ThingSpeak exibe os dados processados, permitindo a visualização em tempo real.
Conclusão
A implementação do protocolo MQTT garantiu um sistema de comunicação robusto, leve e eficiente. A escolha do ESP8266 como publicador e do ThingSpeak como interface para exibição dos dados simplificou o desenvolvimento e a integração, tornando o projeto escalável para futuras melhorias, como envio de alertas e controle remoto de atuadores.
