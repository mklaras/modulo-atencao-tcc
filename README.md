# Modulo de monitoramento visual

Este repositorio executa, como ponto de entrada principal, somente o monitor de
atencao/dispersao por webcam. Ele nao controla a aplicacao do estudo: observa o
participante em paralelo e registra intervalos temporais para sincronizacao posterior.

## Execucao

```powershell
.venv\Scripts\python.exe main.py --participant-id P001
```

A execucao comeca com a calibracao de cinco pontos (3 segundos por ponto). Os
primeiros 0,5 segundos de cada fixacao sao descartados. Depois, uma janela de
diagnostico mostra `EM_FOCO`, `DISTRACTION_GAZE`, `DISTRACTION_COGNITIVE` ou
`SLEEPY`. Pressione `Q` ou `Esc` para encerrar e fechar um evento ainda aberto.

Os arquivos sao gravados continuamente em `monitoring_logs/`, nos formatos CSV e
JSON. Use um identificador pseudonimizado para o participante.

Opcoes importantes:

- `--camera 1`: seleciona outra webcam;
- `--aoi 0.1,0.1,0.9,0.9`: limita a area de interesse (coordenadas normalizadas);
- `--no-preview`: monitora sem manter a janela da webcam depois da calibracao;
- `--cognitive-threshold 0.0004`: ajusta o limiar empirico de variancia;
- `--output caminho`: altera a pasta dos logs.

O sistema solicita 1280x720 a 30 FPS e mostra a latencia por quadro no preview. A
taxa efetiva depende da webcam e do computador. A distancia recomendada e 60--75 cm.

## Testes

```powershell
.venv\Scripts\python.exe -m unittest discover -s tests -v
```

O limiar de distracao cognitiva e empirico e deve ser validado no protocolo do
estudo. Os eventos gerados nao constituem avaliacao clinica do participante.
