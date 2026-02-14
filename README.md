# 🛡️ Análise de Varredura de Portas: Wireshark

## 📝 Descrição do Projeto
Este projeto demonstra a análise técnica de um reconhecimento de rede em um ambiente de laboratório controlado. O objetivo é observar e documentar o comportamento do protocolo **TCP** durante um **Stealth Scan (-sS) e a atividade de uma varredura de portas utilizando o Wireshark no Kali Linux contra o Metasploitable 2.

## 🛠️ Topologia do Laboratório
* **Virtualização**: VMware Workstation
* **Atacante:** Kali Linux (IP: `192.168.17.130`)
* **Alvo:** Metasploitable 2 (IP: `192.168.17.129`)
* **Ferramentas:** Nmap & Wireshark
* **Rede:** Host-Only (Isolada)
* 
  ![image alt](https://github.com/Dudasantluiz/Port-scan-no-Wireshark/blob/main/Tela1.png?raw=true)

## 🚀 Metodologia
No terminal do Kali Linux, executei o seguinte comando para identificar portas abertas de forma eficiente:

sudo nmap -sS  192.168.17.129 
![image alt](https://github.com/Dudasantluiz/Port-scan-no-Wireshark/blob/main/Tela2.png?raw=true)


Durante o scan, o Wireshark foi utilizado para monitorar a interface de rede. Filtrei o tráfego pelo IP do alvo para isolar os pacotes relevantes:
ip.addr == 192.168.17.129 
   ![image alt](https://github.com/Dudasantluiz/Port-scan-no-Wireshark/blob/main/Tela3.png?raw=true)


🔍 Análise Técnica 
Comportamento da Porta Aberta (Handshake Incompleto)
Diferente de uma conexão normal, o SYN Scan não completa o Three-Way Handshake.
Kali → Alvo: Envia um pacote SYN (Request).
Alvo → Kali: Responde com SYN, ACK (Porta disponível).
Kali → Alvo: Envia um RST (Reset) para fechar a conexão abruptamente.

Análise: Isto evita que a aplicação alvo registe uma conexão completa, tornando o scan mais rápido e "silencioso" para logs de aplicação simples.

  **Vantagens e Desvantagens**
Vantagem: Velocidade,"Não espera a conclusão da conexão, permitindo escanear milhares de portas rapidamente."
Vantagem: Discrição,"Por não completar o handshake, muitos serviços de log de aplicação não registram a tentativa."
Desvantagem: Privilégio,Requer permissões de root/sudo para manipular pacotes crus (raw sockets).
Desvantagem: Detecção,Firewalls modernos e sistemas IDS detectam facilmente o padrão de pacotes RST em massa.


. **Forma de identificar scan de portar no Wireshark**:
. Filtro de exibição para pacotes principais: tcp.flags.syn == 1 && tcp.flags.ack == 0
.  ![image alt](https://github.com/Dudasantluiz/Port-scan-no-Wireshark/blob/main/Tela4.png?raw=true)

. Ir na aba Estatisticas > conversations > tcp : Verificando se teria um IP (address A) com a mesma porta e outro IP (address B) com  varias portas alvo diferentes em curto espaço de tempo. 

10. ![image alt](https://github.com/Dudasantluiz/Port-scan-no-Wireshark/blob/main/Tela5.png?raw=true)
   
