# Corpus ALiB-Twitter

O conjunto de dados tem a cobertura de um período de 10 anos, entre 01 de janeiro de 2013 à 31 de dezembro de 2022, período este que foi dividido em duas janelas de 5 anos cada, nomeadas **Janelas A e B**. A **Janela A** compreende o período de 01 de janeiro de 2013 à 31 de dezembro de 2017 e a **Janela B** o período de 01 de janeiro de 2018 à 31 de dezembro de 2022. 
Nomeado de CorpusALiB-Twitter, este é oriundo da coleta de tweets (Um tweet é uma mensagem curta, com um limite de 140 ou 280 caracteres, publicada na plataforma de mídia social Twitter. Os tweets podem conter texto, imagens, GIFs, vídeos e links) dos últimos 10 anos com a ocorrência de unidades lexicais selecionados do Atlas Linguístico do Brasil (ALiB). 

Para a primeira etapa, coleta e criação de corpus, foi utilizada a ferramenta  [Twarc](https://github.com/DocNow/twarc), uma biblioteca em Python para a coleta dos tweets via API do Twitter, graças à licença de uso de dados para fins acadêmicos, oferecida gratuitamente pela rede social à época da coleta, que permitiu a coleta de 10 milhões de tweets por mês e acesso ao histórico completo de tweets públicos.
    
Para a criação do corpus, foram coletados tweets com ocorrência de termos polissêmicos do Atlas Linguístico do Brasil, publicados entre o período de 01 de janeiro de 2013 a 31 de dezembro de 2022, contemplando uma janela de 10 anos. 

A coleta de tweets é um processo que requer cuidadosa seleção de palavras-chave relevantes e a escolha de ferramentas de coleta adequadas. Além da janela de tempo, foi necessária a utilização de filtros para coleta através do Twarc que excluísse do retorno das buscas tweets de publicidade ou patrocinados, retweets, e foi utilizado o filtro de linguagem para que as buscas retornassem apenas tweets em língua portuguesa. Uma vez que nosso objeto de estudo são os textos dos tweets, também foram removidas, através do parâmetro de busca `--no-context-annotations`, informações de contexto do tweets, que são informações de rótulos de domínio ou entidade inferidas pelo Twitter a partir do texto e consequentemente resultam em arquivos maiores de dados. Podemos observar um exemplo de consulta realizada utilizando a instrução abaixo.

    !twarc2 search --archive --start-time 2013-01-01 --end-time 2022-12-31 --no-context-annotations "{termo} -is:retweet -is:nullcast lang:pt" {termo}.json
      
Uma vez coletados os tweets, foi necessário realizar a limpeza dos dados, como links, imagens, emojis e símbolos que não correspondessem a caracteres da língua portuguesa utilizados na plataforma. Além disso, também foi realizada a remoção de menção a nomes de usuários, garantindo a anonimização dos dados coletados. Em seguida, foi preciso realizar a segmentação dos tweets em tokens, para que pudessem ser analisados com maior precisão. Dessa forma, todas as ocorrências de uma determinada unidade lexical em um período foram substituídos pelo token `{unidade}20132017` para as ocorrências na **Janela A** e `{unidade}20182022` para as ocorrências na **Janela B**.

> O texto acima foi retirado do documento original: [Dissertação de mestrado](https://repositorio.ufba.br/handle/ri/40511) 

## Arquivos

A pasta `corpus` contém os arquivos csv após preprocessamento.
O arquivo `preprocess.py` contém o código utilizado para a limpeza dos dados.
