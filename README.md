# <BH1750> — Sensores na BitDogLab

**Dupla:** Lívia Viana (206505 / @l206505-maker), Helena Mitsutani (187828 / @helenamit)  
**Turma:** EA801 — 2025S2  
**Repositório:** ([URL deste repo](https://github.com/l206505-maker/sensor_-bh1750-_-viana-_-mitsutani-/edit/main/README.md))

## 1. Descrição do sensor
- Fabricante / modelo: ROHM Semiconductor / BH1750FVI
- Princípio de funcionamento: Sensor digital de intensidade luminosa que utiliza um fotodiodo e um conversor ADC integrado para medir a luz ambiente. O sensor converte a luz incidente em sinal elétrico e processa digitalmente através de interface I2C.
- Tensão/consumo típicos: 2.4V - 3.6V (3.3V recomendado)
                          Corrente consumida: 120μA em operação, 1μA em modo sleep
- Faixa de medição / resolução: 1 - 65535 lux
                                Resolução: 1 lx (alta precisão), 0.5 lx (alta precisão mode 2)
- Datasheet (URL): https://www.mouser.com/datasheet/2/348/bh1750fvi-e-186247.pdf

## 2. Conexões de hardware
- Tabela indicando as conexões entre BitDogLab e sensor:
  
| Pino BitDogLab | Pino BH1750 | Função        | Observações                     |
|----------------|-------------|---------------|---------------------------------|
| 3.3V           | VCC         | Alimentação   | Tensão de operação 3.3V         |
| GND            | GND         | Terra         | Referência comum                |
| GPIO21         | SDA         | Dados I2C     | Serial Data                     |
| GPIO22         | SCL         | Clock I2C     | Serial Clock                    |
| GND            | ADDR        | Endereço I2C  | Define endereço como 0x23       |

- Observações (resistores, alimentação externa, níveis lógicos):

- Resistores: Não são necessários resistores externos, pois a BitDogLab já possui pull-ups no barramento I2C
- Alimentação: Utilizar exclusivamente 3.3V da BitDogLab - não conectar em 5V
- Níveis lógicos: Compatível com 3.3V da BitDogLab
- Endereço I2C:
    ADDR conectado ao GND: endereço 0x23 (padrão)
    ADDR conectado ao VCC: endereço 0x5C
- Interface: Comunicação puramente digital via I2C, não requer componentes externos adicionais

**Tabela de conexões (imagem em `docs/`):**  
![conexoes](docs/conexoes.jpg)

## 3. Dependências
- MicroPython/C versão: Arduino IDE 2.x / ESP32 Arduino Core
- Bibliotecas utilizadas: - `Wire.h` (biblioteca I2C nativa do Arduino)
                          - `BH1750.h` (biblioteca específica para o sensor)
- Como instalar (passo a passo):

### Instalação manual (GitHub):
1. Acesse: https://github.com/claws/BH1750
2. Baixe o repositório como ZIP
3. No Arduino IDE: **Sketch** → **Incluir Biblioteca** → **Adicionar Biblioteca .ZIP...**
4. Selecione o arquivo ZIP baixado

### Verificação da instalação:
Após a instalação, verifique se a biblioteca está disponível em:
**Arquivo** → **Exemplos** → **BH1750** → **BH1750test**

## 4. Como executar
```bash
# MicroPython (Thonny): copiar src/main.py para a placa e rodar
# C (Pico SDK): ver docs/compilacao.md
```

## 5. Exemplos de uso
- `src/exemplo_basico.py` — leitura bruta  
- `src/exemplo_filtrado.py` — leitura com média móvel  
- `test/` — códigos de teste com instruções  

## 6. Resultados e validação
- Prints/plots, fotos do setup, limitações, ruídos, dicas.

## 7. Licença
- Ver arquivo `LICENSE`.

---

> **Checklist de entrega**
> - [ ] README preenchido  
> - [ ] Foto/diagrama em `docs/`  
> - [ ] Código comentado em `src/`  
> - [ ] Testes em `test/` com instruções  
> - [ ] `relatorio.md` com lições aprendidas

## 📁 7. Estrutura do Repositório

O projeto segue o padrão definido pela disciplina EA801 — Sistemas Embarcados, 
visando padronizar as entregas e facilitar o reuso dos códigos e documentação.

Todos os arquivos de código devem estar em src/.
Diagramas, fotos, gráficos e documentos vão em docs/.
Scripts ou logs de teste ficam em test/.
O relatório técnico (relatorio.md) documenta todo o processo de engenharia.

Mantenha os nomes dos arquivos em minúsculas, sem acentos ou espaços, usando _ ou -.

```text
template_sensor/
├── README.md          → Descrição completa do projeto (sensor, ligações, execução e checklist)
├── relatorio.md       → Relatório técnico da dupla (resultados, análise e conclusões)
├── LICENSE            → Licença MIT de uso e distribuição
├── .gitignore         → Regras para ignorar arquivos temporários e binários
│
├── docs/              → Documentação e mídias
│   ├── ligacao.jpg    → Diagrama ou foto da ligação na BitDogLab
│   ├── esquema.pdf    → Esquemático opcional
│   └── outros arquivos de apoio
│
├── src/               → Códigos-fonte principais
│   ├── main.py        → Código principal (MicroPython)
│   ├── main.c         → Versão alternativa (C / Pico SDK)
│   ├── exemplos/      → Códigos ilustrativos adicionais
│   └── bibliotecas/   → Drivers, módulos auxiliares
│
└── test/              → Testes e validações
    ├── test_basico.py → Teste de leitura e resposta do sensor
    ├── test_ruido.py  → Avaliação de ruído ou estabilidade
    └── logs/          → Registros experimentais, dados e gráficos

```
