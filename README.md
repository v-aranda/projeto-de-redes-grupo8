# Projeto Final de Fundamentos de Redes - Grupo 8

## Secao 1: Identificacao

| Item | Informacao |
| --- | --- |
| Instituicao | Instituto Federal de Alagoas - IFAL |
| Curso/Turma | Bacharelado em Sistemas de Informacao - BSI 2026.1 |
| Disciplina | Fundamentos de Redes de Computadores |
| Professor | PENDENTE: preencher nome do professor |
| Grupo | 8 |
| Repositorio GitHub | <https://github.com/v-aranda/projeto-de-redes-grupo8> |
| Drive com .OVA | <https://drive.google.com/drive/folders/1ucorBAdl78kvFctQbuMzVcrS2Cc-R316?usp=sharing> |

### Integrantes do grupo

| Nome completo | Usuario adotado no Linux |
| --- | --- |
| Ronalde Kelvyn Santos de Omena | `ronalde.omena` |
| Edgar de Oliveira Pereira | `edgar.pereira` |
| Vinicius Aranda Lima da Silva | `vinicius.aranda` |
| Luiz Arthur Lisboa Cirilo Torres | `luiz.torres` |

> Observacao: os nomes de usuario seguem o formato em letras minusculas, sem acentos e com separacao por ponto, conforme o padrao indicado nas aulas e na lista oficial da turma.

## Secao 2: Especificacoes de Hardware e Ambiente

O ambiente foi planejado com 8 maquinas virtuais Ubuntu Server no Oracle VM VirtualBox. As VMs foram criadas como servidores independentes para o projeto final e conectadas em rede interna.

| Item | Valor |
| --- | --- |
| Sistema operacional | Ubuntu Server |
| Hipervisor | Oracle VM VirtualBox |
| Tipo de rede no VirtualBox | Rede Interna |
| Nome da rede interna | `labredes-grupo8` |
| Interface de rede nas VMs | `enp0s3` |
| Tipo de disco | VDI dinamico |

### Hardware das maquinas virtuais

| VM | RAM | CPU/Cores | Disco virtual | Disco em uso aproximado | Sistema operacional |
| --- | --- | --- | --- | --- | --- |
| `srv01` | 2048 MB | 1 vCPU | 25 GB | 6,6 GB | Ubuntu Server |
| `srv02` | 2048 MB | 1 vCPU | 25 GB | 6,6 GB | Ubuntu Server |
| `srv03` | 2048 MB | 1 vCPU | 25 GB | 6,6 GB | Ubuntu Server |
| `srv04` | 2048 MB | 1 vCPU | 25 GB | 6,6 GB | Ubuntu Server |
| `srv05` | 2048 MB | 1 vCPU | 25 GB | 6,6 GB | Ubuntu Server |
| `srv06` | 2048 MB | 1 vCPU | 25 GB | 6,6 GB | Ubuntu Server |
| `srv07` | 2048 MB | 1 vCPU | 25 GB | 6,6 GB | Ubuntu Server |
| `srv08` | 2048 MB | 1 vCPU | 25 GB | 6,6 GB | Ubuntu Server |

## Secao 3: Redes, IPs e Dominios

A turma `bsi-26-1` utiliza a rede `192.168.26.0/24`. Para o Grupo 8, foi utilizada a sub-rede `192.168.26.112/28`, com mascara `255.255.255.240`.

| Item | Valor |
| --- | --- |
| Rede da turma | `192.168.26.0/24` |
| Sub-rede do Grupo 8 | `192.168.26.112/28` |
| Mascara | `255.255.255.240` |
| Endereco de rede | `192.168.26.112` |
| Enderecos utilizaveis | `192.168.26.113` a `192.168.26.126` |
| Broadcast | `192.168.26.127` |
| Dominio do grupo | `grupo8.bsi-26-1.maceio.lab` |

### Tabela de enderecamento

| VM | Hostname | FQDN | Alias | Endereco IP | Mascara |
| --- | --- | --- | --- | --- | --- |
| `srv01` | `srv01` | `srv01.grupo8.bsi-26-1.maceio.lab` | `srv01` | `192.168.26.113` | `/28` |
| `srv02` | `srv02` | `srv02.grupo8.bsi-26-1.maceio.lab` | `srv02` | `192.168.26.114` | `/28` |
| `srv03` | `srv03` | `srv03.grupo8.bsi-26-1.maceio.lab` | `srv03` | `192.168.26.115` | `/28` |
| `srv04` | `srv04` | `srv04.grupo8.bsi-26-1.maceio.lab` | `srv04` | `192.168.26.116` | `/28` |
| `srv05` | `srv05` | `srv05.grupo8.bsi-26-1.maceio.lab` | `srv05` | `192.168.26.117` | `/28` |
| `srv06` | `srv06` | `srv06.grupo8.bsi-26-1.maceio.lab` | `srv06` | `192.168.26.118` | `/28` |
| `srv07` | `srv07` | `srv07.grupo8.bsi-26-1.maceio.lab` | `srv07` | `192.168.26.119` | `/28` |
| `srv08` | `srv08` | `srv08.grupo8.bsi-26-1.maceio.lab` | `srv08` | `192.168.26.120` | `/28` |

