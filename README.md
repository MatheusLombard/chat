**Agente de IA — Lógica Proposicional**

Este projeto consiste em uma aplicação web capaz de traduzir sentenças de Linguagem Natural (PT-BR) para a Lógica Proposicional (CPC) e vice-versa, utilizando uma estratégia de dicionário fixo e integração com IA.

**🎨 Front-end**

**Tecnologias Utilizadas**

- HTML

- Tailwind CSS

- JavaScript

**Arquitetura de Arquivos**

- index.html

**Como funciona**

A interface foi desenvolvida utilizando HTML e Tailwind CSS, estruturando o formulário em duas seções principais: mapeamento de proposições e entrada do argumento.

Foram implementados três campos para definição de proposições (sendo um obrigatório e dois opcionais) e uma área de texto para a sentença lógica.

O sistema dispõe de um seletor de contexto que alterna entre 'Linguagem Natural para CPC' e 'CPC para Linguagem Natural'. Com base nessa seleção, o script injeta automaticamente o prompt de comando adequado na requisição enviada à API, instruindo o modelo sobre qual tipo de tradução deve ser executada.

Funcionalidade de Exemplo: Outro ponto interessante do front-end é que ele permite, através de um botão, dar um exemplo de como preencher e executar as frases, mostrando ao usuário a forma correta de distribuir os inputs de texto.

**⚙️ Back-end**

**Tecnologias Utilizadas**

- NodeJS

- ExpressJS

- HuggingFace API

**Arquitetura de Arquivos**

- server.js

- api/chat.js

- services/cpcConverter.js

- services/huggingFaceService.js

- Contexto.txt

**Como funciona**

A aplicação é inicializada via node server.js. Este arquivo de entrada é responsável por instanciar o Express, aplicar configurações de segurança (CORS) e levantar o servidor na porta 3000 (ou conforme as variáveis de ambiente).

O fluxo de requisições é gerenciado pelo chatRoutes, que estabelece um endpoint POST na rota api/chat. Ao receber uma chamada, o sistema extrai a propriedade question do corpo da requisição e a encaminha para o serviço de integração.

A comunicação externa é realizada pelo módulo huggingFaceService.js. É nele que reside a função askHuggingFace, configurada com o token de autenticação e o contexto de treinamento específico, servindo de ponte para obter as respostas da IA. Tendo as respostas, é possível levar o JSON para o frontend, onde é tratado e mostrado ao usuário.

**🧠 Estratégia de Tradução**

A estratégia usada para a tradução foi a criação de um dicionário fixo, que permite a substituição literal da Linguagem Natural para o CPC ou vice-versa.

A regra é simples:

- Se aparece um "e", troca pelo símbolo ^

- Se aparece um "ou", vira v

- Se tem um "se... então", vira uma seta -> (representando a implicação).

**Exemplos de Conversão**

CPC -> Linguagem Natural (NL)

Input:

P = João estuda; Q = Maria trabalha; R = Pedro passa;
Transforme para linguagem natural: (P^Q)->R

**Output:**

Se João estuda e Maria trabalha, então Pedro passa.

**Linguagem Natural (NL) -> CPC
**
**Input:**

X = Rafael é filósofo; J = João é médico; Y = Lucas é doutor;
Transforme para o CPC: Se Rafael é filósofo e João é médico, então Lucas é doutor.
**
Output:**

(X^J)->Y
**
⚠️ Limitações e Possibilidades de Melhoria**

Como dito anteriormente, a estratégia utilizou um dicionário fixo, o que acaba limitando o dinamismo da aplicação. Ou seja, o sistema ficou restrito a estruturas de frases específicas ('composições perfeitas'), exigindo que o usuário siga um padrão exato para obter sucesso na tradução entre Linguagem Natural e CPC.

**Melhoria Futura: **Para evoluir o projeto, sugere-se a implementação de campos dinâmicos ou o aumento do limite de inputs para proposições. Isso permitiria escalar a complexidade dos argumentos processados, aceitando fórmulas com mais variáveis do que o limite atual.

**🔗 Links e Recursos**

**Vídeo de Demonstração: ** [Assistir no YouTube](https://youtu.be/h6z3tSNHMu0.)

**Site para Teste:** [Acessar Aplicação](https://chat-alpha-three-59.vercel.app)

**Repositórios**

**🖥️ Frontend: GitHub -** [FrontEnd](https://github.com/MatheusLombard/chat.git)

⚙️** Backend: GitHub -** [BackendChat](https://github.com/MatheusLombard/backendChat.git)
