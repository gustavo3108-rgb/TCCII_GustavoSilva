# Apêndice B — Relatório Completo do Modelo CNN (STM32Cube.AI)

Este apêndice apresenta o relatório completo gerado pela ferramenta STM32Cube.AI para o modelo CNN quantizado, organizado de forma estruturada para documentação e reprodutibilidade.

---

## 1. Configuração da Análise

| Parâmetro | Valor |
|:----------|:------|
| Ferramenta | STM32Cube.AI v8.1.0 |
| Runtime | Neural Network Tools v1.7.0 |
| Target | STM32F4 |
| Tipo de modelo | TensorFlow Lite |
| Otimização | balanced |
| Compressão | none |

---

## 2. Identificação do Modelo

| Campo | Valor |
|:------|:------|
| Nome interno | cnn_model_int8_1 |
| Hash | 9e1f212da70e8cf7c11d09a6406e7b12 |
| Parâmetros | 2.754 |
| Tamanho | 2.93 KiB |
| Formato | ss/sa per channel |

---

## 3. Entrada e Saída do Modelo

### Entrada

| Campo | Valor |
|:------|:------|
| Nome | serving_default_input_layer_50 |
| Tipo | INT8 |
| Shape | (1, 128, 1) |
| Escala | 0.01467704 |
| Zero-point | -2 |
| Tamanho | 128 bytes |

---

### Saída

| Campo | Valor |
|:------|:------|
| Nome | nl_12 |
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
| Pesos (Flash) | 3.000 | 2,93 |
| Ativações (RAM) | 6.672 | 6,52 |

---

### Sistema Completo

| Categoria | Flash (bytes) | RAM (bytes) |
|:----------|-------------:|-----------:|
| Runtime | 32.166 | 3.008 |
| Modelo | 3.000 | 0 |
| Ativações | 0 | 6.672 |
| **Total** | **35.166** | **9.680** |

---

## 5. Complexidade Computacional

| Métrica | Valor |
|:--------|------:|
| MACC | **104.912** |
| Operações totais | 104.912 |

---

## 6. Arquitetura Detalhada da Rede

### Camadas Convolucionais

| Camada | Tipo | Parâmetros | MACC |
|:-------|:------|----------:|-----:|
| Conv1 | Conv2D | 112 | 6.064 |
| Conv1 (ativação) | Conv2D | — | 2.016 |
| Conv2 | Conv2D | 1.664 | 93.728 |
| Conv2 (ativação) | Conv2D | — | 1.952 |

---

### Pooling

| Camada | Tipo | MACC |
|:-------|:------|-----:|
| Pool1 | MaxPooling | 2.016 |
| Pool2 | Mean (Global) | 1.952 |

---

### Camadas Densas

| Camada | Tipo | Parâmetros | MACC |
|:-------|:------|----------:|-----:|
| Dense1 | Fully Connected | 1.024 | 1.056 |
| Dense2 | Fully Connected | 64 | 66 |

---

### Saída

| Camada | Tipo | MACC |
|:-------|:------|-----:|
| Softmax | Ativação | 30 |

---

## 7. Distribuição de Complexidade

| Camada | % MACC | % Memória |
|:-------|-------:|----------:|
| Conv1 | 5,8% | 3,7% |
| Pool1 | 1,9% | 0% |
| Conv2 | 89,3% | 55,5% |
| Pool2 | 1,9% | 0% |
| Dense1 | 1,0% | 38,4% |
| Dense2 | 0,1% | 2,4% |
| Softmax | ~0% | ~0% |

---

## 8. Tipos de Operações

| Tipo | Quantidade | % |
|:------|----------:|--:|
| smul_s8_s8 | 100.914 | 96,2% |
| op_s8_s8 | 3.998 | 3,8% |

---

## 9. Operações por Camada

| Camada | Tipo | Operações |
|:-------|:------|----------:|
| conv2d_1 | Convolução | 6.064 |
| pool_4 | Pooling | 2.016 |
| conv2d_7 | Convolução | 93.728 |
| pool_9 | Pooling | 1.952 |
| gemm_10 | Dense | 1.056 |
| gemm_11 | Dense | 66 |
| nl_12 | Softmax | 30 |

---

## 10. Uso de Memória por Segmento

| Módulo | text | rodata | data | bss |
|:-------|-----:|------:|----:|----:|
| Runtime | 27.848 | 0 | 0 | 0 |
| cnn.o | 676 | 726 | 2.724 | 196 |
| cnn_data.o | 56 | 48 | 88 | 0 |
| **RT Total** | 28.580 | 774 | 2.812 | 196 |
| Pesos | 0 | 3.000 | 0 | 0 |
| Ativações | 0 | 0 | 0 | 6.672 |

---

## 11. Memória Total por Tipo

| Tipo | Flash (bytes) | RAM (bytes) |
|:-----|-------------:|-----------:|
| Runtime | 32.166 | 3.008 |
| Total | 35.166 | 9.680 |

---

## 12. Resumo Final do Modelo

| Item | Valor |
|:------|:------|
| Flash total | 36.32 KiB |
| RAM total | 9.57 KiB |
| Pesos | 2.93 KiB |
| Ativações | 6.52 KiB |
| MACC | 104.912 |

---

## 13. Observações Técnicas

- O modelo apresenta predominância de operações inteiras (INT8), resultado da quantização;
- O custo computacional está fortemente concentrado na segunda camada convolucional;
- O uso de memória RAM é majoritariamente associado às ativações intermediárias;
- O runtime representa parcela significativa do uso total de memória do sistema.

---

## 14. Observação sobre Uso no TCC

As informações apresentadas neste apêndice correspondem ao relatório completo gerado pela ferramenta STM32Cube.AI. No corpo principal do trabalho, foi realizada a seleção das métricas mais relevantes para análise comparativa, enquanto este apêndice mantém a totalidade dos dados para fins de documentação.
