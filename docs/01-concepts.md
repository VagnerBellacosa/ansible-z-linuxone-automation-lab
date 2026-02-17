# 🧠 Ansible + LinuxONE + Mainframe (IBM Z)
## Guia Completo para Padawan 🚀

Bem-vindo ao seu primeiro passo no universo de automação enterprise.

Este guia foi criado para quem:

- Já conhece um pouco de Mainframe (COBOL, JCL, CICS)
- Ou vem do Linux
- Ou quer entrar no mundo DevOps Mainframe

Aqui você vai entender:

✔ O que é Ansible  
✔ O que é IBM Z  
✔ O que é LinuxONE  
✔ Como tudo isso se conecta  
✔ Conceitos fundamentais  
✔ Como começar na prática  

---

# 🏗 1️⃣ O que é IBM Z (Mainframe)?

IBM Z é a plataforma mainframe da IBM.

Ela roda:

- z/OS
- CICS
- DB2
- Batch
- Sistemas bancários
- Grandes volumes transacionais

É conhecida por:

- Alta disponibilidade
- Segurança
- Escalabilidade
- Confiabilidade

Mainframe não é legado.
É core bancário mundial.

---

# 🐧 2️⃣ O que é LinuxONE?

LinuxONE é um servidor Linux rodando no mesmo hardware do IBM Z.

Ou seja:

Mesmo poder do mainframe  
Rodando Linux enterprise

Permite:

- Containers
- Microserviços
- APIs REST
- Cloud híbrida
- DevOps moderno

É a ponte entre o mundo tradicional e o mundo cloud.

---

# 🤖 3️⃣ O que é Ansible?

Ansible é uma ferramenta de automação.

Ele permite:

- Criar usuários
- Instalar pacotes
- Criar datasets no z/OS
- Submeter JCL
- Reiniciar serviços
- Automatizar deploy

Ele funciona com:

- Arquivos YAML
- Conexão SSH
- Sem agente (agentless)
- Infraestrutura como Código

---

# 🧠 4️⃣ Conceitos Fundamentais

## 🔹 Playbook

Arquivo `.yml` que descreve tarefas.

Exemplo:

```yaml
- name: Criar usuário
  hosts: linux
  tasks:
    - name: Add user
      user:
        name: devuser
        state: present
🔹 Inventory
Lista de servidores que o Ansible vai acessar.

Exemplo:

all:
  hosts:
    linux1:
      ansible_host: 192.168.1.10
🔹 Idempotência
Se rodar duas vezes, o estado final será o mesmo.

Isso significa:

Sem duplicação
Sem erro
Sem alteração desnecessária

🔹 Infraestrutura como Código (IaC)
Tudo versionado no Git.

Servidor não é mais configurado manualmente.
É descrito em código.

🔄 5️⃣ Como Ansible conversa com o Mainframe?
No z/OS ele usa:

SSH

APIs do z/OS

Módulos específicos zos_*

Exemplo:

Criar dataset

Submeter JCL

Executar comando no CICS

No LinuxONE ele usa:

SSH padrão Linux

Módulos normais (user, package, systemd)

🏦 6️⃣ Arquitetura Moderna
Fluxo real corporativo:

Developer → Git → Pipeline → Ansible → z/OS / LinuxONE

Isso significa:

Deploy automático
Sem intervenção manual
Controle total
Auditoria

🔐 7️⃣ Segurança
No z/OS:

Permissões controladas via RACF

Controle de acesso por grupo

Auditoria

No Linux:

Usuários dedicados

Chave SSH

Sudo controlado

Automação precisa ser segura.

📦 8️⃣ O que você pode automatizar
No Mainframe:

Criar PDS / PDSE

Submeter JCL

Compilar COBOL

Dar NEWCOPY no CICS

Validar RC

No LinuxONE:

Criar usuários

Instalar aplicações

Configurar systemd

Deploy de APIs

Subir containers

🎓 9️⃣ Roadmap do Padawan
Etapa 1:
Aprender YAML básico

Etapa 2:
Instalar Ansible em Linux

Etapa 3:
Criar playbook simples (ex: criar usuário)

Etapa 4:
Criar playbook para z/OS (ex: criar dataset)

Etapa 5:
Integrar com Git

Etapa 6:
Automatizar deploy completo

🚀 1️⃣0️⃣ Evolução de Carreira
Se você dominar:

Mainframe tradicional

Linux

Ansible

Git

DevOps

Você se torna:

Mainframe DevOps Engineer

Não apenas programador.
Mas arquiteto de automação.

⚠️ Erros Comuns do Iniciante
❌ Usar TAB no YAML
❌ Esquecer indentação
❌ Não validar RC
❌ Executar como root sem necessidade
❌ Não versionar no Git

📈 Conclusão
Ansible não substitui o Mainframe.

Ele moderniza a forma de operar.

LinuxONE não substitui o z/OS.

Ele complementa o ecossistema.

O profissional que entende os dois mundos:

Tradicional + Cloud

é o mais valioso no mercado.