# Polycarater (Enamore)

Mod de Crusader Kings III que reúne interações de prisão e um sistema de casamento múltiplo, o **Enamore**. Feito para o jogo **1.20.1.1 (Crozier)**.

O mod foi refeito a partir de três mods de outros autores, que estavam misturados e desatualizados. Todos os arquivos e chaves passaram a usar o prefixo `pcr_`, os erros de script foram corrigidos e tudo foi ajustado à versão 1.20. A localização está em inglês, e os comentários do código, em português.

## Recursos

### Enamore

- **Traço Enamore** (`pcr_enamore`): permite ter até **10 esposas**, independentemente do que a fé ou a cultura permitem. Aparece no designer de personagem (custo 20).
- **Tradição Enamore Customs** (`tradition_pcr_enamore_customs`): só quem tem o traço pode ter várias esposas; os outros membros da cultura ficam com uma. Substitui as tradições Monogamous, Polygamous e Concubines.
- **Decisão Establish Enamore Customs**: o governante com o traço adota a tradição na própria cultura.
- **Decisão Embrace Enamore**: o jogador que vive numa cultura com a tradição recebe o traço por **500 de piedade**.
- As concubinas seguem as regras vanilla e as da fé.

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
- **Love Marriage Family**: se a regra de gravidez realista estiver ligada, ela cancela gravidezes em que mãe e pai não estão no mesmo lugar. O evento marca a prisioneira com o flag `allow_event_pregnancy`, que é a exceção que o próprio Love Marriage usa para gravidez criada por evento. Sem o Love Marriage, esse flag não faz nada.

## Estrutura

| Arquivo | Conteúdo |
|---|---|
| `common/character_interactions/pcr_prison_interactions.txt` | As duas interações de prisão |
| `common/scripted_effects/pcr_marriage_effects.txt` | Efeito do casamento forçado |
| `common/scripted_triggers/pcr_marriage_triggers.txt` | Gatilho de quem pode ser casado à força |
| `common/scripted_triggers/zz_pcr_marriage_overrides.txt` | Sobrescrita do `can_marry_trigger` (limite do Enamore) |
| `common/opinion_modifiers/pcr_opinions.txt` | Opiniões do casamento forçado e da gravidez forçada |
| `common/traits/pcr_traits.txt` | Traço Enamore |
| `common/culture/traditions/pcr_traditions.txt` | Tradição Enamore Customs |
| `common/decisions/pcr_decisions.txt` | Decisões Establish Enamore Customs e Embrace Enamore |
| `common/on_action/pcr_on_actions.txt` | Ligação do aviso de nascimento ao `on_birth_child` |
| `events/pcr_impregnate_events.txt` | Evento da gravidez forçada e aviso de nascimento |
| `localization/english/pcr_l_english.yml` | Localização |

## Validação

- Validado com o [ck3-tiger](https://github.com/amtep/tiger) para 1.20, sem nenhum erro ou aviso.
- Testado em jogo na 1.20.1.1 em 16/10/2026, sem nenhum erro do mod no `error.log`.

## Créditos

Baseado em três mods de outros autores:

- **Forcefully Marry Prisoner**: casamento forçado de prisioneiro.
- **Impregnate**: interação de gravidez forçada.
- **MWT Unbound Unions**: traço, tradição e decisão que deram origem ao Enamore.
