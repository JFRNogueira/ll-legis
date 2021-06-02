<h1 align="center">Decisões estratégicas</h1>

> Decisões iniciais do projeto que afetam a aplicação no longo prazo

[🏠 Voltar para HOME](../README.md)




## Estrutura de dados do banco

### Qual estrutura de dados utilizar?

Optou-se por estruturar a legislação como uma árvore. Os nós, do nível mais alto para o mais baixo seguem a seguinte ordem:

1. Lei (com preâmbulo, ementa e assinatura)
2. Título
3. Capítulo
4. Seção
5. Subseção
6. Artigo
7. Parágrafo
8. Inciso
9. Alínea

Deve-se atentar ao fato de que alguns dos nós dessa árvore podem ser pulados. Por exemplo: na maioria das leis passa-se diretamente de `Lei` para `Artigo`.

### Como isso fica no banco de dados? 

Dado que o banco de dados utilizado é o **MongoDB**, uma boa referência de documentação para esse tipo de estrutura de dados está no próprio [MongoDB](https://docs.mongodb.com/manual/applications/data-models-tree-structures/#:~:text=MongoDB%20allows%20various%20ways%20to,hierarchical%20or%20nested%20data%20relationships.&text=%22parent%22%20nodes.-,Presents%20a%20data%20model%20that%20organizes%20documents%20in%20a%20tree,array%20that%20stores%20all%20ancestors.). As opções apresentadas são:

1. [Referenciar os nós pais](https://docs.mongodb.com/manual/tutorial/model-tree-structures-with-parent-references/)
2. [Referenciar os nós filhos](https://docs.mongodb.com/manual/tutorial/model-tree-structures-with-child-references/)
3. [Referenciar os nós ascendentes em um *array*](https://docs.mongodb.com/manual/tutorial/model-tree-structures-with-ancestors-array/)
4. [Referenciar os caminhos da árvore](https://docs.mongodb.com/manual/tutorial/model-tree-structures-with-materialized-paths/)
5. [Conjuntos aninhados](https://docs.mongodb.com/manual/tutorial/model-tree-structures-with-nested-sets/)


Note que, para fazer uma consulta que retorna uma sub-árvore, tem-se que:
- Estruturas 1 e 2 são lentas
- Estruturas 3 e 4 são medianas
- Estrutura 5 é rápida

>❗O primeiro impulso é o de implementar a estratégia `5`, mas sua manutenção pode dar um pouco mais de trabalho do que gostaríamos. Sendo assim, iniciaremos com uma estrutura intermediária, a `3`, e, caso ela se mostre pouco performática, migraremos para a estrutura de dados `5`.

[🏠 Voltar para HOME](../README.md)
