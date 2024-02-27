# labpesquisaai900
## Repositório do laboratório da DIO sobre pesquisa de documentação e avaliação de sentimento para certificação AI-900

Como sempre laboratórios muito proveito!
Mas gostaria de deixar uma dica de complemento dos estudos, que foi passado na mentoria da Glacia, segue link:
[Generative AI for Beginners](https://microsoft.github.io/generative-ai-for-beginners/#/)

Neste laboratório aprendi como criar um sistema de pesquisa utilizando AI.

Criar recursos do Azure
Extrair dados de uma fonte de dados
Enriqueça dados com habilidades de IA
Usar o indexador do Azure no portal do Azure
Consultar seu índice de pesquisa
Revisar resultados salvos em um Knowledge Store

# Criar um recurso de Pesquisa de IA do Azure
Entre no portal do Azure.

Clique no botão + Criar um recurso, procure Pesquisa de IA do Azure e crie um recurso de Pesquisa de IA do Azure com as seguintes configurações:

Assinatura: sua assinatura do Azure.
Grupo de recursos: selecione ou crie um grupo de recursos com um nome exclusivo.
Nome do serviço: um nome exclusivo.
Localização: Escolha qualquer região disponível.
Nível de preços: Básico
Selecione Revisar + criar e, depois de ver a resposta Êxito da validação, selecione Criar.

Após a conclusão da implantação, selecione Ir para o recurso. Na página de visão geral da Pesquisa de IA do Azure, você pode adicionar índices, importar dados e pesquisar índices criados.

# Criar um recurso de serviços de IA do Azure
Você precisará provisionar um recurso de serviços de IA do Azure que esteja no mesmo local que seu recurso de Pesquisa de IA do Azure. Sua solução de pesquisa usará esse recurso para enriquecer os dados no armazenamento de dados com insights gerados por IA.

Retorne à home page do portal do Azure. Clique no botão +Criar um recurso e procure serviços de IA do Azure. Selecione criar um plano de serviços de IA do Azure. Você será levado a uma página para criar um recurso de serviços de IA do Azure. Configure-o com as seguintes configurações:
Assinatura: sua assinatura do Azure.
Grupo de recursos: o mesmo grupo de recursos que seu recurso de Pesquisa de IA do Azure.
Região: o mesmo local que seu recurso de Pesquisa de IA do Azure.
Nome: Um nome exclusivo.
Nível de preços: Standard S0
Ao marcar esta caixa reconheço que li e compreendi todos os termos abaixo: Selecionado
Selecione Revisar + criar. Depois de ver a resposta Validação aprovada, selecione Criar.

Aguarde a conclusão da implantação e exiba os detalhes da implantação.

# Criar uma conta de armazenamento
Retorne à home page do portal do Azure e selecione o botão + Criar um recurso.

Procure uma conta de armazenamento e crie um recurso de conta de armazenamento com as seguintes configurações:
Assinatura: sua assinatura do Azure.
Grupo de recursos: o mesmo grupo de recursos que os recursos da Pesquisa de IA do Azure e dos serviços de IA do Azure.
Nome da conta de armazenamento: um nome exclusivo.
Localização: Escolha qualquer local disponível.
Desempenho: Standard
Redundância: Armazenamento localmente redundante (LRS)
Clique em Rever e, em seguida, clique em Criar. Aguarde a conclusão da implantação e vá para o recurso implantado.

Na conta de Armazenamento do Azure que você criou, no painel de menu esquerdo, selecione Configuração (em Configurações).
Altere a configuração de Permitir acesso anônimo de Blob para Habilitado e selecione Salvar.

# Carregar documentos no Armazenamento do Azure
No painel de menu esquerdo, selecione Contêineres.
Selecione + Contêiner. Um painel do lado direito é aberto.

Insira as seguintes configurações e clique em Criar:
Nome: café-comentários
Nível de acesso público: Contêiner (acesso de leitura anônimo para contêineres e blobs)
Avançado: sem alterações.
Em uma nova guia do navegador, baixe as revisões de café compactadas do e extraia os arquivos para a pasta de comentários.https://aka.ms/mslearn-coffee-reviews
No portal do Azure, selecione seu contêiner de avaliações de café. No contêiner, selecione Carregar.
No painel Carregar blob, selecione Selecionar um arquivo.
Na janela do Explorer, selecione todos os arquivos na pasta de comentários, selecione Abrir e selecione Carregar.
Depois que o carregamento for concluído, você poderá fechar o painel Carregar blob. Seus documentos agora estão em seu recipiente de armazenamento de revisões de café.

# Indexar os documentos
No portal do Azure, navegue até seu recurso de Pesquisa de IA do Azure. Na página Visão geral, selecione Importar dados.
Captura de tela que mostra o assistente de importação de dados.
Na página Conectar aos seus dados, na lista Fonte de Dados, selecione Armazenamento de Blobs do Azure. Conclua os detalhes do armazenamento de dados com os seguintes valores:
Fonte de dados: Armazenamento de Blobs do Azure
Nome da fonte de dados: coffee-customer-data
Dados a serem extraídos: conteúdo e metadados
Modo de análise: Padrão
Cadeia de conexão: *Selecione Escolher uma conexão existente. Selecione sua conta de armazenamento, selecione o contêiner de revisões de café e clique em Selecionar.
Autenticação de identidade gerenciada: Nenhuma
Nome do contêiner: essa configuração é preenchida automaticamente depois que você escolhe uma conexão existente.
Pasta Blob: deixe isso em branco.
Descrição: Comentários a Fourth Coffee shops.
Selecione Avançar: Adicionar habilidades cognitivas (Opcional).
Na seção Anexar Serviços Cognitivos, selecione seu recurso de serviços de IA do Azure.

Na seção Adicionar enriquecimentos:
Altere o nome do Skillset para coffee-skillset.
Marque a caixa de seleção Habilitar OCR e mesclar todo merged_content texto em campo.
Nota É importante selecionar Habilitar OCR para ver todas as opções de campo enriquecidas.

Verifique se o campo Dados de origem está definido como merged_content.
Altere o nível de granularidade de enriquecimento para Páginas (blocos de 5000 caracteres).
Não selecione Habilitar enriquecimento incremental
Selecione os seguintes campos enriquecidos:

Habilidade Cognitiva	Parâmetro	Nome do campo
Extrair nomes de locais	 	Locais
Extrair frases-chave	 	Frases-chave
Detectar sentimento	 	sentimento
Gerar tags a partir de imagens	 	imageTags
Gerar legendas a partir de imagens	 	imageCaption
Em Salvar enriquecimentos em um repositório de conhecimento, selecione:
Projeções de imagens
Documentos
Páginas
Frases-chave
Entidades
Detalhes da imagem
Referências de imagens
Nota Se um aviso solicitando uma Cadeia de Conexão da Conta de Armazenamento for exibido.

Captura de tela que mostra o aviso da tela de conexão da conta de armazenamento com a opção "Escolher uma conexão existente" selecionada.

Selecione Escolher uma conexão existente. Escolha a conta de armazenamento criada anteriormente.
Clique em + Contêiner para criar um novo contêiner chamado knowledge-store com o nível de privacidade definido como Privado e selecione Criar.
Selecione o contêiner de armazenamento de conhecimento e clique em Selecionar na parte inferior da tela.
Selecione Projeções de blob do Azure: Documento. Uma configuração para Nome do contêiner com as exibições preenchidas automaticamente pelo contêiner do repositório de conhecimento. Não altere o nome do contêiner.

Selecione Avançar: Personalizar índice de destino. Altere o nome do índice para coffee-index.

Verifique se a chave está definida como metadata_storage_path. Deixe o nome do Sugeridor em branco e o modo de Pesquisa preenchido automaticamente.

Revise as configurações padrão dos campos de índice. Selecione filtrável para todos os campos que já estão selecionados por padrão.

Captura de tela que mostra o painel personalizar índice com o nome do índice inserido e 'Filtrável' selecionado para um campo de índice padrão.

Selecione Avançar: Criar um indexador.

Altere o nome do indexador para coffee-indexer.

Deixe a Agenda definida como Uma vez.

Expanda as opções Avançadas. Verifique se a opção Base-64 Encode Keys está selecionada, pois as chaves de codificação podem tornar o índice mais eficiente.

Selecione Enviar para criar a fonte de dados, o conjunto de habilidades, o índice e o indexador. O indexador é executado automaticamente e executa o pipeline de indexação, que:
Extrai os campos de metadados do documento e o conteúdo da fonte de dados.
Executa o conjunto de habilidades cognitivas para gerar campos mais enriquecidos.
Mapeia os campos extraídos para o índice.
Retorne à página de recursos da Pesquisa de IA do Azure. No painel esquerdo, em Gerenciamento de Pesquisa, selecione Indexadores. Selecione o indexador de café recém-criado. Aguarde um minuto e selecione &orarr; Atualize até que o Status indique êxito.

Selecione o nome do indexador para ver mais detalhes.

Captura de tela que mostra o indexador de café criado com êxito.

Consultar o índice
Use o Gerenciador de pesquisa para escrever e testar consultas. O explorador de pesquisa é uma ferramenta incorporada no portal do Azure que oferece uma maneira fácil de validar a qualidade do seu índice de pesquisa. Você pode usar o Gerenciador de pesquisa para escrever consultas e revisar resultados em JSON.

Na página Visão geral do serviço de Pesquisa, selecione Gerenciador de pesquisa na parte superior da tela.

Captura de tela de como encontrar o Gerenciador de pesquisa.

Observe como o índice selecionado é o índice de café que você criou. Abaixo do índice selecionado, altere a exibição para JSON view.

Captura de ecrã do explorador de pesquisa.

No campo Editor de consultas JSON, copie e cole:

Código
{
    "search": "*",
    "count": true
}
Selecione Pesquisar. A consulta de pesquisa retorna todos os documentos no índice de pesquisa, incluindo uma contagem de todos os documentos no campo @odata.count. O índice de pesquisa deve retornar um documento JSON contendo os resultados da pesquisa.

Agora vamos filtrar por localização. No campo Editor de consultas JSON, copie e cole:
Código
{
 "search": "locations:'Chicago'",
 "count": true
}
Selecione Pesquisar. A consulta pesquisa todos os documentos no índice e filtra por revisões com um local de Chicago. Você deve ver no campo.3@odata.count

Agora vamos filtrar por sentimento. No campo Editor de consultas JSON, copie e cole:
Código
{
 "search": "sentiment:'negative'",
 "count": true
}
Selecione Pesquisar. A consulta pesquisa todos os documentos no índice e filtra por avaliações com um sentimento negativo. Você deve ver no campo.1@odata.count

Nota Veja como os resultados são classificados por . Esta é a pontuação atribuída pelo mecanismo de pesquisa para mostrar o quanto os resultados correspondem à consulta dada.@search.score

Um dos problemas que podemos querer resolver é por que pode haver certas revisões. Vamos dar uma olhada nas frases-chave associadas à avaliação negativa. O que você acha que pode ser a causa da revisão?
Revisar o repositório de conhecimento
Vamos ver o poder do armazenamento de conhecimento em ação. Ao executar o assistente Importar dados, você também criou um repositório de conhecimento. Dentro da loja de conhecimento, você encontrará os dados enriquecidos extraídos pelas habilidades de IA persistem na forma de projeções e tabelas.

No portal do Azure, navegue de volta para sua conta de armazenamento do Azure.

No painel de menu esquerdo, selecione Contêineres. Selecione o contêiner de armazenamento de conhecimento.

Captura de tela do contêiner do armazenamento de conhecimento.

Selecione qualquer um dos itens e clique no arquivo objectprojection.json.

Captura de tela do objectprojection.json.

Selecione Editar para ver o JSON produzido para um dos documentos do armazenamento de dados do Azure.

Captura de tela de como localizar o botão de edição.

Selecione a trilha de blob de armazenamento no canto superior esquerdo da tela para retornar aos Contêineres da conta de armazenamento.

Captura de tela da trilha de blob de armazenamento.

Em Contêineres, selecione o contêiner coffee-skillset-image-projection. Selecione qualquer um dos itens.

Captura de tela do contêiner do conjunto de habilidades.

Selecione qualquer um dos .jpg arquivos. Selecione Editar para ver a imagem armazenada do documento. Observe como todas as imagens dos documentos são armazenadas dessa maneira.

Captura de tela da imagem salva.

Selecione a trilha de blob de armazenamento no canto superior esquerdo da tela para retornar aos Contêineres da conta de armazenamento.

Selecione Navegador de armazenamento no painel esquerdo e selecione Tabelas. Há uma tabela para cada entidade no índice. Selecione a tabela coffeeSkillsetKeyPhrases
