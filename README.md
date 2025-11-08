🤖 Controle de Acesso Inteligente com Foco em Eficiência Energética

Projeto Integrador - Engenharia da Computação 2

Este repositório contém o código-fonte e a documentação do protótipo de um sistema de controle de acesso RFID que também gerencia o consumo de energia de uma sala de aula, com o objetivo de reduzir o desperdício de energia elétrica.

🎯 Objetivo Principal:

O projeto demonstra como um sistema de controle de acesso pode ir além da segurança, tornando-se uma ferramenta de automação predial e eficiência energética.

O protótipo foi desenhado para simular o gerenciamento dos principais circuitos de energia de uma sala de aula (iluminação, ar-condicionado, projetores). A energia só é liberada quando um usuário autorizado entra na sala e é cortada automaticamente quando o ambiente não está em uso, evitando consumo desnecessário.

✨ Funcionalidades (Features):

1. Controle de Acesso: Validação de usuários via cartões/tags RFID (MFRC522);
2. Gestão de Energia: Acionamento de um Relé 5V (simulando a rede elétrica da sala) apenas para usuários autorizados;
3. Feedback Visual Unificado: Uso de um LED RGB para indicar o status do sistema:
  i - Azul: Ocioso (Aguardando cartão).
  ii - Verde: Acesso Liberado (Energia ligada).
  iii - Vermelho: Acesso Negado.
4. Atuadores Físicos: Controle de um Servo Motor (simulando uma cancela ou fechadura elétrica).
5. Relógio em Tempo Real (RTC): O sistema utiliza um módulo RTC DS1302 para registrar data/hora de cada acesso e permitir futuras lógicas de "horário de funcionamento".
6. Display de Status: Um LCD 16x2 exibe informações em tempo real:
  i - Modo Ocioso: Alterna entre o nome do projeto e o relógio (Data/Hora).
  ii - Modo de Ação: Exibe "Acesso Liberado" (com data/hora do evento) ou "Acesso Negado".
7. Ventoinha com Led integrado, simulando um sistema de arcondicionado.

📸 Protótipo em Ação:

Aqui é um ótimo lugar para colocar um GIF ou vídeo curto do protótipo funcionando.

(Ex: GIF mostrando a aproximação do cartão, o LED ficando verde, o servo girando e a ventoinha (cooler) ligando ao mesmo tempo)

Adicione também fotos do seu protótipo montado.

Display LCD

Placa Montada (Protoboard)

⚙️ Componentes Utilizados:

1x Arduino Uno;
1x Leitor RFID MFRC522 com cartão e tag;
1x Módulo Relé 5V (1 Canal) - Active HIGH;
1x Módulo LED RGB Cátodo Comum (HW-479);
1x Módulo RTC DS1302 (com bateria);
1x Display LCD I2C 16x2 com módulo I2C integrado;
1x Micro Servo 9g (SG90);
1x Buzzer Ativo;
1x Protoboard e Jumpers;
1x Fonte Externa 12V (para a carga);
1x Cooler (Ventoinha) 12V (simulando a carga).

🔌 Esquema de Ligação:

AUTODESK - Tinkercad: https://www.tinkercad.com/things/7d8Z6DJloJX-projeto-integrador-engenharia-da-computacao

🚀 Como Utilizar:

1. Bibliotecas Necessárias

Para compilar o código, você precisará das seguintes bibliotecas na sua IDE Arduino:

SPI.h (Nativa da IDE)
MFRC522 (por GitHubCommunity)
Servo.h (Nativa da IDE)
Wire.h (Nativa da IDE)
LiquidCrystal_I2C (por Frank de Brabander)
RtcDS1302 (por Makuna)
2. Configurando o Código
Ajustar o Relógio (RTC)

Na primeira vez que carregar o código, você deve acertar o relógio:

=> No arquivo .ino, localize a função setup(), descomente a linha: // Rtc.SetDateTime(RtcDateTime(2025, 11, 7, 11, 45, 0)).
=> Altere para a data e hora atuais (Ano, Mês, Dia, Hora, Minuto, Segundo). 
=> Faça o upload do código.
=>Comente a linha novamente e faça o upload mais uma vez. (Se não fizer isso, o relógio será reiniciado toda vez que o Arduino ligar).

Adicionar seus Cartões (UIDs):

=> Abra o Monitor Serial (9600 baud).
=> Aproxime um cartão que você deseja adicionar. O monitor serial mostrará o UID dele (ex: "UID lido: 91 42 91 04").
=> Copie esse UID.
=> No código, encontre o loop() e adicione o UID à condição de acesso liberado, conforme exemplo a seguir:

// UIDs Permitidos: (Adicione o seu aqui)
if (uid == "91 42 91 04" || uid == "77 E7 7B 05" || uid == "SEU_NOVO_UID_AQUI")
{
  // ... Acesso Liberado ...
}


🧠 Melhorias Futuras (Próximos Passos)

Este protótipo é a base para um sistema completo. As próximas etapas com foco em economia incluem:

[ ] Adicionar Sensor de Presença (PIR): Manter a energia ligada (Relé) apenas se o PIR detectar movimento, desligando automaticamente após X minutos de ociosidade, mesmo que a pessoa não tenha "saído" (passado o cartão).
[ ] Adicionar Sensor de Luminosidade (LDR): Ligar o circuito de lâmpadas (simulado por um 2º Relé ou LED) apenas se a sala estiver escura.
[ ] Adicionar Sensor de Temperatura (DHT11): Ligar o ar-condicionado (Relé principal) apenas se a temperatura estiver acima de um limite (ex: 23°C).
[ ] Migrar para ESP32/ESP8266: Adicionar conectividade Wi-Fi para logs na nuvem, dashboard de monitoramento e agendamento de horários de funcionamento via web.

👨‍💻 Autores

1. BENÍZIO LÁZARO JÚNIOR;
2. IAGO CAVALCANTE DEORCE OLIVEIRA;
3. RAZIEL LUCAS MARCOS FERREIRA;
4. ROBERLI SCHUINA SILVA, 
5. VÍTOR LUCAS MIGUEL MASCARENHAS.

📄 Licença

Este projeto está sob a licença MIT - veja o arquivo LICENSE para detalhes.
