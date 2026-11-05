# Módulo de Monitoramento Visual

Este repositório executa, como ponto de entrada principal, exclusivamente o monitoramento de atenção e dispersão por meio de webcam. Ele não controla a aplicação do estudo: sua função é observar o participante em paralelo e registrar intervalos temporais para posterior sincronização.

## Execução

```powershell
.venv\Scripts\python.exe main.py --participant-id P001
```

A execução começa com a calibração de cinco pontos, com duração de 3 segundos por ponto. Os primeiros 0,5 segundos de cada fixação são descartados. Em seguida, uma janela de diagnóstico apresenta um dos seguintes estados: `EM_FOCO`, `DISTRACTION_GAZE`, `DISTRACTION_COGNITIVE` ou `SLEEPY`.

Para encerrar a execução, pressione `Q` ou `Esc`. Caso exista algum evento em aberto, ele será finalizado automaticamente.

Os arquivos são gravados continuamente no diretório `monitoring_logs/`, nos formatos CSV e JSON. Recomenda-se utilizar um identificador pseudonimizado para cada participante.

### Opções importantes

- `--camera 1`: seleciona outra webcam.
- `--aoi 0.1,0.1,0.9,0.9`: delimita a área de interesse (coordenadas normalizadas).
- `--no-preview`: realiza o monitoramento sem manter a janela de visualização da webcam após a calibração.
- `--cognitive-threshold 0.0004`: ajusta o limiar empírico de variância.
- `--output caminho`: altera o diretório de armazenamento dos registros.

O sistema solicita uma resolução de 1280 × 720 pixels e uma taxa de 30 FPS, além de exibir a latência por quadro na janela de visualização. A taxa efetiva depende das características da webcam e do computador utilizado. A distância recomendada entre o participante e a câmera é de 60 a 75 cm.

## Testes

```powershell
.venv\Scripts\python.exe -m unittest discover -s tests -v
```

O limiar de detecção de distração cognitiva é empírico e deve ser validado de acordo com o protocolo do estudo. Os eventos registrados pelo sistema não constituem uma avaliação clínica do participante.
