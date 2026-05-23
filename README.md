# Campo Wi-Fi — Ferramenta de Campo

Ferramenta interativa de diagnóstico e planejamento de redes Wi-Fi desenvolvida como material complementar ao livro **Diagnóstico e Planejamento de Redes Wi-Fi**, de Rodrigo Ronner Tertulino da Silva (IFRN Campus Mossoró).

---

## Como usar

O arquivo `campo-wifi.html` é uma aplicação web completa e autossuficiente. Não requer instalação, servidor local ou conexão com a internet para funcionar (apenas para carregar as fontes tipográficas no primeiro acesso). Basta abrir o arquivo em qualquer navegador moderno.

```
Abrir campo-wifi.html diretamente no navegador
```

A interface é organizada em **nove abas**, acessíveis pelo menu superior, com rolagem horizontal.

---

## Abas e funcionalidades

### ⊞ Calculadoras

Doze calculadoras com valores padrão, prontas para uso em campo. Todas exibem o resultado em tempo real à medida que os valores são alterados. Cada card possui um badge **Exemplo do Livro** com o cenário exato mencionado na seção correspondente.

| # | Calculadora | Fórmula | Referência no livro |
|---|---|---|---|
| 1 | Conversão de Potência (dBm ↔ mW) | P_dBm = 10 · log₁₀(P_mW) | Cap. 4, Seção 4.1 |
| 2 | EIRP com verificação Anatel | EIRP = P_TX + G_TX − L_cabo | Cap. 4, Seção 4.1 |
| 3 | Comprimento de onda (λ) | λ = 30 / f_GHz cm | Cap. 1, Seção 1.1 |
| 4 | Perda em espaço livre (Friis) | L_FS = 32,45 + 20·log(d) + 20·log(f) | Cap. 4, Seção 4.2 |
| 5 | Perda Log-Distance | L = L₀ + 10·n·log(d) | Cap. 4, Seção 4.3 |
| 6 | One-Slope com obstáculos | L = L₀ + 10·n·log(d) + ΣL_obst | Cap. 4, Seção 4.3 |
| 7 | Orçamento de enlace (RSSI) | RSSI = P_TX + G_TX + G_RX − L | Cap. 4, Seção 4.0.1 / 4.4 |
| 8 | SNR e MCS estimados | SNR = RSSI − Noise Floor | Cap. 4, Seção 4.4 / 4.5 |
| 9 | Raio de cobertura máximo | d = 10^((L_max − L₀) / 10n) | Cap. 4, Seção 4.6 |
| 10 | Dimensionamento de APs | N = max(N_cob, N_cap) | Cap. 5 / 6 |
| 11 | Perda em cabo coaxial | L_cabo = (dB/100m) × comprimento | Cap. 11, Seção 11.3 |
| 12 | Orçamento PoE | P_total = Σ(N_i × P_i) | Cap. 11, Seção 11.2 |

**Destaques dos cards:**

O card **Orçamento de Enlace (Card 7)** exibe a fórmula passo a passo em tempo real — `RSSI = P_TX + G_TX + G_RX − L_path` — com os valores atuais substituídos e o resultado colorido conforme a qualidade. Quatro barras de sinal Wi-Fi animadas refletem visualmente o RSSI calculado. Referência à Seção 4.0.1 do livro "Componentes do Orçamento".

O card **Raio de Cobertura (Card 9)** inclui uma animação de radar com três anéis concêntricos cuja velocidade de expansão é proporcional ao raio calculado, além do expoente de perda n como variável ajustável.

O card **One-Slope (Card 6)** suporta quatro tipos de obstáculo: drywall/gesso (+3 dB), alvenaria (+8 dB), laje de concreto (+20 dB) e porta de madeira (+4 dB). O card **SNR (Card 8)** exibe o MCS máximo sustentável e o throughput teórico em um canal de 20 MHz, com base na tabela do livro.

---

### ⊟ Referências

Tabelas de consulta rápida baseadas nos capítulos do livro, sem necessidade de abrir o PDF.

- **Qualidade de RSSI** — cinco faixas (de Excelente a Muito Fraca), com aplicações suportadas e MCS típico. Cap. 4, Seção 4.4.
- **SNR × MCS** — MCS 0 a 11, com modulação, codificação, SNR mínimo e throughput em 20 MHz. Cap. 4, Seção 4.5 / Cap. 9.
- **Expoente de perda por ambiente** — oito cenários, do corredor aberto ao galpão industrial. Cap. 4, Seção 4.3.
- **Atenuação por material** — doze materiais com faixas de atenuação em dB. Cap. 1, Seção 1.3.
- **Reason Codes 802.11** — doze códigos mais comuns, com causa provável e ação recomendada. Cap. 8, Seção 8.2.
- **Classes PoE** — 802.3af, 802.3at e 802.3bt com potência máxima. Cap. 11, Seção 11.2.

---

### ◈ Canais

Visualizador gráfico do plano de canais para as três faixas.

**2,4 GHz** — grid com os 13 canais disponíveis no Brasil. Os canais não sobreponíveis (1, 6 e 11) são destacados em laranja. Cap. 9, Seção 9.3.

