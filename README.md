# IntelliRota: Otimização de Transporte Multimodal no Brasil 🚛🚂

Bem-vindo ao **IntelliRota**, um sistema inteligente desenvolvido para otimizar o transporte de cargas entre as capitais brasileiras utilizando técnicas avançadas de Inteligência Artificial.

Este projeto foi desenvolvido como trabalho avaliativo para a disciplina de Inteligência Artificial do curso de Ciência da Computação (IFSC - Lages).

---

## 📖 Índice

* [Introdução](#-introdução)
* [Objetivos do Sistema](#-objetivos-do-sistema)
* [Arquitetura do Sistema](#-arquitetura-do-sistema)
* [Funcionalidades](#-funcionalidades)
* [Algoritmos de Inteligência Artificial](#-algoritmos-de-inteligência-artificial)
* [Tecnologias Utilizadas](#-tecnologias-utilizadas)
* [Como Executar o Projeto](#-como-executar-o-projeto)
* [Modelagem do Problema](#-modelagem-do-problema)

---

## 🎯 Introdução

O transporte de cargas no Brasil enfrenta altos custos operacionais devido à vasta extensão territorial do país. O **IntelliRota** propõe uma solução baseada em computação inteligente para auxiliar na tomada de decisões logísticas. 

Modelando as capitais brasileiras como um grafo (onde vértices são cidades e arestas são as fronteiras estaduais), o sistema aplica algoritmos de busca e otimização para encontrar rotas econômicas e propor melhorias na infraestrutura ferroviária do país.

---

## 📌 Objetivos do Sistema

O sistema visa minimizar os custos operacionais do transporte de cargas através dos seguintes objetivos específicos:

* **Roteamento Inteligente:** Determinar a rota de menor custo entre duas capitais selecionadas utilizando o algoritmo $A^{*}$.
* **Infraestrutura Ferroviária (MST):** Gerar uma malha ferroviária que conecte todas as capitais com o menor custo de implantação utilizando o Algoritmo de Kruskal.
* **Otimização de Orçamento:** Otimizar a seleção de trechos ferroviários a serem construídos, respeitando restrições orçamentárias (60% do custo total da MST) e considerando a demanda de transporte, utilizando um Algoritmo Genético.
* **Análise Multimodal:** Permitir a comparação entre cenários logísticos puramente rodoviários e cenários híbridos (rodoviário + ferroviário com taxa de transbordo).
* **Interface Interativa:** Disponibilizar uma aplicação web clara e intuitiva para visualização dinâmica do grafo e dos resultados.

---

## 🏗 Arquitetura do Sistema

O projeto segue uma arquitetura Cliente-Servidor separada em duas camadas:

### Backend
Desenvolvido em **Java com Spring Boot**, é responsável por:
* Carregar e processar os dados do grafo a partir de arquivos CSV.
* Executar os algoritmos de busca ($A^{*}$) e otimização (Kruskal e Genético).
* Fornecer uma API REST (`/api/`) para comunicação.

### Frontend 
Desenvolvido em **React com Vite** e estilizado com Bootstrap e ReactFlow, permite:
* A seleção intuitiva de cidades de origem, destino e modal de transporte.
* A visualização topológica do Brasil em forma de grafo iterativo.
* Animações visuais das rotas traçadas e das malhas ferroviárias construídas.

---

## 🚀 Funcionalidades

Através do painel lateral da aplicação, o usuário pode interagir com duas frentes principais de logística:

1. **Busca de Rota ($A^{*}$)**
   * **A* Apenas Rodoviário:** Traça o caminho mais barato usando apenas rodovias.
   * **A* Híbrido (Kruskal):** Traça a melhor rota aproveitando a malha ferroviária completa (MST).
   * **A* Híbrido (Genético):** Traça a melhor rota aproveitando a malha ferroviária reduzida pelo orçamento.
2. **Infraestrutura Ferroviária**
   * **Gerar Malha Kruskal:** Conecta todas as capitais brasileiras através de ferrovias.
   * **Evoluir Genético:** Otimiza a malha ferroviária cortando trechos menos vitais para se adequar ao limite orçamentário.

---

## 🧠 Algoritmos de Inteligência Artificial

O sistema é alimentado por três algoritmos clássicos de IA:

### 1. Busca Heurística: Algoritmo $A^{*}$
Utilizado para encontrar a rota de menor custo. Ele avalia os caminhos combinando o custo real já percorrido ($g(n)$) e uma estimativa heurística admissível do custo até o destino ($h(n)$). A heurística do projeto baseia-se na distância em linha reta entre as capitais.

### 2. Árvore Geradora Mínima: Algoritmo de Kruskal
Aplicado para projetar a malha ferroviária ideal. O Kruskal ordena todas as possíveis ligações entre estados pelo menor peso (custo) e adiciona-as à solução final, garantindo que não se formem ciclos e que todas as capitais fiquem conectadas.

### 3. Otimização Global: Algoritmo Genético
Utilizado para lidar com a restrição orçamentária (limite de 60% do custo da malha de Kruskal).
* **Indivíduo (Cromossomo):** Uma combinação binária representando quais trechos da malha serão construídos ou descartados.
* **Aptidão (Fitness):** Calculada somando os custos de frete das rotas (usando o A* internamente para cada indivíduo) para satisfazer a demanda de transporte. Soluções que estouram o orçamento recebem penalidade máxima.
* **Evolução:** A população passa por ciclos de Seleção, Cruzamento e Mutação até encontrar a malha ferroviária mais útil para o país.

---

## 💻 Tecnologias Utilizadas

* **Backend:** Java 17+, Spring Boot, Estruturas de Dados para Grafos.
* **Frontend:** React, Vite, JavaScript, CSS.
* **Bibliotecas UI:** ReactFlow (visualização de grafos), Bootstrap (estilização).
* **Armazenamento:** Arquivos CSV (`conexoes_reais.csv`, `heuristica.csv`, `cargas_anexo.csv`).

---

## ⚙️ Como Executar o Projeto

Para rodar o IntelliRota localmente na sua máquina:

### 1. Backend (Spring Boot)
1. Certifique-se de ter o JDK instalado.
2. Navegue até a pasta do backend.
3. Execute o comando Maven:
   ```bash
   ./mvnw spring-boot:run
4. O servidor iniciará na porta http://localhost:8080.

### 2. Frontend (React/Vite)
1. Certifique-se de ter o Node.js instalado.
2. Navegue até a pasta do frontend.
3. Instale as dependências:
   ```bash
   npm install
4. Inicie o servidor de desenvolvimento:
    ```bash
   npm run dev
5. Acesse a aplicação no navegador através da porta indicada (geralmente `http://localhost:5173`).

---

## 🗺️ Modelagem do Problema

O cenário logístico brasileiro foi modelado como um **Grafo Não Direcionado**:
* **Vértices:** As 27 capitais dos estados brasileiros.
* **Arestas:** As conexões diretas entre capitais que compartilham fronteira geográfica.
* **Pesos:** Distâncias em quilômetros obtidas a partir de dados reais.
* **Exceção Regra de Negócio:** Foi forçada uma conexão direta entre Brasília e Belo Horizonte, conforme as diretrizes do problema.

<details>
    <summary>**Descrição Completa do Trabalho:**</summary>
        O Ministério dos Transportes deseja modernizar o transporte de cargas no Brasil, reduzindo
    os custos operacionais. Para isto, pretende analisar os custos logísticos para transportar cargas
    entre as capitais das 27 unidades federativas (26 estados e o Distrito Federal) com o intuito de
    realizar investimentos que possibilitem a redução de tais custos. Para a implementação deste
    trabalho, considere que:
    • Existe uma rodovia que conecta diretamente as capitais de dois estados que possuem
    fronteira em comum;
    • Não existem rodovias ligando diretamente as capitais de dois estados que não fazem
    fronteira. 
    • A única exceção é Brasília, no Distrito Federal, que além de uma rodovia que a liga a
    Goiânia, possui uma ligação direta com Belo Horizonte em Minas Gerais.
    a) Elabore o grafo que representa este mapa, incluindo a distância entre as cidades (obtida no
    Google Maps) como o peso das arestas.
    b) Implemente o algoritmo A* para encontrar a rota mais barata entre duas cidades selecionadas
    pelo usuário e apresente o custo para transportar uma carga entre elas, considerando que o custo
    é de R$ 5,00 por quilômetro rodado.
    Visando reduzir o custo logístico, o governo pretende implantar ferrovias entre algumas
    capitais, de forma que todas as capitais estejam conectadas por, pelo menos, uma ferrovia. 
    c) Implemente o algoritmo de Kruskal para gerar a malha ferroviária capaz de conectar todas as
    capitais com o menor custo de implantação para o governo e apresente o custo total da obra.
    Considere que o custo para a construção de uma ferrovia é R$ 2.000.000,00 por km. 
    d) Implemente uma nova versão do algoritmo A* para encontrar a rota mais barata entre duas
    cidades selecionadas pelo usuário e apresente o custo para transportar uma carga entre elas. O
    transporte nas rotas não contempladas com ferrovia continuará sendo realizado por rodovias, com
    custo de R$ 5,00 por quilômetro rodado. Nas rotas em que foram construídas ferrovias, o
    transporte pode ser feito pela ferrovia, a um custo de R$ 1,20, ou ainda pela rodovia a um custo de
    R$ 5,00. Uma mesma rota pode ser composta por trechos rodoviários e ferroviários, contudo há
    um custo de R$ 1.000,00 para cada transbordo realizado.
    O Algortimo de Kruskal permitirá a ligação entre todas as capitais com o menor custo
    possível, entretanto, é possível que a malha ferroviária gerada não seja a mais otimizada, pois
    sabe-se que grande parte das cargas circula entre as grandes metrópoles. Além disto, sabe-se que
    o governo não tem recursos para implantar todas as rodovias planejadas, ele possui apenas 60%
    do recurso necessário, conforme calculado no item “c”. Visando otimizar a aplicação dos recursos,
    o governo registrou em uma tabela (Anexo I) as rotas mais utilizadas no transporte de cargas, bem
    como a quantidade de cargas transportadas diariamente entre elas.
    e) Implemente um Algoritmo Genético que determine trechos de ferrovia devem ser construídos,
    de forma que o valor de implantação seja igual ou inferior ao disponibilizado pelo governo e que a
    soma do custo do transporte das cargas nas rotas registradas pelo governos seja o menor possível.
    f) Implemente uma nova versão do algoritmo A* para encontrar a rota mais barata entre duas
    cidades selecionadas pelo usuário e apresente o custo para transportar uma carga entre elas,
    considerando a malha ferroviária gerada pelo Algoritmo Genético. Os custos para transporte e
    transbordo são os mesmos descritos no item “d”
</details>
