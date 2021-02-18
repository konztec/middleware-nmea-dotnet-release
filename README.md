# Middleware NMEA - S.IoT

Middleware de integração de NMEA para SIOT padrão MQTT.

[Codecs NMEA](https://gpsd.gitlab.io/gpsd/NMEA.html) disponíveis:
   - `GGA`
   - `HDT`
   - `VTG`


### Instalação execução

Necessário instalar [.NET 5](https://dotnet.microsoft.com/download/dotnet/5.0)


Realizar o download da última versão do `Middleware.NMEA`

Extrair os arquivos compactados em um diretório.

Copiar `config.example.json` para `config.json` e configurar
```sh
$ cp config.example.json config.json
```

Configurar as váriaveis do ambiente no `appsettings.json`