**5 GHz** — canais organizados em sub-bandas (UNII-1, UNII-2A, UNII-2C e UNII-3), com indicação visual de quais exigem DFS. Cap. 9, Seção 9.3.

**6 GHz** — painel informativo sobre os 59 canais de 20 MHz aprovados pela Anatel (Resolução 754/2021), com recomendações de largura de canal para Wi‑Fi 6E e Wi‑Fi 7. Cap. 10, Seção 10.2.

O **Recomendador de Canal** cruza três variáveis — faixa, proximidade a radar e densidade de redes vizinhas — e sugere canal e largura de canal com justificativa técnica.

---

### ⊕ Diagnóstico

Ferramentas para uso direto em campo durante o diagnóstico de problemas.

**Lookup de Reason Code** — digita o código numérico do frame de deauthentication e recebe a causa provável e a ação recomendada imediatamente. Baseado na Seção 8.2 do livro.

**Gerador de Filtros Wireshark** — seleciona o sintoma em um menu e retorna o filtro de exibição correto, com explicação do que observar na captura e, quando aplicável, um filtro complementar. Inclui um campo para inserir o endereço MAC ou o reason code. Botão de copiar em todos os filtros. Baseado no Cap. 7, Seção 7.2/7.3.

| Sintoma | Filtro principal |
|---|---|
| Falha de autenticação WPA | `eapol` |
| Desconexões frequentes | `wlan.fc.type_subtype == 0x0c` |
| Alta taxa de retransmissão | `wlan.fc.retry == 1` |
| Sinal fraco | `radiotap.dbm_antsignal < -75` |
| Ver beacons do AP | `wlan.fc.type_subtype == 0x08` |
| Probe requests do cliente | `wlan.fc.type_subtype == 0x04` |
| Filtrar por AP (BSSID) | `wlan.bssid == AA:BB:CC:DD:EE:FF` |
| Filtrar por dispositivo (MAC) | `wlan.addr == AA:BB:CC:DD:EE:FF` |
| Reason code específico | `wlan.fixed.reason_code == X` |
| Handshake WPA completo | `eapol` |

**Gerador de Comandos iPerf3** — configura o IP do servidor, o cenário (TCP, UDP, bidirecional ou rápido de campo), a duração, o número de threads e o intervalo de relatórios. Exibe os comandos completos para o servidor e o cliente, com botão de copiar. Baseado no Cap. 7, Seção 7.2.

**Seletor Sintoma → Ferramenta** — seleciona a queixa do usuário e retorna a ferramenta recomendada, a referência ao capítulo e o procedimento passo a passo. Cobre nove cenários do Cap. 8.

---

### ⊗ Ferramentas

Diretório completo das 35 ferramentas mencionadas nos capítulos do livro, com link direto para download ou site oficial, badges de plataforma e custo, e referência à seção correspondente. Organizadas em 9 categorias:

| Categoria | Exemplos | Capítulos |
|---|---|---|
| Captura e Análise de Tráfego | Wireshark, Aircrack-ng, Kismet | Cap. 7 |
| Teste de Desempenho | iPerf3 (Linux/macOS/Windows), Magic iPerf (iOS) | Cap. 7 |
| Análise de Canais e Espectro | WiFi Analyzer, inSSIDer, WiFi Explorer, Acrylic, Linssid, horst | Cap. 7, 9 |
| Survey e Mapeamento | NetSpot, Ekahau Pro, CommScope TAMOS | Cap. 5, 7 |
| Diagnóstico Mobile | HE.NET Network Tools, Network Analyzer Pro | Cap. 7 |
| Utilitários do Sistema Operacional | netsh, iw, wdutil, Wireless Diagnostics | Cap. 7 |
| Monitoramento de Redes | LibreNMS, Zabbix, PRTG, Grafana | Cap. 12 |
| Documentação e Base de Conhecimento | Nautobot, NetBox, Notion, Confluence, Outline, MediaWiki | Cap. 12 |
| Armazenamento e Colaboração | Google Sheets, OneDrive, Dropbox | Cap. 12 |

Cada card exibe: link ↗ para o site oficial, badges de plataforma coloridos (Win / Linux / macOS / Android / iOS / Web), badge de custo (Open Source / Gratuito / Freemium / Pago) e referência ao capítulo. As URLs foram extraídas diretamente das notas de rodapé dos capítulos.

---

### ⊕ Site Survey

Planta baixa interativa de um apartamento típico com seis cômodos. Permite posicionar o AP clicando em qualquer ponto do mapa e visualizar, em tempo real, o RSSI estimado de cada cômodo.

**Modelo de propagação:** Log-Distance (n configurável) com penalidades de parede calculadas por ray casting. Paredes de alvenaria (−8 dB, tracejado em vermelho) e de drywall (−3 dB, tracejado em azul) são exibidas no mapa. Ondas de propagação animadas partem do ponto onde o AP foi posicionado.

**Cômodos do modelo:** Sala de Estar, Quarto 1, Cozinha, Corredor, Banheiro e Quarto 2.

