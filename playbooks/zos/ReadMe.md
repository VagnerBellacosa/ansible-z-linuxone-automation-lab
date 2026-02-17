```yaml
# 📘 Guia Completo de Playbooks Ansible (YAML)

Este documento explica em detalhes:

- O que é um Playbook
- Como funciona a sintaxe YAML
- Estrutura básica
- Como criar
- Como executar
- Como interpretar o resultado
- Boas práticas para automação em Mainframe (IBM Z)

---

# 1️⃣ O que é um Playbook?

Um Playbook é um arquivo `.yml` que descreve tarefas que o Ansible deve executar em um ou mais servidores.

Ele é:

- Declarativo
- Idempotente
- Baseado em YAML
- Executado a partir de um Control Node (Linux)

---

# 2️⃣ O que é YAML?

YAML significa:

YAML Ain’t Markup Language

É um formato simples baseado em:

- Indentação (espaços, nunca TAB)
- Estrutura hierárquica
- Lista com hífen (-)
- Chave: valor

Exemplo simples:

```yaml
name: Criar dataset
state: present
type: seq
Indentação é crítica.
Use sempre 2 espaços.

3️⃣ Estrutura Básica de um Playbook
---
- name: Nome do Playbook
  hosts: grupo_do_inventory
  gather_facts: no

  tasks:
    - name: Nome da tarefa
      modulo_ansible:
        parametro1: valor
        parametro2: valor
Explicação:

name → descrição do play

hosts → grupo definido no inventory

gather_facts → coleta de informações do sistema

tasks → lista de ações

modulo_ansible → ação executada

4️⃣ Exemplo Real no Mainframe (z/OS)
Criar dataset sequencial:

---
- name: Create QSAM Dataset
  hosts: zos
  gather_facts: no

  tasks:
    - name: Criar dataset FB
      zos_data_set:
        name: USERID.TEST.FILE
        type: seq
        record_format: fb
        record_length: 80
        state: present
5️⃣ Inventory (Arquivo de Hosts)
Exemplo:

inventory/zos.yml

all:
  hosts:
    zos:
      ansible_host: 192.168.1.10
      ansible_user: USERID
      ansible_connection: ssh
O inventory define:

Onde conectar

Usuário

Método de conexão

6️⃣ Como Executar um Playbook
Comando:

ansible-playbook -i inventory/zos.yml playbook.yml
Explicação:

-i → arquivo inventory

playbook.yml → arquivo que será executado

7️⃣ Como Ler a Saída
Exemplo de resultado:

TASK [Criar dataset FB] **********************************
changed: [zos]

PLAY RECAP ***********************************************
zos : ok=1 changed=1 failed=0
Significado:

ok → tarefa executada corretamente

changed → houve alteração no sistema

failed → falha na execução

unreachable → erro de conexão

8️⃣ Idempotência
Se executar novamente:

ok: [zos]
Significa:

O estado desejado já estava correto.
Nada foi alterado.

Isso é automação declarativa.

9️⃣ Tratamento de Erros
Exemplo:

- name: Falhar se RC diferente de zero
  fail:
    msg: "Erro detectado"
  when: resultado.rc != 0
Permite controle inteligente da execução.

🔟 Variáveis
Podemos usar variáveis:

vars:
  dataset_name: USERID.APP.DATA

name: "{{ dataset_name }}"
Facilita reutilização e padronização.

1️⃣1️⃣ Estrutura Recomendada de Projeto
inventory/
playbooks/
roles/
docs/
Boa prática profissional.

1️⃣2️⃣ Boas Práticas
✔ Use nomes descritivos
✔ Nunca use TAB
✔ Separe playbooks por função
✔ Use variáveis
✔ Valide RC
✔ Versione no Git
✔ Documente tudo

1️⃣3️⃣ Principais Erros Comuns
❌ Indentação errada
❌ Esquecer hífen na lista
❌ Usar TAB
❌ Erro no nome do módulo
❌ Inventory incorreto

1️⃣4️⃣ Playbook no Contexto IBM Z
Em ambientes IBM Z:

Conexão via SSH

Uso de módulos zos_*

Integração com z/OSMF

Permissões controladas via RACF

Integração com CI/CD

📈 Conclusão
Um Playbook Ansible é:

Infraestrutura como Código.

No Mainframe ele permite:

Criar datasets

Submeter JCL

Executar comandos CICS

Automatizar deploy COBOL

Integrar com DevOps

Automação não substitui o Mainframe.

Ela eleva o profissional