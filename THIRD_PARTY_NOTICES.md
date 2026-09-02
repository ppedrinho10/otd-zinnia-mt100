# Third-Party Notices and Credits

Este projeto documenta e adapta suporte para a **Zinnia Momentum MT100 / T505 (VID:PID 08F2:6811)** no OpenTabletDriver 0.6.7.

Nenhum componente de terceiros listado abaixo deve ser interpretado como autoria de Pedro Paulo Lima ou da OpenAI.

## Trabalho deste projeto

### Pedro Paulo Lima (`ppedrinho10`)

Responsável pelos testes no hardware Zinnia Momentum MT100, investigação prática, calibração, validação do clique e da pressão, testes no Krita e Adobe Photoshop e publicação/manutenção deste repositório.

### OpenAI ChatGPT (GPT-5.6 Sol)

Assistência técnica durante a investigação, análise e depuração do parser, normalização da pressão, testes do fluxo Windows Ink/VMulti e preparação da documentação.

## OpenTabletDriver

**OpenTabletDriver** é o projeto upstream no qual esta adaptação se baseia.

- Projeto: OpenTabletDriver
- Repositório: https://github.com/OpenTabletDriver/OpenTabletDriver
- Versão utilizada/testada neste projeto: 0.6.7
- Licença: LGPL-3.0

O código, os binários e a marca OpenTabletDriver pertencem aos seus respectivos autores/contribuidores e permanecem sujeitos à licença do projeto upstream.

## VoiDPlugins / Windows Ink

O suporte Windows Ink utilizado nos testes é fornecido pelo projeto **VoiDPlugins**.

- Repositório: https://github.com/X9VoiD/VoiDPlugins
- Licença: GPL-3.0

Este repositório não reivindica autoria do plugin Windows Ink. Obtenha-o pela fonte upstream e respeite sua respectiva licença.

## VMulti

**VMulti** fornece o dispositivo HID virtual necessário ao fluxo Windows Ink usado nos testes.

- Distribuição utilizada/recomendada: https://github.com/X9VoiD/vmulti-bin

VMulti deve ser obtido de sua fonte upstream e permanece sujeito às licenças e créditos dos respectivos autores.

Este repositório não reivindica autoria do VMulti.

## Configuração 10moon / 1060N usada como referência

A investigação da MT100 partiu de material/configuração relacionado à família **10moon/10moons 1060N** e ao hardware `08F2:6811`.

O arquivo histórico:

`configurations/1060N-reference.json`

é mantido separadamente da configuração final:

`configurations/1060N.json`

para preservar a origem da investigação e deixar claro que a configuração de referência não é apresentada como criação original deste projeto.

### Crédito do blog/fonte original

Durante a investigação foi consultado material publicado no blog **Linux Universe**, no artigo **“Mesa Digitalizadora”**, que documenta tablets `08F2:6811` e o uso do `DIGImend/10moons-tools`:

https://linuxuniverse.com.br/linux/digitalizadora

Até o fechamento deste arquivo, foi possível confirmar o artigo e o material técnico nele descrito, mas **não foi possível confirmar com segurança o nome pessoal do autor do artigo/arquivo que serviu de referência**.

Por esse motivo, o crédito é dado ao **Linux Universe e à fonte original**, sem inventar ou atribuir um nome pessoal não verificado. Assim que a autoria nominal puder ser comprovada, este aviso deverá ser atualizado.

## DIGImend / 10moons-tools

O artigo acima referencia o projeto **DIGImend/10moons-tools**, trabalho anterior relacionado à habilitação/configuração de tablets 10moons/Gotop.

- Repositório: https://github.com/DIGImend/10moons-tools

O projeto DIGImend e seus contribuidores mantêm seus próprios direitos, créditos e licenças.

## Investigação pública da MT100 / T505

Existe também uma solicitação pública de suporte no OpenTabletDriver para a **Zinnia Momentum MT100 / SZ PING-IT INC. T505 / 08F2:6811**, aberta pelo usuário GitHub **zondonaidejr**:

https://github.com/OpenTabletDriver/OpenTabletDriver/issues/4301

Esse crédito é pela investigação pública e pelos dados de dispositivo publicados nessa issue. Ele **não significa** que `zondonaidejr` seja o autor do artigo do Linux Universe ou do arquivo-base; não encontramos evidência suficiente para fazer essa atribuição.

## Redistribuição

Antes de redistribuir binários ou código derivados de OpenTabletDriver, VoiDPlugins, VMulti, DIGImend ou qualquer outro projeto, consulte e cumpra a licença correspondente.

A preferência deste repositório é:

- manter as modificações e documentação próprias claramente identificadas;
- creditar os projetos upstream;
- apontar usuários para as fontes oficiais de componentes de terceiros;
- não reivindicar autoria de código, drivers, plugins ou configurações criados por terceiros.
