# Apêndice C — Relatório Completo do Modelo CNN Deep (STM32Cube.AI)

Este apêndice apresenta o relatório completo gerado pela ferramenta STM32Cube.AI para o modelo CNN Deep quantizado, organizado de forma estruturada para documentação e reprodutibilidade.

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
| Nome interno | cnn_deep_model_int8_1 |
| Hash | e5140f217f438eb97091e8d0897e2667 |
| Parâmetros | 12.130 |
| Tamanho | 12.37 KiB |
| Formato | ss/sa per channel |

---

## 3. Entrada e Saída do Modelo

### Entrada

| Campo | Valor |
|:------|:------|
| Nome | serving_default_input_layer_60 |
| Tipo | INT8 |
| Shape | (1, 128, 1) |
| Escala | 0.01504106 |
| Zero-point | -1 |
| Tamanho | 128 bytes |

---

### Saída

| Campo | Valor |
|:------|:------|
| Nome | nl_18 |
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
| Pesos (Flash) | 12.664 | 12,37 |
| Ativações (RAM) | 9.152 | 8,94 |

---

### Sistema Completo

| Categoria | Flash (bytes) | RAM (bytes) |
|:----------|-------------:|-----------:|
| Runtime | 33.448 | 3.680 |
| Modelo | 12.664 | 0 |
| Ativações | 0 | 9.152 |
| **Total** | **46.112** | **12.832** |

---

## 5. Complexidade Computacional

| Métrica | Valor |
|:--------|------:|
| MACC | **281.936** |
| Operações totais | 281.936 |

---

## 6. Arquitetura Detalhada da Rede

### Camadas Convolucionais

| Camada | Tipo | Parâmetros | MACC |
|:-------|:------|----------:|-----:|
| Conv1 | Conv2D | 112 | 6.064 |
| Conv2 | Conv2D | 1.664 | 93.728 |
| Conv3 | Conv2D | 6.400 | 172.096 |

---

### Pooling

| Camada | Tipo | MACC |
|:-------|:------|-----:|
| Pool1 | MaxPooling | 2.016 |
| Pool2 | MaxPooling | 1.920 |
| Pool3 | Mean (Global) | 1.792 |

---

### Camadas Densas

| Camada | Tipo | Parâmetros | MACC |
|:-------|:------|----------:|-----:|
| Dense1 | Fully Connected | 4.096 | 4.160 |
| Dense2 | Fully Connected | 128 | 130 |

---

### Saída

| Camada | Tipo | MACC |
|:-------|:------|-----:|
| Softmax | Ativação | 30 |

---

## 7. Distribuição de Complexidade

| Camada | % MACC | % Memória |
|:-------|-------:|----------:|
| Conv1 | 2,2% | 0,9% |
| Pool1 | 0,7% | 0% |
| Conv2 | 33,2% | 13,1% |
| Pool2 | 0,7% | 0% |
| Conv3 | 61,0% | 50,5% |
| Pool3 | 0,6% | 0% |
| Dense1 | 1,5% | 34,4% |
| Dense2 | ~0% | 1,1% |
| Softmax | ~0% | ~0% |

---

## 8. Tipos de Operações

| Tipo | Quantidade | % |
|:------|----------:|--:|
| smul_s8_s8 | 276.178 | 98,0% |
| op_s8_s8 | 5.758 | 2,0% |

---

## 9. Operações por Camada

| Camada | Tipo | Operações |
|:-------|:------|----------:|
| conv2d_1 | Convolução | 6.064 |
| pool_4 | Pooling | 2.016 |
| conv2d_7 | Convolução | 93.728 |
| pool_10 | Pooling | 1.920 |
| conv2d_13 | Convolução | 172.096 |
| pool_15 | Pooling | 1.792 |
| gemm_16 | Dense | 4.160 |
| gemm_17 | Dense | 130 |
| nl_18 | Softmax | 30 |

---

## 10. Uso de Memória por Segmento

| Módulo | text | rodata | data | bss |
|:-------|-----:|------:|----:|----:|
| Runtime | 27.848 | 0 | 0 | 0 |
| cnn_deep.o | 772 | 1.280 | 3.356 | 236 |
| cnn_deep_data.o | 56 | 48 | 88 | 0 |
| **RT Total** | 28.676 | 1.328 | 3.444 | 236 |
| Pesos | 0 | 12.664 | 0 | 0 |
| Ativações | 0 | 0 | 0 | 9.152 |

---

## 11. Memória Total por Tipo

| Tipo | Flash (bytes) | RAM (bytes) |
|:-----|-------------:|-----------:|
| Runtime | 33.448 | 3.680 |
| Total | 46.112 | 12.832 |

---

## 12. Resumo Final do Modelo

| Item | Valor |
|:------|:------|
| Flash total | 45.03 KiB |
| RAM total | 12.53 KiB |
| Pesos | 12.37 KiB |
| Ativações | 8.94 KiB |
| MACC | 281.936 |

---

## 13. Observações Técnicas

- O modelo apresenta predominância de operações inteiras (INT8), resultado da quantização;
- O custo computacional está fortemente concentrado na terceira camada convolucional;
- O uso de memória RAM é majoritariamente associado às ativações intermediárias;
- O aumento da profundidade da rede impacta diretamente o custo computacional e o uso de memória.

---

## 14. Observação sobre Uso no TCC

As informações apresentadas neste apêndice correspondem ao relatório completo gerado pela ferramenta STM32Cube.AI. No corpo principal do trabalho, foi realizada a seleção das métricas mais relevantes para análise, enquanto este apêndice mantém a totalidade dos dados para fins de documentação e rastreabilidade.
