# Morse-code-COMPLETE-WEB-SITE
Site: https://rui0340.github.io/Morse-code-COMPLETE-WEB-SITE/Morse_Code.html
# Código Morse

Site para **codificar e decodificar código Morse**, com som, voz e ajustes de velocidade, frequência e volume. Funciona em celular, tablet e computador, com tema cinza escuro. E um detector de dispositivo

É uma página única (`HTML`, `CSS` e `JavaScript` no mesmo arquivo), **sem dependências e sem etapa de build**.

## Recursos
Gui Adapter, Carregamento e Detector de dispositivo.
### Decodificar

- A caixa de texto só aceita quatro entradas: `.` (ponto), `-` (traço), `/` (separa letras) e `//` (separa palavras). Qualquer outro caractere é removido na hora, inclusive quando colado.
- Abaixo da caixa aparece o que foi escrito, desenhado como bolinhas (pontos), barras (traços) e riscos (separadores), com um cursor branco que mostra onde o próximo símbolo entra.
- A tradução em letras e números aparece em tempo real.
- Botões na tela (`.`, `-`, `/`, `//`, apagar e limpar) inserem os símbolos **sem abrir o teclado do Android**.
- Botões `<` e `>` movem o cursor de letra em letra, para corrigir um trecho no meio da mensagem.

### Codificar

- Escreva um texto normal e veja o código Morse correspondente, em símbolos e em texto.
- Acentos são ignorados (`á` vira `A`) e caracteres sem equivalente em Morse são pulados.
- **Copiar Morse** copia o resultado.
- **Abrir no decodificador** leva o Morse para a outra aba.

### Som

- Toca o som de cada `.` e `-` enquanto você digita, com o botão **Som ao digitar** ativado.
- **Tocar mensagem** reproduz a mensagem inteira, com os intervalos corretos entre símbolos, letras e palavras. O mesmo botão vira **Parar** durante a reprodução.
- **Testar som** toca um ponto e um traço com os ajustes atuais e vira **Parar teste** enquanto toca.
- Ajustes:

| Ajuste | Faixa | Padrão |
| --- | --- | --- |
| Velocidade | 1 a 60 WPM (menu e caixa de texto) | 12 WPM |
| Frequência | 200 a 1500 Hz (slider e caixa de texto) | 615 Hz |
| Volume | 0 a 100% | 30% |

O volume máximo é limitado de propósito para proteger os ouvidos. Ao soltar um slider, toca um ponto curto para você ouvir o resultado.

### Voz

- O botão **Voz do Google** liga e desliga a leitura em voz alta. Com ela ativada, a voz fala cada letra assim que ela é completada com `/` e a palavra inteira quando é completada com `//`.
- **Repetir frase** lê de novo a tradução inteira (ou, na aba Codificar, o texto escrito), mesmo com a voz desligada.
- A voz usa a Web Speech API. O navegador escolhe a voz do Google no idioma selecionado quando ela existe no aparelho. O que é falado depende das vozes instaladas no dispositivo.

### Idioma da voz

O site escolhe o idioma da voz na primeira visita, sem pedir nada ao usuário:

1. Pelo **fuso horário** do aparelho (por exemplo, `America/Maceio` vira português do Brasil).
2. Se o fuso não for reconhecido, pelo **idioma do aparelho**.
3. Se nada funcionar, português (Brasil).

O botão **Detectar localização** é mais preciso. Ele pede a **permissão de localização** do navegador e usa a posição do aparelho para achar a cidade de referência mais próxima e o idioma dela. Se a permissão for negada, ou o navegador não oferecer localização, ele volta para o fuso horário e o idioma do aparelho. Se o navegador já tiver concedido essa permissão ao site, a detecção por localização roda sozinha na primeira visita. Também dá para escolher o idioma no menu. Idiomas disponíveis: português (Brasil e Portugal), inglês (EUA e Reino Unido), espanhol (Espanha e América Latina), francês, alemão, italiano, japonês, chinês, hindi, russo, árabe e coreano.

O idioma aparece no endereço como `#pt-br`, `#en-us` etc. Abrir o site com `#en-us` no final do endereço já deixa a voz em inglês.

> **Como a localização é usada:** a posição é comparada, no próprio navegador, com uma lista interna de cidades de referência: as capitais do Brasil, algumas cidades grandes do interior e grandes cidades de outros países. O resultado é a **cidade de referência mais próxima**, não a cidade exata, e o site mostra a distância até ela. Nenhuma coordenada é enviada para fora nem guardada; só o idioma escolhido é salvo. Perto de fronteiras o resultado pode errar, e nesse caso basta trocar o idioma no menu. Não há consulta a serviços externos, então o site não descobre o nome exato de cidade e estado fora da lista.
>
> Prioridade do idioma: endereço (`#pt-br`), depois o salvo, depois o detectado.

### Auto save

O site guarda no navegador (`localStorage`) a velocidade, a frequência, o volume, os botões liga/desliga, o idioma, a aba atual e o texto das duas caixas. Ao voltar, tudo está como você deixou. O botão **Restaurar padrões** volta os ajustes ao original sem apagar os textos.

## Convenção usada

| Símbolo | Significado |
| --- | --- |
| `.` | ponto |
| `-` | traço |
| `/` | fim de letra |
| `//` | fim de palavra |

Caracteres suportados: letras `A–Z`, números `0–9` e a pontuação `. , ? ! - : ; ( ) ' = + @`.

Temporização (padrão PARIS): a unidade dura `1200 / WPM` milissegundos. O ponto dura 1 unidade e o traço 3. O intervalo entre símbolos de uma letra é 1 unidade, entre letras 3 e entre palavras 7.

## Como usar

### Localmente

Baixe o arquivo e abra no navegador. Não precisa de servidor nem de instalação.

## Estrutura

```
.
├── index.html   # a página inteira (HTML, CSS e JavaScript)
└── README.md
```

## Tecnologias

- HTML, CSS e JavaScript puro
- Web Audio API (geração dos tons)
- Web Speech API (leitura em voz alta)
- Geolocation API (detecção do idioma pela localização)
- `localStorage` (auto save)
- Fonte [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono) via Google Fonts. Sem internet, a página usa uma fonte monoespaçada do sistema.

## Compatibilidade e limitações

- O navegador só libera o som depois do primeiro toque ou clique na página.
- A localização só funciona em página com **HTTPS** (como o GitHub Pages) e depende da permissão do usuário. O navegador pode bloquear o pedido em páginas embutidas em outros sites.
- As vozes disponíveis variam por aparelho e navegador. No Chrome para Android, a voz do Google costuma ser a padrão.
- O botão de copiar depende da permissão de área de transferência do navegador. Se for bloqueado, o botão avisa.
- Se o armazenamento do navegador estiver bloqueado (por exemplo, em aba anônima), o site funciona normalmente, mas não guarda as configurações.

## Licença

Nothing.
