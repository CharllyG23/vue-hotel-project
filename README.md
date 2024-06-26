# Hotel Nordico

> Aplicação usando Vue.js 3 para simular parte do sistema de reserva de hotéis.

> Vue.js 3 + Typescript + Pinia + Vue Router
>
> <img src="src/assets/img/hotel-proyect.png" alt="projeto">

## Build Setup

``` bash
#clone the repository
git clone 

# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

```

# Critérios Técnicos

Embora meu código pareça complexo, ele é surpreendentemente simples, ele utiliza diversas ferramentas e técnicas avançadas para garantir desempenho ideal e uma estrutura organizada:

- Pinia: Utilizado para gerenciamento de dados.
- Vue Router: Utilizado para gerenciamento de rotas.
- Sass (scss): Simplifica e melhora o design através do uso de Sass.
- Componentes Reutilizáveis: Uma boa estrutura de componentes garantindo que o código permaneça limpo e organizado.
- TypeScript: É implementado para manter os dados tipados na maior extensão possível.
- Hotel Mock: Inclui uma maquete de hotel com 5 cidades predefinidas, limitando a busca nesta primeira versão do projeto. Funções aleatórias são aplicadas para cada atributo necessário,
  adicionando realismo aos dados simulados.
- Responsive: Uma experiência de usuário consistente e adaptável (Mobile-Web).
- BEM CSS: é uma metodologia CSS (ou convenção de nomenclatura) usada no mundo todo e em meu projeto.

# Funcionalidades

1. Pesquisa de Hotéis
    
Criei vários componentes para tornar a pesquisa mais compreensível e prática:

- Campo Destino: Limitamos a busca de hotéis a apenas 6 cidades do Brasil para ter mais controle nesta primeira versão funcional.
- Campos de Entrada e Saída: São campos de data validados para evitar que o usuário reserve um hotel em data anterior a hoje e garantir que a data de saída não seja anterior à data de chegada.
- Campos Quartos e Hóspedes: Ambos são predefinidos com valor 1 para manter a consistência.
- Botão Pesquisar: Permite pesquisar de forma simples e rápida.
  
-----------------------------------------------------------------------------

2. Resultados da pesquisa

Dividi os resultados da pesquisa de hotéis em vários componentes essenciais para ter um código mais organizado e gerenciável. Estes componentes constituem uma base sólida para a visualização dos diferentes elementos dos cartões, concebidos para apresentar a informação de forma clara e atrativa para o utilizador.

- Componentes de resultado: Cada cartão de hotel é dividido em componentes individuais para melhor gerenciar informações e design.

- Cabeçalho do Cartão: Mostra o nome do hotel e sua localização, destacando a cidade previamente selecionada.
- Imagem do Hotel: Imagem atrativa do hotel para melhor visualização.
- Detalhes do hotel: informações essenciais como preço, quartos.
- Botões de Ação: Botões para “Comparação de ofertas” e “Reserva” com funcionalidades específicas.

-----------------------------------------------------------------------------

2. Filtros

Los filtros son fundamentales para que el usuario tenga más control sobre lo que quiere ver. He implementado los siguientes filtros para facilitar la búsqueda:

- Preço (mais barato): Ordena los resultados por precio, mostrando primero los hoteles más económicos.
- Preço (mais caro): Ordena los resultados por precio, mostrando primero los hoteles más costosos.
- Melhores avaliações: Ordena los resultados según las mejores evaluaciones de los usuarios.
  
Estos filtros ayudan a los usuarios a encontrar rápidamente las opciones que mejor se ajustan a sus preferencias y necesidades.

-----------------------------------------------------------------------------

4. Comparação

Permitir ao usuário visualizar sua seleção múltipla de hotéis e comparar as características de dois resultados de pesquisa para facilitar a decisão de reserva.

-----------------------------------------------------------------------------

5. Reservar

Al hacer clic em reservar, se abre un modal que muestra al usuario cuál hotel desea reservar y solicita los datos necesarios para hacer la reserva.
Todos los campos en el modal son validados como requeridos para garantizar una correcta gestión de los datos.
   
