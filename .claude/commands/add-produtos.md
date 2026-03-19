Adiciona novas entradas de "Produtos da Semana" no arquivo raw do ano correspondente.

O usuário vai fornecer o número do episódio e uma lista de entradas no formato:
```
Nome: Produto
```

Ou pode colar uma lista mais solta que você vai interpretar. Cada linha representa um par ouvinte → produto.

## Passos

1. Leia os argumentos: `$ARGUMENTS`

2. Identifique o número do episódio. Se não for informado explicitamente, leia o arquivo raw do ano atual para descobrir qual é o episódio mais recente e pergunte ao usuário se é o próximo.

3. Determine o ano do episódio (baseado no número ou informado pelo usuário) e encontre o arquivo correto:
   - 2024 → `2024/lista_2024_raw.md`
   - 2025 → `2025/lista_2025_raw.md`
   - 2026 → `2026/lista_2026_raw.md`

4. Leia o arquivo raw para entender a formatação atual das colunas (largura dos campos).

5. Parse cada linha da lista fornecida no formato `Nome: Produto` (ou variações razoáveis como `Nome - Produto`). Ignore linhas em branco. **Cada produto vira uma linha separada na tabela — se um ouvinte mencionou múltiplos produtos, cada um fica na sua própria linha com o nome repetido.** Por exemplo:
   ```
   | 109 | Arthur | Notion    |
   | 109 | Arthur | Obsidian  |
   ```

6. Formate cada entrada como uma linha da tabela markdown, seguindo o padrão de alinhamento do arquivo (padding com espaços). Use o mesmo estilo visual das outras linhas.

7. **Verificação de nomes similares:** Para cada ouvinte na lista fornecida, extraia todos os nomes únicos que já existem no arquivo raw (e nos demais arquivos raw de outros anos, se útil) e compare com o nome fornecido. Use critérios como:
   - Diferença de acentuação (ex: "Aiquis" vs "Aíquis")
   - Capitalização diferente (ex: "arthur" vs "Arthur")
   - Nomes parciais ou abreviados (ex: "Alexandre" vs "Alexandre Pereira")
   - Erros de digitação comuns (letras trocadas, faltando ou sobrando)

   Se encontrar um nome parecido mas não idêntico, apresente ao usuário:
   ```
   ⚠️  "Alexand Pereira" não foi encontrado. Nome similar existente: "Alexandre Pereira"
   Usar "Alexandre Pereira"? (s/n ou outro nome)
   ```

   Aguarde a resposta do usuário antes de continuar para o próximo nome com dúvida. Nomes claramente novos (sem similar) podem ser aceitos diretamente.

8. Mostre ao usuário um preview das linhas finais que serão inseridas (com os nomes já corrigidos), e peça confirmação antes de escrever.

9. Após confirmação, insira as novas linhas **logo abaixo da linha separadora do cabeçalho** (linha 2), antes das entradas existentes — ou seja, as entradas do novo episódio ficam no topo da lista.

10. Não faça commit automaticamente. Apenas atualize o arquivo.

## Notas

- Respeite acentuação e caracteres especiais nos nomes (ex: Aíquis, não "Aiquis").
- Se o usuário colar os dados sem formato claro, tente inferir quem é o ouvinte e qual é o produto, e confirme com ele antes de gravar.
- Não altere as linhas existentes no arquivo.
