# 🔐 Segurança no Mainframe Moderno
## RACF + Ansible + LinuxONE (Guia para Padawan)

Este documento explica como funciona a segurança em um ambiente moderno envolvendo:

- IBM Z (z/OS)
- RACF
- Ansible
- LinuxONE

Se você quer automatizar sem comprometer segurança, este guia é obrigatório.

---

# 🧠 1️⃣ O que é RACF?

RACF significa:

Resource Access Control Facility

É o sistema de segurança do z/OS.

Ele controla:

- Quem pode logar
- Quem pode acessar dataset
- Quem pode submeter JCL
- Quem pode executar comandos de operador
- Quem pode acessar CICS
- Quem pode acessar DB2

RACF é o guardião do mainframe.

---

# 🏦 2️⃣ Por que RACF é crítico?

Mainframe roda:

- Bancos
- Seguradoras
- Governo
- Cartões de crédito

Qualquer erro de permissão pode ser catastrófico.

Por isso:

Automação sem RACF correto = risco sistêmico.

---

# 🤖 3️⃣ Onde Ansible entra na segurança?

Ansible executa ações como:

- Criar dataset
- Submeter JCL
- Dar NEWCOPY no CICS
- Executar comando no console

Mas ele executa usando um usuário real.

Esse usuário é controlado pelo RACF.

---

# 🔐 4️⃣ Modelo de Segurança Arquitetural

Arquitetura típica:

Ansible Control Node → SSH → z/OS → RACF valida → Executa ação

Sem autorização RACF:
Nada acontece.

---

# 👤 5️⃣ Usuário de Automação

Nunca use usuário pessoal para automação.

Boa prática:

Criar um usuário dedicado:

ANSIBLEUSR

Permissões mínimas necessárias:

✔ Submeter JCL  
✔ Criar dataset em HLQ específico  
✔ Executar comandos CICS específicos  
✔ Acesso restrito a ambientes DEV/QA  

Nunca PROD sem controle formal.

---

# 📂 6️⃣ Controle de Dataset

RACF controla por HLQ.

Exemplo:

USERID.APP.*

Podemos permitir:

ANSIBLEUSR → ALTER → USERID.APP.*

E negar:

ANSIBLEUSR → SYS1.*

Princípio do menor privilégio.

---

# 🧾 7️⃣ Controle de Submissão de Job

RACF controla:

- Classe JESJOBS
- Classe DATASET
- Classe OPERCMDS

Automação precisa:

Permissão explícita.

---

# ⚙ 8️⃣ Segurança em Comandos de Operador

Comando:

F CICSPROD,NEWCOPY PROG01

Isso é controlado por:

Classe OPERCMDS no RACF.

Nunca conceda autoridade ampla.

Permita somente comandos específicos.

---

# 🐧 9️⃣ Segurança no LinuxONE

No Linux:

- Controle via sudo
- Grupos
- Chaves SSH
- SELinux (se aplicável)

Nunca:

Permitir root direto via SSH.

Boa prática:

Usuário ansible com sudo controlado.

---

# 🔑 🔟 Autenticação

Melhor prática:

✔ Chave SSH
✔ Sem senha em texto plano
✔ Vault do Ansible para segredos
✔ Rotação periódica de chave

Nunca coloque senha no playbook.

---

# 🔒 1️⃣1️⃣ Ansible Vault

Ansible possui recurso chamado:

Vault

Permite:

- Criptografar senha
- Proteger variáveis
- Proteger tokens
- Proteger credenciais

Exemplo:

ansible-vault encrypt secrets.yml

Segurança começa no código.

---

# 📊 1️⃣2️⃣ Auditoria

No z/OS:

- SMF registra eventos
- RACF registra acesso
- Logs ficam auditáveis

No Linux:

- journald
- syslog

Automação deve ser auditável.

---

# 🚨 1️⃣3️⃣ Riscos Comuns

❌ Dar ALTER em SYS1  
❌ Permitir operador irrestrito  
❌ Usar usuário pessoal  
❌ Executar como root sem controle  
❌ Não separar DEV/QA/PROD  

---

# 🏗 1️⃣4️⃣ Separação de Ambientes

Boa arquitetura:

ANSIBLE-DEV
ANSIBLE-QA
ANSIBLE-PROD

Cada um com:

Permissões específicas.

Nunca misture.

---

# 🧠 1️⃣5️⃣ Princípios Fundamentais

1. Menor privilégio
2. Segregação de função
3. Auditoria ativa
4. Automação controlada
5. Versionamento seguro

---

# 📈 1️⃣6️⃣ Segurança na Arquitetura Completa

Developer → Git → Pipeline → Ansible → RACF → z/OS

Se RACF negar:
Pipeline falha.

Isso é segurança por design.

---

# 🎓 1️⃣7️⃣ Roadmap do Padawan

Nível 1:
Entender o que é RACF

Nível 2:
Entender controle por HLQ

Nível 3:
Entender OPERCMDS

Nível 4:
Entender segregação de ambiente

Nível 5:
Integrar com automação segura

---

# 🏁 1️⃣8️⃣ Conclusão

Automação sem segurança é perigo.

Segurança sem automação é lentidão.

O equilíbrio é:

RACF + Ansible + Arquitetura correta.

Quem domina isso:

Não é apenas técnico.
É guardião do core bancário.

---

# 🌌 Próximo Passo

Aprenda:

- Criar usuário RACF
- Criar grupo
- Permitir acesso por HLQ
- Testar automação controlada

May the security be with you.