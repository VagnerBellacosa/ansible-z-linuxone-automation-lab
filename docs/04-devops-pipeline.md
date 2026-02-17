# 🚀 DevOps Pipeline com Ansible + LinuxONE + Mainframe (IBM Z)
## Guia Completo para Padawan

Este guia explica como funciona um pipeline DevOps moderno integrando:

- IBM Z (z/OS)
- LinuxONE
- Ansible
- Git
- CI/CD

Se você quer entender como o mainframe entra no mundo DevOps, este é seu mapa.

---

# 🧠 1️⃣ O que é DevOps?

DevOps é uma cultura e conjunto de práticas que unem:

Development (Desenvolvimento)
Operations (Operações)

Objetivo:

✔ Entrega rápida
✔ Redução de erro humano
✔ Automação
✔ Versionamento
✔ Integração contínua

---

# 🏗 2️⃣ O que é um Pipeline?

Pipeline é uma sequência automatizada de etapas que executa:

1. Build
2. Teste
3. Validação
4. Deploy

Tudo automaticamente após um commit no Git.

---

# 🌍 3️⃣ Arquitetura Moderna

Fluxo padrão:

Developer → Git → Pipeline → Ansible → z/OS / LinuxONE

Sem e-mail.
Sem operador manual.
Sem planilha.

Infraestrutura como Código.

---

# 👨‍💻 4️⃣ Camada 1 – Developer

Desenvolvedor altera:

- COBOL
- JCL
- APIs
- Aplicações Linux

Depois faz:

git commit
git push

Pipeline dispara automaticamente.

---

# 📂 5️⃣ Camada 2 – Git

Git armazena:

- Código fonte
- Playbooks Ansible
- Templates
- Configurações

Permite:

✔ Rastreabilidade
✔ Auditoria
✔ Rollback

---

# 🔄 6️⃣ Camada 3 – Pipeline CI/CD

Ferramentas comuns:

- Jenkins
- GitLab CI
- GitHub Actions
- Azure DevOps

Pipeline executa:

- Testes
- Build
- Chamada do Ansible
- Deploy automático

---

# 🤖 7️⃣ Camada 4 – Ansible

Ansible é o orquestrador.

Ele:

- Conecta via SSH
- Executa playbooks
- Garante estado desejado
- Automatiza o deploy

Ele roda em:

- Linux tradicional
- LinuxONE

---

# 🏦 8️⃣ Camada 5 – Mainframe (z/OS)

No z/OS, Ansible pode:

- Criar dataset
- Submeter JCL
- Compilar COBOL
- Atualizar LOADLIB
- Dar NEWCOPY no CICS
- Validar RC

Mainframe entra no pipeline moderno.

---

# 🐧 9️⃣ Camada 6 – LinuxONE

LinuxONE permite:

- Microserviços
- APIs
- Containers
- Aplicações Java/Python

Ansible pode:

- Criar usuário
- Instalar aplicação
- Reiniciar serviço
- Atualizar versão

---

# 🔐 🔟 Segurança no Pipeline

Boa prática:

✔ Usuário dedicado para automação
✔ Permissões mínimas
✔ Separação DEV / QA / PROD
✔ Auditoria ativa
✔ Uso de Ansible Vault

Pipeline seguro é obrigatório.

---

# 📊 1️⃣1️⃣ Exemplo de Pipeline Real

1. Desenvolvedor altera COBOL
2. Commit no Git
3. Pipeline executa teste
4. Ansible sobe fonte
5. Submete compilação
6. Valida RC
7. Atualiza LOADLIB
8. NEWCOPY no CICS
9. Gera log de auditoria

Tudo automatizado.

---

# 📦 1️⃣2️⃣ Exemplo de Deploy Linux

1. Commit no Git
2. Pipeline executa build
3. Ansible copia artefato
4. Atualiza diretório /opt/app
5. Reinicia systemd
6. Valida serviço ativo

---

# 🧠 1️⃣3️⃣ Conceitos Importantes

## Idempotência

Rodar duas vezes → mesmo resultado final.

## Infraestrutura como Código

Ambiente descrito em YAML.

## Observabilidade

Logs e monitoramento integrados.

---

# ⚠️ 1️⃣4️⃣ Erros Comuns do Iniciante

❌ Automatizar sem controle de acesso
❌ Não validar RC
❌ Misturar ambientes
❌ Deploy direto em produção
❌ Não versionar playbooks

---

# 🎓 1️⃣5️⃣ Roadmap do Padawan

Nível 1:
Entender Git

Nível 2:
Criar playbook Linux simples

Nível 3:
Criar playbook z/OS

Nível 4:
Integrar com pipeline

Nível 5:
Automatizar deploy completo

Nível 6:
Criar rollback automático

---

# 📈 1️⃣6️⃣ Benefícios Estratégicos

✔ Redução de erro humano
✔ Deploy mais rápido
✔ Padronização
✔ Auditoria
✔ Integração híbrida
✔ Valorização profissional

---

# 🚀 1️⃣7️⃣ Evolução de Carreira

Se você domina:

- Mainframe
- Linux
- Ansible
- Git
- DevOps Pipeline

Você se torna:

Mainframe DevOps Engineer

Não apenas programador.
Mas arquiteto de automação.

---

# 🏁 Conclusão

O pipeline não substitui o mainframe.

Ele conecta:

Tradição + Cloud
Batch + API
Manual + Automação

Quem entende isso:

Não fica no passado.
Constrói o futuro.

---

# 🌌 Próximo Passo

Crie seu primeiro pipeline simples.
Automatize um deploy pequeno.
Versione tudo.
E evolua.



May the pipeline be with you.