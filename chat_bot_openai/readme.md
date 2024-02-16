# Conversa com PDFs

Este projeto é um chatbot que permite que você faça perguntas a um PDF. Ele extrai o texto do PDF, divide o texto em pedaços menores para otimizar a busca, cria um vetorstore (base de dados para a busca das respostas) usando a OpenAI, e cria uma cadeia de conversação para a conversa com o PDF.

## Como usar

1. Insira o caminho para o seu PDF quando solicitado.
2. Faça perguntas ao PDF.

## Código

O código principal do projeto está no arquivo `main.py`. Ele usa várias bibliotecas, incluindo `PyPDF2` para ler PDFs, `langchain` para a cadeia de conversação, e `OpenAI` para a criação do vetorstore.

As principais funções do código são:

- `get_pdf_text(pdf_docs)`: Extrai os textos dos PDFs.
- `get_text_chunks(text)`: Divide o texto em pedaços menores, a fim de otimizar a busca.
- `get_vectorstore(text_chunks)`: Cria o vetorstore, que é a base de dados que será usada para a busca das respostas, usando a OpenAI.
- `get_conversation_chain(vectorstore)`: Cria a cadeia de conversação, que é a base para a conversa com o PDF.
- `handle_userinput(user_question, conversation)`: Trata a entrada do usuário e retorna a resposta do PDF.

## Dependências

- PyPDF2
- langchain
- OpenAI

## Contribuições

Contribuições são bem-vindas! Por favor, faça um fork do projeto e abra um Pull Request com suas alterações.

## Licença

Este projeto está licenciado sob a licença MIT.
