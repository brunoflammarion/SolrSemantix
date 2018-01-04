# Teste Solr Semantix
Teste Solr Semantix

Desafio Solr 

1. Baixe, instale e rode o Solr na sua última versão e envie um print dos comandos para descompactar e rodar e um print do dashboard do Solr rodando com JVM Oracle HotSpot configurada para usar qualquer valor de memória diferente do default da instalação. 

![alt text](https://github.com/brunoflammarion/SolrSemantix/blob/master/download.png)

sudo apt-get update
java -version
sudo apt-get install default-jre
bin/solr start -force -h localhost -p 8983 -s solr -m 3g

![alt text](https://github.com/brunoflammarion/SolrSemantix/blob/master/homesolr.png)

2. Indexar o conteúdo de um arquivo CSV baixado do Portal da Transparência do governo brasileiro. Pode ser qualquer CSV de qualquer informação que tenha textos e números. Enviar prints dos comandos ou código usados para indexar o conteúdo do arquivo. Pode ser por código em qualquer linguagem ou utilizando as ferramentas do Solr para indexação (DIH, Post ou outro). 

Utilizei o seguinte arquivo
http://www.portaltransparencia.gov.br/downloads/mensal.asp?c=BolsaFamiliaFolhaPagamento#meses10
 
Despesas – Transferências – Programas Sociais – Bolsa Família - Pagamentos
Nesta seção estão disponíveis informações, em formato aberto, das transferências de recursos federais diretamente repassados a cidadãos, referentes ao pagamento do Bolsa Família, realizadas pelo Ministério do Desenvolvimento Social, por meio da Caixa Econômica Federal.
Os arquivos abaixo apresentam:

UF; Código SIAFI Município; Nome Município; Código Função; Código Subfunção; Código Programa; Código Ação; NIS Favorecido; Nome Favorecido; Fonte-Finalidade; Valor Parcela e Mês Competência.
Atualização dos arquivos: Mensal
Modelo do nome do arquivo: AAAAMM_BolsaFamiliaFolhaPagamento.csv
Origem das informações: Caixa Econômica Federal

Foi necessário passar o arquivo para UTF8, utilizei seguinte comando
iconv -f ISO-8859-1 -t UTF-8//TRANSLIT input.file -o out.file

Coloquei o arquivo em:
![alt text](https://github.com/brunoflammarion/SolrSemantix/blob/master/arquivo.png)

3. Corrija o schema para indexar os campos que tenham conteúdo em português com o tipo text_pt com copyField para um campo text_general. 

Criei dois fields para tratar as buscas com text_pt, serao utilizados como copyField de campos originais que importei com o tipo string
![alt text](https://github.com/brunoflammarion/SolrSemantix/blob/96f9caa44ed5148246e510880610aea606352e5e/copyfield.PNG)

4. Crie CopyFields em string para armazenar conteúdos que serão usados em um facet. 
![alt text](https://github.com/brunoflammarion/SolrSemantix/blob/96f9caa44ed5148246e510880610aea606352e5e/Configuracoes%20field.PNG)

5. Configure o solrconfig.xml no requestHandler /browse para usar os campos de facet corretos. 
![alt text](https://github.com/brunoflammarion/SolrSemantix/blob/master/browse.PNG)

6. Configure os query fields com pesos adequados para encontrar as informações indexadas dentro do contexto escolhido. 
![alt text](https://github.com/brunoflammarion/SolrSemantix/blob/master/browse.PNG)

7. Envie print da tela /browse do Solr com uma busca com os facets escolhidos e com o resultado desejado. 
![alt text](https://github.com/brunoflammarion/SolrSemantix/blob/master/consulta%20com%20facet.png)
![alt text](https://github.com/brunoflammarion/SolrSemantix/blob/master/consulta%20texto.png)

<b>Itens a melhorar</b><br>
Colocar Highlight<br>
Colocar Spellcheck<br>
Colocar Mlt<br>

