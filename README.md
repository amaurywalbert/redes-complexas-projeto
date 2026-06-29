# Redes Complexas Aplicadas à Análise Estrutural de Proteínas

Projeto desenvolvido para a disciplina **Redes Complexas** do Programa de Doutorado em Ciência da Computação (UFU), com o objetivo de modelar proteínas como redes complexas, analisar suas propriedades topológicas e detectar comunidades biologicamente relevantes.

## Objetivos

O projeto investiga a aplicação de técnicas de Redes Complexas na análise estrutural de proteínas, contemplando:

* modelagem de proteínas como Redes de Contato por Resíduos (Residue Contact Networks – RCN), Afinidade Bioquímica e Homologia entre Cadeias;
* análise topológica da rede;
* cálculo de medidas de centralidade;
* análise espectral da matriz Laplaciana;
* detecção de comunidades utilizando:

  * Bipartição Espectral (Vetor de Fiedler);
  * Louvain;
  * Infomap;
* validação biológica das comunidades detectadas.

A proteína **1A3N** foi utilizada para validação e escolha da modelagem da rede. A proteína **6B1T** constitui o estudo de caso principal do projeto.

---

# Estrutura do repositório

```
.
├── doc/
│   ├── Relatorio.pdf
│   └── Slides.pdf
│
├── 01_1A3N_spatial_8A.ipynb
├── 02_1A3N_biophysical_8A.ipynb
├── 03_1A3N_mixed_chain_8A.ipynb
├── 04_1A3N_mixed_chain_6A.ipynb
├── 05_1A3N_mixed_chain_10A.ipynb
├── 06_1A3N_mixed_chain_4A.ipynb
├── 07_6B1T_mixed_chain_8A.ipynb
├── 08_6B1T_mixed_chain_6A.ipynb
│
└── README.md
```

Os notebooks estão numerados de acordo com a sequência em que o projeto foi desenvolvido, permitindo acompanhar toda a evolução metodológica.

---

# Notebooks do projeto

## Validação da modelagem (Proteína 1A3N)

| Notebook | Descrição                                                | Google Colab                                                                                                           |
| -------- | -------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| 01       | Modelagem utilizando apenas contatos espaciais (8 Å)     | https://colab.research.google.com/github/amaurywalbert/redes-complexas-projeto/blob/main/01_1A3N_spatial_8A.ipynb      |
| 02       | Modelagem espacial + afinidade bioquímica                | https://colab.research.google.com/github/amaurywalbert/redes-complexas-projeto/blob/main/02_1A3N_biophysical_8A.ipynb  |
| 03       | Modelo híbrido (espacial + bioquímica + homologia) – 8 Å | https://colab.research.google.com/github/amaurywalbert/redes-complexas-projeto/blob/main/03_1A3N_mixed_chain_8A.ipynb  |
| 04       | Modelo híbrido – 6 Å                                     | https://colab.research.google.com/github/amaurywalbert/redes-complexas-projeto/blob/main/04_1A3N_mixed_chain_6A.ipynb  |
| 05       | Modelo híbrido – 10 Å                                    | https://colab.research.google.com/github/amaurywalbert/redes-complexas-projeto/blob/main/05_1A3N_mixed_chain_10A.ipynb |
| 06       | Modelo híbrido – 4 Å                                     | https://colab.research.google.com/github/amaurywalbert/redes-complexas-projeto/blob/main/06_1A3N_mixed_chain_4A.ipynb  |

## Estudo de caso (Proteína 6B1T)

| Notebook | Descrição                              | Google Colab                                                                                                          |
| -------- | -------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| 07       | Modelagem final da proteína 6B1T (8 Å) | https://colab.research.google.com/github/amaurywalbert/redes-complexas-projeto/blob/main/07_6B1T_mixed_chain_8A.ipynb |
| 08       | Teste adicional da proteína 6B1T (6 Å) | https://colab.research.google.com/github/amaurywalbert/redes-complexas-projeto/blob/main/08_6B1T_mixed_chain_6A.ipynb |

Todos os notebooks podem ser executados diretamente no **Google Colab**, sem necessidade de instalação local.

---

# Como executar o projeto

## Opção 1 – Google Colab (recomendado)

Todos os notebooks podem ser executados diretamente no **Google Colab** utilizando os links apresentados anteriormente.

Antes de executar qualquer notebook, é necessário criar a estrutura de diretórios utilizada pelo projeto e adicionar os arquivos PDB correspondentes.

### Estrutura esperada

```text
data/
└── raw/
    ├── 1A3N/
    │   └── 1A3N.pdb
    │
    └── 6B1T/
        ├── 6b1t-pdb-bundle1.pdb
        └── 6b1t-pdb-bundle2.pdb
```

### Arquivos necessários

**Proteína 1A3N**

Disponível em:

[data/raw/1A3N/1A3N.pdb](./data/raw/1A3N/1A3N.pdb)

ou

https://www.rcsb.org/structure/1A3N

**Proteína 6B1T**

Esses arquivos fazem parte do pacote compactado (**PDB Bundle**) disponibilizado pelo RCSB para a estrutura 6B1T.

Disponível em:

[data/raw/6B1T/6b1t-pdb-bundle1.pdb](./data/raw/6B1T/6b1t-pdb-bundle1.pdb)
[data/raw/6B1T/6b1t-pdb-bundle2.pdb](./data/raw/6B1T/6b1t-pdb-bundle2.pdb)

ou

https://www.rcsb.org/structure/6B1T

Após criar os diretórios e copiar os arquivos PDB para os respectivos locais, o notebook poderá ser executado normalmente.


---

## Opção 2 – Execução local

### Requisitos

* Python 3.11+
* Jupyter Notebook

### Instalação das bibliotecas

```bash
pip install biopython
pip install pandas
pip install numpy
pip install scipy
pip install networkx
pip install matplotlib
pip install plotly
pip install scikit-learn
pip install python-louvain
pip install infomap
```

---

# Fluxo do projeto

O projeto foi desenvolvido seguindo o pipeline abaixo:

1. Download do arquivo PDB;
2. Extração dos resíduos utilizando BioPython;
3. Construção da Rede de Contatos por Resíduos;
4. Construção da matriz de similaridade entre cadeias;
5. Construção da rede híbrida:

   * contatos espaciais;
   * afinidade bioquímica;
   * homologia entre cadeias;
6. Análise topológica;
7. Cálculo das medidas de centralidade;
8. Análise espectral da Laplaciana;
9. Detecção de comunidades:
   
   * Vetor de Fiedler;
   * Louvain;
   * Infomap;
10. Validação biológica utilizando as anotações do RCSB.

---

# Resultados produzidos

Os notebooks geram automaticamente:

* estatísticas topológicas da rede;
* distribuição dos graus;
* medidas de centralidade;
* espectro da Laplaciana;
* visualizações 2D e 3D da proteína;
* detecção de comunidades;
* comparação entre comunidades e famílias biológicas;
* tabelas de validação (NMI, ARI e Purity).

As visualizações tridimensionais produzidas com **Plotly** permanecem interativas quando executadas no Google Colab ou Jupyter Notebook.

---

# Material complementar

A pasta **doc/** contém:

*   [Relatório do Projeto em PDF](./docs/Relatório.pdf)
*   [Slides em PDF](./docs/Slides.pdf)

---

# Autor

**Amaury Walbert**

Doutorando em Ciência da Computação – Universidade Federal de Uberlândia (UFU)
Disciplina: Redes Complexas
