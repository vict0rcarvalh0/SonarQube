## Relatório
Inicialmente, criei o meu repositório e o acessei por meio do comando `cd SonarQube`, em seguida, clonei o projeto de exemplo por meio do comando `git clone`e executei o container docker, que demonstrou o comportamento esperado por meio do comando `docker container ls`.

<img src="https://github.com/vict0rcarvalh0/SonarQube/blob/main/assets/image.png">

Após essa etapa, instalei o dotnet-sonarscanner e tentei o comando que executa a análise por meio do mesmo, que falhou por eu não ter "buildado" a solução e não ter a versão correta do Java.

<img src="https://github.com/vict0rcarvalh0/SonarQube/blob/main/assets/image2.png">
<img src="https://github.com/vict0rcarvalh0/SonarQube/blob/main/assets/image3.png">

Após o upgrade de minha versão do Java(17) e do build da solução, tentei novamente o mesmo comando, e funcionou perfeitamenete. Portanto, consegui utilizar o `dotnet sonarscanner begin /k:"project-key" /d:sonar.login=admin /d:sonar.password=admin`, que inicia a análise do código-fonte usando o SonarScanner, onde os parâmetros fornecidos são a project key, que é usada para identificar o projeto no SonarQube, o login e a password, que são a autenticação para acessar o SonarQube na porta definida no container. Depois disso, o comando do build em si, que compila a solução do projeto antes de enviá-lo para análise. Por fim, o comando `dotnet sonarscanner end /d:sonar.login=admin /d:sonar.password=admin`, que finaliza a análise do código-fonte e envia ao SonarQube, com os mesmos parâmetros de autenticação detalhados no primeiro comando.

<img src="https://github.com/vict0rcarvalh0/SonarQube/blob/main/assets/image4.png">
<img src="https://github.com/vict0rcarvalh0/SonarQube/blob/main/assets/image6.png">

Por fim, acessei o SonarQube na porta 9000, de acordo com o que foi definido para o container e consegui obter alguns insights do projeto. As 124 linhas de código foram analisadas e o projeto "passou", que indica uma qualidade "OK". Além disso, a cobertura(Coverage) de testes do código está como 0%, que é um possível ponto de melhoria, as duplicações estão em 0%, como já esperado, a segurança e manutenabilidade tiveram uma nota boa e a confiabilidade uma nota mediana, que indica um possível ponto de melhoria no código-fonte analisado.

<img src="https://github.com/vict0rcarvalh0/SonarQube/blob/main/assets/image7.png">

Acessando o overview, foi possível observar uma visão geral o descrito anteriormente, e notar que possui um ponto de atenção grande em "Security Hotspot", que precisa ser analisado em detalhes.

<img src="https://github.com/vict0rcarvalh0/SonarQube/blob/main/assets/image8.png">

Buscando uma resolução desses pontos de atenção, a aba Issues pode ser analisada para ver todos os "problemas" e pontos de melhoria do código. Como a remoção de fields não lidos, alteração em modificadores de acesso de variáveis, entre outros pontos.

<img src="https://github.com/vict0rcarvalh0/SonarQube/blob/main/assets/image9.png">

Na aba "Security Hotspots", foi possível entender o problema de segurança informado, que está relacionado ao uso de uma criptografia fraca por meio do "Random".

<img src="https://github.com/vict0rcarvalh0/SonarQube/blob/main/assets/image10.png">

Na aba "Measures", é possível observar um gráfico de cobertura x débito técnico, que é um conceito visto em autoestudo que envolve se refere ao custo futuro associado às escolhas de design ou implementações de baixa qualidade no presente.

<img src="https://github.com/vict0rcarvalh0/SonarQube/blob/main/assets/image11.png">

Por fim, a aba "Activity" mostra o histórico de análises e a aba "Code" exibe uma tabela que mostra o número de ocorrências de eventos(ex: linhas de código, bugs, duplicações, etc) para cada arquivo do código.

<img src="https://github.com/vict0rcarvalh0/SonarQube/blob/main/assets/image12.png">

## Aprendizados
### Uso do SonarQube
Aprendi a subir um container docker do SonarQube e realizar uma análise em um projeto .Net. Além dos comandos, me aprofundei bastante na interface do Sonar e entendi como posso analisar cada Issue relatada no código fonte, ou seja, interpretar os resultados, para que o código fique mais limpo e otimizado.

### Atualização do Java
Confesso que uma boa parte do tempo que gastei foi atualizando o Java, para que fosse atualizado corretamente, aprendi como acessar as variáveis de ambiente no linux, em outras palavras, o "PATH", inserir e remover variáveis nele e utilizar de comandos de remoção e instalação do Java no sistema.

### Débito Técnico
Gostei bastante de ter encontrado um gráfico que exibe o débito técnico em um dos eixos, pois tinha noção teórica do conceito e consegui associar de forma mais tangível a sua relação com a qualidade do código.
