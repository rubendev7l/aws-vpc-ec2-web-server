# ☁️ AWS re/Start Lab | Build a VPC and Deploy a Web Server

<p align="center">

<img src="assets/banner.png" width="100%">

</p>

<p align="center">

Laboratório desenvolvido durante a formação <strong>AWS re/Start</strong>, oferecida pela <strong>Escola da Nuvem</strong>, documentando a criação de uma infraestrutura completa na AWS com implantação automática de um servidor web utilizando Amazon EC2.

</p>

---

# 🚀 Sobre o Projeto

Este repositório documenta um laboratório prático realizado durante a formação **AWS re/Start**, da **Escola da Nuvem**.

Mais do que executar o laboratório, o objetivo foi compreender cada recurso utilizado, registrar todas as etapas da implantação e documentar a resolução dos problemas encontrados durante a execução.

Durante o desenvolvimento foi necessário adaptar parte do laboratório devido às mudanças do **Amazon Linux 2023**, utilizando análise de logs do sistema para identificar e corrigir o problema.

Toda a documentação foi reorganizada em formato de guia para facilitar futuras consultas e auxiliar outros estudantes.

---

# 🎯 Objetivos

✔ Criar uma Amazon VPC

✔ Criar sub-redes públicas e privadas

✔ Configurar Internet Gateway

✔ Configurar Route Tables

✔ Criar Security Groups

✔ Provisionar uma instância Amazon EC2

✔ Automatizar a instalação do Apache utilizando User Data

✔ Publicar uma aplicação Web

✔ Diagnosticar problemas utilizando logs do sistema

---

# 🏗 Arquitetura

<p align="center">

<img src="images/architecture.png">

</p>

---

# 🛠 Tech Stack

<p align="center">

<img src="https://skillicons.dev/icons?i=linux,bash,github"/>

</p>

<p align="center">

<img src="https://img.shields.io/badge/AWS-VPC-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white">

<img src="https://img.shields.io/badge/AWS-EC2-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white">

<img src="https://img.shields.io/badge/Amazon%20Linux-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white">

<img src="https://img.shields.io/badge/Apache-CA2134?style=for-the-badge&logo=apache&logoColor=white">

<img src="https://img.shields.io/badge/Bash-121011?style=for-the-badge&logo=gnubash&logoColor=white">

<img src="https://img.shields.io/badge/Cloud-Computing-0A66C2?style=for-the-badge">

<img src="https://img.shields.io/badge/Infrastructure-as%20Code-Learning-blue?style=for-the-badge">

</p>

---

# ☁️ Serviços AWS utilizados

| Serviço | Finalidade |
|----------|------------|
| Amazon VPC | Rede privada virtual |
| Amazon EC2 | Máquina virtual Linux |
| Internet Gateway | Comunicação com Internet |
| Route Tables | Roteamento |
| Security Groups | Firewall |
| Amazon Linux 2023 | Sistema Operacional |
| Apache HTTP Server | Servidor Web |

---

# 📂 Estrutura da Infraestrutura

```text
Internet
     │
     ▼
Internet Gateway
     │
     ▼
Public Route Table
     │
     ▼
Public Subnet
     │
     ▼
Amazon EC2
     │
     ▼
Apache HTTP Server
     │
     ▼
Website
```

---

# ⚙️ User Data utilizado

```bash
#!/bin/bash

dnf install -y httpd php wget unzip

systemctl enable httpd
systemctl start httpd

wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-100-RESTRT-1/267-lab-NF-build-vpc-web-server/s3/lab-app.zip

unzip lab-app.zip -d /var/www/html/
```

---

# 📸 Evidências

## Amazon VPC

<img src="images/vpc.png"> 
<img width="1024" height="469" alt="image" src="https://github.com/user-attachments/assets/2eef6bfa-c084-4101-a4b5-839a6970558f" />


---

## Security Group

<img src="images/security-group.png">

---

## Amazon EC2

<img src="images/ec2-running.png">

---

## Servidor Web

<img src="images/apache-homepage.png">

---

# 🔍 Troubleshooting

Durante a execução do laboratório foi identificado que o script disponibilizado originalmente pela AWS não era totalmente compatível com a versão atual do Amazon Linux.

Ao invés de apenas substituir comandos por tentativa e erro, foi realizado um processo de investigação utilizando os próprios logs da instância.

## Processo de investigação

### 1️⃣ Verificação do serviço

```bash
systemctl status httpd
```

Resultado:

```text
Unit httpd.service could not be found.
```

---

### 2️⃣ Investigação do Cloud-Init

```bash
sudo cat /var/log/cloud-init-output.log
```

Esse log mostrou que o script enviado pelo User Data não havia sido executado corretamente.

---

### 3️⃣ Validação do User Data

```bash
sudo cat /var/lib/cloud/instance/user-data.txt
```

Com essa validação foi possível confirmar o conteúdo realmente recebido pela instância.

---

### 4️⃣ Correção

Foi realizada a adaptação do script para o Amazon Linux 2023 utilizando:

- dnf
- systemctl
- instalação correta do Apache
- inicialização automática do serviço

---

## Resultado

✔ Apache instalado

✔ Serviço iniciado

✔ Página publicada

✔ Instância acessível via navegador

---

# 💡 Principais Aprendizados

Durante este laboratório foram praticados conceitos importantes de Cloud Computing:

- Planejamento de redes na AWS
- CIDR e Sub-redes
- Internet Gateway
- Route Tables
- Security Groups
- Amazon EC2
- Apache HTTP Server
- Amazon Linux 2023
- User Data
- Cloud-Init
- Diagnóstico através de logs
- Troubleshooting em ambientes Cloud

---

# 📚 Documentação

Este repositório possui uma documentação própria criada durante os estudos contendo:

- Passo a passo completo
- Configurações realizadas
- Capturas de tela
- Problemas encontrados
- Soluções adotadas
- Observações para versões atuais da AWS

O objetivo é servir como material de revisão e também auxiliar outros estudantes da formação AWS re/Start.

---

# ⭐ Destaque Técnico

O maior aprendizado deste laboratório não foi apenas provisionar a infraestrutura, mas compreender como diagnosticar falhas em um ambiente Linux na AWS.

A análise dos logs gerados pelo **Cloud-Init** permitiu identificar rapidamente a origem do problema, validar o User Data executado pela instância e adaptar o script para a versão atual do Amazon Linux.

Essa experiência reforçou a importância da investigação baseada em evidências, prática essencial para profissionais de Cloud Computing, Infraestrutura e DevOps.

---

# 👨‍💻 Autor

**Ruben Neto**

🎓 Tecnólogo em Análise e Desenvolvimento de Sistemas

☁️ Estudante da formação AWS re/Start — Escola da Nuvem

🎨 Designer Gráfico em transição para Cloud Computing

📍 Minas Gerais - Brasil

---

## ⭐ Se este material foi útil

Considere deixar uma ⭐ no repositório.
