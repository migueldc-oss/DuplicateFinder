# Manual do utilizador — DuplicateFinder

> ![Captura de ecrã da aplicação](capturas/main.png)
> *Vista principal do DuplicateFinder com a barra de análise e a tabela de resultados.*

---

## Índice

1. [Introdução](#1-introdução)
2. [Requisitos do Sistema](#2-requisitos-do-sistema)
3. [Interface Principal](#3-interface-principal)
4. [Selecionar Pastas](#4-selecionar-pastas)
5. [Modos de Deteção](#5-modos-de-deteção)
6. [Progresso da Análise](#6-progresso-da-análise)
7. [Resultados](#7-resultados)
8. [Ações sobre Ficheiros](#8-ações-sobre-ficheiros)
9. [Exportar Resultados](#9-exportar-resultados)
10. [Preferências](#10-preferências)
11. [Dicas e Boas Práticas](#11-dicas-e-boas-práticas)

---

## 1. Introdução

O **DuplicateFinder** é uma aplicação macOS que encontra e gere ficheiros duplicados no seu disco. Analisa uma ou mais pastas, calcula uma impressão digital SHA-256 para cada ficheiro e agrupa os idênticos, permitindo-lhe rever, abrir, eliminar ou exportar um relatório.

### Funcionalidades Principais

- Análise recursiva de múltiplas pastas em simultâneo.
- Dois modos de deteção: **Fiável** (baseado no conteúdo, SHA-256) e **Rápido** (nome + tamanho).
- Filtros por tamanho, extensões e pastas excluídas.
- Tabela ordenável com pesquisa nos resultados.
- Ações individuais e em lote: abrir, revelar no Finder, mover para o Lixo ou eliminar permanentemente.
- Exportação para CSV e JSON com a localização de cada ficheiro duplicado.
- Interface localizada em 8 idiomas.

---

## 2. Requisitos do Sistema

- **macOS** 14.0 (Sonoma) ou superior.
- **Apple Silicon** ou **Intel**.
- Não requer pacotes externos nem dependências.

---

## 3. Interface Principal

![Disposição da interface](capturas/interfaz.png)

A janela está dividida em três áreas:

| Área | Descrição |
|------|-----------|
| **Barra superior (ScanView)** | Seleção de pastas, seletor de modo de deteção, controlos de iniciar/cancelar. |
| **Barra de estatísticas** | Métricas globais (total de ficheiros, duplicados, grupos, espaço recuperável) e botão de exportação. |
| **Tabela de resultados** | Lista ordenável de grupos de duplicados com pesquisa. |

---

## 4. Selecionar Pastas

![Seleção de pastas](capturas/seleccion-carpetas.png)

1. Clique no botão **"Escolher Pasta…"** (ícone de pasta).
2. O diálogo padrão do macOS abre. Selecione **uma ou várias pastas** premindo ⌘ (Command).
3. As pastas **acumulam-se** na lista. Pode adicionar mais pastas em seleções subsequentes.
4. Para limpar a seleção, clique no botão **"Limpar"** (ícone ✕) que aparece ao lado.

> O botão **"Iniciar Análise"** permanece desativado até que pelo menos uma pasta seja selecionada. Também pode arrastar uma pasta do Finder diretamente para a janela.

---

## 5. Modos de Deteção

O DuplicateFinder oferece dois modos, selecionáveis através de um controlo segmentado na barra superior:

| Modo | Descrição |
|------|-----------|
| **Fiável** | Calcula o hash SHA-256 do **conteúdo completo** de cada ficheiro. Garante a ausência de falsos positivos, mas é mais lento porque lê todos os ficheiros. |
| **Nome + Tamanho** | Compara apenas o nome (sem distinção de maiúsculas/minúsculas) e o tamanho em bytes. Muito rápido (sem leitura de ficheiros), mas pode produzir falsos positivos se ficheiros diferentes partilharem o mesmo nome e tamanho. |

> O modo predefinido é definido em **Preferências → Deteção**.

---

## 6. Progresso da Análise

Durante uma análise, a barra superior mostra a fase atual:

| Fase | Indicador |
|------|-----------|
| **A analisar…** | Contador de ficheiros processados na pasta. |
| **A comparar…** | Barra de progresso com o número de hashes calculados em relação ao total de candidatos. |
| **A calcular…** | Progresso da inserção na base de dados e cálculo de agregados. |
| **Concluída** | Ícone de visto verde. |
| **Cancelada** | Ícone laranja. |

Pode cancelar a análise a qualquer momento clicando no botão **"Cancelar"**.

---

## 7. Resultados

![Tabela de resultados](capturas/resultados.png)

Assim que a análise termina, a tabela de resultados aparece com as seguintes colunas:

| Coluna | Descrição |
|--------|-----------|
| **Nome** | Nome do ficheiro com o seu ícone. |
| **Tamanho** | Tamanho de cada cópia. |
| **Cópias** | Número de duplicados para este ficheiro. |
| **Tamanho × Cópias** | Espaço total ocupado por todas as cópias. |
| **Localização** | Caminho completo de cada cópia, com botões de ação. |

Pode **ordenar** a tabela clicando em qualquer cabeçalho de coluna. Também pode **pesquisar** ficheiros por nome ou caminho usando o campo de pesquisa na parte inferior.

### Barra de estatísticas

Quatro métricas são apresentadas acima dos resultados:

- **Total de ficheiros**: todos os ficheiros analisados.
- **Duplicados**: ficheiros pertencentes a um grupo de duplicados.
- **Grupos**: conjuntos de ficheiros idênticos.
- **Recuperável**: espaço libertado se todas as cópias duplicadas (menos uma por grupo) forem removidas.

---

## 8. Ações sobre Ficheiros

Cada ficheiro duplicado na coluna "Localização" tem botões de ação:

| Botão | Ação |
|-------|------|
| 👁 (Olho) | Abrir o ficheiro com a aplicação predefinida. |
| 📁 (Pasta) | Revelar o ficheiro no Finder. |
| 🗑 (Lixo) | Mover para o Lixo (ou eliminar permanentemente, dependendo das preferências). |

### Eliminação em lote

Pode selecionar vários ficheiros marcando a caixa quadrada ao lado de cada um:

1. Marque os ficheiros que pretende eliminar.
2. O botão **"Eliminar selecionados (N)"** aparece na barra de estatísticas.
3. Clique nele para confirmar e concluir a eliminação.

> Pode alterar o comportamento de eliminação em **Preferências → Geral**: ativar/desativar "Mover ficheiros para o Lixo".

---

## 9. Exportar Resultados

Clique no botão **"Exportar"** (ícone de partilha) na barra de estatísticas e escolha:

- **CSV** — Ficheiro de texto separado por vírgulas, compatível com Excel, Numbers e folhas de cálculo.
- **JSON** — Formato estruturado, ideal para processamento programático.

Ambos os formatos incluem **todas as cópias de cada ficheiro duplicado** (não apenas uma por grupo), com os campos: nome, caminho, tamanho, número de cópias, espaço total ocupado e hash SHA-256.

Um diálogo `NSSavePanel` abre para escolher o destino e o nome do ficheiro.

---

## 10. Preferências

Prima `⌘,` (Command + ,) para abrir as preferências, organizadas em quatro separadores.

### Geral

| Opção | Descrição |
|-------|-----------|
| **Top N resultados** | Número máximo de linhas na tabela de resultados (10–100.000). |
| **Mover para o Lixo** | Quando ativado, os ficheiros são enviados para o Lixo em vez de serem eliminados permanentemente. |
| **Estratégia de conservação** | Estratégia para selecionar automaticamente qual cópia manter (mais antiga, mais recente ou caminho mais curto). |
| **Aparência** | Modo de aparência claro, escuro ou sistema. |

### Deteção

| Opção | Descrição |
|-------|-----------|
| **Modo predefinido** | Modo de deteção selecionado ao abrir a aplicação. |

### Filtros

| Opção | Descrição |
|-------|-----------|
| **Tamanho mín. / máx.** | Intervalo de tamanho em bytes. Ficheiros fora deste intervalo são ignorados. |
| **Incluir ocultos** | Incluir ficheiros e pastas ocultos (que começam por `.`). |
| **Seguir ligações simbólicas** | Quando ativado, as ligações simbólicas são seguidas durante a análise. |
| **Extensões permitidas** | Lista separada por vírgulas (ex.: `jpg, png, mp4`). Vazio = todas as extensões. |
| **Pastas excluídas** | Lista separada por vírgulas de nomes de pastas ignoradas durante a análise (ex.: `node_modules, .git`). |

### Idioma

Altere o idioma da interface entre os 8 disponíveis. Poderá ser necessário reiniciar a aplicação para que a alteração seja totalmente aplicada.

---

## 11. Dicas e Boas Práticas

1. **Comece com o modo Rápido** se tiver muitas pastas. É muito mais rápido e pode encontrar a maioria dos duplicados.
2. **Use o modo Fiável para decisões finais** antes de eliminar — especialmente quando os nomes dos ficheiros não coincidem — para evitar falsos positivos.
3. **Escolha pastas específicas**, não o disco inteiro. Analisar apenas as pastas Downloads, Documentos e Ambiente de Trabalho reduz drasticamente o tempo e o ruído.
4. **Reveja as localizações** na coluna "Localização" antes de eliminar. Um duplicado pode estar numa pasta do sistema onde deve permanecer.
5. **Exporte um CSV** antes de limpar para manter um registo dos ficheiros eliminados.
6. **Configure filtros** quando procurar tipos de ficheiro específicos (ex.: apenas imagens `.jpg` e `.png`).
7. **Use o botão "Limpar"** para recomeçar com uma nova seleção de pastas sem sair da aplicação.

---

> **DuplicateFinder** — [mdc](https://github.com/migueldc-oss/DuplicateFinder)
>
> Documentação gerada a 1 de julho de 2026.
