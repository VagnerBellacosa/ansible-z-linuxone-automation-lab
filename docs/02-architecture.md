# 🏗 Arquitetura Ansible + LinuxONE + Mainframe (IBM Z)
## Guia Arquitetural para Padawan 🚀

Este documento explica como funciona a arquitetura moderna de automação envolvendo:

- IBM Z (Mainframe)
- LinuxONE
- Ansible
- DevOps Pipeline

Se você quer entender como o mundo tradicional e o mundo cloud se conectam,
este é seu ponto de partida.

---

# 🧠 1️⃣ Visão Geral da Arquitetura

Fluxo moderno corporativo:

Developer → Git → Pipeline → Ansible → z/OS / LinuxONE

Isso significa:

Código versionado
Deploy automatizado
Sem intervenção manual
Infraestrutura como Código

---

# 🏢 2️⃣ Camadas da Arquitetura

A arquitetura pode ser dividida em 5 camadas:

1️⃣ Camada de Desenvolvimento  
2️⃣ Camada de Controle (Control Node)  
3️⃣ Camada de Automação  
4️⃣ Camada Mainframe (z/OS)  
5️⃣ Camada LinuxONE  

---

# 👨‍💻 3️⃣ Camada 1 – Developer

Aqui está o desenvolvedor.

Ele trabalha com:

- COBOL
- JCL
- APIs
- Aplicações Java/Python
- Git

Nada é mais enviado por e-mail.
Tudo vai para o repositório Git.

---

# 🧾 4️⃣ Camada 2 – Git

Git é o versionador.

Ele armazena:

- Código COBOL
- Playbooks Ansible
- Configurações
- Templates
- Scripts

Isso permite:

Rastreabilidade
Auditoria
Rollback

---

# 🔄 5️⃣ Camada 3 – Pipeline CI/CD

Aqui acontece a automação orquestrada.

Pipeline executa:

- Build
- Testes
- Validações
- Chamada do Ansible

O pipeline chama o Ansible automaticamente.

---

# 🤖 6️⃣ Camada 4 – Ansible (Control Node)

Ansible roda normalmente em:

- Servidor Linux
- VM
- Container
- LinuxONE

Ele é o "orquestrador".

Funções:

- Conectar via SSH
- Chamar APIs do z/OS
- Executar tarefas
- Garantir estado desejado

Ele não precisa de agente.

---

# 🏦 7️⃣ Camada 5 – IBM Z (z/OS)

Aqui está o mainframe tradicional.

Componentes típicos:

- z/OS
- CICS
- DB2
- Batch
- JES

Ansible pode:

- Criar datasets
- Submeter JCL
- Compilar COBOL
- Dar NEWCOPY no CICS
- Consultar status de job

---

# 🐧 8️⃣ Camada 6 – LinuxONE

LinuxONE roda Linux no mesmo hardware IBM Z.

Permite:

- Microserviços
- Containers
- APIs REST
- Aplicações modernas

Ansible aqui funciona como em qualquer Linux.

Pode:

- Criar usuários
- Instalar pacotes
- Deploy de aplicações
- Configurar serviços

---

# 🔐 9️⃣ Segurança na Arquitetura

No z/OS:

- Controle via RACF
- Permissões para SSH
- Autorização para JCL
- Controle de operador

No Linux:

- Sudo controlado
- Chaves SSH
- Grupos de acesso

Automação segura é obrigatória.

---

# 📦 🔟 Comunicação entre Camadas

Ansible conversa com:

Linux → via SSH  
z/OS → via SSH e APIs  

Tudo autenticado.
Tudo auditável.

---

# 🧩 1️⃣1️⃣ Infraestrutura como Código

Antes:

Administrador configurava manualmente.

Agora:

Servidor e mainframe são descritos em código YAML.

Isso permite:

Repetibilidade
Padronização
Escalabilidade

---

# 🧠 1️⃣2️⃣ Idempotência na Arquitetura

Se o estado já estiver correto:

Nada é alterado.

Isso evita:

Erros
Duplicações
Problemas operacionais

---

# 📊 1️⃣3️⃣ Exemplo de Fluxo Real

1. Desenvolvedor altera COBOL
2. Faz commit no Git
3. Pipeline é disparado
4. Ansible copia fonte
5. Submete compilação
6. Valida RC
7. Atualiza LOADLIB
8. Executa NEWCOPY
9. Gera log de auditoria

Tudo automatizado.

---

# 🚀 1️⃣4️⃣ Benefícios Arquiteturais

✔ Redução de erro humano  
✔ Padronização  
✔ Auditoria  
✔ Velocidade de entrega  
✔ Integração com cloud  
✔ Mainframe híbrido  

---

# ⚠️ 1️⃣5️⃣ Erros Arquiteturais Comuns

❌ Automação sem controle de acesso  
❌ Misturar ambientes (DEV/QA/PROD)  
❌ Não versionar playbooks  
❌ Permitir execução manual paralela  

---

# 🎓 1️⃣6️⃣ Como Evoluir na Arquitetura

Padawan nível 1:
Entender YAML e SSH

Padawan nível 2:
Criar playbook Linux

Padawan nível 3:
Criar playbook z/OS

Padawan nível 4:
Integrar com pipeline

Padawan nível 5:
Automatizar deploy completo

---

# 🏁 1️⃣7️⃣ Conclusão

A arquitetura moderna não elimina o mainframe.

Ela conecta:

Tradição + Cloud  
z/OS + Linux  
Batch + API  
Manual + Automação  

Quem entende essa arquitetura:

Não é apenas programador.
É arquiteto de automação.

---

# 🌌 Próximo Passo

Crie um diagrama.
Monte um laboratório.
Automatize algo simples.
E evolua.

May the automation be with you.