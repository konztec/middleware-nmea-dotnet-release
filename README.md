# Middleware NMEA - S.IoT

Middleware de integração de NMEA para SIOT padrão MQTT.

[Codecs NMEA](https://gpsd.gitlab.io/gpsd/NMEA.html) disponíveis até a versão atual `v1.1.0`:
   - `GGA`
   - `HDT`
   - `VTG`
   - `DBK`
   - `DBS`
   - `DBT`
   - `DPT`
   - `GLL`
   - `GSA`
   - `MTW`
   - `MWD`
   - `RMC`
   - `RPM`
   - `VHW`
   - `ZDA`

### Instalação execução

Necessário instalar [.NET 5](https://dotnet.microsoft.com/download/dotnet/5.0)


Realizar o download da última versão do [Middleware.NMEA](https://github.com/konztec/middleware-nmea-dotnet-release/releases/download/v1.1.0/Middleware.NMEA.1.1.0.zip)

Extrair os arquivos compactados em um diretório.

Copiar `config.example.json` para `config.json` e configurar
```sh
$ cp config.example.json config.json
```

Configurar as váriaveis do ambiente no `appsettings.json`
```
{
  "NMEA": { // configurações de conexão com o NMEA
    "Mode": "SERIAL", // modo de conexão (utilizar SERIAL ou TCP)
    "Serial": { // configurações para o modo SERIAL, informar apenas se o `Mode: SERIAL`
      "Port": "COM2", // Serial Port
      "Baudrate": 9600 // Baudrate
    },
    "TCP": { // configurações para o modo TCP, informar apenas se o `Mode: TCP`
      "Endpoint": "localhost", // Endpoint TCP
      "Port": 3000 // Porta TCP
    }
  },
  "MQTT": { // configurações da conexão MQTT para envio dos sinais para o broker do SIoT
    "Endpoint": "siot-broker-mqtt-dev.konztec.com.br", // endpoint do MQTT
    "Port": 8883, // porta MQTT
    "TLS": true // utiliza SSL/TLS (true ou false)
  },
  "BUFFER": { // configurações do buffer de sinais
    "CronSend": "0/30 * * * * ?", // intervalo de tempo no formato CRON para verificar o buffer e enviar os sinais
    "TotalFiles": 10000 // limite de arquivos a serem enviados no intervalo
  }
}
```

<br/>
<br/>

 Mais informações e integrações com S.IoT, acesse [Blog Documentações](https://blog.konztec.com/documentacao)

 Conheça o S.IoT, acesse [S.IoT](https://www.konztec.com/)