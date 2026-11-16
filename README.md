# PAI, Performance Analysis Interface

Protótipo de um Sistema de Apoio à Decisão para a disciplina de Sistemas de Apoio à Decisão da UFBA.

O PAI ajuda uma pessoa a escolher o plano de dieta, treino e cardio mais adequado ao seu objetivo, que pode ser cutting, bulking, recomposição ou manutenção. O sistema gera planos candidatos seguros, avalia cada um por critérios ponderados, agrupa as alternativas e mostra a dieta e a projeção de peso, cintura e gordura de cada uma. A escolha final é sempre do usuário.

## Acesso

- Link do protótipo: https://SEU-USUARIO.github.io/pai-sad/
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
- **Painel**, com indicadores de peso, cintura, gordura e IMC, gráficos com regressão linear e um plano sugerido de acordo com o objetivo.
- **Plano e simulação**, onde o usuário informa metas, treinos, cardio e alimentos e recebe cinco alternativas de plano, a dieta por refeição e a projeção.
- **Histórico**, com os registros de medidas e um formulário de novo registro.
- **Metodologia**, com o modelo de decisão, os parâmetros e as fontes.

## Funções analíticas e modelo de decisão

- **Sumarização.** Indicadores do painel, variações desde o primeiro registro e comparação com faixas de referência.
- **Agrupamento.** K-means com início determinístico sobre as notas ponderadas dos planos candidatos, em cinco grupos, com coeficiente de silhueta.
- **Regressão.** Regressão linear por mínimos quadrados sobre o histórico de peso, cintura e gordura.
- **Decisão multicritério.** Método SAW hierárquico, com três dimensões, segurança, eficácia e viabilidade, e oito critérios. Os pesos são definidos a priori e ficam na configuração no início do script. O índice é usado só nos cálculos e não aparece na interface.
- **Regras de segurança.** Bloqueio para menores de 18 anos e para IMC abaixo de 18,5 em perda de peso, além de pisos calóricos e limites de variação semanal de peso.
- **Projeção.** Gasto energético por Mifflin-St Jeor recalculado com o peso projetado a cada semana, com adaptação do gasto limitada, em uma heurística inspirada no modelo de Hall.

Os parâmetros, as regras e as referências estão na aba Metodologia do sistema.

## Estrutura

```
index.html   protótipo completo
README.md    este arquivo
```

## Limitações

- Os dados dos usuários são fictícios e gerados por regras.
- As projeções são estimativas educativas, e o modelo não representa bem a recomposição corporal.
- Os pesos dos critérios são definidos a priori, sem calibração com dados reais.
- Os valores de dieta são ilustrativos e não substituem a orientação de um nutricionista ou de um médico.
- Nada é salvo entre sessões.
