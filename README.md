# Projeto de Controle de um Conversor CC-CC Buck

**Modelagem matemática, projeto de compensadores e análise de desempenho em malha fechada.**

Projeto acadêmico desenvolvido na disciplina de **Eletrônica de Potência**, do curso de Engenharia de Controle e Automação do Instituto Federal de Goiás (IFG), Câmpus Itumbiara.

O trabalho aborda a modelagem de um conversor CC-CC Buck, o projeto de compensadores utilizando o lugar geométrico das raízes e a avaliação da resposta dinâmica por meio de ferramentas computacionais.

A implementação combina análise e projeto de controle no MATLAB com simulação do circuito no PSIM.

---

## Sumário

* [1. Sobre o projeto](#1-sobre-o-projeto)
* [2. Objetivos](#2-objetivos)
* [3. Fundamentação teórica](#3-fundamentação-teórica)
* [4. Modelagem matemática](#4-modelagem-matemática)
* [5. Projeto dos compensadores](#5-projeto-dos-compensadores)
* [6. Metodologia de desenvolvimento](#6-metodologia-de-desenvolvimento)
* [7. Tecnologias utilizadas](#7-tecnologias-utilizadas)
* [8. Estrutura do repositório](#8-estrutura-do-repositório)
* [9. Instalação e execução](#9-instalação-e-execução)
* [10. Resultados e análise de desempenho](#10-resultados-e-análise-de-desempenho)
* [11. Limitações e considerações](#11-limitações-e-considerações)
* [12. Possíveis melhorias](#12-possíveis-melhorias)
* [13. Autores](#13-autores)
* [14. Referências](#14-referências)

---

## 1. Sobre o projeto

Conversores CC-CC são circuitos eletrônicos utilizados para converter um nível de tensão contínua em outro, de acordo com a topologia e as condições de operação do sistema.

O conversor Buck é uma topologia abaixadora de tensão, amplamente utilizada em fontes de alimentação, sistemas embarcados, acionamentos eletrônicos e aplicações de conversão de energia.

O desempenho de um conversor depende das características elétricas de seus componentes e da estratégia de controle empregada. Por isso, a modelagem matemática e a análise da resposta dinâmica são etapas importantes para o desenvolvimento de sistemas de conversão de energia.

Neste trabalho, é estudado o modelo de um conversor Buck por meio de sua função de transferência. A partir desse modelo, são analisadas as características dinâmicas da planta e projetados compensadores para modificar o comportamento do sistema em malha fechada.

O projeto utiliza o lugar geométrico das raízes (*Root Locus*) como ferramenta para estudar a localização dos polos de malha fechada e orientar a seleção dos parâmetros de controle.

A implementação é complementada por um circuito de simulação desenvolvido no PSIM, permitindo relacionar o modelo matemático à representação do sistema eletrônico.

## 2. Objetivos

### 2.1. Objetivo geral

Modelar um conversor CC-CC Buck e desenvolver uma estratégia de compensação para melhorar sua resposta dinâmica, utilizando ferramentas de análise e simulação de sistemas de controle.

### 2.2. Objetivos específicos

* Representar a dinâmica do conversor por meio de uma função de transferência.
* Analisar o comportamento da planta sem compensação.
* Utilizar o lugar geométrico das raízes para orientar o projeto dos compensadores.
* Desenvolver uma configuração com compensação PD.
* Acrescentar ação integral por meio de um compensador PI.
* Avaliar a resposta ao degrau do sistema em malha fechada.
* Comparar o sobressinal e o tempo de acomodação com os valores de referência do projeto.
* Utilizar o MATLAB e o PSIM para analisar o comportamento do sistema.

## 3. Fundamentação teórica

### 3.1. Conversor CC-CC Buck

O conversor Buck é uma topologia de eletrônica de potência utilizada para obter uma tensão contínua de saída inferior à tensão contínua de entrada, dentro das condições de operação para as quais o circuito foi projetado.

Sua operação envolve a comutação de dispositivos semicondutores e a transferência de energia por elementos como indutores e capacitores.

A modelagem do conversor permite representar sua dinâmica e analisar como as variações na entrada de controle influenciam a variável de saída.

O modelo empregado neste trabalho é representado por uma função de transferência de segunda ordem.

### 3.2. Função de transferência

A função de transferência de um sistema linear invariante no tempo é definida, sob condições iniciais nulas, pela razão entre a transformada de Laplace da saída e a transformada de Laplace da entrada.

De forma geral:

$G(s)=\frac{Y(s)}{U(s)}$

Essa representação permite analisar os polos e zeros da planta, sua resposta transitória e os efeitos da introdução de compensadores.

### 3.3. Lugar geométrico das raízes

O lugar geométrico das raízes (*Root Locus*) representa a trajetória dos polos de malha fechada conforme um parâmetro de ganho varia.

Essa ferramenta auxilia o projeto de controladores porque permite investigar como a alteração dos ganhos e a introdução de polos e zeros modificam a estabilidade e o desempenho transitório do sistema.

No trabalho, o MATLAB é utilizado para visualizar o lugar geométrico das raízes da planta original e das configurações compensadas.

### 3.4. Compensador PD

O compensador proporcional-derivativo combina ações proporcional e derivativa.

Em uma representação ideal, sua função de transferência pode ser expressa como:

$G_{PD}(s)=K_p+K_ds$

ou, de forma equivalente:

$G_{PD}(s)=K_d(s+z)$

em que \(K_p\) é o ganho proporcional, \(K_d\) é o ganho derivativo e \(z\) determina a posição do zero.

A ação derivativa pode modificar a resposta transitória e favorecer o atendimento a requisitos de desempenho. Seus efeitos dependem da planta e dos parâmetros escolhidos.

### 3.5. Compensador PI

O compensador proporcional-integral pode ser representado por:

$G_{PI}(s)=K_p+\frac{K_i}{s}$

Uma forma equivalente é:

$G_{PI}(s)=K_p\frac{s+z}{s}$

A inclusão de um polo na origem introduz ação integral, que pode reduzir ou eliminar o erro em regime permanente para determinadas entradas de referência, desde que as condições de estabilidade e de funcionamento do sistema sejam satisfeitas.

### 3.6. Composição dos compensadores

O projeto utiliza uma composição de compensadores PD e PI:

$G_C(s)=K\,G_{PD}(s)G_{PI}(s)$

Essa estrutura reúne os efeitos das duas etapas de compensação.

O desempenho final depende da função de transferência da planta, da localização dos polos e zeros, do ganho aplicado e da configuração de realimentação.

## 4. Modelagem matemática

O arquivo `ConversorBuck.m` utiliza a seguinte função de transferência para representar a planta:

$G(s)=\frac{1200}{79{,}2\times10^{-9}s^2+0{,}3\times10^{-3}s+12}$

Essa expressão é utilizada para analisar a planta original e estudar o comportamento dos sistemas compensados.

### 4.1. Características do modelo

O denominador é um polinômio de segunda ordem. Portanto, o modelo possui dois polos, considerados na análise de estabilidade e no projeto dos compensadores.

A função de transferência é utilizada diretamente no MATLAB para gerar o lugar geométrico das raízes e calcular as respostas ao degrau.

**Nota:** a interpretação física completa da função de transferência, incluindo a grandeza de entrada, a variável de saída e as hipóteses de modelagem, deve ser consultada no relatório do projeto.

## 5. Projeto dos compensadores

### 5.1. Análise da planta original

Inicialmente, a planta é definida no MATLAB por meio da função `tf()`.

Em seguida, o comando `rlocus()` é utilizado para analisar o lugar geométrico das raízes do sistema sem compensação.

Essa etapa fornece uma referência para avaliar as alterações introduzidas pelos compensadores.

### 5.2. Projeto do compensador PD

O código utiliza o compensador:

$G_{PD}(s)=s+20107{,}76$

O valor do zero é empregado na configuração do sistema compensado.

Os parâmetros de referência indicados no código são:

| Parâmetro                    |                   Valor |
| ---------------------------- | ----------------------: |
| Sobressinal de referência    |                     20% |
| Tempo de acomodação desejado |                  400 µs |
| Zero do compensador PD       |         \(-20107{,}76\) |
| Ganho aplicado               | \(1{,}06\times10^{-6}\) |

O lugar geométrico das raízes é utilizado para estudar a localização dos polos do sistema compensado.

Na sequência, o comando `feedback()` permite construir a função de transferência em malha fechada, e `step()` gera a resposta ao degrau.

### 5.3. Inclusão do compensador PI

Para acrescentar ação integral, o código define:

$G_{PI}(s)=\frac{s+8500}{s}$

O zero é posicionado em \(-8500\), e o polo na origem introduz a ação integral.

O controlador combinado é dado por:

$G_C(s)=K_2G_{PD}(s)G_{PI}(s)$

com:

$K_2=1{,}84\times10^{-6}$

Essa configuração é utilizada para estudar a resposta do sistema em malha fechada.

### 5.4. Realimentação unitária

O código utiliza a função `feedback()` do MATLAB para formar a malha fechada com realimentação unitária.

De maneira geral, para uma planta compensada \(L(s)\), a função de transferência em malha fechada é:

$T(s)=\frac{L(s)}{1+L(s)}$

Essa expressão corresponde à configuração de realimentação negativa unitária utilizada na análise.

A resposta ao degrau é obtida por meio do comando `step()`.

## 6. Metodologia de desenvolvimento

O desenvolvimento é organizado nas seguintes etapas:

1. **Modelagem:** definição da função de transferência do conversor.
2. **Análise inicial:** estudo do lugar geométrico das raízes da planta original.
3. **Compensação PD:** introdução de um zero e seleção do ganho.
4. **Avaliação transitória:** análise da resposta ao degrau da primeira configuração compensada.
5. **Compensação adicional:** inclusão do compensador PI.
6. **Análise do sistema combinado:** estudo do lugar geométrico das raízes e da resposta em malha fechada.
7. **Simulação do circuito:** utilização do arquivo do PSIM para avaliar a configuração implementada no ambiente de simulação.
8. **Comparação:** análise do sobressinal e do tempo de acomodação em relação aos requisitos de projeto.

A metodologia conecta a análise matemática da planta ao estudo de seu comportamento transitório.

## 7. Tecnologias utilizadas

| Tecnologia             | Aplicação no projeto                                                                                |
| ---------------------- | --------------------------------------------------------------------------------------------------- |
| MATLAB                 | Modelagem por função de transferência, análise do lugar geométrico das raízes e resposta ao degrau. |
| Control System Toolbox | Funções de análise e projeto de sistemas de controle utilizadas pelo script.                        |
| PSIM                   | Representação e simulação do circuito eletrônico.                                                   |
| Markdown               | Documentação técnica do projeto.                                                                    |

A execução do script MATLAB depende da disponibilidade das funções utilizadas no código. Em particular, as funções de sistemas de controle requerem o ambiente e os recursos compatíveis com o MATLAB.

## 8. Estrutura do repositório

```text
ELP-ConversorBuck/
├── README.md
├── ConversorBuck.m
├── Simulação Final Conversor Buck.psimsch
└── Relatório Final.pdf
```

### Descrição dos arquivos

| Arquivo                                  | Descrição                                                                                               |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `README.md`                              | Documentação do projeto, dos modelos, dos compensadores e dos resultados.                               |
| `ConversorBuck.m`                        | Script MATLAB para modelagem, análise do lugar geométrico das raízes e avaliação da resposta ao degrau. |
| `Simulação Final Conversor Buck.psimsch` | Arquivo de circuito para utilização no PSIM.                                                            |
| `Relatório Final.pdf`                    | Relatório acadêmico com o desenvolvimento do trabalho, os resultados e as conclusões.                   |

## 9. Instalação e execução

### 9.1. Pré-requisitos

Para reproduzir as análises, são necessários:

* MATLAB com os recursos de sistemas de controle utilizados pelo script;
* PSIM para abrir e executar a simulação do circuito;
* acesso aos arquivos deste repositório.

### 9.2. Clonagem do repositório

Execute no terminal:

```bash
git clone https://github.com/coelhp/ELP-ConversorBuck.git
```

Entre no diretório:

```bash
cd ELP-ConversorBuck
```

### 9.3. Execução no MATLAB

1. Abra o MATLAB.
2. Configure o diretório de trabalho para a pasta do repositório.
3. Abra o arquivo `ConversorBuck.m`.
4. Execute o script.
5. Analise os gráficos do lugar geométrico das raízes e as respostas ao degrau.

O script apresenta as análises da planta original, da configuração compensada com PD e da configuração que incorpora a ação PI.

### 9.4. Execução no PSIM

1. Abra o PSIM.
2. Carregue o arquivo `Simulação Final Conversor Buck.psimsch`.
3. Verifique os componentes, os parâmetros e as configurações do circuito.
4. Execute a simulação.
5. Analise as formas de onda e os indicadores de desempenho disponíveis.
6. Compare os resultados com as previsões do modelo matemático.

A comparação deve considerar as diferenças entre o modelo utilizado no MATLAB e o circuito simulado no PSIM.

## 10. Resultados e análise de desempenho

O script MATLAB registra, para a configuração final com compensação PD e PI, os seguintes resultados:

| Indicador           | Referência de projeto | Resultado registrado |
| ------------------- | --------------------: | -------------------: |
| Sobressinal         |                   20% |                  18% |
| Tempo de acomodação |                400 µs |               438 µs |

### 10.1. Sobressinal

O sobressinal reportado é de 18%, inferior ao valor de referência de 20%.

Esse resultado indica que, segundo os valores registrados no script, o pico da resposta apresenta um excedente percentual menor que o limite de projeto.

### 10.2. Tempo de acomodação

O tempo de acomodação reportado é de 438 µs, enquanto o objetivo indicado no código é de 400 µs.

A diferença é:

$\Delta T_s=438-400=38\,\mu s$

Em termos percentuais:

$\frac{438-400}{400}\times100=9{,}5\%$

Assim, o tempo de acomodação registrado é 9,5% superior ao objetivo de referência.

### 10.3. Interpretação geral

Os valores registrados indicam um compromisso entre os indicadores de desempenho: o sobressinal ficou abaixo da referência, enquanto o tempo de acomodação ficou acima do objetivo.

Portanto, não se deve afirmar que todos os requisitos de projeto foram atendidos sem qualificar essa conclusão.

É recomendável verificar a resposta simulada e os critérios empregados na medição dos indicadores antes de apresentar os valores como resultados validados.

### 10.4. Comparação entre MATLAB e PSIM

Uma avaliação mais completa deve comparar a resposta do modelo matemático com as formas de onda obtidas na simulação do circuito.

A comparação pode incluir:

* valor final da variável de saída;
* sobressinal;
* tempo de acomodação;
* erro em regime permanente;
* comportamento transitório;
* diferenças entre a resposta do modelo e a do circuito simulado.

Essa análise permite avaliar a consistência entre o projeto de controle e a representação do conversor no PSIM.

## 11. Limitações e considerações

* O modelo utilizado no MATLAB é representado por uma função de transferência de segunda ordem.
* As conclusões dependem das hipóteses adotadas na modelagem da planta.
* Os resultados registrados no script precisam ser confrontados com as simulações para confirmar seu atendimento aos requisitos.
* A análise linear não representa necessariamente todos os efeitos de comutação, não linearidades e limitações físicas do circuito.
* A equivalência entre o modelo matemático e o circuito no PSIM deve ser verificada.
* Os parâmetros do controlador dependem da planta e das condições para as quais foram projetados.
* O projeto tem finalidade acadêmica e não constitui, por si só, validação de um conversor para aplicação operacional.

## 12. Possíveis melhorias

Como evolução do projeto, recomenda-se:

* documentar as condições de operação e as hipóteses utilizadas na modelagem;
* apresentar os parâmetros elétricos do conversor;
* incluir gráficos da resposta sem compensação e das configurações compensadas;
* comparar numericamente o desempenho das diferentes configurações;
* registrar as métricas calculadas automaticamente pelo MATLAB;
* verificar o atendimento aos requisitos de sobressinal e tempo de acomodação;
* comparar os resultados do MATLAB e do PSIM;
* incluir imagens das formas de onda e do circuito simulado;
* organizar as referências bibliográficas utilizadas no relatório;
* documentar as versões dos softwares empregados.

## 13. Autores

**Patrick Coelho**
**Keldson Alves**

Trabalho desenvolvido na disciplina de Eletrônica de Potência do curso de Engenharia de Controle e Automação do Instituto Federal de Goiás (IFG), Câmpus Itumbiara.

## 14. Referências

As referências bibliográficas devem corresponder às fontes efetivamente utilizadas no desenvolvimento do projeto.

Recomenda-se incluir:

* bibliografia de eletrônica de potência utilizada na modelagem do conversor Buck;
* referências sobre projeto de compensadores e análise pelo lugar geométrico das raízes;
* documentação oficial do MATLAB para as funções de sistemas de controle empregadas;
* documentação oficial do PSIM, quando pertinente;
* o relatório acadêmico do próprio projeto.

**Relatório completo:** [`Relatório Final.pdf`](Relatório%20Final.pdf).

---

Projeto acadêmico desenvolvido para aplicação de conceitos de eletrônica de potência, modelagem matemática e sistemas de controle.