### Configuracao de hostname
<img width="300" height="70" alt="image" src="https://github.com/user-attachments/assets/e35f2a67-ca29-4d01-831d-0be90cded215" />

Cada maquina recebeu seu hostname completo com `hostnamectl`. Exemplo:

```bash
sudo hostnamectl set-hostname srv01.grupo8.bsi-26-1.maceio.lab
hostnamectl
hostname -f
```

O mesmo padrao foi aplicado de `srv01` ate `srv08`, alterando apenas o numero do servidor.

### Configuracao de rede com Netplan
<img width="843" height="184" alt="image" src="https://github.com/user-attachments/assets/c0690064-8c3f-41d8-b852-b7aa153096cc" />


Exemplo da configuracao da `srv01`:

```yaml
network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: false
      addresses:
        - 192.168.26.113/28
```

Em cada VM, o endereco foi alterado conforme a tabela de enderecamento.

Comandos de aplicacao e validacao:

```bash
sudo netplan apply
ip addr show enp0s3
```

### Arquivo `/etc/hosts`

<img width="793" height="346" alt="image" src="https://github.com/user-attachments/assets/a8dd4360-821f-4810-8031-294bf668529b" />


O mapeamento abaixo deve estar presente no arquivo `/etc/hosts` de todas as VMs:

```text
192.168.26.113 srv01.grupo8.bsi-26-1.maceio.lab srv01
192.168.26.114 srv02.grupo8.bsi-26-1.maceio.lab srv02
192.168.26.115 srv03.grupo8.bsi-26-1.maceio.lab srv03
192.168.26.116 srv04.grupo8.bsi-26-1.maceio.lab srv04
192.168.26.117 srv05.grupo8.bsi-26-1.maceio.lab srv05
192.168.26.118 srv06.grupo8.bsi-26-1.maceio.lab srv06
192.168.26.119 srv07.grupo8.bsi-26-1.maceio.lab srv07
192.168.26.120 srv08.grupo8.bsi-26-1.maceio.lab srv08
```

Comandos de verificacao:

```bash
getent hosts srv01
getent hosts srv08.grupo8.bsi-26-1.maceio.lab
```

## Secao 4: Usuarios e Acessos

Cada VM deve conter o usuario administrador padrao das aulas e os usuarios individuais dos integrantes do grupo.

### Usuario administrador

| Usuario | Senha | Tipo | Observacao |
| --- | --- | --- | --- |
| `administrador` | `adminifal` | Administrador com `sudo` | Padrao utilizado nas aulas |
| `super` | `1234` | `sudo` de criação | usuário definido na criação das VM's |

Comandos de criacao ou ajuste, quando necessario:

```bash
sudo adduser administrador
sudo usermod -aG sudo administrador
groups administrador
```

Para validar o acesso administrativo:

```bash
su - administrador
sudo whoami
```

O resultado esperado para `sudo whoami` e:

```text
root
```

### Usuarios dos integrantes

| Usuario | Integrante | Tipo |
| --- | --- | --- |
| `ronalde.kelvin` | Ronalde Kelvyn Santos de Omena | Usuario individual |
| `edgar.oliveira` | Edgar de Oliveira Pereira | Usuario individual |
| `vinicius.aranda` | Vinicius Aranda Lima da Silva | Usuario individual |
| `luiz.arthur` | Luiz Arthur Lisboa Cirilo Torres | Usuario individual |

Comandos usados para criacao dos usuarios individuais:

```bash
sudo adduser ronalde.omena
sudo adduser edgar.pereira
sudo adduser vinicius.aranda
sudo adduser luiz.torres
```

#### Comandos de verificacao:
<img width="770" height="198" alt="image" src="https://github.com/user-attachments/assets/b2b98d47-bf03-46a9-aae3-394432169bc3" />


```bash
id administrador
id ronalde.kelvin
id edgar.oliveira
id vinicius.aranda
id luiz.arthur
```

## Secao 5: Testes e Evidencias

Os testes devem validar comunicacao por IP, por FQDN e acesso SSH usando os usuarios criados. As saidas reais dos comandos devem ser registradas nesta secao ou anexadas como prints no repositorio.

### Testes de usuários
<img width="706" height="233" alt="image" src="https://github.com/user-attachments/assets/1b5fd2b1-1a49-4fad-866e-e7fccef9e7fc" />
<img width="693" height="66" alt="image" src="https://github.com/user-attachments/assets/4222712d-5ee0-4ab8-a359-33e349bf65f6" />
<img width="673" height="60" alt="image" src="https://github.com/user-attachments/assets/b29c3d61-5c36-48ea-8c57-92ba878dd8b0" />
<img width="675" height="63" alt="image" src="https://github.com/user-attachments/assets/9e6aedf4-09e0-4cea-bd97-0ce6faf59427" />
<img width="685" height="57" alt="image" src="https://github.com/user-attachments/assets/966fba50-feb4-4494-b2c9-a594e3fcf3c5" />
<img width="694" height="60" alt="image" src="https://github.com/user-attachments/assets/8053cea4-afdf-4c4a-97e8-0ca6cc2a4a33" />
<img width="680" height="61" alt="image" src="https://github.com/user-attachments/assets/b5efa772-2664-43fc-88a2-6d4d86daf697" />
<img width="686" height="65" alt="image" src="https://github.com/user-attachments/assets/aa43235a-d67f-4306-958c-c29855db1b16" />





