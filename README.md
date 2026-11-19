# Gêmeo digital térmico de hardware computacional

**Fundamentos de Engenharia · CEUB · Engenharia de Software**  

**Autores:** Nicolas Melo e Alisson Lima Borba Lopes · **Contas acadêmicas:** [gitnick-ceub](https://github.com/gitnick-ceub) e [alissonblopes](https://github.com/alissonblopes)

Este projeto apresenta o estudo de um dissipador térmico híbrido de alumínio e cobre, desenvolvido para uma fonte térmica equivalente à de uma GPU. O trabalho integra conhecimentos de ciência dos materiais, química, sustentabilidade, expressão gráfica, transferência de calor e mecânica dos sólidos, abordando diferentes aspectos envolvidos na concepção e análise da solução proposta.

O repositório reúne os principais materiais produzidos ao longo do projeto, incluindo o relatório final, modelos CAD, simulações, conjuntos de dados, figuras e um aplicativo web complementar, proporcionando uma visão abrangente do desenvolvimento e dos resultados obtidos.

**Repositório:** https://github.com/gitnick-ceub/gemeo-digital-termico-gpu  
**Versão de entrega:** [`entrega-2026-10-18`](https://github.com/gitnick-ceub/gemeo-digital-termico-gpu/releases/tag/entrega-2026-10-18)  
**Pacote para envio:** [baixar o ZIP da entrega](https://github.com/gitnick-ceub/gemeo-digital-termico-gpu/releases/download/entrega-2026-10-18/Entrega_Final_Nicolas_Melo.zip)

## Entregáveis e acesso rápido

| Entregável | Arquivo / acesso |
| --- | --- |
| Relatório técnico final em PDF, incluindo o desenho A3 | [Abrir PDF](report/Relatorio_Tecnico_Nicolas_Melo.pdf) |
| Fonte editável do relatório | [Baixar DOCX](report/Relatorio_Tecnico_Nicolas_Melo.docx?raw=true) |
| Modelo FreeCAD paramétrico nativo | [Baixar FCStd](cad/heatsink.FCStd?raw=true) |
| Modelo neutro para interoperabilidade | [Baixar STEP](cad/heatsink.step?raw=true) |
| Desenho técnico cotado, A3 horizontal | [PDF](drawings/heatsink_drawing.pdf) · [SVG](drawings/heatsink_drawing.svg) |
| Notebook autocontido, com saídas preservadas | [Ver notebook](simulation/gpu_thermal_study.ipynb) · [Executar no Colab](https://colab.research.google.com/github/gitnick-ceub/gemeo-digital-termico-gpu/blob/entrega-2026-10-18/simulation/gpu_thermal_study.ipynb) |
| Simulação Energy2D nativa | [Baixar E2D](energy2d/heatsink.e2d?raw=true) · [Reproduzir](energy2d/README.md) |
| Quadro de seleção de materiais | Tabela 2 do relatório; o enunciado aceita a tabela no PDF |
| Capturas, renderização CAD e gráficos | [Figuras](figures/) |
| Dados numéricos e verificações | [Resultados CSV/JSON](results/) |
| Cálculos mecânicos, de materiais e ambientais | [Código](report/engineering_calculations.py) · [Resultados](report/engineering_results.json) |
| Parâmetros e referências | [Configuração](parameters.json) · [Fontes e rastreabilidade](report/references.json) |
| Aplicativo web interativo e seu solver | [GPU Lab](gpu-twin/README.md) · [Método térmico](gpu-twin/solver.md) |

O enunciado declara FreeCAD, Energy2D e Colab obrigatórios. Os artefatos das três ferramentas estão incluídos; o aplicativo web é complementar e não os substitui.

## Correspondência com os seis eixos

| Eixo | Evidência no relatório e nos artefatos |
| --- | --- |
| Ciência dos Materiais | Seção 2: comparação Al 6063-T6 × Cu C11000, propriedades, massa, custo ilustrativo e processamento |
| Química | Seção 3: pasta térmica, contatos, oxidação, passivação e corrosão galvânica |
| Ciências do Ambiente | Seção 9: consumo, cenário de carbono, ciclo de vida, reciclabilidade e descarte |
| Expressão Gráfica | Seção 4 e Anexo A: modelo FreeCAD, vistas, cotas, escala, carimbo e folha A3 |
| Fenômenos de Transporte | Seções 5–7: solver Python, convergência, balanço energético e estudo Energy2D |
| Mecânica dos Sólidos | Seção 8: dilatação, hipótese de restrição, tensões e descasamento de CTE |

![Campo de temperatura calculado na base do dissipador do estudo acadêmico](figures/temperature_map.png)

## Dois modelos, finalidades diferentes

| Característica | Estudo acadêmico do relatório | Aplicativo GPU Lab |
| --- | --- | --- |
| Geometria | Dissipador autoral 180 × 90 × 29 mm, 20 aletas e contato de cobre | Montagem visual inspirada na RTX 3060, 49 aletas e 2/4/6 heat pipes equivalentes |
| Cálculo | Python: base 2D por volumes finitos, aletas analíticas e nós equivalentes | TypeScript em Web Worker: duas bases 2D, aletas analíticas e tubos equivalentes |
| Uso | Análise documentada dos seis eixos da disciplina | Exploração interativa de material, potência, ambiente, convecção e quantidade de tubos |
| Resultado | Valores, hipóteses e verificações apresentados no relatório | Heatmap espacial e evolução térmica calculados para a configuração escolhida |

**Não misturar os resultados dos dois modelos.** O cenário nominal do relatório chega a 83,68 °C na fonte equivalente sob as hipóteses declaradas; a meta de 85 °C não é um limite oficial da GPU. O h é prescrito, não medido. A triagem de restrição mecânica total não atende à meta ilustrativa adotada e não libera uma montagem rígida. Nenhum modelo certifica uma RTX 3060 real ou substitui validação experimental.

## Reprodução

### 1. Obter o projeto

```sh
git clone https://github.com/gitnick-ceub/gemeo-digital-termico-gpu.git
cd gemeo-digital-termico-gpu
git checkout entrega-2026-10-18
```

O ZIP da release contém os arquivos da entrega sem histórico Git, ambientes locais, credenciais ou dependências instaladas.

### 2. Notebook no Google Colab

Use o acesso da tabela de entregáveis, entre na sua conta e selecione **Executar tudo**. O notebook incorpora configuração e código, instala dependências ausentes e exporta resultados. Não depende de caminhos desta estação, de Drive ou do aplicativo web.

### 3. Cálculos Python locais

Requisito de referência: **Python 3.12**. A partir da raiz do projeto:

```sh
python3.12 -m venv .venv
. .venv/bin/activate
python -m pip install -r requirements.txt
python simulation/thermal_solver.py
python report/engineering_calculations.py
```

`simulation/build_notebook.py` remonta e executa o notebook a partir das fontes. Os resultados ficam em `results/`, `figures/` e `report/engineering_results.json`. Os arquivos de requisitos fixam as versões utilizadas no estudo.

### 4. Modelo FreeCAD e desenho

Abra o FCStd no FreeCAD. A planilha `Parameters` permite editar dimensões; alterar o número de aletas exige executar novamente `cad/build_heatsink.FCMacro`. A macro consulta `parameters.json` na raiz. O desenho é vetorial e gerado por `drawings/build_drawing.py`, não por uma página TechDraw nativa.

A folha do desenho está em **A3 horizontal**. Imprima em **tamanho real/100%**, sem ajustar à página, para preservar a escala. A furação e a fixação são didáticas e não estão liberadas para fabricação ou instalação em hardware real.

### 5. Energy2D

Abra o E2D na ferramenta oficial. `energy2d/README.md` documenta a obtenção do JAR, as condições e os comandos para reproduzir a execução e a captura com `RunEnergy2D.java`. O JAR não foi modificado nem incluído como dependência instalada no repositório.

O estudo Energy2D é qualitativo e transiente; sua seção, extrusão e convecção diferem do modelo Python. Não usar suas cores como validação quantitativa da temperatura da GPU.

### 6. Aplicativo web complementar

Requisitos: **Bun 1.3+** e navegador moderno com WebGL. Dentro de `gpu-twin/`:

```sh
bun install
bun run dev
```

O endereço local é informado pelo Vite. Para verificar o código e gerar o build estático:

```sh
bun run check
bun test
bun run build
```

O aplicativo mantém a física separada da renderização. Ocultar peças, explodir a montagem e animar as ventoinhas não alteram a refrigeração; h é um parâmetro explícito. Controles, equações, limites dos tubos e verificações numéricas estão documentados no diretório do aplicativo.

## Editar o relatório sem perder as alterações

A fonte do texto final é o DOCX em `report/`. Edite-o no Word ou LibreOffice, atualize os campos do sumário e exporte o PDF pelo próprio editor. O relatório contém links para este repositório e para os artefatos da versão de entrega.

Os antigos geradores de texto/PDF e os DOCX intermediários não integram o repositório, evitando substituir as edições finais do autor por uma versão anterior. Alterar dimensões ou hipóteses exige atualizar CAD, cálculos, imagens e relatório de forma coerente; executar o Python não atualiza automaticamente os demais artefatos.

## Referências, autoria e licenças de terceiros

As referências científicas estão no PDF e no arquivo de rastreabilidade. Fontes livres utilizadas no desenho e seus termos estão em `assets/fonts/`, incluindo as licenças Liberation e DejaVu. As figuras foram produzidas pelos artefatos e ferramentas identificados no relatório; não representam medições físicas de uma GPU comercial.

A assistência de inteligência artificial permanece declarada no relatório. A revisão e a responsabilidade acadêmica são do autor.

## Item externo da atividade

O vídeo demonstrativo de 3–5 minutos, publicado no YouTube como não listado, é exigido no enunciado. Seu link ainda não foi disponibilizado neste repositório. Se o trabalho for realizado em grupo, cada integrante deve enviar a atividade na própria conta.
