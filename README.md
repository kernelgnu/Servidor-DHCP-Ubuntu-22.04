# Servidor DHCP no Ubuntu 22.04

Este projeto documenta a configuração de um servidor DHCP (Dynamic Host Configuration Protocol) no Ubuntu 22.04, permitindo que dispositivos na rede recebam endereços IP automaticamente.

## Pré-requisitos

- Ubuntu 22.04 instalado
- Acesso root ou permissões sudo

## Instalação

### Passo 1: Atualizar o Sistema

Antes de instalar o servidor DHCP, é recomendável atualizar os pacotes do sistema:

```bash
sudo apt update
sudo apt upgrade -y
```

### Passo 2: Instalar o ISC DHCP Server

Instale o servidor DHCP usando o comando:

```bash
sudo apt install isc-dhcp-server -y
```
### Passo 3: Configurar o DHCP

Edite o arquivo de configuração principal do DHCP:

```bash
sudo nano /etc/dhcp/dhcpd.conf
```
Adicione ou modifique as configurações conforme necessário. Um exemplo de configuração é:

```bash
# Defina o domínio e os servidores DNS
option domain-name "exemplo.com";
option domain-name-servers 8.8.8.8, 8.8.4.4;

# Permitir o leasing de endereços
default-lease-time 600;
max-lease-time 7200;

# Configuração da sub-rede
subnet 192.168.1.0 netmask 255.255.255.0 {
    range 192.168.1.100 192.168.1.200;
    option routers 192.168.1.1;
    option subnet-mask 255.255.255.0;
    option broadcast-address 192.168.1.255;
}
```

- Nota: Ajuste as configurações de acordo com a sua rede.

### Passo 4: Configurar a Interface de Rede

Edite o arquivo de configuração da interface de rede:

```bash
sudo nano /etc/default/isc-dhcp-server
```

Defina a interface de rede que o servidor DHCP usará, como:

```bash
INTERFACESv4="eth0"
```

- Nota: Substitua eth0 pelo nome da interface de rede correspondente.

### Passo 5: Reiniciar o Servidor DHCP

Reinicie o serviço do DHCP e habilite-o para iniciar automaticamente:

```bash
sudo systemctl restart isc-dhcp-server
sudo systemctl enable isc-dhcp-server
```
### Passo 6: Verificar o Status do Serviço

Verifique se o serviço está em execução corretamente

```bash
sudo systemctl status isc-dhcp-server
```

### Conclusão

Após seguir estes passos, o servidor DHCP deve estar configurado e funcionando, permitindo que dispositivos na rede recebam endereços IP automaticamente.
