# Middleware NMEA - S.IoT

Middleware de integração de NMEA para SIOT padrão MQTT.

[Codecs NMEA](https://gpsd.gitlab.io/gpsd/NMEA.html) disponíveis até a versão atual `v1.0.0`:
   - `GGA`
   - `HDT`
   - `VTG`


### Instalação execução

Necessário instalar [.NET 5](https://dotnet.microsoft.com/download/dotnet/5.0)


Realizar o download da última versão do [Middleware.NMEA](https://github.com/konztec/middleware-nmea-dotnet-release/releases/download/1.0.0/Middleware.NMEA.1.0.0.zip)

Extrair os arquivos compactados em um diretório.

Copiar `config.example.json` para `config.json` e configurar
```sh
$ cp config.example.json config.json
```

Configurar as váriaveis do ambiente no `appsettings.json`

<br/>
<br/>

 Mais informações e integrações com S.IoT, acesse [Blog Documentações](https://blog.konztec.com/documentacao)

 Conheça o S.IoT, acesse [S.IoT](https://www.konztec.com/)