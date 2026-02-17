# 🔐 REQUISITOS RACF PARA AUTOMAÇÃO SEGURA

Vou dividir em 6 camadas:

1️⃣ Identidade
 2️⃣ Autenticação
 3️⃣ Autorização Dataset
 4️⃣ Autorização Job
 5️⃣ Operações de Sistema
 6️⃣ Auditoria

------

# 1️⃣ 👤 Identidade – Nunca usar USER pessoal

❌ Erro clássico: usar USERID de desenvolvedor no playbook.

✔ Criar um ID técnico dedicado:

```
ANSIBLE.ZOS
```

Características:

- Não interativo
- Sem TSO logon
- Sem senha humana
- Uso via SSH key

------

# 2️⃣ 🔑 Autenticação Segura

Requisitos:

✔ SSH ativo no z/OS
 ✔ Autenticação via chave pública
 ✔ Sem senha hardcoded

Configuração típica:

- Classe RACF: `USER`
- Permissão para OMVS
- UID único
- HOME definido

Exemplo:

```
ALTUSER ANSIBLE.ZOS OMVS(UID(12345) HOME('/u/ansible') PROGRAM('/bin/sh'))
```

------

# 3️⃣ 📂 Controle de Dataset

Automação mexe com:

- SOURCE
- LOADLIB
- PROCLIB
- PARMLIB (⚠️ extremo cuidado)

Você deve proteger via classe:

```
DATASET
```

Exemplo:

```
PERMIT USERID.SOURCE.** CLASS(DATASET) ID(ANSIBLE.ZOS) ACCESS(UPDATE)
```

⚠️ Nunca dar ALTER genérico em HLQ corporativo.

------

# 4️⃣ 📜 Controle de Submissão de JOB

Automação submete JCL via:

- SSH
- z/OSMF

Controle envolve:

- Classe `JESSPOOL`
- Classe `SURROGAT`
- Classe `OPERCMDS` (se operador)

Se for permitir submissão em nome de outro ID:

```
RDEFINE SURROGAT USERID.SUBMITTER UACC(NONE)
PERMIT USERID.SUBMITTER CLASS(SURROGAT) ID(ANSIBLE.ZOS) ACCESS(READ)
```

Sem isso, risco de impersonação.

------

# 5️⃣ 🖥️ Comandos de Operador (CICS / System)

Se playbook usa:

```
zos_operator:
  cmd: "F CICSREG,NEWCOPY PROG01"
```

Você precisa proteger via:

```
OPERCMDS
```

Exemplo:

```
RDEFINE OPERCMDS MVS.MCSOPER.CICSREG UACC(NONE)
PERMIT MVS.MCSOPER.CICSREG CLASS(OPERCMDS) ID(ANSIBLE.ZOS) ACCESS(CONTROL)
```

Nunca liberar:

```
MVS.*
```

Isso é porta aberta para desastre.

------

# 6️⃣ 📊 Auditoria e Compliance

Ativar LOG:

```
SETROPTS LOGOPTIONS(DATASET OPERCMDS)
```

Registrar:

- Submissões automáticas
- Alterações de dataset
- Comandos de operador

Auditoria pode ser integrada com:

- SMF
- SIEM corporativo
- Ferramentas de compliance

------

# 🧠 Modelo Correto de Segurança (Boas Práticas)

✔ Princípio do menor privilégio
 ✔ ID técnico exclusivo
 ✔ Separação DEV / QA / PROD
 ✔ Sem acesso direto a PARMLIB
 ✔ Sem autoridade SPECIAL
 ✔ Sem OPERATIONS

------

# 🏦 Modelo Banco (Nível Enterprise)

Ambiente PROD:

- ID Ansible separado por LPAR
- Perfis restritos por HLQ
- Controle de SURROGAT
- Auditoria ativa
- Aprovação via pipeline

------

# 🚨 Riscos Reais se Mal Configurado

❌ Alteração de PROCLIB
 ❌ STOP região errada
 ❌ Submissão de JCL malicioso
 ❌ Escalada de privilégio
 ❌ Incidente de segurança auditável

Automação amplia velocidade — inclusive de erro.

------

# 🏗 Arquitetura Segura

------

# 🎯 Checklist Final – Senior Level

Se você é Senior e quer implementar Ansible no Z, confirme:

✔ Existe ID técnico dedicado
 ✔ SSH com chave pública
 ✔ z/OSMF protegido
 ✔ Dataset controlado por HLQ
 ✔ SURROGAT configurado
 ✔ OPERCMDS restrito
 ✔ Auditoria ativa

------

# 💎 Insight Estratégico

Automação não reduz governança.

Ela exige mais governança.

O Senior que entende:

- Automação
- RACF
- Segregação
- Auditoria

não é apenas programador.

Ele vira arquiteto de controle do core bancário.

------

