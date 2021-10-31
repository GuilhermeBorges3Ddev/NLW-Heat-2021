# NLW 10/2021 - Backend - ✨Node Heat
___

## Instruções para executar o projeto:

- Em uma pasta de sua preferência clone o projeto: ```git clone https://github.com/GuilhermeBorges3Ddev/node_heat.git```
- Dentro da pasta do projeto instale as dependências: ```yarn install```
- Como o projeto usa Node com TSX e Prisma como ORM será necessário rodar as migrations para popular as tabelas: ```yarn prisma migrate dev```
- Com as dependências instaladas, rode o Prisma Studio: ```yarn prisma studio```, será aberta uma janela com a rota http://localhost:5555/
- Rode o Node através do comando: ```yarn dev```. Dessa forma as APIs estarão disponíveis à partir da rota: http://localhost:4000/
- Dentro do projeto deixei uma collection do Imsominia para que você teste os endpoints, o arquivo chama-se: `NlwRequests.json`

## Fluxo dos endpoints depois do projeto executado:

Execute as rotas conforme a ordem de apresentação da tabela, ou seja, a primeira linha da tabela será a primeira requisição a ser chamada,
e assim sucessivamente.

| Endpoint | Função |
| ------ | ------ |
| http://localhost:4000/github | Essa rota lhe devolverá um user_id pego em Applications-OAuth no Github. Lembrando que para executar esse projeto é necessário se logar no Github |
| http://localhost:4000/signin/callback?code={user_id} | Essa rota é automaticamente chamada após sucesso na obtenção do user_id da rota anterior, esse {user_id} é enviado para a nossa aplicação node e é exibido tanto na URI quanto no body da página |
| http://localhost:4000/authenticate | Pegue o {{user_id}} obtido na rota anterior e abra o Imnsomnia, colocando no body do tipo JSON dessa rota, da seguinte maneira: ```{"code": {{user_id}}}```. Execute o send desta requisição POST para obter na response o Bearer Token. Em caso de expiração do token ou de token inválido existem duas tratativas para estes casos.    |
| http://localhost:4000/messages | Temos aqui outra requisição do tipo POST, esta serve para a criação de uma mensagem, abra o Imnsomnia, colocando no body do tipo JSON dessa rota, uma mensagem qualquer, exemplo: ```{"message": "Testando Comunicação}"```. Execute o send desta requisição POST para obter na response os dados da mensagem e também os dados do usuário que enviou esta mensagem, no caso virão seus próprio dados públicos do Github. |
| http://localhost:4000/messages/last3 | Esta requisição do tipo GET retorna as 3 últimas mensagens criadas, pode-se usar tanto o Imnsommia para testar o request quanto o próprio browser, já que esta API não necessita da autenticação via Bearer Token. |
| http://localhost:4000/profile | Essa requisição também é um GET para retorno dos dados do usuário logado, no caso trará informações como o Id gerado no controller de autenticação e as informações do Github. Esta requisição necessita que seja passado o Bearer Token no Imnsommia, para que usuários não autenticados não tenham acesso ao dado retornado na consulta do perfil. |

## Observação:

Como esta aplicação se utiliza de websocket para fazer a messageria em tempo real, acesse o diretório: /node_heat/public/index.html. E com esse HTML simples rode alguma extensão para rodar o client-side, no meu caso eu uso o Live Server do próprio VS Code. 

⊂(◉‿◉)つ Divirta-se! 

