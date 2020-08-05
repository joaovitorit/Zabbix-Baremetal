# Zabbix-Baremetal
Zabbix-Baremetal

# Sistema operaciona

Ubuntu Server 18.04

TÚNNEL GRE

FRR (BGP) 7.3.1

Zabbix 5.0

Grafana 7.0

#################################################### Instalação FRR #########################################################################

URL: https://deb.frrouting.org/
# add GPG key
curl -s https://deb.frrouting.org/frr/keys.asc | sudo apt-key add -
# possible values for FRRVER: frr-6 frr-7 frr-stable
# frr-stable will be the latest official stable release

FRRVER="frr-stable"

echo deb https://deb.frrouting.org/frr $(lsb_release -s -c) $FRRVER | sudo tee -a /etc/apt/sources.list.d/frr.list

# update and install FRR

sudo apt update && sudo apt install frr frr-pythontools

#################################################### CONFIGURAÇÃO FRR #########################################################################

#CONFIGURAR O DAEMON BGP E VTYSH (SHELL DO FRR)
vi /etc/frr/daemons

#ativar como yes os daemons que precisa utilizar no nosso caso bgpd
bgpd=yes

#CONFIGURAR SESSÃO BGP USANDO ASN PRIVADO 64512 <---> 65534

#Digite no terminal

Vtysh

#QUANDO LOGAR NO TERMINAL DIGITE

configure

#ENTRANDO NA INSTÂNCIA DE BGP

router bgp 64512

#CONFIGURANDO A SESSÃO BGP

neighbor XXX.XXX.XXX.XXX remote-as 64513

neighbor XXX.XXX.XXX.XXX description ALGUM NOME

neighbor XXX.XXX.XXX.XXX password SUASENHA

neighbor XXX.XXX.XXX.XXX ebgp-multihop 15




