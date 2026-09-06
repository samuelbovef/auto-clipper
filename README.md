<div align="center">
  
  <h1>AutoClipper v5.0.0</h1>
  
  **Automação Inteligente para Cortes de Vídeo, Legendagem Dinâmica (.ass) e IA**

  [![Python](https://img.shields.io/badge/Python-3.10-blue.svg?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
  [![PyTorch](https://img.shields.io/badge/PyTorch-CUDA_12.1-EE4C2C.svg?style=for-the-badge&logo=pytorch&logoColor=white)](https://pytorch.org/)
  [![License: MIT](https://img.shields.io/badge/License-MIT-success.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
  [![Suporte](https://img.shields.io/badge/Central_de_Suporte-24292e?style=for-the-badge&logo=github&logoColor=white)](https://github.com/samuelbovef/suporte)

  Uma ferramenta de código aberto que transforma vídeos longos em clipes curtos (Shorts, Reels, TikTok) de forma automatizada e autônoma. 
</div>

<br>

O **AutoClipper** utiliza inteligência artificial local para detectar picos acústicos, transcrever áudios com alta precisão e aplicar legendas avançadas. Desenvolvido para criadores de conteúdo e editores que buscam escalar sua produção sem depender de APIs de terceiros.

---

## Índice
- [Principais Recursos](#principais-recursos)
- [Demonstração](#demonstração)
- [Pré-requisitos](#pré-requisitos)
- [Instalação](#instalação)
- [Como Usar](#como-usar)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Como Contribuir](#como-contribuir)
- [Suporte e Serviços](#suporte-e-serviços)

---

## Principais Recursos

* **Processamento de IA Local:** Utiliza `WhisperX` e `PyTorch` para transcrição e alinhamento perfeito de palavras, sem custo de APIs. Suporte dinâmico para CPU e aceleração via GPU (CUDA).
* **Motores de Decisão Duplos:**
  * **Modo Emoção:** O motor acústico utiliza `Librosa` para rastrear ondas sonoras e isolar picos de emoção (ênfases, risadas), respeitando o ritmo e as pausas naturais.
  * **Modo Palavras-Chave:** Varredura textual para extração de cortes baseados em nichos semânticos.
* **Legendagem Cinematográfica (.ASS):** Motor de renderização que aplica matemática espacial para gerar efeitos programáticos dinâmicos, como *Fade*, *Slide In*, *Bounce (Pop)*, *Flip 3D* e *Shear*.
* **Processamento em Lote (Batch):** Capacidade de ler listas de URLs e processar múltiplos vídeos em fila, incluindo rotinas de autolimpeza de arquivos temporários.
* **Pipeline de Color Grading:** Validador integrado de arquivos LUTs (`.cube`) para aplicação de filtros de cor direto no processamento.

---

## Demonstração

A operação do **AutoClipper v5.0.0** é feita diretamente via terminal interativo:

**1. Seleção de Mídia e Motor de Corte** 
<br>Escolha entre processamento único ou em lote, defina o motor inteligente desejado e insira a URL do YouTube.

<img width="939" height="478" alt="Captura de tela 2026-05-11 044736" src="https://github.com/user-attachments/assets/19ad30a5-000b-4bfb-bf77-a7d51a65ad53" />

<br>

**2. Configuração Estética das Legendas** 
<br>Controle total sobre a posição na tela, densidade de palavras por bloco e aplicação de efeitos de animação.

<img width="939" height="1018" alt="Captura de tela 2026-05-11 045014" src="https://github.com/user-attachments/assets/81f4f897-1dd2-4ded-9a73-eb9450544414" />

<br>

**3. Processamento Automatizado** 
<br>O sistema realiza o download na melhor qualidade, transcreve, corta e renderiza o vídeo final de forma autônoma.

<img width="939" height="1016" alt="Captura de tela 2026-05-11 045041" src="https://github.com/user-attachments/assets/69387c3e-d014-4975-85f0-e6eccbee999f" />

## Pré-requisitos

Para rodar o ambiente localmente, é necessário:

* **Python 3.10.x:** Versões superiores (como 3.12) podem gerar conflitos com as dependências atuais do PyTorch. Marque a opção *"Add Python to PATH"* durante a instalação.
* **FFmpeg:** Essencial para o processamento de mídia. No Windows, faça o download do `ffmpeg.exe` e `ffprobe.exe` e coloque-os dentro da pasta `bin/` na raiz do projeto. O sistema os mapeará automaticamente.

---

## Instalação

### Opção A: Instalação Automática (Windows)
Recomendado pela praticidade. Cria o ambiente virtual e instala as dependências via script.

**1.** Clone o repositório:
```bash
git clone [https://github.com/samuelbovef/auto-clipper.git](https://github.com/samuelbovef/auto-clipper.git)

```

**Passo 2:** Adicione os binários do FFmpeg na pasta `bin/`.

**Passo 3:** Dê dois cliques no arquivo **`Instalar.bat`**. O script validará o Python, criará o ambiente virtual (venv) e instalará o PyTorch (com CUDA) e os requisitos definidos em requirements.txt.

<br>

### Opção B: Instalação Manual (Avançada / Unix)
Para controle total ou uso em distribuições Linux e macOS.

**Passo 1:** Clone o repositório e acesse a pasta:
```bash
git clone [https://github.com/samuelbovef/auto-clipper.git](https://github.com/samuelbovef/auto-clipper.git)
cd auto-clipper
```

**Passo 2:** Crie e ative o ambiente virtual:
```bash
# Windows
python -m venv venv
venv\Scripts\activate

# Linux/macOS
python3.10 -m venv venv
source venv/bin/activate
```

**Passo 3:** Instale o PyTorch (CUDA) e os requisitos:
```bash
pip install torch torchaudio --index-url [https://download.pytorch.org/whl/cu121](https://download.pytorch.org/whl/cu121)
pip install -r requirements.txt
```

---

---

## Como Usar

Com o ambiente configurado, inicie o orquestrador:

* **Via Script (Windows):** Execute o arquivo **`Iniciar.bat`**.
* **Via Terminal:**
```bash
  python src/autoclipper.py
  ```

Siga as instruções no painel para colar a URL, selecionar o motor de corte e customizar as legendas.

---

## Estrutura do Projeto

A arquitetura separa a lógica de inteligência da manipulação de mídia:

```text
auto-clipper/
├── bin/                 # Diretório para binários (ffmpeg.exe, ffprobe.exe)
├── luts/                # Diretório para filtros de color grading (.cube)
├── src/                 # Código-fonte principal (Orquestrador, Motores, Estilos)
├── temp/                # Diretório de trabalho (Autolimpável)
│   ├── cortes/          # Clipes isolados em estado bruto
│   ├── legendas/        # Arquivos .ass renderizados
│   └── subs/            # Transcrições em JSON (WhisperX)
├── Instalar.bat         # Script de setup automatizado (Windows)
├── Iniciar.bat          # Script de inicialização (Windows)
└── requirements.txt     # Mapeamento de dependências
```

---

## Como Contribuir

Contribuições para o aprimoramento da ferramenta são bem-vindas:
1. Faça um *Fork* do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/NovaFeature`)
3. Faça o commit das suas alterações (`git commit -m 'Adicionando nova feature'`)
4. Faça o push para a branch (`git push origin feature/NovaFeature`)
5. Abra um *Pull Request*

---

## Suporte e Serviços

Precisou de ajuda com dúvidas, erros ou suporte? Acesse a Central para abrir um protocolo de atendimento.

<div align="center">

[![Central de Atendimento](https://img.shields.io/badge/ACESSAR_CENTRAL_DE_ATENDIMENTO-24292e?style=for-the-badge&logo=github&logoColor=white)](https://github.com/samuelbovef/suporte)

</div>

---

Distribuído sob a licença **MIT**. É permitida a utilização, modificação e distribuição comercial, desde que mantidos os avisos originais.
