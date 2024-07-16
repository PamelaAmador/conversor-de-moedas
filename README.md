💻 Sobre o Projeto

Explicação do Código
Bibliotecas Importadas: Importamos a biblioteca Gson para desserializar o JSON e as bibliotecas padrão para entrada de dados e conexão HTTP.

Menu de Opções: Usamos o Scanner para receber a entrada do usuário e exibimos as seis opções de conversão de moedas.

Função obterTaxaConversao: Mapeia a opção selecionada para as moedas de origem e destino, obtém a resposta da API e retorna a taxa de conversão.

Função getJsonResponse: Conecta-se à API usando a chave fornecida, lê a resposta JSON e a retorna como uma String.

Classe ApiResponse: Representa a estrutura da resposta da API para facilitar a desserialização usando Gson.
