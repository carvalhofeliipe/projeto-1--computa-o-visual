# Projeto 1: Processamento Digital de Imagens (PDI) 
### Disciplina: Computação Visual 

## Integrantes do Grupo
* **Giulia Araki** - RA: 10408954
* **Felipe Carvalho** - RA: 10409804
* **Gabriel Rodrigues** - RA: 10409071

Este projeto consiste em um processador de imagens desenvolvido em linguagem C utilizando a biblioteca **SDL3**. O software é capaz de carregar imagens, convertê-las para escala de cinza, analisar histogramas (brilho e contraste) e realizar a equalização de histograma para melhoria visual.

---

## Demonstração em Vídeo
Como o projeto foi desenvolvido em ambiente **macOS**, decidimos disponibilizar uma demonstração completa para garantir a visualização dos requisitos em funcionamento, caso o professor não utilize esse processador:

 **[ASSISTIR VÍDEO DE DEMONSTRAÇÃO NO YOUTUBE](https://youtu.be/ysX5F_Pxfzc)**

---

## Integrantes do Grupo
* **Giulia Araki** - RA: 10408954
* **Felipe Carvalho** - RA: 10409804
* **Gabriel Rodrigues** - RA: 10409071

---

## Funcionalidades Realizadas
- [x] **Carregamento Multiformato:** Suporte a PNG, JPG e BMP via `SDL_image`.
- [x] **Tratamento de Erros:** Verificação de integridade de arquivos e caminhos.
- [x] **Conversão Gray:** Transformação de cores usando a fórmula de luminância:  
  $$Y = 0.2125 \cdot R + 0.7154 \cdot G + 0.0721 \cdot B$$
- [x] **Análise de Histograma:** Cálculo em tempo real de Média (Brilho) e Desvio Padrão (Contraste).
- [x] **Classificação Automática:** Textos dinâmicos classificando a imagem (Ex: "Imagem Escura", "Contraste Baixo").
- [x] **Equalização de Histograma:** Algoritmo baseado na Função de Distribuição Acumulada (CDF).
- [x] **Interface Interativa:** Botão dinâmico com estados de cor (Hover/Click) e alternância entre original/equalizado.
- [x] **Exportação:** Tecla `S` para salvar o resultado final como `output_image.png`.

---

## Como Compilar e Executar (macOS)

### Pré-requisitos
Certifique-se de ter o **Homebrew** instalado e as bibliotecas necessárias:
```bash
brew install sdl3 sdl3_image sdl3_ttf

---
## 🛡️ Provas de Implementação (Defesa do Projeto)

Esta seção detalha exatamente onde e como cada requisito obrigatório do projeto foi cumprido no código-fonte `main.c`.

### 1. Requisitos Técnicos e Ambiente
- **Linguagem (C99+):** O código utiliza o padrão moderno da linguagem C, permitindo declarações de variáveis dentro do escopo de loops `for`.
  - *Evidência (Linha 28):* `for (int y = 0; y < temp->h; y++)`
- **Bibliotecas Obrigatórias:** Uso de `SDL3`, `SDL3_image` e `SDL3_ttf`.
  - *Evidência (Linhas 8-10):* Inclusões de cabeçalho `#include <SDL3/SDL.h>`, etc.

### 2. Carregamento e Tratamento de Erros
- **Formatos Comuns (PNG, JPG, BMP):** Implementado via `SDL_image`.
  - *Evidência (Linha 127):* Uso da função `IMG_Load(argv[1])`.
- **Tratamento de Arquivo Não Encontrado:** O programa verifica a integridade do ponteiro da imagem e encerra de forma segura caso falte o arquivo.
  - *Evidência (Linhas 128-130):* ```c
    if (!image) { printf("Erro na imagem!\n"); return 1; }
    ```

### 3. Análise e Conversão para Escala de Cinza
- **Fórmula de Luminância ($Y$):** Implementação exata dos pesos solicitados pelo professor.
  - *Evidência (Linha 34):* `Uint8 gray = (Uint8)(0.2125 * r + 0.7154 * g + 0.0721 * b);`
- **Base para Operações:** A imagem convertida (`gray`) é a entrada obrigatória para o histograma e a equalização.

### 4. Análise e Exibição do Histograma
- **Exibição Gráfica:** Desenho proporcional das barras brancas sobre fundo preto.
  - *Evidência:* Função `drawHistogram` (Linhas 87-93).
- **Análise Estatística:** Cálculo matemático de Média (Brilho) e Desvio Padrão (Contraste).
  - *Evidência:* Função `computeHistogram` (Linhas 42-53).
- **Classificação Automática:** Legendagem dinâmica em amarelo usando a biblioteca `SDL_ttf`.
  - *Evidência (Linhas 104-105):* Classificações entre "clara/média/escura" e "alto/médio/baixo contraste".

### 5. Equalização do Histograma (Interatividade)
- **Botão com Primitivas SDL:** Botão desenhado e renderizado nativamente.
  - *Evidência:* Função `renderButton` (Linhas 95-101) via `SDL_RenderFillRect`.
- **Estados de Cor do Botão:** Feedback visual completo para o usuário.
  - *Azul:* Neutro | *Azul Claro:* Hover | *Azul Escuro:* Clicado.
- **Reversão para Original (Toggle):** O sistema alterna texturas e labels entre "Equalizar" e "Ver Original".
  - *Evidência (Linhas 147-152):* Uso da flag `isEqualized` para alternar o estado do sistema.

## Provas de Implementação

Para auxiliar na correção, esta seção detalha exatamente onde e como cada requisito obrigatório do projeto foi cumprido no código-fonte `main.c`.

### 1. Requisitos Técnicos e Ambiente
- **Linguagem (C99+):** O código utiliza o padrão moderno da linguagem C.
  - *Evidência:* Declarações de variáveis dentro do escopo de loops `for` (ex: `for (int y = 0; y < temp->h; y++)` na linha 28), o que é característico do padrão C99 ou superior.
<img width="547" height="123" alt="image" src="https://github.com/user-attachments/assets/9e4e911d-0189-4f03-bb80-6068b41d9a4a" />

- **Bibliotecas Obrigatórias:** Uso de `SDL3`, `SDL3_image` e `SDL3_ttf`.
  - *Evidência:* Inclusões de cabeçalho nas linhas 8-10 (`#include <SDL3/SDL.h>`, etc.).
<img width="239" height="86" alt="image" src="https://github.com/user-attachments/assets/8e42b934-0d25-4029-ae41-25e2fce04116" />


### 2. Carregamento e Tratamento de Erros
- **Formatos Comuns (PNG, JPG, BMP):** Implementado via `SDL_image`.
  - *Evidência:* Chamada de `IMG_Load(argv[1])` na linha 127. No [vídeo de demonstração](https://youtu.be/ysX5F_Pxfzc), testamos arquivos de cada formato com sucesso.
<img width="488" height="67" alt="image" src="https://github.com/user-attachments/assets/48007b38-1a49-432b-8a33-aa4d5dcd3407" />

- **Tratamento de Arquivo Não Encontrado:** O programa avisa o usuário e encerra de forma segura.
<img width="506" height="40" alt="image" src="https://github.com/user-attachments/assets/3889d8e3-5ab9-4c38-acf3-237385aa24b0" />


### 3. Análise e Conversão para Escala de Cinza
- **Fórmula de Luminância ($Y$):** Implementação exata da fórmula pedida.
<img width="529" height="121" alt="image" src="https://github.com/user-attachments/assets/5cbf89a2-a498-4c33-8cdf-ed4f78a2a246" />

- **Base para Operações:** A imagem cinza é usada como entrada para o histograma e equalização.
<img width="1180" height="183" alt="image" src="https://github.com/user-attachments/assets/e9590230-20c9-4ea4-82ab-c882ed5c07d4" />

### 4. Análise e Exibição do Histograma
- **Exibição Gráfica:** Desenho proporcional das barras.
<img width="802" height="127" alt="image" src="https://github.com/user-attachments/assets/3807145f-c0a8-437a-a6fd-8635f46fbe88" />

- **Análise Estatística (Brilho e Contraste):** Cálculo de Média e Desvio Padrão.
<img width="627" height="102" alt="image" src="https://github.com/user-attachments/assets/c46d0d92-c2cc-4a95-b250-8cc02e7d2df6" />

- **Classificação Automática (via SDL_ttf):** Legendagem dinâmica em amarelo.
<img width="765" height="166" alt="image" src="https://github.com/user-attachments/assets/0ed9aece-ca2f-484a-ad90-bf0bd7c2012e" />


### 5. Equalização do Histograma (Interatividade)
- **Botão com Primitivas SDL:** Desenho nativo sem arquivos externos.
<img width="634" height="206" alt="image" src="https://github.com/user-attachments/assets/d1e870fd-d3d0-479d-bee4-d3e7573c51dd" />

- **Estados de Cor do Botão:** Feedback visual de Neutro (Azul), Hover (Azul Claro) e Click (Azul Escuro).
<img width="651" height="210" alt="image" src="https://github.com/user-attachments/assets/b33d34ab-01df-42e3-be8e-18f241872ece" />

- **Reversão para Original (Toggle):** O botão alterna entre "Equalizar" e "Ver Original".
<img width="569" height="57" alt="image" src="https://github.com/user-attachments/assets/3c38e27e-0e57-4a22-bf23-0e27bc6af1f9" />