### Testes de ping por IP
| Origem | Destino | Comando |
| --- | --- | --- |
| `srv02` | `srv01` | `ping -c 4 192.168.26.113` | 
| `srv02` | `srv08` | `ping -c 4 192.168.26.120` | 
| `srv03` | `srv02` | `ping -c 4 192.168.26.114` | 
| `srv03` | `srv07` | `ping -c 4 192.168.26.119` | 
| `srv04` | `srv03` | `ping -c 4 192.168.26.115` | 
| `srv04` | `srv06` | `ping -c 4 192.168.26.118` | 
| `srv05` | `srv04` | `ping -c 4 192.168.26.116` | 
| `srv05` | `srv08` | `ping -c 4 192.168.26.120` | 

#### Evidências
<img width="519" height="353" alt="image" src="https://github.com/user-attachments/assets/31341e5a-4525-48f2-ba1f-85d10cbc1b11" />
<img width="538" height="347" alt="image" src="https://github.com/user-attachments/assets/bf41ff11-da54-42ed-b1e9-2e0b19a15087" />
<img width="520" height="353" alt="image" src="https://github.com/user-attachments/assets/5ca9baa4-16ce-460f-8771-115ad38cdc5d" />
<img width="520" height="351" alt="image" src="https://github.com/user-attachments/assets/0544b7d5-bf9b-45c3-8135-e61f4dc64d25" />


### Testes de ping por hostname e FQDN
| Origem | Destino | Comando | 
| --- | --- | --- | 
| `srv01` | `srv02` | `ping -c 4 srv02` |
| `srv01` | `srv03` | `ping -c 4 srv03` | 
| `srv01` | `srv04` | `ping -c 4 srv04` | 
| `srv01` | `srv05` | `ping -c 4 srv05` | 
| `srv01` | `srv06` | `ping -c 4 srv06` |
| `srv01` | `srv07` | `ping -c 4 srv07` | 
| `srv01` | `srv08` | `ping -c 4 srv08` | 
| `srv08` | `srv01` | `ping -c 4 srv01` | 

#### Evidências
<img width="799" height="806" alt="image" src="https://github.com/user-attachments/assets/840c1d7e-2b75-431a-9044-be33e5f696ce" />
<img width="798" height="356" alt="image" src="https://github.com/user-attachments/assets/59af5dfa-bd3d-4a4d-b282-82864f4c80f6" />
<img width="796" height="199" alt="image" src="https://github.com/user-attachments/assets/ecaee773-594c-41f7-9f44-39dc1410c41b" />

### Testes de acesso SSH

| Origem | Destino | Usuario | Comando | 
| --- | --- | --- | --- | 
| `srv01` | `srv02` | `administrador` | `ssh administrador@srv02` | 
| `srv01` | `srv08` | `administrador` | `ssh srv08` | 
| `srv01` | `srv02` | `vinicius.aranda` | `ssh vinicius.aranda@192.168.26.114` | 
| `srv08` | `srv01` | `ronalde.kelvin` | `ssh ronalde.kelvin@srv01.grupo8.bsi-26-1.maceio.lab` |
| `srv03` | `srv07` | `edgar.pereira` | `ssh edgar.oliveira@srv04` | 
| `srv05` | `srv06` | `luiz.torres` | `ssh luiz.arthur@srv06` | 

Comandos para comprovar o acesso apos conectar via SSH:

```bash
hostname -f
w
exit
```

#### Evidências
<img width="696" height="631" alt="image" src="https://github.com/user-attachments/assets/900777ff-86d6-45f8-a7bd-9fd615617fb5" />
<img width="665" height="715" alt="image" src="https://github.com/user-attachments/assets/28f127bb-88aa-470b-be1f-a223b0c8e1e3" />
<img width="688" height="674" alt="image" src="https://github.com/user-attachments/assets/297c899b-5cd2-45d3-a2b9-2d837eb7fb1b" />
<img width="664" height="797" alt="image" src="https://github.com/user-attachments/assets/f170b8ea-8fda-40bf-a080-a65ef88b0a8c" />
<img width="665" height="807" alt="image" src="https://github.com/user-attachments/assets/3fd249a8-05ff-43fa-8ac0-a1a173ddab53" />


<img width="803" height="808" alt="image" src="https://github.com/user-attachments/assets/c3b64f0e-9d5b-4987-a2cb-e798915b1acd" />

