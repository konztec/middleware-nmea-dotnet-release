# Middleware NMEA - S.IoT

Middleware de integração de NMEA para SIOT padrão MQTT.

[Codecs NMEA](https://gpsd.gitlab.io/gpsd/NMEA.html) disponíveis até a versão atual `v1.3.0` e suas propriedades/tipo de variável:
   - `GGA` ***Global Positioning System Fix Data***
      - FixTime *TimeSpan*
      - Latitude *Float*
      - Longitude *Float*
      - NumberOfSatellites *Int*
      - HorizontalDilution *Float*
      - AltitudeUnits *String*
      - FixQuality *Int* 
        - Invalid = 0
        - GpsFix = 1
        - DgpsFix = 2
        - PpsFix = 3
        - Rtk = 4
        - FloatRtk = 5
        - Estimated = 6
        - ManualInput = 7
        - Simulation = 8
      - Altitude *Float*
      - HeightOfGeoId *Float*
      - HeightOfGeoIdUnits *String*
      - TimeSpanSinceDgpsUpdate *Int*
      - DgpsStationId *Int*
   - `HDT` ***Heading - True***
      - Heading *Float*
   - `VTG` ***Track made good and Ground speed***
      - TrackTrue *Float*
      - TrackMagnetic *Float*
      - SpeedKnots *Float*
      - SpeedKmph *Float*
      - FaaMode  *String*
   - `DBK` ***Depth Below Keel***
      - DepthFeet *Float*
      - DepthMeters *Float*
      - DepthFathoms *Float*   
   - `DBS` ***Depth Below Surface***
      - DepthFeet *Float*
      - DepthMeters *Float*
      - DepthFathoms *Float*
   - `DBT` ***Depth below transducer***
      - DepthFeet *Float*
      - DepthMeters *Float*
      - DepthFathoms *Float*
   - `DPT` ***Depth of Water***
      - Depth *Float*
      - OffsetTransducer *Float*
      - MaximumRangeScale *Float*
   - `GLL` ***Geographic Position - Latitude/Longitude***
      - Latitude *Float*
      - Longitude *Float*
      - Time *TimeSpan*
      - Status *String*
      - FaaMode *String*
   - `GSA` ***Active satellites and dilution of precision***
      - SelectionMode *Int*
        - Auto = 0
        - Manual = 1
      - FixMode *Int*
        - NotAvailable = 1
        - Fix2D = 2
        - Fix3D = 3
      - SatelliteIDs *Int[]*
      - Pdop *Float*
      - Hdop *Float*
      - Vdop *Float*
   - `MTW` ***Mean Temperature of Water***
      - Degrees *Float*
      - UnitMeasurement *String*
   - `MWD` ***Wind Direction***
      - WindAngleTrue *Float*
      - WindAngleMagnetic *Float*
      - SpeedKnots *Float*
      - SpeedMps *Float*
   - `MWV` ***Wind Speed and Angle***
      - WindAngle *Float*
      - Speed *Float*
      - Reference *Int*
        - Relative = 0
        - True = 1
      - Units *String* *(K = km/hr, M = m/s, N = knots, S = statute)*
      - Status *Int*
        - Valid = 0
        - Invalid = 1
   - `RMC` ***Recommended Minimum Navigation Information***
      - DateTime *DateTime*
      - Status *String*
      - Latitude *Float*
      - Longitude *Float*
      - SpeedKnots *Float*
      - TrackTrue *Float*
      - Variation *Float*
      - VariationPole *String* *(E or W)*
      - FaaMode *String*
   - `RPM` ***Revolutions***
      - Source *Int*
        - Shaft = 0
        - Engine = 1
      - SourceValue *Float*
      - SpeedMinute *Float*
      - PropellerPitch *Float*
      - Status *Int*
        - Valid = 0
        - Invalid = 1
   - `VHW` ***Water speed and heading***
      - DegreesTrue *Float*
      - DegreesMagnetic *Float*
      - SpeedKnots *Float*
      - SpeedKmph *Float*
   - `ZDA` ***Time & Date - UTC, day, month, year and local time zone***
      - DateTime *DateTime*
      - LocalZoneHours *Int*
      - LocalZoneMinutes *Int*

### Instalação execução

Necessário instalar [.NET 5](https://dotnet.microsoft.com/download/dotnet/5.0)


Realizar o download da última versão do [Middleware.NMEA](https://github.com/konztec/middleware-nmea-dotnet-release/releases/download/v1.3.0/Middleware.NMEA.1.3.0.zip)

Extrair os arquivos compactados em um diretório.

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
  },
  "IntervalSend": 10000 // Intervalo para envio dos sinais de NMEA para o SIoT
}
```

Copiar `config.example.json` para `config.json` e configurar
```sh
$ cp config.example.json config.json
```

Verifique a documentação do [cadastro e geração de token no SIoT](https://blog.konztec.com/cadastro-maquina-token-integracao-siot/) para gerar os valores do token e idMachine
```
{ 
  "idMachine": "maquina1", // ID da máquina no SIoT
  "token": "token", // Token da máquina no SIoT 
  "items": [
    {
      "sentenceId": "MTW", // Tipo de setença NMEA (Utilizar as listadas acima)
      "sensorId": "temperatura_agua", // ID do sensor no SIoT
      "signals": [
        {
          "signalId": "atual", // ID do sinal no SIoT
          "packet": "Degrees" // Propriedade da setença NMEA  (Utilizar a propriedade das sentenças listadas acima)
        }
      ]
    }
  ]
}
```

<br/>
<br/>

 Mais informações e integrações com S.IoT, acessando [Blog Documentações](https://blog.konztec.com/documentacao)

 Conheça o S.IoT, acessando [S.IoT](https://www.konztec.com/)