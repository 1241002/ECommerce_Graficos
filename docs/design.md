# Regras de design da interface

Aplicam-se a todo o UI do dashboard (páginas, gráficos, filtros, tooltips, drill-down/through).
Para rever um ecrã contra "aspeto de IA" usar a skill `/unslop` (plugin `unslop@heydamir`).

## 1. Movimento (12 princípios da animação aplicados a UI)
- **Squash & stretch**: as coisas achatam no impacto e esticam em movimento, o que lhes dá peso.
- **Antecipação**: um pequeno recuo antes do movimento grande, para se ver o que vem aí.
- **Staging**: dirigir o olhar para uma coisa de cada vez.
- **Pose a pose**: definir os estados-chave e deixar o browser interpolar o resto.
- **Follow through**: partes continuam a mexer depois de o corpo principal parar, e depois assentam.
- **Slow in & slow out**: acelerar e desacelerar; nunca velocidade constante (nada de `linear`).
- **Arcos**: mover em curvas, não em linhas retas.
- **Ação secundária**: um pequeno detalhe que reforça a ação principal.
- **Timing rápido**: a duração dá o tom; animações de UI **abaixo de 300 ms**.
- **Feedback exagerado**: ir além do real para o momento se notar.
- **Desenho sólido / 3D**: dar profundidade e volume a coisas planas.
- **Apelo geral**: a soma de todos os detalhes, feitos com cuidado.
- **Frequência de uso**: quanto mais algo se usa, menos deve animar (filtros e tooltips: quase nada).

## 2. Leis de UX
- **Fitts**: alvos maiores e mais próximos são mais rápidos de acertar.
- **Áreas de clique maiores**: a área clicável pode ser maior do que o que se vê.
- **Hick**: mais opções = decisões mais lentas (poucos filtros visíveis, o resto recolhido).
- **Miller**: ~7 coisas na cabeça de cada vez → agrupar informação (KPIs em blocos).
- **Doherty**: responder em **< 400 ms** ou parece lento (API e filtros têm de cumprir; mostrar estado de carregamento).
- **Postel**: aceitar input desarrumado, devolver output limpo (ex.: datas e pesquisas tolerantes).
- **Jakob**: as pessoas esperam que funcione como as apps que já usam (padrões de dashboard conhecidos).

## 3. Tipografia
| Estilo | Fontes |
|---|---|
| Suíço limpo | ABC Diatype, TWK Lausanne, Switzer, Saans, Areal, Strichpunkt Sans |
| Amigável | Studio Feixen Sans, PP Mori, Aeonik, Degular, GT Walsheim, Circular |
| Com personalidade | Apfel Grotezk, Aktiv Grotesk, ABC Favorit, Familjen Grotesk, ABC Monument Grotesk, ABC Oracle |
| Técnico (mono) | ABC Diatype Mono, Söhne Mono, GT America Mono, IBM Plex Mono, Commit Mono, Departure Mono |

**Proibidas (aspeto de IA):** Geist, Space Grotesk, Bricolage Grotesque, Instrument Sans, JetBrains Mono, Space Mono.

Nota de licença: muitas destas são pagas. Gratuitas: Switzer (Fontshare), Familjen Grotesk (Google Fonts),
IBM Plex Mono, Commit Mono, Departure Mono. A escolha final fica registada num ADR.

## 4. Regras de CSS em todos os componentes
- **Cantos arredondados encaixados**: raio interior = raio exterior − padding.
- **Bordas** com cor alfa, ex. `rgb(0 0 0 / 0.12)`, não hex sólido, para se misturarem com qualquer fundo.
- **Paletas em OKLCH**, não HSL, para luminosidade igual parecer igual (vale também para as séries dos gráficos).
- **Gradientes** com `in oklch`, ex. `linear-gradient(90deg in oklch, blue, orange)`, para não ficarem cinzentos a meio
  (escalas sequenciais/divergentes de heatmaps e mapas).
- **Ícones**: espessura do traço igual ao peso do texto ao lado.
- **Carrosséis**: esbater as pontas com `mask: linear-gradient(90deg, transparent, black 15% 85%, transparent)`.
- **Troca de ícones**: desfocar o ícone que sai enquanto desaparece (`filter: blur(4px)`).
- **Modo escuro**: mostrar profundidade com superfícies mais claras, porque as sombras quase não se veem.
- **Secções de altura total**: `100dvh`, nunca `100vh` (parte no Safari).
- **Fotos de produto em fundo branco**: `mix-blend-mode: multiply`, para o branco desaparecer.
