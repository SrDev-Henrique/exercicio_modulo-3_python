# Módulo 3 — Python: Fluxo Condicional & Repetição

Notas e aprendizados do exercício **Dados de interação de usuários com propagandas online** (EBAC).

---

## Sobre o exercício

O exercício trabalha com uma lista de dicionários (`propaganda_online`), onde cada item representa um usuário que visitou um site. Os campos incluem tempo no site, idade, renda, cidade, país e se clicou em um anúncio.

O objetivo foi filtrar e extrair informações específicas usando três estruturas fundamentais do Python:

1. **`for / in`** — percorrer a lista
2. **`if / else`** — aplicar condições
3. **`try / except`** — tratar dados incompletos ou inválidos

---

## Estrutura dos dados

Cada registro é um dicionário com chaves como:

| Campo | Tipo | Descrição |
|---|---|---|
| `tempo_gasto_site` | `float` ou `None` | Segundos no site |
| `idade` | `int` | Idade do usuário |
| `renda_area` | `float` | Renda na região |
| `tempo_gasto_internet` | `float` | Tempo de internet |
| `cidade` | `str` | Cidade |
| `pais` | `str` | País |
| `clicou_no_ad` | `0` ou `1` | Se clicou na propaganda (pode estar ausente) |

Dois registros foram propositalmente “imperfeitos” para exercitar o tratamento de erros:

- Um usuário com `tempo_gasto_site: None`
- Um usuário sem a chave `clicou_no_ad`

Isso simula dados reais de analytics, onde nem todo campo vem preenchido.

---

## Soluções e resultados

### 1.1 — Países de usuários com mais de 30 anos

```python
paises = []
for dado_de_usuario in propaganda_online:
  if dado_de_usuario['idade'] > 30:
    paises.append(dado_de_usuario['pais'])
```

**Resultado:** `['Tunisia', 'Nauru', 'Iceland', 'Myanmar', 'Australia']`

**Aprendizado:** o operador `>` é estrito. Usuários com exatamente 30 anos **não** entram na lista — apenas quem tem 31 ou mais.

---

### 1.2 — Renda dos usuários que clicaram na propaganda

```python
leads = []
for dado_de_usuario in propaganda_online:
  try:
    if dado_de_usuario['clicou_no_ad'] == 1:
      leads.append(dado_de_usuario['renda_area'])
  except KeyError:
    pass
```

**Resultado:** `[24593.33]`

**Aprendizado:** acessar uma chave inexistente em um dicionário gera `KeyError`. O `try/except` evita que o programa pare quando encontra um registro sem `clicou_no_ad`. Em Python, o equivalente ao `catch` de outras linguagens é `except`.

---

### 1.3 — Cidades de usuários com mais de 70 segundos no site

```python
cidades = []
for dado_de_usuario in propaganda_online:
  try:
    if dado_de_usuario['tempo_gasto_site'] > 70:
      cidades.append(dado_de_usuario['cidade'])
  except TypeError:
    pass
```

**Resultado:** `['West Jodi', 'Brandonstad', 'West Colin']`

**Aprendizado:** comparar `None > 70` gera `TypeError`, porque `None` não é um número. O `except TypeError` ignora registros com valor ausente e continua processando os demais.

---

## Conceitos-chave

### Loop `for / in`

Percorre cada elemento de uma sequência (lista, tupla, string etc.):

```python
for item in lista:
  # faz algo com item
```

No exercício, cada `dado_de_usuario` é um dicionário dentro da lista `propaganda_online`.

### Condicional `if`

Executa um bloco somente quando a condição é verdadeira:

```python
if condicao:
  # código
```

Condições usadas no exercício:

- `idade > 30`
- `clicou_no_ad == 1`
- `tempo_gasto_site > 70`

### Tratamento de erros `try / except`

Em Python não existe `catch` — usa-se `except`:

```python
try:
  # código que pode falhar
except TipoDoErro:
  # o que fazer se falhar
```

| Erro | Quando ocorre |
|---|---|
| `KeyError` | Chave inexistente no dicionário |
| `TypeError` | Operação inválida entre tipos (ex.: `None > 70`) |

O `pass` dentro do `except` significa “não faça nada” — apenas pule aquele registro e siga em frente.

---

## Padrão geral do exercício

Os três problemas seguem a mesma estrutura:

1. Criar uma lista vazia
2. Iterar com `for`
3. Aplicar uma condição com `if`
4. Adicionar o valor desejado com `.append()`
5. Tratar exceções quando os dados podem estar incompletos

Esse padrão aparece com frequência em análise de dados, APIs e ETL: percorrer registros, filtrar e montar uma nova coleção.

---

## Arquivos do projeto

| Arquivo | Descrição |
|---|---|
| `Python_M3_support material03_exercise.ipynb` | Notebook com o exercício e as soluções |

---

## Como executar

1. Abra o notebook no Jupyter, VS Code ou Google Colab
2. Execute as células na ordem, começando pela definição de `propaganda_online`
3. Confira os `print()` ao final de cada exercício

---

## Referências

- Módulo EBAC: **Python — Fluxo Condicional & Repetição**
- Professor: [André Perez](https://www.linkedin.com/in/andremarcosperez/)
