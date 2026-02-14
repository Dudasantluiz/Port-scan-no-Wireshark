# 🛡️ Análise de Varredura de Portas: Nmap (SYN Scan) + Wireshark

## 📝 Descrição do Projeto
Este projeto demonstra a análise técnica de um reconhecimento de rede em um ambiente de laboratório controlado. O objetivo é observar e documentar o comportamento do protocolo **TCP** durante um **Stealth Scan (-sS) e a atividade de uma varredura de portas utilizando o Wireshark no Kali Linux contra o Metasploitable 2.

## 🛠️ Topologia do Laboratório
* **Virtualização**: VMware Workstation
* **Atacante:** Kali Linux (IP: `192.168.17.130`)
* **Alvo:** Metasploitable 2 (IP: `192.168.17.129`)
* **Ferramentas:** Nmap & Wireshark
* **Rede:** Host-Only (Isolada)

---

## 🚀 Metodologia

1. No terminal do Kali Linux, executei o seguinte comando para identificar portas abertas de forma eficiente:

Bash
sudo nmap -sS  192.168.17.129


2.Durante o scan, o Wireshark foi utilizado para monitorar a interface de rede. Filtrei o tráfego pelo IP do alvo para isolar os pacotes relevantes:
ip.addr == 192.168.17.129


4. 🔍 🔍 Análise Técnica (O Diferencial)
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


6. **Forma de identificar scan de portar no Wireshark**:
7. Filtro de exibição para pacotes principais: tcp.flags.syn == 1 && tcp.flags.ack == 0

8. Ir na aba Estatisticas > conversations > tcp : Verificando se teria um IP (address A) com a mesma porta e outro IP (address B) com  varias portas alvo diferentes em curto espaço de tempo. 
9.
10.
11. 
12.
13. 📁 Arquivos no Repositórioanalysis_capture.pcapng: Ficheiro de captura para análise detalhada no Wireshark.screenshots/: Imagens do laboratório.Dicas para finalizar no GitHub:Cria o ficheiro: Clica em "Add file" -> "Create new file" e dá o nome de README.md.Sobe o PCAP: Não te esqueças de subir o arquivo do Wireshark (Export Specified Packets). Isso dá muita credibilidade.Personaliza os IPs: No texto, usa os IPs reais que apareceram nos teus prints para haver coerência.
