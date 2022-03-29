# graph_tools
Ferramenta de geração de gráficos usando Plotly, de forma mais àgil


Classe Atalho para Geração de Gráficos usando o Plotly.
    
    [ATENÇÃO] Essa classe não tem o intuíto de clonar as funções do Plotly e sim
    tornar a geração de alguns gráficos mais práticas. Dessa forma, para personalizações 
    avançadas e detalhamentos mais apurados, crie o gráfico diretamente pelo Potly!

    ~~~ Parâmetros Padrões ~~~  
      
      1. Gráficos de Linha
        * __line_mode: `String` com o Tipo de Linha do Gráfico, ex: `lines`, `lines+markers`, `markers`.
        * __line_fill: `String` com o Tipo de preenchimento do gráfico, ex: `None`, `tonexty`, `tozeroy`.
        
      2. Gráfico de Barras
        * __bar_mode: `String` com o Modo que devem ser agrupadas as colunas, `group`(agrupamento) e `stack`(empilhamento).
      
      3. Cores
        * __pastel_colors: `List` com paleta de 8 cores pasteis, em RGB.
        * __semipastel_colors: `List` com paleta de 8 cores semi pasteis, em RGB.
        * __brilhant_colors: `List` com paleta de 26 cores brilhantes, em HEX.
        
      4. Subplots
        * __figure_coluns: `Int` com quantidade de colunas que deve haver no subplot.
        * __figure_is_subplot: `Bool` identificador do tipo de gráfico, comum ou subplot.

    ~~~ Métodos ~~~
    
      * update_layout: Inicializa o layout modelo e pode ser evocado para atualizar o layout.
      * __subplot_validate: Validador se o gráfico é um subplot e os parâmetros (rows, row_width) foram passados corretamente.
      * __line_parameters_validade: Validador dos parâmetros passados em Line.
      * line: Gera gráfico de linhas, recebendo como parâmetros:
        1. x_col: coluna do eixo x.
        2. y_cols: lista coluna(s) do eixo y.
        3. y_col_names: lista de nome(s) das coluna(s) para legenda. [OPCIONAL]
        4. cols_colors: lista de cores para as coluna(s). [OPCIONAL]
        5. modes: lista de Tipos de Linhas. [OPCIONAL]
        6. fills: lista de Tipos de preenchimento de Linhas. [OPCIONAL]
        7. row: numero da linha do gráfico. [APENAS SUBPLOT]
      * bar: Gera gráfico de barras, recebendo como parâmetros:
        * x_col: coluna do eixo x.
        * y_cols: lista coluna(s) do eixo y.
        * y_col_names: lista de nome(s) das coluna(s) para legenda. [OPCIONAL]
        * barmode: tipo de barra (`group`/`stack`). [OPCIONAL]
        * marker_colors: lista de cores para as coluna(s). [OPCIONAL]
        * row: numero da linha do gráfico. [APENAS SUBPLOT]
      * show: Retorna a figura completa do gráfico;
      
    ~~~ Instanciação do Objeto ~~~  
    
      1. Parâmetros de Inicialização:
      
        * df: Dataset do tipo `DataFrame`;
        * title: `String` com o título do Gráfico, por padrão inicializa vazio;
        * tit_is_bold: `Bool` que define se o título será negrito, por padrão inicializa com `True`;
        * is_subplot: `Bool` identificador do tipo de gráfico, comum ou subplot, por padrão inicializa com `False`.
        * rows: Quantidade de Linhas que o subplot deve ter, por padrão inicializa com 2; [APENAS P/ SUBPLOTS]
        * row_width: Proporcionamento das linhas no subplot, por padrão inicializa com 30% e 70%; [APENAS P/ SUBPLOTS]
        
      2. Exemplos de evocação da função:
      
        0. Dataset de Exemplo:
        
          json={'data_relatorio': {0: '2020-03-31', 1: '2020-03-30', 2: '2020-03-28', 3: '2020-03-27', 4: '2020-03-26', 5: '2020-03-25', 6: '2020-03-24', 7: '2020-03-23'},
               'msg': {0: 309, 1: 141, 2: 31, 3: 346, 4: 223, 5: 148, 6: 213, 7: 443},
               'canais': {0: 1, 1: 1, 2: 1, 3: 1, 4: 1, 5: 1, 6: 1, 7: 2},
               'env_canal': {0: 192, 1: 99, 2: 14, 3: 209, 4: 134, 5: 97, 6: 122, 7: 259},
               'env_contato': {0: 117, 1: 42, 2: 17, 3: 137, 4: 89, 5: 51, 6: 91, 7: 184},
               'read': {0: 113.0, 1: 68.0, 2: 11.0, 3: 135.0, 4: 87.0, 5: 75.0, 6: 114.0, 7: 186.0},
               'failed': {0: 3.0, 1: 9.0, 2: None, 3: 3.0, 4: 7.0, 5: 14.0, 6: 4.0, 7: None}}

          df=pd.DataFrame(json)

         df = a.sort_values('data_relatorio').query('ano =="2022"').copy()

        1. GRÁFICO DE LINHA:
          #Linha Comum
          Graph(df, title='MENSAGENS').line(x_col='data_relatorio', y_cols=['env_contato' , 'env_canal']).show()

          #Configurações Avançadas
          # >>> Preenchimento
          # Graph(df, 'MENSAGENS').line('data_relatorio', ['env_contato' , 'env_canal'], fills=['tonexty', 'tozeroy']).show()

          # >>> Modos
          # Graph(df, 'MENSAGENS').line('data_relatorio', ['env_contato' , 'env_canal'], modes=['lines+markers', 'markers']).show()

          # >>> Subplots
          Graph(df, 'MENSAGENS',is_subplot=True).line('data_relatorio', ['env_contato' , 'env_canal'], row = 1
          ).line('data_relatorio', ['msg_madrugada_rec' , 'msg_madrugada_env'], cols_colors=['gray', 'green'], row = 2).show()

        2. GRÁFICO DE BARRA 
          #Barra Comum
          Graph(df, title='MENSAGENS').bar('data_relatorio', ['env_canal', 'env_contato']).show()

          #Configurações Avançadas
          # >>> Modos
          Graph(df, title='MENSAGENS').bar('data_relatorio', ['env_canal', 'env_contato'], barmode="stack").show()
          Graph(df, title='MENSAGENS').bar('data_relatorio', ['env_canal', 'env_contato'], barmode="group").show()

          # >>> Cores
          Graph(df, title='MENSAGENS').bar('data_relatorio', ['env_canal', 'env_contato'], marker_colors=['green', 'red']).show()

          # >>> Subplots
          Graph(df, title='MENSAGENS', is_subplot=True).bar('data_relatorio', ['env_canal', 'env_contato'], row=1
                                                         ).bar('data_relatorio', ['env_canal', 'env_contato'], row=2).show()

        3. SUBPLOTS MESCLADOS
          Graph(df, title='MENSAGENS', is_subplot=True, rows=3, row_width=[0.33, 0.33, .33]).bar('data_relatorio', ['env_canal', 'env_contato'], row=1
                                                           ).line(x_col='data_relatorio', y_cols=['env_contato' , 'env_canal'], row=1
                                                           ).line(x_col='data_relatorio', y_cols=['env_contato' , 'env_canal'], row=2
                                                           ).bar('data_relatorio', ['env_canal', 'env_contato'], row=3).show()
