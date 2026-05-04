# Apêndice A — Relatório Completo do Modelo MLP (STM32Cube.AI)

Este apêndice apresenta o relatório completo gerado pela ferramenta STM32Cube.AI durante a análise do modelo MLP quantizado. O objetivo é disponibilizar todas as informações produzidas pela ferramenta, organizadas de forma estruturada para referência e reprodutibilidade dos resultados.

---

## 1. Configuração da Análise

| Parâmetro | Valor |
|:----------|:------|
| Ferramenta | STM32Cube.AI (v8.1.0) |
| Runtime | Neural Network Tools v1.7.0 |
| Comando | `stm32ai analyze` |
| Target | STM32F4 |
| Tipo de modelo | TensorFlow Lite |
| Otimização | balanced |
| Compressão | none |

---

## 2. Identificação do Modelo

| Campo | Valor |
|:------|:------|
| Nome interno | mlp_model_int8_1 |
| Hash | 5c0f739585918b53d7c43623c55d5368 |
| Parâmetros | 10.402 |
| Tamanho | 10.45 KiB |
| Formato | ss/sa per channel |

---

## 3. Estrutura de Entrada e Saída

### Entrada

| Campo | Valor |
|:------|:------|
| Nome | serving_default_input_layer_40 |
| Tipo | INT8 |
| Shape | (1, 128) |
| Escala | 0.01416750 |
| Zero-point | 1 |
| Tamanho | 128 bytes |

### Saída

| Campo | Valor |
|:------|:------|
| Nome | nl_3 |
| Tipo | INT8 |
| Shape | (1, 2) |
| Escala | 0.00390625 |
| Zero-point | -128 |
| Tamanho | 2 bytes |

---

## 4. Uso de Memória

### Modelo

| Tipo | Bytes | KB |
|:-----|------:|---:|
| Pesos (Flash) | 10.696 | 10,45 |
| Ativações (RAM) | 1.088 | 1,06 |

---

### Sistema Completo

| Categoria | Flash (bytes) | RAM (bytes) |
|:----------|-------------:|-----------:|
| Runtime | 14.983 | 1.944 |
| Modelo | 10.696 | 0 |
| Ativações | 0 | 1.088 |
| **Total** | **25.679** | **3.032** |

---

## 5. Complexidade Computacional

| Métrica | Valor |
|:--------|------:|
| MACC | 10.432 |
| Operações totais | 10.432 |

---

## 6. Arquitetura Detalhada da Rede

### Camada 1

| Elemento | Valor |
|:---------|:------|
| Tipo | Fully Connected |
| Entrada | 128 |
| Saída | 64 |
| MACC | 8.256 |

---

### Camada 2

| Elemento | Valor |
|:---------|:------|
| Tipo | Fully Connected |
| Entrada | 64 |
| Saída | 32 |
| MACC | 2.080 |

---

### Camada 3

| Elemento | Valor |
|:---------|:------|
| Tipo | Fully Connected |
| Entrada | 32 |
| Saída | 2 |
| MACC | 66 |

---

### Saída

| Tipo | Operações |
|------|----------|
| Softmax | 30 |

---

## 7. Distribuição de Complexidade

| Camada | % MACC | % Memória |
|:-------|-------:|----------:|
| Dense 1 | 79.1% | 79.0% |
| Dense 2 | 19.9% | 20.3% |
| Dense 3 | 0.6% | 0.7% |
| Softmax | 0.3% | 0.0% |

---

## 8. Tipos de Operações

| Operação | Quantidade | Percentual |
|:---------|----------:|-----------:|
| smul_s8_s8 | 10.402 | 99.7% |
| op_s8_s8 | 30 | 0.3% |

---

## 9. Operações por Camada

| Camada | Tipo | Operações |
|:-------|:------|----------:|
| gemm_0 | Dense | 8.256 |
| gemm_1 | Dense | 2.080 |
| gemm_2 | Dense | 66 |
| nl_3 | Softmax | 30 |

---

## 10. Uso de Memória por Segmento

| Módulo | text | rodata | data | bss |
|:-------|-----:|------:|----:|----:|
| Runtime | 11.764 | 0 | 0 | 0 |
| mpl.o | 584 | 703 | 1.740 | 116 |
| mpl_data.o | 56 | 48 | 88 | 0 |
| **Total RT** | 12.404 | 751 | 1.828 | 116 |
| Pesos | 0 | 10.696 | 0 | 0 |
| Ativações | 0 | 0 | 0 | 1.088 |

---

## 11. Uso por Tipo de Memória

| Tipo | Flash | RAM |
|:-----|------:|---:|
| Runtime | 14.983 | 1.944 |
| Total | 25.679 | 3.032 |

---

## 12. Observações Técnicas

- O modelo utiliza quantização INT8 com alta predominância de operações inteiras;
- O custo computacional está concentrado na primeira camada;
- O uso de memória RAM é majoritariamente associado às ativações;
- O runtime representa parcela significativa do consumo total de memória.

---

## 13. Observação sobre Uso no TCC

As informações apresentadas neste apêndice correspondem ao relatório completo gerado pela ferramenta STM32Cube.AI. No corpo principal do trabalho, foi realizada uma seleção das métricas mais relevantes (memória e MACC), com o objetivo de facilitar a análise comparativa entre arquiteturas.
