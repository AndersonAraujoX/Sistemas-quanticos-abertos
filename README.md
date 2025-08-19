# Resolução Numérica da Equação Mestra de Lindblad

## Autor
**Anderson Araujo de Oliveira**
*Instituto de Física de São Carlos (IFSC) - Universidade de São Paulo (USP)*

---

## Introdução

Este projeto foca na investigação e análise da Equação Mestra de Lindblad, uma ferramenta essencial para descrever a evolução temporal de sistemas quânticos abertos. A equação modela fenômenos de decoerência e dissipação que surgem da interação de um sistema quântico com seu ambiente.

O objetivo principal é explorar a aplicação da equação em modelos específicos, como:
* **Modelo Jaynes-Cummings:** Descreve a interação entre um átomo de dois níveis e um modo de campo eletromagnético.
* **Modelo Spin-Boson:** Aborda a decoerência de um qubit em um ambiente dissipativo.

O notebook `Lindblad_numerico.ipynb` contém as implementações e simulações numéricas para estes modelos, e os resultados são aqui apresentados e discutidos.

---

## Modelos Teóricos

### Equação Mestra de Lindblad

A equação de Lindblad descreve a evolução temporal da matriz de densidade reduzida $\rho(t)$ de um sistema de interesse que interage com um ambiente. Derivada sob as aproximações de Born, Markov e da Onda Giratória (RWA), ela garante a positividade da matriz de densidade, resultando em uma descrição física consistente da dinâmica quântica aberta.

A forma geral da equação é:
$$
\dot{\rho}(t) = -i[H+H_{Ls}, \rho(t)] + \sum_{i} \left( L_i \rho(t) L_i^\dagger - \frac{1}{2} \{L_i^\dagger L_i, \rho(t)\} \right)
$$

Onde:
- $H$ é o Hamiltoniano do sistema.
- $H_{Ls}$ é o Hamiltoniano de deslocamento de Lamb, que renormaliza os níveis de energia do sistema.
- $L_i$ são os "operadores de salto", que modelam a interação com o ambiente.

### Modelo Jaynes-Cummings

Este modelo descreve a interação entre um átomo de dois níveis e um modo quantizado de uma cavidade óptica. É fundamental para investigar fenômenos como emissão e absorção espontânea de fótons. A Hamiltoniana total é dada por:
$$
H_T = \hat{\sigma}_z - \hbar \hat{\sigma}_x ig(\hat{a} - \hat{a}^\dagger) + \hbar\omega(\hat{a}^\dagger\hat{a})
$$

Um fenômeno notável neste modelo são as **oscilações de Rabi**, que se manifestam como uma troca coerente de energia entre o átomo e o campo, resultando em oscilações periódicas nas probabilidades de ocupação dos estados.

### Modelo Spin-Boson

Este modelo descreve um sistema de dois níveis (qubit) acoplado a um banho de osciladores harmônicos (campo bosônico), sendo amplamente utilizado para estudar a decoerência pura de um qubit. A Hamiltoniana do sistema pode incluir um termo de correção ($\epsilon\sigma_x$) vindo de um campo externo, que altera os poços de potencial do sistema. A forma geral da Hamiltoniana é:
$$
H = \frac{\hbar\Omega\sigma_z}{2} + \epsilon\sigma_x + \hbar\omega\hat{b}^\dagger\hat{b} + \hbar\sigma_z\sum_{\lambda}(g_{\lambda}\hat{b}_{\lambda} + g_{\lambda}^{*}\hat{b}_{\lambda}^{\dagger})
$$

---

## Implementação Numérica

As simulações foram realizadas em Python utilizando a biblioteca **QuTiP (Quantum Toolbox in Python)**, uma poderosa ferramenta para a dinâmica de sistemas quânticos abertos. As bibliotecas `Numpy` e `Matplotlib` também foram utilizadas para manipulação de dados e visualização dos resultados.

O notebook `Lindblad_numerico.ipynb` contém todo o código para a definição das Hamiltonianas, operadores de colapso (salto), estados iniciais e para a resolução da equação mestra usando a função `mesolve` do QuTiP.

---

## Resultados

### Simulações do Modelo Jaynes-Cummings

#### 1. Decaimento do Estado
Os gráficos abaixo mostram o valor esperado para os dois níveis de energia do átomo, com o estado inicial $\psi(0) = |1\rangle$. A simulação demonstra como o sistema evolui para diferentes taxas de acoplamento com o ambiente. O estado excitado ($|1\rangle$) decai enquanto o estado fundamental ($|0\rangle$) é populado.

*Figuras 2a e 2b no relatório.*

#### 2. Oscilações de Rabi
A simulação da interação matéria-radiação evidencia as oscilações de Rabi. A energia é trocada de forma coerente entre o átomo e o campo, gerando oscilações nas probabilidades de ocupação dos estados, acompanhadas de um decaimento exponencial devido à decoerência.

*Figura 3 no relatório.*

#### 3. Emissão Espontânea
Neste cenário, considera-se um átomo no estado fundamental interagindo com um campo inicialmente excitado. Ocorre uma troca de energia que excita o átomo enquanto o número de fótons no campo decai.

*Figura 4 no relatório.*

### Simulações do Modelo Spin-Boson (Decoerência de Qubit)

As simulações exploram a decoerência pura de um qubit para diferentes estados iniciais: $|\psi_1\rangle = \frac{|0\rangle + |1\rangle}{\sqrt{2}}$ e $|\psi_2\rangle = |1\rangle$.

#### 1. Decoerência sem Campo Externo ($\epsilon=0$)
Sem o termo de correção do campo externo, a decoerência ocorre de maneira uniforme, levando o sistema a um estado de mistura estatística.

*Figuras 5a e 5b no relatório.*

#### 2. Decoerência com Campo Externo ($\epsilon \neq 0$)
Ao adicionar o termo de correção $\epsilon\sigma_x$, observam-se oscilações nos valores esperados dos estados. Este fenômeno é explicado pelo tunelamento quântico entre os dois poços de potencial do sistema, induzido pelo campo externo.

*Figuras 6a e 6b no relatório.*

---

## Como Executar a Simulação

### Pré-requisitos
- Python 3.x
- Jupyter Notebook ou Jupyter Lab

### Instalação
Para executar o notebook, instale as bibliotecas necessárias:
```bash
pip install qutip numpy matplotlib
