# 📊 Guia Completo: Economia dos Recursos Naturais - Recursos Pesqueiros

## Atividade: Planilhas 1, 2, 3 e 4 - Módulos 1 e 2

---

## 📋 PARTE 1: PREPARAÇÃO INICIAL (Todas as Planilhas)

### Passo 1: Instalar o Solver no Excel
Se não encontrar "Solver" em "Dados":
1. Clique em **Office/Arquivo → Opções → Suplementos**
2. Selecione **Suplementos do Excel**
3. Marque **Solver** e clique em **OK**

### Passo 2: Configurar os Parâmetros (Planilhas 1 e 2)

Nas planilhas 1 e 2, insira em:
- **A3 a A5:** `r`, `K`, `a`
- **B3 a B5:** `1`, `1`, `0.5` (respectivamente)

Nas células **A6 a A9** insira os rótulos:
- **A6:** `Xss`
- **A7:** `Yss`
- **A8:** `|G'(Xss)|`
- **A9:** `Xo`

---

## 📈 PLANILHA 1: EQUILÍBRIO DE ESTADO ESTACIONÁRIO

### Configuração das Fórmulas:

**Célula B6 (Xss):**
```
=($B$4*($B$3-$B$5))/$B$3
```
Equivalente a: Xss = K(r-a)/r

**Célula B7 (Yss):**
```
=$B$3*$B$6*(1-$B$6/$B$4)
```
Equivalente a: Yss = rXss(1 - Xss/K)

**Célula B8 (|G'(Xss)|):**
```
=ABS(1-$B$3+$B$5)
```
Equivalente a: |1 - r + a| < 1

**Célula B9 (Xo):**
```
0.1
```

### Criar a Tabela de Valores:

**Linha 12 (cabeçalho):**
- A12: `X`
- B12: `F(X) = r*X*(1-X/K)`
- C12: `Y = a*X`

**A13:** `0` (inicia em zero)

**A14:** `=A13+0.025` (incrementa 0.025)
- Copie até A53 (para X ir até ~1)

**B13:**
```
=A13
```

**B14:**
```
=$B$3*A14*(1-A14/$B$4)
```
(Copie até B53)

**C13:**
```
=A13
```

**C14:**
```
=$B$5*A14
```
(Copie até C53)

### Criar o Gráfico:
1. Selecione **A12:C53**
2. Insira **Gráfico de Dispersão com Linhas**
3. Eixo X: valores de A (X)
4. Eixo Y: valores de B e C (F(X) e Y)
5. Títulos: "Equilíbrio no estado estacionário"

---

## 🔄 PLANILHA 2: CAMINHO "ÓTIMO" PARA O ESTADO ESTACIONÁRIO

### Configuração das Fórmulas:

**Linha 12 (cabeçalho):**
- A12: `t`
- B12: `Xt`
- C12: `Yt`

**A13:** `0`

**A14 a A32:** `1, 2, 3, ...` (até 19)

**B13 (valor inicial):**
```
=$B$9
```
(Isto é, X₀ = 0.1)

**B14 (dinâmica):**
```
=B13*(1+$B$3-$B$5-$B$3*B13/$B$4)
```
Equivalente a: Xt₊₁ = Xt(1 + r - a - r*Xt/K)

- Copie a fórmula de B14 até B32

**C13:**
```
=$B$5*B13
```

**C14:**
```
=$B$5*B14
```

- Copie até C32

### Criar o Gráfico:
1. Selecione **A12:C32**
2. Insira **Gráfico de Dispersão com Linhas**
3. Eixo X: tempo (t)
4. Eixo Y: Xt e Yt
5. Título: "Caminhos ótimos para Xt e Yt"

---

## 💰 PLANILHA 3: POLÍTICA DE EXTRAÇÃO LINEAR ÓTIMA

### Passo 1: Copiar a Planilha 2
Copie as colunas A, B e C da linha 12 para a linha 16 (para a linha 16 para baixo).

### Passo 2: Adicionar Parâmetros de Extração

**Linha 11 (cabeçalho):**
- A11: `p` (preço)
- B11: `c` (custo)
- C11: `δ` (desconto)
- D11: `ρ` (fator de desconto)

**Valores (Linha 12):**
- A12: `5` (preço)
- B12: `1` (custo)
- C12: `0.05` (desconto)
- D12: `=1/(1+C12)` ou `=1/(1+0.05)`

### Passo 3: Criar Coluna de Lucro e Valor Presente

**Linha 16 (cabeçalho):**
- D16: `π(t)`
- E16: `ρᵗ*π(t)`

**D17 (lucro instantâneo):**
```
=(A12-B12)*C17
```
(C17 é Yt da planilha 2 copiada)

**E17 (valor presente):**
```
=$D$12^A17*D17
```

- Copie E17 até E36

### Passo 4: Calcular Valor Total

**Célula E37:**
```
=SUM(E17:E36)
```

### Passo 5: Usar o Solver

1. Clique em **Dados → Solver**
2. Configure:
   - **Célula de objetivo:** `$E$37` (maximize)
   - **Alterando células:** `$B$5` (valor de a)
   - **Restrições:** `$B$8 < 1` (estabilidade)
3. Clique em **Resolver**

---

## 📊 PLANILHA 4: COMPARAÇÃO E SIMULAÇÕES

Faça alterações nos parâmetros (r, K, a, X₀) das planilhas 1 e 2:

**Exemplos de simulações:**
- Mude `a` para 1.3 ou 2.6
- Mude `r` para valores diferentes
- Observe como os gráficos mudam

---

## ✅ Checklist Final

- [ ] Planilha 1 criada com gráfico de equilíbrio
- [ ] Planilha 2 criada com dinâmica temporal
- [ ] Planilha 3 com Solver configurado
- [ ] Todos os gráficos visualizando corretamente
- [ ] Simulações realizadas

---

## 🎯 Dúvidas Comuns

**P: Minha fórmula dá erro?**
R: Verifique se as referências ($B$3, etc.) estão corretas e se os valores em B3:B5 estão preenchidos.

**P: O Solver não acha solução?**
R: Tente mudar o valor inicial de `a` (B5) para algo próximo de 0.5 antes de rodar.

**P: Como interpretar os gráficos?**
R: Na Planilha 1, veja onde F(X) (crescimento) e Y (extração) se cruzam. Na Planilha 2, veja como Xt converge para equilíbrio.

---

**Pronto! Agora é só seguir passo a passo! 🚀**
