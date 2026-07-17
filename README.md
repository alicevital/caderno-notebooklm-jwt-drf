# Caderno Temático com NotebookLM: Autenticação JWT e Segurança em APIs REST

> Projeto desenvolvido para o desafio da [DIO](https://www.dio.me/), utilizando Inteligência Artificial como ferramenta de aprendizagem ativa, curadoria de fontes e organização do conhecimento.

## 📌 Sobre o projeto

Este repositório documenta a criação de um caderno temático no NotebookLM sobre **autenticação JWT e segurança em APIs REST desenvolvidas com Django REST Framework**.

O tema foi escolhido por sua relevância no desenvolvimento backend e por estar diretamente relacionado à construção de aplicações que precisam identificar usuários, controlar acessos e proteger dados e endpoints.

Além de reunir conceitos técnicos, o projeto registra a evolução dos prompts utilizados, as limitações encontradas durante as consultas e um miniguia final para futuras revisões.

## 🎯 Objetivos de estudo

- Compreender a diferença entre autenticação e autorização.
- Entender a estrutura e o funcionamento de um JSON Web Token.
- Diferenciar access tokens e refresh tokens.
- Compreender como o Django REST Framework processa a autenticação.
- Conhecer o uso do Simple JWT em APIs Django.
- Identificar riscos comuns relacionados à autenticação de APIs.
- Desenvolver prompts mais específicos, verificáveis e reutilizáveis.
- Consolidar o conteúdo em um material de revisão rápida.

## 🧠 Ferramenta utilizada

O **NotebookLM** foi utilizado para organizar as fontes, formular perguntas e gerar respostas fundamentadas no material selecionado.

> Link do caderno no NotebookLM: **[https://notebooklm.google.com/notebook/4ff9de20-6ae4-457d-aa07-f44ed179c65e]**

## 📚 Curadoria de fontes

Foram priorizadas fontes oficiais, abertas e diretamente relacionadas ao tema.

| Fonte | Conteúdo principal | Motivo da escolha |
|---|---|---|
| [RFC 7519 — JSON Web Token](https://www.rfc-editor.org/info/rfc7519/) | Definição técnica do padrão JWT | É a especificação oficial do formato JWT |
| [Sistema de autenticação do Django](https://docs.djangoproject.com/en/6.0/topics/auth/default/) | Usuários, senhas, sessões, autenticação e autorização | Apresenta a base de autenticação utilizada pelo Django |
| [Authentication — Django REST Framework](https://www.django-rest-framework.org/api-guide/authentication/) | Classes e fluxo de autenticação em APIs DRF | Explica como o DRF identifica o usuário de uma requisição |
| [Simple JWT — Getting Started](https://django-rest-framework-simplejwt.readthedocs.io/en/stable/getting_started.html) | Instalação e configuração da autenticação JWT | Mostra a implementação de JWT no Django REST Framework |
| [OWASP API Security Top 10 — 2023](https://owasp.org/API-Security/editions/2023/en/0x11-t10/) | Principais riscos de segurança em APIs | Relaciona falhas de autenticação e autorização a riscos reais |

## 🔎 Critérios utilizados na curadoria

As fontes foram avaliadas de acordo com os seguintes critérios:

1. autoria ou manutenção por organização reconhecida;
2. acesso público ao conteúdo;
3. relação direta com o tema;
4. presença de definições técnicas ou recomendações práticas;
5. possibilidade de comparação entre documentação, padrão técnico e segurança.

## 🧪 Engenharia de prompts

A estratégia adotada foi começar com perguntas gerais e, em seguida, melhorar os prompts com contexto, formato de resposta, critérios de comparação e exigência de referências.

### Experimento 1 — Conceito de JWT

**Prompt inicial**

```text
O que é JWT?
```

**Limitação identificada**

A pergunta é ampla e pode gerar uma explicação genérica, sem diferenciar estrutura, assinatura, criptografia e finalidade.

**Prompt melhorado**

```text
Com base exclusivamente nas fontes adicionadas, explique o que é um JSON Web Token para uma pessoa desenvolvedora backend iniciante. Apresente sua estrutura, a função de cada parte, o que a assinatura garante e o que ela não garante. Cite as fontes utilizadas.
```

**Aprendizado consolidado**

JWT é um formato compacto e seguro para transporte em URLs, usado para representar declarações, chamadas de *claims*, entre duas partes. Normalmente, um token assinado possui três partes separadas por pontos: cabeçalho, payload e assinatura.

A assinatura permite verificar a integridade e a autenticidade do token, mas não torna automaticamente o conteúdo secreto. O payload pode ser decodificado, portanto dados sensíveis não devem ser armazenados nele sem uma estratégia adicional de proteção.

**Referências esperadas no NotebookLM**

- RFC 7519;
- documentação do Simple JWT.

---

### Experimento 2 — Autenticação e autorização

**Prompt inicial**

```text
Qual é a diferença entre autenticação e autorização?
```

**Limitação identificada**

A resposta inicial pode apresentar apenas definições abstratas, sem demonstrar como os conceitos aparecem em uma API.

**Prompt melhorado**

```text
Compare autenticação e autorização em uma tabela. Inclua definição, pergunta respondida por cada processo, exemplo em uma API Django REST Framework e consequência de uma implementação incorreta. Use apenas as fontes fornecidas e cite as referências.
```

**Aprendizado consolidado**

| Conceito | Pergunta principal | Exemplo |
|---|---|---|
| Autenticação | Quem está fazendo a requisição? | Validar um token e associar a requisição a um usuário |
| Autorização | O usuário pode realizar esta ação? | Permitir que apenas o proprietário altere uma tarefa |

A autenticação identifica o usuário. A autorização verifica suas permissões. Uma API pode autenticar corretamente uma pessoa e, ainda assim, apresentar uma falha grave de autorização caso permita que ela acesse objetos pertencentes a outros usuários.

**Referências esperadas no NotebookLM**

- documentação de autenticação do Django;
- documentação de autenticação do Django REST Framework;
- OWASP API Security Top 10.

---

### Experimento 3 — Access token e refresh token

**Prompt inicial**

```text
Explique access token e refresh token.
```

**Limitação identificada**

A pergunta não exige a explicação do fluxo completo nem considera expiração, renovação e comprometimento dos tokens.

**Prompt melhorado**

```text
Explique o ciclo de autenticação com access token e refresh token no Simple JWT. Organize a resposta em etapas, desde o login até a renovação do acesso. Inclua finalidade, duração relativa, riscos e boas práticas para cada token.
```

**Aprendizado consolidado**

1. O usuário envia suas credenciais para o endpoint de autenticação.
2. A aplicação valida as credenciais.
3. O servidor retorna um access token e um refresh token.
4. O access token é enviado nas requisições protegidas.
5. Quando o access token expira, o refresh token pode solicitar um novo token de acesso.
6. Quando necessário, o refresh token deve ser invalidado, rotacionado ou incluído em uma lista de bloqueio.

O access token deve ter vida mais curta porque circula com maior frequência. O refresh token costuma permanecer válido por mais tempo e, por isso, exige proteção adicional.

---

### Experimento 4 — Segurança da autenticação

**Prompt inicial**

```text
Como proteger uma API com JWT?
```

**Limitação identificada**

O termo “proteger” é muito amplo. A resposta pode misturar autenticação, autorização, transporte, armazenamento e validação sem estabelecer prioridades.

**Prompt melhorado**

```text
Crie um checklist priorizado para revisar a segurança de uma API Django REST Framework que utiliza JWT. Separe os itens em: transporte, emissão, validação, expiração, autorização, armazenamento e revogação. Relacione os riscos às fontes adicionadas.
```

**Aprendizado consolidado**

- utilizar HTTPS;
- manter access tokens com expiração curta;
- proteger refresh tokens;
- validar assinatura, algoritmo, expiração e claims relevantes;
- não armazenar informações sensíveis no payload;
- aplicar permissões em todos os endpoints protegidos;
- validar o acesso no nível do objeto;
- prever rotação ou bloqueio de refresh tokens;
- limitar tentativas de autenticação;
- registrar eventos suspeitos sem expor credenciais ou tokens nos logs.

## 🩹 Cicatrizes e troubleshooting

### 1. Prompts genéricos produzem respostas genéricas

Perguntas como “O que é JWT?” ajudam em uma introdução, mas não são suficientes para um estudo técnico. A qualidade melhorou quando o prompt passou a definir:

- público-alvo;
- fontes permitidas;
- estrutura da resposta;
- exemplos desejados;
- necessidade de citar evidências;
- pontos que deveriam ser comparados.

### 2. Autenticação não substitui autorização

Uma dificuldade recorrente foi separar os dois conceitos. A solução foi pedir exemplos de endpoints e formular duas perguntas distintas:

```text
Quem está realizando a requisição?
```

```text
Essa pessoa pode acessar ou modificar este recurso específico?
```

### 3. JWT assinado não significa JWT criptografado

Uma resposta superficial pode transmitir a ideia de que o payload está protegido por ser parte de um token assinado. A consulta foi refinada para exigir que a IA explicasse separadamente:

- integridade;
- autenticidade;
- confidencialidade;
- possibilidade de decodificação do payload.

### 4. Compatibilidade entre versões

A documentação consultada do Simple JWT informa versões oficialmente suportadas de Python, Django e Django REST Framework. Isso mostrou que não se deve assumir compatibilidade apenas porque a instalação foi concluída.

Em projetos que utilizam versões mais recentes do Django, é necessário verificar a documentação atual do pacote, executar testes e validar o comportamento antes de utilizar a biblioteca em produção.

### 5. Limites das fontes

As fontes selecionadas explicam bem o backend, o padrão JWT e riscos de APIs, mas não resolvem sozinhas todas as decisões sobre armazenamento de tokens no frontend. Quando uma resposta ultrapassava o conteúdo das fontes, o prompt foi ajustado para solicitar que a IA:

```text
Informe explicitamente quando as fontes não forem suficientes para responder com segurança, sem completar a resposta com suposições.
```

## 📖 Miniguia de estudo

### 1. O que é autenticação?

Autenticação é o processo utilizado para verificar a identidade de quem está fazendo uma requisição.

Em uma API, ela pode ser realizada por sessão, token, credenciais básicas ou outros mecanismos. Após autenticar a requisição, o Django REST Framework disponibiliza informações como o usuário identificado e os dados de autenticação utilizados.

### 2. O que é autorização?

Autorização determina quais ações um usuário autenticado pode realizar.

Exemplos:

- visualizar somente suas próprias tarefas;
- permitir edição apenas ao proprietário de um recurso;
- restringir determinada rota a administradores;
- permitir leitura pública, mas exigir autenticação para escrita.

### 3. O que é JWT?

JSON Web Token é um formato padronizado para representar claims de maneira compacta.

Um JWT assinado geralmente possui:

```text
header.payload.signature
```

#### Header

Informa metadados do token, como o tipo e o algoritmo utilizado.

#### Payload

Contém as claims, como identificador do usuário, emissor e data de expiração.

#### Signature

Permite verificar se o token foi alterado e se foi assinado pela entidade esperada.

> O payload não deve ser tratado como secreto apenas por estar codificado em Base64URL.

### 4. Claims importantes

| Claim | Significado |
|---|---|
| `sub` | Sujeito representado pelo token |
| `exp` | Data e hora de expiração |
| `iat` | Data e hora de emissão |
| `nbf` | Momento antes do qual o token não deve ser aceito |
| `iss` | Emissor |
| `aud` | Público ou serviço destinatário |
| `jti` | Identificador único do token |

Nem toda aplicação precisa utilizar todas essas claims, mas os campos adotados devem ser validados corretamente.

### 5. Access token

É utilizado para acessar endpoints protegidos.

Características recomendadas:

- expiração curta;
- envio apenas por conexão segura;
- validação em cada requisição;
- conteúdo mínimo necessário;
- ausência de dados sensíveis.

### 6. Refresh token

É utilizado para obter um novo access token sem exigir novamente usuário e senha.

Por permanecer válido por mais tempo, deve receber proteção especial. Dependendo da arquitetura, podem ser adotadas estratégias de rotação, revogação e blacklist.

### 7. Fluxo simplificado no Django REST Framework

```text
1. O cliente envia as credenciais.
2. O servidor valida o usuário e a senha.
3. O servidor emite os tokens.
4. O cliente envia o access token no cabeçalho Authorization.
5. A classe de autenticação valida o token.
6. O DRF identifica o usuário.
7. As classes de permissão avaliam se a ação é permitida.
8. A view processa ou rejeita a requisição.
```

Exemplo de cabeçalho:

```http
Authorization: Bearer <access_token>
```

### 8. Autenticação versus permissão no DRF

A classe de autenticação verifica a identidade apresentada na requisição.

A classe de permissão decide se a requisição poderá continuar.

Exemplo conceitual:

```python
from rest_framework.permissions import IsAuthenticated
from rest_framework.viewsets import ModelViewSet

class TaskViewSet(ModelViewSet):
    permission_classes = [IsAuthenticated]

    def get_queryset(self):
        return Task.objects.filter(owner=self.request.user)
```

A permissão exige um usuário autenticado, enquanto o filtro evita que tarefas de outros usuários sejam retornadas.

> Em uma aplicação real, operações de recuperação, atualização e exclusão também devem validar o acesso ao objeto.

### 9. Principais riscos

#### Broken Authentication

Ocorre quando o mecanismo de autenticação é implementado incorretamente e permite comprometimento de credenciais ou tokens.

#### Broken Object Level Authorization

Ocorre quando a API aceita um identificador de objeto, mas não verifica se o usuário pode acessar aquele recurso.

Exemplo de risco:

```text
GET /api/tasks/52/
```

Mesmo autenticado, um usuário não deveria acessar a tarefa `52` quando ela pertence a outra pessoa.

### 10. Checklist de revisão

#### Transporte

- [ ] A API utiliza HTTPS?
- [ ] Tokens e credenciais estão ausentes dos logs?
- [ ] Dados sensíveis não são enviados em URLs?

#### Emissão e validação

- [ ] A assinatura é validada?
- [ ] O algoritmo permitido está definido?
- [ ] A expiração é validada?
- [ ] Claims como emissor e público são verificadas quando aplicáveis?
- [ ] O token contém apenas dados necessários?

#### Autorização

- [ ] Todos os endpoints privados possuem classes de permissão?
- [ ] O acesso é validado no nível do objeto?
- [ ] Consultas são filtradas pelo usuário quando necessário?
- [ ] Perfis administrativos possuem regras explícitas?

#### Renovação e revogação

- [ ] O access token possui duração curta?
- [ ] O refresh token é armazenado de forma protegida?
- [ ] Existe uma estratégia de rotação ou revogação?
- [ ] O logout invalida os tokens conforme a necessidade do sistema?

#### Monitoramento

- [ ] Tentativas repetidas de login são limitadas?
- [ ] Eventos suspeitos são registrados?
- [ ] Segredos e chaves possuem estratégia de rotação?

## 📘 Glossário

| Termo | Definição |
|---|---|
| API | Interface utilizada para comunicação entre sistemas |
| Autenticação | Verificação da identidade de um usuário ou cliente |
| Autorização | Verificação das ações permitidas para uma identidade |
| Claim | Informação declarada dentro de um JWT |
| JWT | Formato compacto para representação de claims |
| Access token | Token usado para acessar recursos protegidos |
| Refresh token | Token usado para solicitar um novo access token |
| Bearer token | Token cujo portador pode utilizá-lo para acessar um recurso |
| Payload | Parte do JWT que armazena as claims |
| Assinatura | Mecanismo que permite verificar integridade e autenticidade |
| Expiração | Limite de tempo de validade de um token |
| Revogação | Processo de invalidar um token antes de sua expiração |
| Rotação | Substituição de um token ou segredo por uma nova versão |
| Blacklist | Lista de tokens que não devem mais ser aceitos |
| HTTPS | Protocolo HTTP protegido por TLS |
| BOLA | Falha de autorização no nível do objeto |
| DRF | Django REST Framework |
| Endpoint | Endereço de uma operação disponibilizada por uma API |

## ♻️ Prompts reutilizáveis

### Resumo estruturado

```text
Com base somente nas fontes do caderno, produza um resumo do tema [TEMA]. Organize em definição, funcionamento, exemplo, riscos e boas práticas. Cite as fontes em cada seção.
```

### Comparação de conceitos

```text
Compare [CONCEITO A] e [CONCEITO B] em uma tabela com definição, finalidade, exemplo prático, riscos e situação recomendada de uso. Não utilize informações externas às fontes.
```

### Revisão para entrevista

```text
Crie 10 perguntas de entrevista técnica sobre [TEMA], divididas entre nível básico, intermediário e avançado. Após cada pergunta, apresente uma resposta esperada e indique a fonte.
```

### Identificação de lacunas

```text
Analise as fontes e identifique quais questões importantes sobre [TEMA] não podem ser respondidas de forma completa. Não faça suposições. Sugira quais tipos de fontes adicionais seriam necessários.
```

### Checklist técnico

```text
Crie um checklist para revisar uma implementação de [TECNOLOGIA]. Organize os itens por prioridade e relacione cada recomendação ao risco que ela procura reduzir.
```

### Aprendizagem ativa

```text
Atue como tutor. Faça uma pergunta por vez sobre [TEMA], espere minha resposta, identifique possíveis erros conceituais e explique a correção usando as fontes do caderno.
```

### Cenário prático

```text
Crie um cenário de falha em uma API relacionada a [TEMA]. Peça que eu encontre o problema antes de revelar a solução. Depois, explique o risco, a correção e as fontes utilizadas.
```

## 💡 Principais aprendizados

- A qualidade da resposta depende da qualidade das fontes e da precisão do prompt.
- Pedir citações facilita a verificação das respostas.
- Prompts com contexto e formato definido produzem materiais mais úteis.
- A IA não substitui a leitura crítica da documentação.
- Uma resposta coerente ainda pode ultrapassar ou interpretar incorretamente as fontes.
- Segurança exige autenticação, autorização e validações no nível do objeto.
- JWT é um formato de token, não uma solução completa de segurança.
- Compatibilidade de bibliotecas deve ser confirmada, não presumida.

## 🛠️ Como reproduzir este projeto

1. Acesse o NotebookLM.
2. Crie um novo caderno.
3. Adicione de três a cinco fontes.
4. Execute os prompts iniciais.
5. Registre respostas, citações e limitações.
6. Reformule os prompts com critérios mais específicos.
7. Compare as novas respostas com as fontes.
8. Consolide os aprendizados no miniguia.
9. Revise os trechos marcados neste README.
10. Publique o repositório no GitHub.

## 👩‍💻 Autoria

Desenvolvido por **[Alice Emily Vital do Nascimento]**.

- GitHub: [https://github.com/alicevital]
- LinkedIn: [https://www.linkedin.com/in/alice-nascimento-3821bb2b7/]
