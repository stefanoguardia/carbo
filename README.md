# Carbô

Calculadora de estratégia de gel de carboidrato para corredores. Responde cinco perguntas e devolve
três géis em pódio, o plano de sachês minuto a minuto e o kit a comprar.

Base técnica: *Gel Book*, de Carla Bogéa, revisão 2026. O app é educativo e não substitui
prescrição individual com nutricionista.

## Como está montado

Página única, sem build e sem dependência. Todo o motor e o catálogo vivem em `index.html`.

| arquivo | o que é |
|---|---|
| `index.html` | a aplicação inteira: estilo, catálogo de géis e motor de cálculo |
| `manifest.webmanifest` | deixa o app instalável no celular |
| `sw.js` | service worker: rede primeiro no HTML, cache nos ícones |
| `icon-192.png`, `icon-512.png` | ícones de instalação |

## Onde mexer

**Catálogo de géis** — array `GEIS`, perto do começo do `<script>`. Cada item:

```js
{id, n: nome, c: gramas de carboidrato, na: sódio em mg (null se o fabricante não informa),
 r: proporção glicose:frutose, pal: tem palatinose, hid: é hidrogel, caf: tem versão com cafeína,
 pt: faixa de preço 1 a 3, tx: textura, sb: sabores, cl: clean label, f: fases, d: descrição}
```

Sódio desconhecido vai como `null`, nunca chutado: o motor penaliza quem não informa.

**Links de afiliado** — objeto `CFG` na primeira linha do `<script>`:

```js
const CFG = { amazonTag: "carbo-20", mlTool: "" };
```

`amazonTag` é a tag do Amazon Associados. `mlTool` é o `matt_tool` do programa de afiliados do
Mercado Livre, que só existe depois da conta aprovada.

**Metas de carboidrato por distância** — objetos `IDEAL` (referência do Gel Book) e `TETO`
(limite máximo por distância).

**Perguntas** — array `PASSOS`. Um passo com `when` só aparece se a condição bater, que é como a
pergunta de gramas por hora só surge para quem já treina com gel.

## Publicar

Qualquer push na branch principal republica. Nada para compilar: o host só serve os arquivos.
