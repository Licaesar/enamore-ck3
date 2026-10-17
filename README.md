# Polycarater (Enamore)

Mod de Crusader Kings III que reúne interações de prisão, uma interação de família e um sistema de casamento múltiplo, o **Enamore**. Feito para o jogo **1.20.1.1 (Crozier)**.

O mod foi refeito a partir de três mods de outros autores, que estavam misturados e desatualizados. Todos os arquivos e chaves passaram a usar o prefixo `pcr_`, os erros de script foram corrigidos e tudo foi ajustado à versão 1.20. A localização está em inglês, e os comentários do código, em português.

## Recursos

### Enamore

- **Traço Enamore** (`pcr_enamore`): permite ter até **10 esposas**, independentemente do que a fé ou a cultura permitem. Aparece no designer de personagem (custo 20).
- **Tradição Enamore Customs** (`tradition_pcr_enamore_customs`): só quem tem o traço pode ter várias esposas; os outros membros da cultura ficam com uma. Substitui as tradições Monogamous, Polygamous e Concubines.
- **Decisão Establish Enamore Customs**: o governante com o traço adota a tradição na própria cultura.
- **Decisão Embrace Enamore**: o jogador que vive numa cultura com a tradição recebe o traço por **500 de piedade**.
- As concubinas seguem as regras vanilla e as da fé.
- **Ficha de personagem**: a linha de esposas secundárias se comporta como a de concubinas. Até 2, retratos lado a lado; a partir de 3, retratos sobrepostos; a partir de 4, um contador "+N" e o cabeçalho abre a lista completa.

### Interação pessoal

- **Join Concubine Parent's House** (`pcr_concubine_parent_house_interaction`): só para o jogador. No vanilla, o filho de concubina nasce na casa de quem tem a concubina; esta interação passa o filho para a casa (e a dinastia) da concubina ou do concubino.
  - Aparece para um filho do jogador que ainda está na casa dele e cujo outro genitor é ou foi concubina ou concubino do jogador, mesmo que já tenha morrido.
  - Bloqueada se esse genitor for plebeu ou já for da mesma casa.
  - Custa **10 de renome** da dinastia do jogador, que não precisa ser o chefe da dinastia.
  - Só o filho muda de casa; os descendentes dele ficam onde estão.

### Interações de prisão

- **Forcefully Marry Prisoner** (`pcr_force_marriage_interaction`): casa o prisioneiro com o captor, com um cortesão ou com um filho do captor. Desfaz o casamento anterior do prisioneiro, e o ex-cônjuge passa a ter rancor do captor.
- **Impregnate Captive** (`pcr_impregnate_interaction`): só para o jogador.
  - A prisioneira sempre engravida.
  - A opinião dela sobre o captor muda para -100 (80% de chance) ou +100 (20%).
  - Cooldown de 30 dias para a mesma prisioneira.
  - Se ela for solteira, o jogador recebe um aviso quando a criança nasce.

## Instalação

1. Copie a pasta para `Documents\Paradox Interactive\Crusader Kings III\mod\polycarater`.
2. Crie `mod\polycarater.mod` com o conteúdo do `descriptor.mod` mais a linha `path="<caminho completo da pasta>"`.
3. Ative o mod no launcher, de preferência perto do fim da ordem de carga.

## Compatibilidade

- O mod sobrescreve um único gatilho vanilla, o `can_marry_trigger`, em `common/scripted_triggers/zz_pcr_marriage_overrides.txt`. Mods que também o sobrescrevem entram em conflito; vence o que carregar por último.
- O aviso de nascimento é anexado ao `on_birth_child` por um on_action próprio. Os eventos vanilla desse on_action continuam funcionando.
- O mod sobrescreve o arquivo inteiro `gui/window_character.gui` (base: vanilla 1.20.1.1) para a linha de esposas. Mods que também sobrescrevem esse arquivo, como o **Ethnicities and Portraits Expanded**, entram em conflito: vence o que carregar por último, e as mudanças do outro somem da ficha de personagem. Para usar os dois, é preciso um patch que junte as duas versões e carregue depois de ambos.
- **Love Marriage Family**: se a regra de gravidez realista estiver ligada, ela cancela gravidezes em que mãe e pai não estão no mesmo lugar. O evento marca a prisioneira com o flag `allow_event_pregnancy`, que é a exceção que o próprio Love Marriage usa para gravidez criada por evento. Sem o Love Marriage, esse flag não faz nada.

## Estrutura

| Arquivo | Conteúdo |
|---|---|
| `common/character_interactions/pcr_prison_interactions.txt` | As duas interações de prisão |
| `common/character_interactions/pcr_personal_interactions.txt` | Interação Join Concubine Parent's House |
| `common/scripted_effects/pcr_marriage_effects.txt` | Efeito do casamento forçado |
| `common/scripted_triggers/pcr_marriage_triggers.txt` | Gatilhos de quem pode ser casado à força e de concubina atual ou antiga |
| `common/scripted_triggers/zz_pcr_marriage_overrides.txt` | Sobrescrita do `can_marry_trigger` (limite do Enamore) |
| `common/opinion_modifiers/pcr_opinions.txt` | Opiniões do casamento forçado e da gravidez forçada |
| `common/traits/pcr_traits.txt` | Traço Enamore |
| `common/culture/traditions/pcr_traditions.txt` | Tradição Enamore Customs |
| `common/decisions/pcr_decisions.txt` | Decisões Establish Enamore Customs e Embrace Enamore |
| `common/on_action/pcr_on_actions.txt` | Ligação do aviso de nascimento ao `on_birth_child` |
| `events/pcr_impregnate_events.txt` | Evento da gravidez forçada e aviso de nascimento |
| `gui/window_character.gui` | Ficha de personagem com a linha de esposas no estilo das concubinas |
| `localization/english/pcr_l_english.yml` | Localização |

## Validação

- Validado com o [ck3-tiger](https://github.com/amtep/tiger) para 1.20. O único aviso são 2 erros de `datafunctions` em linhas vanilla do `window_character.gui`, que são falsos positivos: o Tiger ainda não conhece essas funções da 1.20.
- Testado em jogo na 1.20.1.1 em 16/10/2026, sem nenhum erro do mod no `error.log`. A interação pessoal e a ficha de personagem foram testadas no mesmo dia, com 2, 3, 4 e 10 esposas.

## Créditos

Baseado em três mods de outros autores:

- **Forcefully Marry Prisoner**: casamento forçado de prisioneiro.
- **Impregnate**: interação de gravidez forçada.
- **MWT Unbound Unions**: traço, tradição e decisão que deram origem ao Enamore.
