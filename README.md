# Detector de Sites Hackeados e Spam SEO

[![Detector Spam SEO](https://img.shields.io/badge/TAVARDT-Antispam%20SEO-5b3cf5.svg)](https://tools.tavardt.com/br/detector-seo-spam-site-hackeado/)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

O **TAVARDT Detector de Sites Hackeados e Spam SEO** oferece inspeção forense em aplicações web para identificar cloaking direcionado a rastreadores, injeção oculta de links de farmácia ou cassino, iframes não autorizados e códigos ofuscados no Brasil.

***

## Arquitetura de Detecção e Matriz Forense de Vetores

O cloaking e as injeções ocultas de conteúdo manipulam os motores de busca enquanto permanecem invisíveis para visitantes humanos. Esse comprometimento acarreta penalidades manuais imediatas, desindexação no Google e danos severos à autoridade da marca.

Esta ferramenta diagnóstica analisa a divergência de respostas entre diferentes User-Agents, audita blocos CSS ocultos e revela rastreadores invasivos sem depender de bibliotecas externas.

O motor analítico avalia a integridade do DOM, o tamanho das respostas diferenciais e assinaturas de scripts maliciosos a partir de uma base de 100 pontos:

<table>
  <thead>
    <tr>
      <th>Vetor de Comprometimento</th><th>Lógica de Detecção</th><th>Dedução</th><th>Impacto na Integridade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Cloaking Diferencial</strong></td><td>Compara o User-Agent do navegador com o Googlebot. Sinalizado quando a taxa de divergência de bytes for > 0,40 e o delta absoluto > 1000 bytes.</td><td>-30 pts</td><td>Risco crítico de penalização algorítmica e desindexação sumária nas buscas.</td>
    </tr>
    <tr>
      <td><strong>Injeção de Spam Oculto</strong></td><td>Analisa blocos com <code>display:none</code>, <code>opacity:0</code> ou margens negativas contendo termos de cassino e medicamentos ilegais.</td><td>-35 pts</td><td>Indício inequívoco de invasão com injeção de banco de dados ou templates corrompidos.</td>
    </tr>
    <tr>
      <td><strong>iframes Ocultos Suspeitos</strong></td><td>Identifica iframes com largura/altura zero ou estilos ocultos ausentes na lista de parceiros de segurança homologados.</td><td>-20 pts</td><td>Vetor comum para redirecionamentos maliciosos, downloads ocultos e roubo de sessões.</td>
    </tr>
    <tr>
      <td><strong>Código Ofuscado</strong></td><td>Detecta padrões repetidos de execução dinâmica como <code>eval()</code>, <code>unescape()</code> e <code>base64_decode</code> (>2 ocorrências).</td><td>-15 pts</td><td>Comportamento característico de droppers e backdoors persistentes em JavaScript/PHP.</td>
    </tr>
    <tr>
      <td><strong>Falha de Conexão</strong></td><td>Tempo limite de requisição excedido ou falha no handshake TLS/HTTP.</td><td>-20 pts</td><td>Indisponibilidade do host que impede a validação forense completa.</td>
    </tr>
  </tbody>
</table>

### Escala de Integridade e Níveis de Alerta

O utilitário consolida a pontuação de integridade classificando o domínio examinado:

* <strong>85 a 100 (CLEAN)</strong>: Nenhum indício de comprometimento detectado; integridade do DOM e consistência de payload preservadas.
* <strong>60 a 84 (SUSPICIOUS)</strong>: Anomalias estruturais no CSS, iframes não homologados ou variações parciais exigindo auditoria imediata.
* <strong>0 a 59 (COMPROMISED)</strong>: Presença confirmada de cloaking, injeção de links ou scripts ofuscados exigindo saneamento emergencial.

***

## Instalação e Execução

Desenvolvido estritamente com a biblioteca padrão do Python 3.8+, sem dependências externas.

```bash
git clone https://github.com/TAVARDT-Brasil/hacked-site-seo-spam-detector-br.git
cd hacked-site-seo-spam-detector-br
```

### Execução Padrão via CLI

```bash
python seo_spam_detector.py exemplo.com.br
```

### Saída Estruturada para Pipelines em JSON

```bash
python seo_spam_detector.py exemplo.com.br -j
```

### Configuração de Timeout Personalizado

```bash
python seo_spam_detector.py exemplo.com.br -j -t 15
```

***

## Conformidade LGPD e Proteção de Ativos Digitais

O saneamento de invasões e cloaking atende aos requisitos de segurança e governança da **Lei Geral de Proteção de Dados (LGPD)** e normas técnicas brasileiras. Ambientes invadidos colocam em risco dados de clientes e a reputação comercial da marca.

Recomenda-se a inclusão de auditorias automatizadas de integridade do DOM e rastreamento de User-Agents em pipelines de deploy para prevenir comprometimentos não autorizados.

***

## Perguntas Frequentes Técnicas

### Como funciona o algoritmo de detecção de cloaking?

A ferramenta envia duas requisições consecutivas para a URL alvo, uma com User-Agent de navegador moderno e outra simulando o Googlebot oficial. Se a discrepância relativa de tamanho do conteúdo exceder 0,40 com variação absoluta superior a 1000 bytes, o sistema reporta cloaking e deduz 30 pontos.

### O que qualifica um iframe oculto como suspeito?

Qualquer elemento iframe com dimensões zeradas ou atributos de estilo oculto (<code>display:none</code>) que não pertença a serviços de validação legítimos (como Cloudflare, Google reCAPTCHA, Google Tag Manager ou hCaptcha) é marcado como suspeito, gerando dedução de 20 pontos.

### Quais termos de spam são identificados em blocos CSS ocultos?

A análise varre elementos ocultados via <code>display:none</code>, <code>visibility:hidden</code>, <code>opacity:0</code> ou coordenadas negativas extremas buscando palavras como viagra, cialis, casino, payday loan, replica watch, poker, roulette, baccarat, vape e ketamine, aplicando penalidade de 35 pontos.

### Por que códigos com eval e unescape recebem penalidades?

Aplicações web modernas não devem utilizar <code>eval()</code> ou <code>unescape()</code> em páginas de produção. Mais de duas ocorrências dessas funções indicam probabilidade de execução dinâmica de scripts maliciosos injetados por atacantes, gerando dedução de 15 pontos.

### Como integrar a validação do scanner em rotinas automatizadas?

Basta invocar o utilitário com o parâmetro curto <code>-j</code> para obter a resposta estruturada em formato JSON. Essa saída pode ser facilmente consumida por plataformas de monitoramento, pipelines CI/CD ou robôs de alerta de segurança.

***

## Resposta a Incidentes e Desinfecção de Sites

Para suporte emergencial na remoção de malware, recuperação de penalizações do Google e blindagem sob Segurança de Aplicações e Proteção de Reputação Web, contate os peritos da **TAVARDT**.

***

## Links Úteis

* **Portal Corporativo:** https://ag.tavardt.com/br/
* **Suíte de Diagnósticos:** https://tools.tavardt.com/br/
* **Contato Técnico:** https://ag.tavardt.com/br/contato/

***

### Licença
Distribuído sob a Licença MIT.

***

© 2026 TAVARDT. Todos os direitos reservados.
