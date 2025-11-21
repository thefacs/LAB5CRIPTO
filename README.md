#  Lab 5 — SSH, OpenSSH y Captura de Tráfico en Docker

**Autor:** Felipe Cuevas  
**Fecha:** Noviembre 2025  
**Correo:** felipe.cuevas1@mail.udp.cl  

---

Este laboratorio utiliza múltiples contenedores Docker para analizar el comportamiento del protocolo SSH durante su fase inicial (Protocol String, KEI, HASSH).  
Se levantaron clientes con distintas versiones de Ubuntu/OpenSSH y un servidor S1 para comparar el tráfico generado y replicar la captura del informante.

---

##  Estructura del proyecto

```
lab5/
│── C1/
│   └── Dockerfile
│── C2/
│   └── Dockerfile
│── C3/
│   └── Dockerfile
│── C4_S1/
│   └── Dockerfile
└── README.md
```

---

##  Levantamiento del servidor S1

```bash
docker build -t s1:latest S1/
docker run -d --name S1 -p 2222:22 s1:latest
```

Crear usuario de pruebas:

```bash
docker exec -it S1 /bin/bash
useradd -m prueba
echo "prueba:prueba" | chpasswd
exit
```

---

## Levantamiento de los clientes (C1–C4)

### C1 (Ubuntu 16.10 — OpenSSH 7.3p1)
```bash
docker build -t c1:latest C1/
docker run -d --name C1 c1:latest sleep infinity
```

### C2 (Ubuntu 18.10 — OpenSSH 7.7p1)
```bash
docker build -t c2:latest C2/
docker run -d --name C2 c2:latest sleep infinity
```

### C3 (Ubuntu 20.10 — OpenSSH 8.3p1)
```bash
docker build -t c3:latest C3/
docker run -d --name C3 c3:latest sleep infinity
```

### C4 (Ubuntu 22.10 — OpenSSH 9.0p1)
```bash
docker build -t c4:latest C4_S1/
docker run -d --name C4 c4:latest sleep infinity
```

---

## Generación del tráfico SSH

Acceso a un cliente:

```bash
docker exec -it C1 /bin/bash
```

Conexión SSH al servidor:

```bash
ssh prueba@172.17.0.1 -p 2222
```

Captura en el host (Wireshark):

```
tcp.port == 2222
```

---

##  Resultado

- Se identificó que el cliente que replica el tráfico del informante es **C3 (OpenSSH 8.3p1)**.
- Se analizó el KEI, HASSH y el comportamiento del protocolo SSH.
- Se comprobó que **no es posible generar un KEI menor a 300 bytes** en OpenSSH.

---
