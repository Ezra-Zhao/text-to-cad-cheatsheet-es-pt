# 📐 Guía rápida: text-to-cad — tu agente dibuja CAD desde texto (ES · PT)

Una sola página para usar **text-to-cad** (de earthtojake): describir una pieza en lenguaje natural y obtener un modelo CAD editable, con el flujo completo de la idea a la fabricación, los skills que trae y los errores que arruinan una pieza.

**Autor:** Guangyi Zhao · Octubre 2026

Proyecto original: https://github.com/earthtojake/text-to-cad (21.193 estrellas, consultado el 17 de octubre de 2026)

> **Nota de autoría:** esta guía es una síntesis original, redactada por el autor a partir de la documentación pública del proyecto y de su propio uso. No es una traducción ni una copia de la documentación oficial, y no es un proyecto oficial de earthtojake. Para el detalle completo, ve al repositorio enlazado.

---


Apoyo y más: [GitHub Sponsors](https://github.com/sponsors/Ezra-Zhao) · [Gumroad — plantillas y cuadernos que uso](https://ezraflow28.gumroad.com) · [Ko-fi](https://ko-fi.com/ezra777zhao)

## 🇪🇸 Español

### Qué es

text-to-cad es un plugin que le da a tu agente (Claude Code, Codex, Cursor, Gemini, Grok y otros compatibles con plugins o skills) la capacidad de generar modelos CAD en local. Describes la pieza con palabras o con una imagen y el agente produce geometría real: el formato principal es **STEP**, con exportación a **STL, 3MF y GLB**. Por debajo corre `cadgen` (Python, sobre build123d y Open CASCADE) vía `uv`, con un visor local y un servidor MCP para revisar cada modelo antes de fabricarlo.

### Instalación

1. **Pídeselo a tu agente** (la vía recomendada): «Install text-to-cad from https://github.com/earthtojake/text-to-cad». Necesitas `uv` instalado; la primera ejecución descarga el runtime de CAD, así que requiere conexión.
2. **En Claude Code**, a mano:
   ```bash
   claude plugin marketplace add earthtojake/text-to-cad#latest
   claude plugin install text-to-cad@earthtojake
   ```
3. **Reinicia la app.** Instala el plugin **o** los skills sueltos en cada app, nunca ambos: dos copias duplican cada skill.

### El flujo completo

1. **Describe** la pieza con medidas: forma, dimensiones, agujeros, espesores. Sin números, el agente adivina.
2. **Revisa en el visor** el modelo generado; pide cambios en lenguaje natural («sube el agujero 5 mm», «redondea esa arista»).
3. **Exporta** en el formato que pida tu proceso: STEP para mecanizado y edición, STL/3MF para impresión 3D, GLB para visualización.
4. **Pasa los chequeos** de fabricación (DFM/DfAM, tabla siguiente) antes de gastar material.
5. **Fabrica**: corta con el G-code generado, envía a tu impresora Bambu o valida el archivo para un servicio externo.

### Los skills que trae

| Skill | Para qué sirve |
|---|---|
| **CAD** | Crear y editar modelos desde texto o imágenes; salida STEP (+ STL, 3MF, GLB) |
| **step.parts** | Buscar piezas comerciales en STEP: tornillos, rodamientos, motores, conectores |
| **Engineering Drawing** | Planos de ingeniería en PDF con cotas, vistas, líneas ocultas y cajetín |
| **DXF** | Dibujos 2D: perfiles, plantillas, juntas y layouts de corte |
| **URDF / SRDF / SDF** | Archivos de robots (enlaces, articulaciones, límites) y mundos de simulación |
| **DFM** | Revisión para chapa, CNC o inyección: ángulos de desmoldeo, socavados, área proyectada, con la regla citada en cada hallazgo |
| **DfAM Check** | Imprimibilidad: espesor de pared, voladizos, volumen de soportes y orientación |
| **G-code** | Laminado con OrcaSlicer usando los perfiles de tu impresora |
| **Bambu Labs** | Enviar impresiones a impresoras Bambu |
| **SendCutSend** | Validar DXF y STEP antes de subirlos al servicio de corte |

### 5 plantillas de prompt que funcionan

- **Brida:** «Brida circular de 80 mm de diámetro, 8 mm de espesor, agujero central de 30 mm y 6 agujeros de 6 mm en un círculo de 65 mm, equiespaciados.»
- **Soporte en L:** «Soporte en L de 60 × 40 mm, espesor 4 mm, dos agujeros de 5 mm por ala, radio interior de 3 mm.»
- **Caja con tapa:** «Caja para electrónica de 100 × 70 × 35 mm, pared de 2 mm, tapa con 4 tornillos M3 en las esquinas y un recorte lateral de 20 × 10 mm para cables.»
- **Junta (DXF):** «Junta plana con el contorno de la brida anterior, en DXF, con los 6 agujeros.»
- **Polea:** «Polea para correa GT2 de 40 mm de diámetro, 20 dientes, agujero central de 5 mm y tornillo prisionero M3.»

### ⚠️ Errores típicos

- **No dar medidas.** «Hazme un soporte» sin dimensiones produce una pieza bonita e inútil. Cada prompt lleva números y unidades.
- **Imprimir sin pasar DfAM.** Paredes demasiado finas y voladizos sin soporte se descubren en el chequeo, no a mitad de impresión.
- **Saltarse el plano.** Para mecanizado o para que otro fabrique, genera el Engineering Drawing con cotas: el modelo solo no comunica tolerancias.
- **Dejar la telemetría sin decidir.** Por defecto el proyecto envía estadísticas de uso e informes de fallo (con un ID aleatorio, nunca tus archivos ni prompts). Se apaga con `uvx cadgen telemetry off`.

---

## 🇵🇹 Português

### O que é

O text-to-cad é um plugin que dá ao seu agente (Claude Code, Codex, Cursor, Gemini, Grok e outros compatíveis com plugins ou skills) a capacidade de gerar modelos CAD localmente. Você descreve a peça com palavras ou com uma imagem e o agente produz geometria de verdade: o formato principal é **STEP**, com exportação para **STL, 3MF e GLB**. Por baixo roda o `cadgen` (Python, sobre build123d e Open CASCADE) via `uv`, com um visualizador local e um servidor MCP para revisar cada modelo antes de fabricar.

### Instalação

1. **Peça ao seu agente** (o caminho recomendado): «Install text-to-cad from https://github.com/earthtojake/text-to-cad». Você precisa do `uv` instalado; a primeira execução baixa o runtime de CAD, então precisa de conexão.
2. **No Claude Code**, manualmente:
   ```bash
   claude plugin marketplace add earthtojake/text-to-cad#latest
   claude plugin install text-to-cad@earthtojake
   ```
3. **Reinicie o app.** Instale o plugin **ou** os skills soltos em cada app, nunca os dois: duas cópias duplicam cada skill.

### O fluxo completo

1. **Descreva** a peça com medidas: forma, dimensões, furos, espessuras. Sem números, o agente adivinha.
2. **Revise no visualizador** o modelo gerado; peça mudanças em linguagem natural («sobe o furo 5 mm», «arredonda essa aresta»).
3. **Exporte** no formato que o seu processo pede: STEP para usinagem e edição, STL/3MF para impressão 3D, GLB para visualização.
4. **Passe pelas checagens** de fabricação (DFM/DfAM, tabela a seguir) antes de gastar material.
5. **Fabrique**: corte com o G-code gerado, envie para a sua impressora Bambu ou valide o arquivo para um serviço externo.

### Os skills que ele traz

| Skill | Para que serve |
|---|---|
| **CAD** | Criar e editar modelos a partir de texto ou imagens; saída STEP (+ STL, 3MF, GLB) |
| **step.parts** | Buscar peças comerciais em STEP: parafusos, rolamentos, motores, conectores |
| **Engineering Drawing** | Desenhos de engenharia em PDF com cotas, vistas, linhas ocultas e carimbo |
| **DXF** | Desenhos 2D: perfis, gabaritos, juntas e layouts de corte |
| **URDF / SRDF / SDF** | Arquivos de robôs (elos, juntas, limites) e mundos de simulação |
| **DFM** | Revisão para chapa, CNC ou injeção: ângulos de saída, rebaixos, área projetada, com a regra citada em cada achado |
| **DfAM Check** | Imprimibilidade: espessura de parede, balanços, volume de suportes e orientação |
| **G-code** | Fatiamento com OrcaSlicer usando os perfis da sua impressora |
| **Bambu Labs** | Enviar impressões para impressoras Bambu |
| **SendCutSend** | Validar DXF e STEP antes de enviar ao serviço de corte |

### 5 modelos de prompt que funcionam

- **Flange:** «Flange circular de 80 mm de diâmetro, 8 mm de espessura, furo central de 30 mm e 6 furos de 6 mm num círculo de 65 mm, igualmente espaçados.»
- **Suporte em L:** «Suporte em L de 60 × 40 mm, espessura 4 mm, dois furos de 5 mm por aba, raio interno de 3 mm.»
- **Caixa com tampa:** «Caixa para eletrônica de 100 × 70 × 35 mm, parede de 2 mm, tampa com 4 parafusos M3 nos cantos e um recorte lateral de 20 × 10 mm para cabos.»
- **Junta (DXF):** «Junta plana com o contorno do flange anterior, em DXF, com os 6 furos.»
- **Polia:** «Polia para correia GT2 de 40 mm de diâmetro, 20 dentes, furo central de 5 mm e parafuso sem cabeça M3.»

### ⚠️ Erros típicos

- **Não dar medidas.** «Faz um suporte» sem dimensões produz uma peça bonita e inútil. Cada prompt leva números e unidades.
- **Imprimir sem passar pelo DfAM.** Paredes finas demais e balanços sem suporte se descobrem na checagem, não no meio da impressão.
- **Pular o desenho técnico.** Para usinagem ou para outro fabricar, gere o Engineering Drawing com cotas: o modelo sozinho não comunica tolerâncias.
- **Deixar a telemetria sem decisão.** Por padrão o projeto envia estatísticas de uso e relatórios de falha (com um ID aleatório, nunca os seus arquivos nem prompts). Desliga com `uvx cadgen telemetry off`.

---

## 🇬🇧 English summary

One-page cheat sheet (Spanish + Portuguese) for **text-to-cad** (earthtojake): the agent plugin that generates real CAD from plain language or images — STEP as the main output, with STL/3MF/GLB export — running locally on build123d/Open CASCADE through the `cadgen` Python package, a local viewer and an MCP server. Covers installation (ask your agent, or the Claude Code marketplace commands), the five-step flow from description to fabrication, the skill set (CAD, step.parts, engineering drawings, DXF, URDF/SRDF/SDF, DFM and DfAM checks, G-code, Bambu Labs, SendCutSend), five working prompt templates (flange, L-bracket, enclosure, gasket, pulley), and the typical mistakes: no dimensions in the prompt, printing before the DfAM check, skipping the dimensioned drawing, and leaving the default telemetry undecided. Original synthesis by the author from the project's public documentation; not an official earthtojake document and not a translation.

**Author:** Guangyi Zhao · October 2026 · MIT License