**Parâmetros ajustáveis:** EIRP, Noise Floor, expoente n e faixa (2,4 GHz com L₀ = 40 dB ou 5 GHz com L₀ = 46 dB).

Referência: Cap. 5, Seção 5.3 / Cap. 6 (Planejamento por Tipologia).

---

### ◎ Posição do AP

Demonstração animada do padrão de irradiação de um AP em corte lateral de um cômodo de **15 m² (5 m × 3 m)** com mobília proporcional (sofá de 1,8 m, mesa de centro e estante de 2 m). Cinco cenários selecionáveis:

| Cenário | Altura do AP | Cobertura útil | Classificação |
|---|---|---|---|
| No Teto | 3,0 m (teto) | 95% | ⭐⭐⭐⭐⭐ |
| Parede Alta | 2,5 m | 80% | ⭐⭐⭐⭐ |
| Parede Baixa | 1,2 m | 55% | ⭐⭐⭐ |
| Em Móvel | 0,8 m | 38% | ⭐⭐ |
| No Canto | Nível do piso | 18% | ⭐ |

As ondas de propagação são elipses animadas com clipping exato nos limites das paredes — a energia que atingiria a parede é cortada pela Canvas API, o que representa visualmente a absorção pela alvenaria. As zonas são coloridas por qualidade: verde (Excelente), amarelo (Boa), laranja (Regular), vermelho (Fraca). Para cada cenário são exibidos: cobertura útil, uniformidade, zonas mortas, classificação em estrelas e dica técnica.

Referência: Cap. 6, Seção 6.1 / Cap. 11, Seção 11.1.

---

### ☑ Checklists

Três listas interativas com progresso persistente. O estado de cada item é salvo automaticamente no navegador (localStorage) e mantido entre sessões. Cada checklist tem uma barra de progresso e um botão de reset individual.

**Site Survey** (26 itens, 6 grupos) — Levantamento de requisitos, inspeção visual, survey passivo, survey preditivo, survey ativo e relatório. Cap. 5, Seção 5.3.

**Testes Pós-Instalação** (18 itens, 4 grupos) — Posicionamento físico, PoE e alimentação, configuração inicial e testes de aceite. Cap. 11, Seção 11.4.

**Auditoria Periódica** (22 itens, 5 grupos) — Desempenho, ambiente RF, equipamentos, segurança e documentação. Cap. 12, Seção 12.3.

---

### ⊞ Anotações de Campo

Registro estruturado de medições durante o trabalho de campo. Os dados são salvos no navegador (localStorage) e persistem entre sessões.

Campos disponíveis: local ou ponto de medição, RSSI (dBm), SNR (dB), canal e faixa, e observação livre. Cada entrada recebe automaticamente um carimbo de hora e uma classificação de qualidade com base na tabela de RSSI do livro. As anotações são exibidas em uma tabela, com exclusão individual. O botão **Exportar .txt** gera um arquivo de texto estruturado com todas as medições, pronto para inclusão no relatório de campo.

---

## Precisão dos cálculos

Todos os valores numéricos foram verificados contra os exemplos do livro:

- **One-Slope (sobrado):** L₀=46, n=3,5, d=7 m, laje + alvenaria + porta → 107,6 dB ✓ (Seção 4.3)
- **Raio de cobertura (escritório):** EIRP=27, G_RX=1, RSSI=−65, L₀=46, n=3,2 → 29,5 m ✓ (Seção 4.6)
- **Friis:** 5 GHz, 10 m → 66,43 dB ✓ (Seção 4.2)
- **Comprimento de onda:** 2,4 GHz → 12,50 cm · 5 GHz → 6,00 cm · 6 GHz → 5,00 cm ✓
- **Orçamento de enlace:** P_TX=20, G_TX=4, G_RX=0, L=84 dB → RSSI=−60 dBm ✓ (Seção 4.0.1)

---

## Compatibilidade

Testado nos navegadores modernos baseados em Chromium (Chrome, Edge, Brave) e em Firefox. As abas Site Survey e Posição do AP utilizam a Canvas API do HTML5, disponível em todos os navegadores modernos. Funciona em dispositivos móveis — interface adaptada a telas estreitas, com rolagem horizontal nas tabelas. Para uso em campo, recomenda-se salvar o arquivo no dispositivo para acesso offline.

As abas com canvas (Site Survey e Posição do AP) são inicializadas sob demanda, apenas quando acessadas pela primeira vez, para não impactar o desempenho das demais funcionalidades.

---

## Estrutura do arquivo

```
campo-wifi.html      Aplicação completa em arquivo único (~180 KB)
README.md            Este arquivo
```

Não há dependências locais. As fontes Syne e JetBrains Mono são carregadas do Google Fonts no primeiro acesso e armazenadas em cache pelo navegador para uso posterior sem conexão com a internet. A capa do livro está embutida no HTML como imagem em base64, eliminando qualquer dependência de arquivo externo.

---

## Referência bibliográfica

SILVA, Rodrigo Ronner Tertulino da. **Diagnóstico e Planejamento de Redes Wi-Fi**. Mossoró: IFRN, 2026.

---

## Licença

Material didático de uso livre para fins educacionais, vinculado ao livro de referência acima.
