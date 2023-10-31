# O que fazer e o que não fazer ao criar uma imagem Docker?

Lista de dicas simples para você produzir imagens otimizadas e seguras.

[https://github.com/cicerowordb/dockerimagestips](https://github.com/cicerowordb/dockerimagestips)

## Dica1: Tratar tudo na mesma camada.

Cada camada do de uma imagem Docker é como um sistema de arquivos diferente. E as camadas são independentes entre si. Por isso se você cria um arquivo em uma camada e apaga esse mesmo arquivo em outra ele continua presente na camada original. Se você usar a imagem como ela foi planejada o arquivo não vai estar acessível, mas vai continuar ocupando espaço, deixando seu container maior e isso não é bom. Containers maiores demoram mais a carregar, ocupam espaço desnecessário entre outras coisas desagradáveis que devemos evitar.

Explicar e comparar os exemplos 1 e 2.

## Dica2: Tratar corretamente a sequência das camadas.

As camadas são guardadas em cache e são reaproveitadas desde que camadas anteriores não tenham sofrido modificações. Se uma camada sofrer modificações o cache dela e das camadas posteriores vai ser descartado. Então, é preciso organizar as camadas para que sejam colocadas no começo do Dockerfile as camadas que mudam com menos frequência e no fim as camadas que mudam mais. Obviamente, é difícil prever com precisão as camadas que mudam ou não mudam. Isso depende muito mais das demandas do projeto, mas quanto mais assertivo, mais rápido é o build da imagem.

Explicar e comparar os exemplos 3 e 4.

Explicar e comparar os exemplos 5 e 6.

## Dica3: Use o .dockerignore para evitar vazamentos.

O arquivo ".dockerignore" é um arquivo de configuração usado na criação de imagens Docker, que permite especificar quais arquivos e diretórios devem ser ignorados durante a construção da imagem. Semelhante ao uso de um arquivo ".gitignore" em repositórios Git, o ".dockerignore" ajuda a reduzir o tamanho da imagem e o tempo de construção, evitando a inclusão de arquivos desnecessários, como logs, arquivos temporários e diretórios de desenvolvimento, garantindo que apenas os recursos essenciais sejam incluídos na imagem final. Também serve para evitar que arquivos sigilosos que serão carregados de maneira segura durante a execução da imagem possam ser usados no desenvolvimento sem jamais ir para dentro da imagem.

Explicar o exemplo 7.

## Dica4: Use imagens base

Sendo bem simplista, uma imagem base é uma imagem usada para criar outra. No caso usamos sempre a imagem do Debian 12 até agora para criar nossas imagens. Mas imagine que você mesmo quer criar sua imagem base. Imagine que para um deteminado contexto, sempre que você usa a imagem do Debian 12 você instala os mesmos aplicativos. Então você pode fazer uma imagem com esses aplicativos para reaproveitá-la sem ter de instalar esses mesmos aplicativos todas as vezes que for criar suas imagens. No exemplo que vou utilizar, vou usar uma imagem de Python para rodar uma pequena aplicação de cifra de deslocamento.

Explicar os exemplos 8 e 9

## Dica5: Como tratar informações sigilosas

Informações sigilosas nunca deveriam ser incluídas no seu Dockerfile nem na sua imagem. Existem várias estratégias para isso dependendo do que você precisa, mas duas coisas devem ser sempre lembradas: usar build args e usar volumes. Build args são variáveis de ambiente presentes apenas durante o build e são diferente de env vars. Volumes são formas de incluir arquivos sigilosos no container apenas quando forem rodar.

Explicar o exemplo 10.

