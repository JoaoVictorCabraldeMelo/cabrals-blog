---
title: "Como criar seu banco MySQL em um Docker"
date: 2023-05-07T19:17:17-03:00
draft: false
description: "Post"
categories: ["dev"]
tags: ["DevOps", "Banco de Dados", "MySQL"]
---

Primeiro você já parou para pensar que lindo seria se pudéssemos usar um banco de qualquer versão sem ter que necessariamente instalar ele!:hushed_face:

Bem com o **_Docker_** podemos fazer justamente isso e muito mais! Aqui neste artigo em específico vou mostrar um jeito simples de iniciar um banco local para você testar com suas aplicações rodando localmente.

Então vou primeiro explicar em uma frase o que é **_Docker_**:

{{< lead >}}
**Docker é uma tecnologia que facilita rodar e distribuir aplicações e pacotes de forma consistente em um ambiente isolado.**
{{< /lead >}}

Agora dado sua introdução vamos ao passo-a-passo de como instalar **_Docker_** na sua máquina, vou assumir aqui que você esteja usando **_Windows_**. Caso contrário você precisa usar o comando do seu gerenciador de pacotes do seu **Linux** em questão, por exemplo em um sistema baseado em **Debian** tipo o **Ubuntu** você só precisa rodar o seguinte comando:

{{< alert >}}
**Cuidado!** Este comando não instala a última versão do **_Docker_** apenas a versão disponível pelo seu repositório Ubuntu.
{{< /alert >}}

```bash
sudo apt update && sudo apt install docker.io -y
```

Agora sem mais demoras vamos-lá:

## 1. Instalar o **_Docker_** :

Para isso garanta que você tenha o **WSL2** instalado na sua máquina.
Em seguida você só precisa clicar nesse botão que vai instalar o executável.

{{< button href="https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe" target="_self" >}}
Instalar Docker no Windows
{{< /button >}}

Após executar todos os passos do instalador você deve ter o 
**_Docker Desktop_** dessa maneira no seu computador:

![Docker](img/docker.png "Docker Desktop")

Ao abrir o aplicativo ele deve introduzir a um tutorial introdutório. Em seguida, você pode abrir seu **_Prompt_** ou 
**_Powershell_** do seu **_Windows_** e ver se sua linha de comando (CLI) já está ativa com:

```bash
docker --version
```

Se retornou com sua versão, quer dizer que você finalizou a instalação, agora é seguir para o **_MySQL_**. :dolphin:

## 2. Instalando a Imagem do MySQL

Em resumo, o seguinte comando que pode se executado em qualquer terminal está nomeando o **_container_** de **_mysql_**, expondo a porta 3306 que é a porta padrão do banco para porta 3306 local, colocando a senha raiz no banco, criando um volume para persitir os dados caso pare o **_container_** de rodar, rodando o **_container_** como plano de fundo e criando um **_container_** com base na última imagem do **_mysql_** no **Dockerhub**.

```bash
docker run --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=<SUA_SENHA> -v mysql:/var/lib/mysql -d mysql:latest
```

## 3. Testando Conexão

Neste caso vou usar o [MySQLWorkbench](https://www.mysql.com/products/workbench/) para demonstrar que estamos conectando com o banco local no **_container_** sem nenhum problema.

Agora clicando em **Connections** na tela inicial deve aparecer uma tela pedindo o nome da conexão, normalmente para banco dou o nome do meu de LocalDB, depois ele vai pedir a senha raiz que colocamos no comando **_Docker_** em **_Store in Vault_**. Terminado isso só clicar em **_Test Connection_** que está tudo certo.

:smiling_face_with_smiling_eyes:

![MySQLConnection](img/mysql.png "Conexão MySQL")

## Conclusão

Rodar um banco em **_Docker_** é bem simples e vai te salvar uma grande dor de cabeça de instala-lo em seu computador localmente.
