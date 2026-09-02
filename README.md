# Zinnia Momentum MT100 / T505 — OpenTabletDriver 0.6.7
## 📥 Download

**[⬇️ Baixar Zinnia MT100 — OpenTabletDriver v1.0.0](https://github.com/ppedrinho10/otd-zinnia-mt100/releases/download/v1.0.0/ZINNIA-MT100-OpenTabletDriver-v1.0.0.zip)**

> Versão pronta e testada para Windows. Para utilizar pressão via Windows Ink, siga o guia em [`docs/INSTALL-PT-BR.md`](docs/INSTALL-PT-BR.md).

Suporte testado para a mesa digitalizadora **Zinnia Momentum MT100**, identificada pelo Windows como **SZ PING-IT INC. T505 Graphic Tablet** (`VID:PID 08F2:6811`), usando **OpenTabletDriver 0.6.7** no Windows.

> **Status:** detecção, movimento da caneta, clique da ponta e pressão estão funcionando na unidade testada. A pressão foi validada no **Krita** e no **Adobe Photoshop** usando **Windows Ink + VMulti**.

> Este é um projeto comunitário e não é afiliado à Zinnia, OpenTabletDriver, VoiDPlugins ou VMulti.

## Hardware testado

- **Produto:** Zinnia Momentum MT100
- **Identificação interna:** SZ PING-IT INC. T505 Graphic Tablet
- **USB VID:PID:** `08F2:6811`
- **Nome usado pelo perfil no OTD:** `10moon 1060N`
- **OpenTabletDriver:** `0.6.7`
- **Pressão configurada:** `8191`

> Outros tablets podem reutilizar o mesmo VID/PID. Portanto, esta correção é apresentada como suporte especificamente testado na **MT100/T505 usada neste projeto**, e não como garantia de compatibilidade com todo dispositivo `08F2:6811`.

## O problema

O perfil/configuração usado como ponto de partida permitiu que o OpenTabletDriver reconhecesse e recebesse relatórios da MT100, mas a leitura de pressão observada nesta unidade ocupava apenas uma pequena parte da faixa configurada pelo OTD.

Nos testes, a faixa útil medida ficou aproximadamente em `0–854`, enquanto o perfil trabalha com `0–8191`. Como consequência, aplicativos de desenho recebiam apenas uma fração da pressão disponível.

Também foi necessário corrigir o repouso da pressão para que a ponta voltasse corretamente a zero e o clique não permanecesse pressionado.

## Correção da pressão

A alteração em `src/TenMoonTabletReport.cs` usa os valores calibrados na unidade testada:

```csharp
var correctedPressure = 0x05DC - (prePressure - (buttonPressed ? 50 : 0));

const int deadZone = 20;
const int measuredMax = 854;
```

Depois da zona morta, a leitura é normalizada para `0–8191`:

```csharp
var scaledPressure =
    (long)(correctedPressure - deadZone) * 8191 /
    (measuredMax - deadZone);

Pressure = (uint)Math.Clamp(scaledPressure, 0, 8191);
```

Resultado observado:

- hover/sem tocar: `0`;
- clique da ponta: funcionando e soltando normalmente;
- pressão forte no Tablet Debugger: aproximadamente `8180/8191`;
- pressão variável funcionando no Krita;
- pressão funcionando no Adobe Photoshop.

## Arquivos deste repositório

- `config/1060N.json` — configuração local da MT100/T505.
- `src/TenMoonTabletReport.cs` — parser com a correção e normalização da pressão.
- `src/TenMoonReportParser.cs` — roteamento dos relatórios utilizado pelo parser 10moon.
- `docs/INSTALL-PT-BR.md` — instalação completa no Windows.
- `THIRD_PARTY_NOTICES.md` — créditos e avisos sobre componentes de terceiros.

## Instalação resumida

1. Use **OpenTabletDriver 0.6.7 x64 para Windows**.
2. A compilação do OTD precisa conter o parser corrigido deste repositório.
3. Coloque `1060N.json` em `userdata\Configurations\1060N.json` quando estiver usando a instalação portátil.
4. Instale o plugin **Windows Ink** compatível com OTD 0.6.7.
5. Instale o **VMulti** pelo projeto oficial.
6. **Reinicie o Windows depois de instalar o VMulti.**
7. No OTD, selecione **Windows Ink Absolute Mode** e aplique.
8. No Krita, selecione **Windows 8+ Pointer Input (Windows Ink)** e reinicie o Krita.

O passo a passo detalhado está em `docs/INSTALL-PT-BR.md`.

## Testando a pressão

### OpenTabletDriver

Abra:

`Tools → Tablet Debugger`

Sem tocar a mesa, `Pressure` deve voltar a `0`. Aumentando a força gradualmente, o valor deve subir em direção a `8191`.

### Krita

Abra:

`Configurações → Configurar o Krita → Configurações do tablet → Abrir testador de tablet`

A entrada deve apresentar valores de pressão variáveis (`S=`). Para testar no desenho, use um preset que tenha dinâmica de tamanho por pressão, como **Basic-5 Size**.

Se o testador mostrar pressão mas o pincel não responder logo após a instalação do VMulti, reinicie o Windows antes de alterar outras configurações.

## Compatibilidade confirmada neste teste

- Windows 11
- OpenTabletDriver 0.6.7
- Zinnia Momentum MT100 / T505 / `08F2:6811`
- Windows Ink
- VMulti
- Krita
- Adobe Photoshop

## Créditos

### Adaptação e validação

**Pedro Paulo Lima (`ppedrinho10`)**  
Testes de hardware, diagnóstico da MT100, calibração prática, validação do clique e da pressão e manutenção/publicação deste projeto.

### Assistência técnica

**OpenAI ChatGPT (GPT-5.6 Sol)**  
Assistência durante a investigação do protocolo, análise do parser, depuração, normalização da pressão, testes com Windows Ink/VMulti e preparação da documentação.

### Configuração/arquivo-base

Este trabalho partiu de uma configuração/arquivo 10moon/1060N encontrado durante a investigação. **O crédito nominal ao autor original será acrescentado assim que a autoria da fonte do blog for confirmada com segurança.** Não queremos atribuir esse material à pessoa errada.

### Projetos utilizados

- **OpenTabletDriver** — projeto e código-base do driver.
- **VoiDPlugins / Windows Ink** — suporte de saída Windows Ink utilizado nos testes.
- **VMulti** — dispositivo HID virtual necessário para o fluxo Windows Ink testado.

Os componentes de terceiros não são apresentados como autoria deste projeto. Consulte `THIRD_PARTY_NOTICES.md` e as respectivas licenças upstream.

## Histórico da investigação

Este repositório começou como uma investigação de suporte para a MT100/T505. Durante os testes, o dispositivo passou de detecção/movimento básicos para clique funcional e pressão normalizada até a faixa esperada pelo OTD.

O histórico de commits anterior foi mantido de propósito para documentar essa evolução.

## Aviso

A calibração foi obtida por testes práticos em uma unidade específica da **Zinnia Momentum MT100**. Faça backup de qualquer instalação funcional antes de testar alterações.

## Licenças e redistribuição

Este repositório contém material de compatibilidade e alterações destinadas ao OpenTabletDriver. Antes de redistribuir código ou binários derivados de projetos de terceiros, respeite as licenças correspondentes.

VMulti e os plugins Windows Ink devem ser obtidos de suas fontes oficiais; eles não devem ser atribuídos a este projeto.
