# PAI, Performance Analysis Interface

Protótipo de um Sistema de Apoio à Decisão para a disciplina de Sistemas de Apoio à Decisão da UFBA.

O PAI ajuda uma pessoa a decidir qual plano de dieta, treino e cardio seguir para atingir seu objetivo, que pode ser cutting, bulking, recomposição ou manutenção. O sistema gera planos candidatos seguros, avalia cada um por critérios ponderados, agrupa as alternativas e mostra, para cada uma, a dieta por refeição e a projeção de peso, cintura, gordura e massa magra nas próximas 12 semanas. A escolha final é sempre do usuário.

## Acesso

- Link do protótipo: https://gglabreu.github.io/pai-sad/
- Perfis de demonstração: Marina, Rafael, Camila e Diego, escolhidos na tela de login
- E-mail: `demo@pai.demo`
- Senha: `demo1234`

O login é apenas ilustrativo. Não há autenticação real, e qualquer entrada é aceita.

## Como executar

Não há instalação nem backend. É um único arquivo HTML com CSS e JavaScript embutidos.

1. Baixe ou clone o repositório.
2. Abra o arquivo `index.html` em um navegador atual.

Se preferir servir por HTTP, rode `python3 -m http.server 8000` na pasta do projeto e abra `http://localhost:8000`.

A fonte Roboto é carregada do Google Fonts. Sem internet, o sistema usa uma fonte local e continua funcionando.

## Telas

- **Login e cadastro**, com seletor de perfil de demonstração.
- **Painel**, com indicadores de peso, cintura, gordura e IMC coloridos conforme o objetivo, gráficos de evolução com regressão linear e um plano sugerido, que indica se o usuário deve manter ou trocar de objetivo.
- **Plano e simulação**, onde o usuário informa objetivo, metas de peso e cintura, idade, treinos, cardio e passos disponíveis e alimentos por grupo. O sistema devolve cinco alternativas, do mais recomendado ao menos adequado, e para o plano escolhido mostra a dieta por refeição e a projeção semanal de 12 semanas a partir da última medida.
- **Histórico**, com os gráficos de evolução, os registros de medidas e um formulário de novo registro.
- **Metodologia**, com o modelo de decisão, a tabela de parâmetros com o fundamento de cada um e as referências.

## Funções analíticas e modelo de decisão

- **Sumarização.** Indicadores do painel, variação desde o primeiro registro e comparação com faixas de referência de cintura, gordura e IMC.
- **Regressão.** Regressão linear por mínimos quadrados sobre o histórico de peso, cintura e gordura, com inclinação e R².
- **Agrupamento.** K-means com início determinístico sobre as notas ponderadas dos planos candidatos, em cinco grupos, com coeficiente de silhueta.
- **Decisão multicritério.** Método SAW hierárquico, com três dimensões, segurança, eficácia e viabilidade, e oito critérios. Os pesos são definidos a priori e ficam na configuração no início do script. O índice é usado só nos cálculos e não aparece na interface.
- **Projeção.** Gasto basal por Mifflin-St Jeor recalculado com o peso de cada semana, adaptação metabólica inspirada em Hall, divisão da variação de peso entre gordura e massa magra pela relação de Forbes, com perda maior de massa magra em ritmos agressivos, e recomposição corporal perto do equilíbrio calórico.
- **Regras de segurança.** Bloqueio para menores de 18 anos e para perda de peso com IMC abaixo de 18,5, piso calórico de 800 kcal, pisos de 1.200 kcal para mulheres e 1.500 kcal para homens e limites de variação semanal de peso.
- **Dieta.** Distribuição de proteína, carboidrato e gordura em quatro refeições com alimentos da TACO, com reposição automática dentro de cada grupo de alimentos.

A aba Metodologia separa o que vem da literatura, o que é literatura adaptada e o que é decisão de projeto.

## Estrutura

```
index.html   protótipo completo
README.md    este arquivo
```

## Principais referências

- Mifflin et al., 1990, para o gasto basal.
- Jäger et al., 2017, e Helms, Aragon e Fitschen, 2014, para proteína e ritmo de perda de peso.
- NHLBI, 1998, e NICE, 2014, para ritmo seguro de perda e piso calórico.
- Hall et al., 2011, e Hall, 2007, para a adaptação metabólica e a relação de Forbes.
- Garthe et al., 2011, e Barakat et al., 2020, para ritmo de perda, massa magra e recomposição.
- Gallagher et al., 2000, Browning, Hsieh e Ashwell, 2010, e OMS, 2000, para as referências de gordura, cintura e IMC.
- NEPA/UNICAMP, 2006, Tabela Brasileira de Composição de Alimentos, TACO.

As referências completas estão na aba Metodologia.

## Limitações

- Os dados dos usuários são fictícios.
- As projeções são estimativas educativas, com parâmetros de projeto que não foram calibrados com dados reais.
- A massa magra é estimada a partir do peso e do percentual de gordura e herda o erro dessa medida.
- Os pesos dos critérios são definidos a priori.
- Os valores de dieta são ilustrativos e não substituem a orientação de um nutricionista ou de um médico.
- Nada é salvo entre sessões.
