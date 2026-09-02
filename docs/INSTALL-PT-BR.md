# Instalação — Zinnia Momentum MT100 / T505 no Windows

Este guia descreve a configuração que foi testada com:

- **Zinnia Momentum MT100**
- identificação interna **SZ PING-IT INC. T505 Graphic Tablet**
- USB **VID:PID `08F2:6811`**
- **OpenTabletDriver 0.6.7**
- Windows 11
- Windows Ink + VMulti

## 1. Antes de começar

Se você já possui uma instalação funcional, faça um backup antes de substituir arquivos.

Feche o driver oficial da Zinnia e outros drivers de mesa que possam disputar o dispositivo com o OpenTabletDriver.

> Este projeto foi validado em uma unidade específica da MT100/T505. Outros dispositivos podem compartilhar o mesmo VID/PID.

## 2. OpenTabletDriver

Use **OpenTabletDriver 0.6.7 para Windows x64**.

A versão utilizada neste projeto contém a correção do parser 10moon descrita no repositório. Apenas adicionar o JSON a uma compilação oficial sem essa alteração de parser não reproduz necessariamente a correção de pressão.

Na versão portátil, a estrutura esperada é semelhante a:

```text
OpenTabletDriver/
├── OpenTabletDriver.Console.exe
├── OpenTabletDriver.Daemon.exe
├── OpenTabletDriver.UX.Wpf.exe
└── userdata/
```

A presença da pasta `userdata` ao lado dos executáveis mantém os dados do OTD nessa instalação portátil.

## 3. Instalar a configuração da MT100

Copie:

```text
configurations/1060N.json
```

para:

```text
userdata/Configurations/1060N.json
```

Abra `OpenTabletDriver.UX.Wpf.exe`.

Na unidade testada, o OTD identifica a mesa pelo perfil como:

```text
10moon 1060N
```

Isso é esperado neste projeto.

## 4. Conferir a leitura da mesa

No OpenTabletDriver, abra:

```text
Tools → Tablet Debugger
```

Verifique:

- movimento de posição ao mover a caneta;
- `Pressure = 0` quando a ponta não está tocando;
- pressão aumentando gradualmente ao pressionar;
- valores próximos de `8191` com pressão forte.

Na unidade usada para desenvolver esta correção, foram observados valores próximos de `8180/8191` no teste final.

## 5. Windows Ink

Para pressão em aplicativos Windows que utilizam Windows Ink, instale uma versão do plugin **Windows Ink / VoiDPlugins** compatível com OpenTabletDriver 0.6.7.

Depois de instalado, o menu de modos de saída deve disponibilizar opções como:

```text
Windows Ink Absolute Mode
Windows Ink Relative Mode
```

Para desenho convencional, selecione:

```text
Windows Ink Absolute Mode
```

e aplique/salve a configuração.

## 6. Instalar o VMulti

O Windows Ink utilizado nesta configuração depende do **VMulti**, um dispositivo HID virtual.

Instale o VMulti usando a distribuição oficial do projeto correspondente.

Quando o VMulti não está instalado, o OpenTabletDriver pode apresentar uma mensagem semelhante a:

```text
Cannot find VirtualHID.
```

### IMPORTANTE: reinicie o Windows

Depois de instalar o VMulti:

1. feche o OpenTabletDriver;
2. **reinicie o Windows**;
3. abra primeiro o OpenTabletDriver;
4. confirme `Windows Ink Absolute Mode`;
5. aplique a configuração;
6. só então abra o aplicativo de desenho.

Nos testes deste projeto, a pressão podia aparecer no testador do Krita sem se comportar corretamente no pincel antes da reinicialização. Após reiniciar o Windows, a entrada voltou a funcionar normalmente.

## 7. Krita

No Krita, abra:

```text
Configurações
→ Configurar o Krita
→ Configurações do tablet
```

Em **Entrada API do tablet**, selecione:

```text
Entrada de mesa Windows 8+ (Windows Ink)
```

Confirme com **OK** e reinicie o Krita.

### Testador de tablet

Volte para:

```text
Configurações
→ Configurar o Krita
→ Configurações do tablet
→ Abrir testador de tablet
```

Faça riscos variando a força.

Os eventos devem apresentar valores `S=` diferentes conforme a pressão.

### Teste prático com pincel

Use um preset com tamanho controlado por pressão, por exemplo:

```text
Basic-5 Size
```

Faça um traço começando com pouca força, aumentando gradualmente e depois aliviando.

O esperado é:

```text
fino → médio → grosso → médio → fino
```

## 8. Photoshop

Com o OTD em `Windows Ink Absolute Mode`, VMulti instalado e Windows reiniciado, a pressão também foi confirmada no Adobe Photoshop durante os testes deste projeto.

## 9. Solução de problemas

### A mesa não é detectada

Confirme que:

- está usando a configuração `1060N.json`;
- o arquivo está no diretório `Configurations` da instalação realmente aberta;
- não há outra instância do OTD ou driver de tablet mantendo o dispositivo ocupado.

### Movimento funciona, mas não há pressão no aplicativo

Confirme:

- `Pressure` varia no `Tablet Debugger`;
- o modo é `Windows Ink Absolute Mode`;
- Windows Ink/VoiDPlugins está instalado;
- VMulti está instalado;
- o Windows foi reiniciado após a instalação do VMulti;
- o aplicativo está configurado para Windows Ink.

### Krita mostra `S=` variando, mas o pincel não responde

1. confirme **Windows 8+ Pointer Input (Windows Ink)**;
2. feche Krita e OTD;
3. reinicie o Windows;
4. abra primeiro o OTD;
5. aplique `Windows Ink Absolute Mode`;
6. abra o Krita novamente;
7. teste com `Basic-5 Size`.

### Clique fica preso

Na correção validada neste projeto, a pressão em repouso retorna a zero. Se o clique permanecer pressionado, confirme que está usando a compilação com o parser corrigido deste repositório e não uma tentativa antiga de multiplicação direta da pressão.

## 10. Arquivos e componentes de terceiros

Este guia não atribui OpenTabletDriver, Windows Ink/VoiDPlugins ou VMulti aos autores deste repositório.

Obtenha componentes de terceiros por suas fontes oficiais e respeite suas respectivas licenças.

Consulte também:

```text
THIRD_PARTY_NOTICES.md
```

## Configuração validada

A cadeia que funcionou nos testes foi:

```text
Zinnia Momentum MT100 / T505
        ↓
OpenTabletDriver 0.6.7
        ↓
parser 10moon corrigido
        ↓
Windows Ink Absolute Mode
        ↓
VMulti
        ↓
Krita / Adobe Photoshop
```
