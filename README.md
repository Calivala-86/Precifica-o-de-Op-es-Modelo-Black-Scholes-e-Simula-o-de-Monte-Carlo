# Precificação de Opções: Modelo Black-Scholes e Simulação de Monte Carlo

Este notebook apresenta a implementação analítica do modelo **Black-Scholes-Merton (BSM)** e a validação numérica através da **Simulação de Monte Carlo** para opções de compra europeias (*Call Options*).

### 1. Definições de Opções
Uma **opção** é um derivativo financeiro que concede ao titular o direito, mas não a obrigação, de comprar ou vender um ativo subjacente específico a um preço predeterminado (*strike price*) em um período futuro especificado.

*   **Call Option (Compra):** Dá ao titular o direito de comprar um ativo em uma determinada data por um determinado preço.
*   **Put Option (Venda):** Dá ao titular o direito de vender um ativo em uma determinada data por um determinado preço.

Existem dois lados em cada negociação de opções: o **comprador** (*holder*) e o **vendedor** (*writer*).

### 2. Estilos de Opções
Os dois principais estilos de opções no mercado são:
*   **Opções Europeias:** Podem ser exercidas **apenas na data de vencimento**.
*   **Opções Americanas:** Podem ser exercidas a **qualquer momento** durante sua vigência.

---

### 3. O Modelo Black-Scholes (BSM)
O modelo Black-Scholes é um modelo de precificação amplamente difundido e fundamental para a engenharia financeira. Ele estima o valor teórico de opções europeias com base em 5 parâmetros principais:

1.  **$K$ (Strike Price):** Preço de exercício da opção.
2.  **$S_0$ (Current Stock Price):** Preço atual da ação.
3.  **$T$ (Time to Expiration):** Tempo até o vencimento.
4.  **$r$ (Risk-free Rate):** Taxa de juros livre de risco.
5.  **$\sigma$ (Volatility):** Volatilidade do ativo.

---

### 4. Premissas do Modelo (Assumptions)
Para que o modelo seja aplicado, assume-se que:

*   As opções negociadas são do tipo **Europeu**.
*   O comportamento do preço da ação segue uma **distribuição log-normal** com $\mu$ e $\sigma$ constantes.
*   **Não há custos de transação** ou impostos. Todos os títulos são perfeitamente divisíveis.
*   **Não há dividendos** pagos durante a vida da opção.
*   Não existem oportunidades de **arbitragem** livre de risco.
*   Investidores podem tomar ou emprestar capital à mesma **taxa livre de risco**.
### Black-Scholes-Merton (BSM) Fórmula Analítica

O preço de uma call europeia($C$) é:


$$C = S_0 N(d_1) - K e^{-rT} N(d_2)$$


Onde os componentes $d_1$ e $d_2$ are são definidos como:
    

$$d_1 = \frac{\ln(S_0 / K) + (r + \frac{\sigma^2}{2})T}{\sigma \sqrt{T}}$$

$$d_2 = \frac{\ln(S_0 / K) + (r - \frac{\sigma^2}{2})T}{\sigma \sqrt{T}}$$

$$d_2 = d_1 - \sigma \sqrt{T}$$


<br>

### Variáveis do Modelo Black-Scholes-Merton

As variáveis utilizadas na fórmula são:


| Símbolo | Variável | Descrição |
| :--- | :--- | :--- |
| $S_0$ | **Preço do Ativo** | Preço atual da ação |
| $K$ | **Preço de Exercício** | Preço definido para a compra |
| $T$ | **Tempo** | Tempo até o vencimento (expresso em fração de ano) |
| $r$ | **Taxa Livre de Risco** | Taxa de juros anualizada |
| $\sigma$ | **Volatilidade** | Desvio padrão anualizado dos retornos do ativo ($\sigma$) |
| $N(x)$ | **Distribuição Normal** | Função de densidade acumulada da normal padrão |
<br><br>

1. **$N(d_1)$ (O Delta):** 
   - Representa a sensibilidade do preço da opção em relação ao preço da ação. 
   - Se o Delta é 0.60, para cada Kwz 1,00 que o ativo adjacente sobe, a opção sobe Kwz 0,60.
    <br>
2. **$N(d_2)$ (Probabilidade de Exercício):** 
   - É a probabilidade (no mundo neutro ao risco) de a opção terminar "no dinheiro" (*In-the-Money*) na data de vencimento.
    <br>
3. **$S_0 N(d_1)$:** 
   - O valor esperado do que você recebe (ativo adjacente) se exercer a opção.
    <br>
4. **$K e^{-rT} N(d_2)$:** 
   - O valor presente do custo que você terá que pagar (o preço de exercício $K$) se a opção for exercida.
    
    <br>
**Resumo:** O preço da Call é a diferença entre o que você espera **receber** (ativo adjacente) e o que você espera **pagar** (o Strike), ambos trazidos a valor presente.


