# 🚀 Gerenciando Workflows no Mainframe com Ansible

## Experimentando COBOL User-Defined Functions e Pipeline de Deploy

O mainframe sempre foi o coração das operações críticas de negócio.
 Banco, cartão, governo, seguradora — tudo pulsa ali.

Mas vamos ser honestos…

Gerenciar workflows nesse ambiente **nunca foi simples**.

Quando comecei a explorar o uso do Ansible para automação em mainframe, fiquei intrigado com a promessa:

> Simplicidade. Flexibilidade. Infraestrutura como Código.

Mal sabia eu que essa jornada me levaria por:

- Compilação de programas COBOL
- Simulação de ambientes DEV → IT → QA → PROD
- Problemas de encoding EBCDIC
- Templates Jinja2 sabotando delimitadores de JCL
- E aquelas batalhas silenciosas contra espaços antes de `//`

Sim… o clássico erro invisível.

Neste artigo, compartilho minha experiência automatizando workflows no IBM Z usando a coleção IBM z/OS core collection — desde copiar copybooks até compilar, executar e validar retorno de jobs.

E claro… os desafios que ainda estou domando.

------

# 🎯 O Ponto de Partida: Copybooks e Compilação COBOL

Meu objetivo inicial era simples:

> Automatizar a movimentação de copybooks e a compilação de programas COBOL que utilizavam User-Defined Functions (UDFs).

Sim, aquelas introduzidas no COBOL 6.4.

Confesso: ainda não encontrei um grande “killer use case” que substitua totalmente a filosofia clássica de submódulos, mas como laboratório foi excelente.

O cenário envolvia:

- JCL já existentes
- Datasets catalogados… ou não
- Mudanças constantes nas UDFs
- Recompilações frequentes

------

## 📦 Movendo Copybooks com `zos_copy`

Tarefa simples. Elegante. Funcional.

```
- name: Copy copybooks to TEST
  zos_copy:
    src: "{{ ansible_user }}.DEV.COPY(ZIPSRVPT)"
    dest: "{{ ansible_user }}.TEST.COPY(ZIPSRVPT)"            
    remote_src: true            
    force: true
```

Resultado?

Copybook movido.
 Sem ISPF 3.3.
 Sem digitação manual.

Bellacosa aprova.

------

## 🏗 Compilando COBOL com `zos_job_submit`

JCL já preparada no PDSE.
 Só precisava submeter via Ansible.

```
- name: Submit compile JCL in TEST
  zos_job_submit:
    src: "{{ ansible_user }}.COBFUNC.JCL(ZIPMAIN)"
    location: DATA_SET
    wait: true
    return_output: true
  register: compile_result
```

RC validado no spool.
 Confiança aumentou.

Então veio a parte divertida: capturar resultado e SYSOUT via playbook.

------

# 🧪 Brincando com RC e SYSOUT

Extraindo informações do job:

```
- name: Setting fact `Job Results`
  set_fact:
    job_results: "{{ result.jobs[0]}}"
```

Exibindo retorno:

```
- name: Results
  debug:  
    msg: "Job {{ job_results.job_id}} completed with {{ job_results.ret_code.msg}}"
```

Extraindo SYSOUT:

```
- name: Extract SYSOUT content from job output
  set_fact:
    sysout_content: "{{ item.content }}"
  when: item.ddname == 'SYSOUT'
  loop: "{{ job_results.ddnames }}"
```

Ver o playbook processando JES em tempo real?

Fascinante.

Mainframe + YAML = novo mundo.

------

# 🏗 Simulando Ambientes: DEV → IT → QA → PROD

Aqui a coisa ficou mais interessante.

Decidi simular pipeline corporativo completo.

Confissão Bellacosa:

> Não segui 100% as boas práticas de separação de variáveis por ambiente.

Em vez de usar `vars/environments.yml`, concentrei variáveis no próprio playbook.

Funciona? Sim.
 Ideal? Não.

Mas laboratório é para aprender.

------

## 📦 Deploy por Ambiente

Movimentação baseada em `target_env`.

Cada ambiente com:

- Bibliotecas específicas
- Datasets próprios
- JCL customizados

Simulação real de fluxo bancário.

------

# 🎭 Quando Jinja2 entrou na história…

Comecei a criar JCL dinamicamente.

Templates `.j2`.

E aí começaram as aventuras.

------

# 💥 O Problema do Encoding

Copiar template direto para PDSE?

Problema.

Resultado:

- Caracteres gregos
- Texto ilegível
- EBCDIC fazendo o que EBCDIC faz

Solução elegante:

1. Resolver template no USS
2. Copiar para dataset com encoding correto

Exemplo:

```
- name: Copy JCL to z/OS
  zos_copy:
    src:  "{{ temp_dir.path }}/CSTMRUN.jcl"
    dest: "{{ ansible_user }}.TEMP.JCL(CSTMRUN)"
    remote_src: true
    force: true
    encoding:
      from: ISO8859-1
      to: IBM-1047
  when: env == target_env
```

Aqui começa o verdadeiro aprendizado:

> Automação no mainframe exige entender encoding profundamente.

------

# 😅 O Inimigo Invisível: Espaço Antes de `//`

Depois de resolver encoding…

Novo problema:

Espaços antes do delimitador `//`.

Resultado:

- JCL ERROR no spool
- Timeout no playbook
- JES olhando para você com desdém

Isso acontece porque o Jinja2 adiciona whitespace se não for configurado corretamente.

Solução clássica:

- `trim_blocks`
- `lstrip_blocks`
- Controle rígido de indentação

Mainframe não perdoa espaços.

------

# 🎓 Lições Aprendidas

✔ Automação funciona no z/OS
 ✔ Encoding é crítico
 ✔ Jinja2 exige disciplina
 ✔ Pipeline mainframe é possível
 ✔ Infraestrutura como Código é realidade

Mas…

Ainda estou refinando o fluxo completo para atingir aquela “beleza arquitetural” que todo DevOps sonha.

------

# 💎 Conclusão Bellacosa

O mainframe não é um obstáculo para DevOps.

Ele só exige respeito técnico.

Automatizar no IBM Z com Ansible é possível — e poderoso.

Mas exige:

- Entender JCL profundamente
- Entender encoding EBCDIC
- Entender JES
- Entender RACF
- Entender pipeline moderno

Quando você junta tudo isso…

Você não é mais apenas programador COBOL.

Você vira engenheiro de automação do core bancário.