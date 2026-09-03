# Entrega — Atividade Prática Aula 3 (Redis Cloud)

**Disciplina:** IBD-016 — Banco de Dados Não Relacional
**Nome do aluno:** _(Manoel Felipe Vieira Gomes)_
**Data de execução:** _(02/09/2026)_
**Nome do banco criado no Redis Cloud:** _(aula-03)_
**Ferramenta utilizada:** _(Google Colab)_

> Instruções: para cada passo, execute o comando indicado (via RedisInsight, `redis-cli` ou Google Colab) e cole a saída real obtida no campo correspondente, adicionando o print da tela logo abaixo. Se estiver usando o **Google Colab**, o print pode ser da célula executada com seu código e a saída exibida abaixo dela — não é necessário usar a sintaxe nativa do Redis, os métodos Python (`r.set()`, `r.get()`, etc.) são aceitos normalmente. Para inserir uma imagem no GitHub, arraste o arquivo de print para dentro desta caixa de edição — o link é gerado automaticamente no formato `![descrição](nome-da-imagem.png)`.

---

## Passo 1 — Criar o contador zerado

**Comando/código executado:**
```
r.set("visitas:pagina", 0)
r.get("visitas:pagina")
```

**Saída obtida:**
```
(0)
```

**Print da tela:**

![passo 1 - criar contador](/prints/tela01.png)

---

## Passo 2 — Simular 5 acessos (INCR executado 5 vezes)

**Comandos/código executados:**
```
r.incr("visitas:pagina")
r.incr("visitas:pagina")
r.incr("visitas:pagina")
r.incr("visitas:pagina")
r.incr("visitas:pagina")

r.get("visitas:pagina")
```

**Saída obtida (valor final do GET):**
```
5
```

**Print da tela:**

![passo 2 - simular acessos](/prints/tela02.png)

---

## Passo 3 — Definir expiração de 5 minutos (300 segundos)

**Comandos/código executados:**
```
r.expire("visitas:pagina", 300)
r.ttl("visitas:pagina")
```

**Saída obtida:**
```
300
```

**Print da tela:**

![passo 3 - expiração TTL](/prints/tela03.png)

---

## Passo 4 — Criar o cadastro do usuário como hash

**Comandos/código executados:**
```
r.hset("usuario:1", mapping={"nome": "Manoel", "email": "lipemanoel3@gmail.com"})
r.hget("usuario:1", "Manoel")

r.hgetall("usuario:1")
```

**Saída obtida:**
```
{'nome': 'Manoel', 'email': 'lipemanoel3@gmail.com'}
```

**Print da tela:**

![passo 4 - hash usuario](/prints/tela04.png)

---

## Passo 5 — Reflexão final (2 a 3 linhas)

_Explique com suas palavras: por que o comando `INCR` é útil para um contador, e por que faz sentido usar `EXPIRE` nesse cenário?_

```
O comando `INCR` é importante para um contador porque aumenta o valor de uma chave, o que ajuda no controle de quantas vezes algo aconteceu. O `EXPIRE` faz sentido porque permite definir um tempo para o contador, evitando que ele fique armazenado no Redis o tempo todo.

```

---

## Checklist antes de enviar

- [ ] Todos os 4 passos têm comando, saída e print preenchidos
- [ ] As imagens abrem corretamente ao visualizar o arquivo `.md` (confira antes de enviar)
- [ ] A reflexão final do Passo 5 foi respondida
- [ ] Nome do aluno e data preenchidos no topo do arquivo
