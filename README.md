# Diana-Sahian-Quinonez-Yanez-Iot-Stack

# Sistemas Programables
### Alumna: Diana Sahian Quinonez Yanez
## No. Control: 22211637
### Practica Iot Stack

1. Captura de pantalla del panel de administración de Tailscale mostrando el nodo dashboard-server.
![Descripción de la imagen](https://github.com/DiSahian/Diana-Sahian-Quinonez-Yanez-Iot-Stack/blob/b15e326bd1cbcab03da0a89f93ad9695a677e604/SS/Imagen%20de%20WhatsApp%202025-09-24%20a%20las%2023.14.29_44e1f4ed.jpg)

3. Dashboard de Grafana donde se visualicen los datos de InfluxDB y las métricas de Prometheus.
![Descripción de la imagen](https://github.com/DiSahian/Diana-Sahian-Quinonez-Yanez-Iot-Stack/blob/b15e326bd1cbcab03da0a89f93ad9695a677e604/SS/Imagen%20de%20WhatsApp%202025-09-25%20a%20las%2000.17.00_dde0e24d.jpg)
![Descripción de la imagen](https://github.com/DiSahian/Diana-Sahian-Quinonez-Yanez-Iot-Stack/blob/b15e326bd1cbcab03da0a89f93ad9695a677e604/SS/Imagen%20de%20WhatsApp%202025-09-24%20a%20las%2023.38.52_2b99b394.jpg)
![Descripción de la imagen](https://github.com/DiSahian/Diana-Sahian-Quinonez-Yanez-Iot-Stack/blob/b15e326bd1cbcab03da0a89f93ad9695a677e604/SS/Imagen%20de%20WhatsApp%202025-09-24%20a%20las%2023.39.03_54e3aae5.jpg)
![Descripción de la imagen](https://github.com/DiSahian/Diana-Sahian-Quinonez-Yanez-Iot-Stack/blob/b15e326bd1cbcab03da0a89f93ad9695a677e604/SS/Imagen%20de%20WhatsApp%202025-09-24%20a%20las%2023.39.15_4cdfc4ff.jpg)

4. Código Python utilizado para la simulación de datos.
```python
from datetime import datetime
import random
import time
from influxdb_client import InfluxDBClient, Point, WritePrecision

token = "3KJoO7ml0213OBLmfp6x_eeuRkdfWpcjilr0BB0GgMPLlUjeKrl-HCyptUflMoMOBvdAjXg6IMTNOvq3M_NNoA=="
org = "iot-lab"
bucket = "sensores"

client = InfluxDBClient(url="http://localhost:8086", token=token, org=org)
write_api = client.write_api()

while True:
    temp = random.uniform(18, 30)
    hum = random.uniform(40, 70)
    point = (
        Point("ambiente")
        .tag("ubicacion", "laboratorio")
        .field("temperatura", temp)
        .field("humedad", hum)
        .time(datetime.utcnow(), WritePrecision.NS)
    )
    write_api.write(bucket=bucket, record=point)
    print(f"Enviado: temp={temp:.2f}, hum={hum:.2f}")
    time.sleep(5)
```
5. Explicación escrita que conteste:

¿Por qué es útil Tailscale en este escenario? (responde que permite conectar nodos mediante VPN sin exponer puertos públicos): Me permite conectar EC2, PC y Celular en una VPN sin exponer las IPs en internet
Diferencia entre las métricas de IoT (InfluxDB) y las métricas de sistema (Prometheus/Node Exporter): Es mucho mejor la vista desde InfluxDB en mi opinión
