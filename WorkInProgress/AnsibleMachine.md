# Ansible em ZOS



# 🚨 Resposta Curta

👉 **Ansible NÃO roda dentro do z/OS tradicional (como se fosse um started task).**
 👉 Ele roda fora do mainframe, em um “control node” Linux.
 👉 O z/OS é o “managed node”.

------

# 🧠 Arquitetura Correta

```
Linux (Ansible Control Node)
        ↓
   SSH / z/OSMF REST
        ↓
      z/OS
```

Ou seja:

- O engine do Ansible roda em Linux.
- Ele controla o IBM Z remotamente.

------

# 📦 Então qual versão usar?

## ✅ Versão recomendada (2024–2025)

- **Ansible Core 2.14+**
- Melhor prática: 2.15 ou superior

Para ambiente corporativo:

- Red Hat Ansible Automation Platform (AAP 2.x)

------

# 🔧 E no lado do z/OS?

Você NÃO instala Ansible no z/OS.

Você precisa:

✔ z/OS 2.4 ou superior
 ✔ SSH ativo
 ✔ z/OS Management Facility configurado
 ✔ Python NÃO é obrigatório no z/OS
 ✔ IBM Z Ansible Collection instalada no control node

------

# 📚 Coleção necessária

Para z/OS você instala no Linux:

IBM z/OS core collection

Instalação:

```
ansible-galaxy collection install ibm.ibm_zos_core
```

Essa coleção contém:

- zos_job_submit
- zos_data_set
- zos_copy
- zos_operator
- zos_fetch
- etc.

------

# 🐧 E no LinuxONE?

No IBM LinuxONE você pode rodar:

- Ansible Core normalmente
- Ansible Automation Platform
- Inclusive pode usar o próprio LinuxONE como control node

------

# 🧨 Atenção Importante

## ❌ MVS 3.8j (Hercules TK5)

Não suporta:

- z/OSMF
- SSH moderno
- IBM Z collection

Logo:

Ansible moderno não funciona nele.

------

# 🏦 Em ambiente bancário real

Cenário típico:

- Ansible Automation Platform rodando em Linux corporativo
- Integração com GitLab / Jenkins
- Playbooks versionados
- Deploy automatizado para z/OS

------

# 🎯 Resumo Técnico Final

| Componente   | Versão recomendada  |
| ------------ | ------------------- |
| Ansible Core | 2.14+ (ideal 2.15+) |
| AAP          | 2.x                 |
| z/OS         | 2.4+                |
| Collection   | ibm.ibm_zos_core    |

------

# 💎 Insight de Senior

Se alguém disser:

> “Qual versão do Ansible instalar no z/OS?”

Você já sabe:

👉 Nenhuma. Ele não roda dentro do z/OS tradicional.
 👉 Ele controla o z/OS remotamente.