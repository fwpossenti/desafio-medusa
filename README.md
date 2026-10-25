# Laboratório de Testes de Força Bruta com Medusa (FTP e SMB)

## 📌 Visão Geral
Este repositório documenta a execução de testes de intrusão e avaliação de segurança ofensiva focados em ataques de dicionário e força bruta (*brute-force*). Utilizando a ferramenta **Medusa**, foram auditados os serviços vulneráveis de **FTP** e **SMB** na máquina **Metasploitable 2** em um ambiente virtualizado totalmente isolado.

---

## 🛠️ Arquitetura da Rede e Laboratório
O ambiente foi configurado com uma topologia de dupla interface de rede no Kali Linux, garantindo isolamento total dos testes defensivos e mantendo conectividade externa para gerenciamento do repositório.

* **Máquina Atacante (Kali Linux):**
  * `eth0`: IP Estático `192.168.10.1/24` (Rede Interna / Host-Only — Isolada para o Lab)
  * `eth1`: IP via DHCP (NAT — Acesso à Internet para atualização e Git)
* **Máquina Alvo (Metasploitable 2):**
  * `eth0`: IP Estático `192.168.10.2/24` (Rede Interna / Host-Only)

---

## 🎯 Serviços Auditados e Comandos Executados

### 1. Teste de Força Bruta no Serviço FTP (Porta 21)
Validação de credenciais e resistência contra ataques de dicionário no serviço de transferência de arquivos:

```bash
medusa -h 192.168.10.2 -u msfadmin -P /usr/share/wordlists/rockyou.txt -M ftp
2. Teste de Autenticação no Serviço SMB (Porta 445)

Auditoria de robustez de senhas no serviço de compartilhamento de arquivos e recursos de rede:
Bash

medusa -h 192.168.10.2 -u msfadmin -P /usr/share/wordlists/rockyou.txt -M smb

🛡️ Medidas de Mitigação e Recomendações

Para proteger os serviços FTP e SMB contra ataques de autenticação automatizados, recomendam-se as seguintes medidas defensivas:

    Política de Senhas Fortes: Exigir alta complexidade de caracteres e comprimento elevado.

    Bloqueio de Contas (Account Lockout): Restringir tentativas incorretas consecutivas para mitigar ataques automatizados.

    Restrição de Acesso de Rede: Utilizar regras de firewall para limitar o acesso às portas 21 e 445 apenas a IPs autorizados.

    Monitoramento e Logs: Implementar soluções de detecção de anomalias (SIEM/IDS) para alertar sobre múltiplas falhas de autenticação.
