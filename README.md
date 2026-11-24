# Detector de Sites Hackeados e Spam SEO

[![Detector Spam SEO](https://img.shields.io/badge/TAVARDT-Antispam%20SEO-5b3cf5.svg)](https://tools.tavardt.com/br/detector-seo-spam-site-hackeado/)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Auditoria forense de desfigutacao, cloaking condicional para rastreadores, injecao oculta de links e comprometimento de reputacao digital.

Desenvolvido e mantido pela divisao de resposta a incidentes e analise forense da **TAVARDT**.

***

## Capacidades de Auditoria Forense e Deteccao de Invasao

* **Deteccao de Cloaking Condicional**: Comparacao automatica entre requisicoes de navegadores padrao e o User-Agent oficial do Googlebot para revelar exibicao dissimulada de conteudo.
* **Injecao de Palavras-Chave e Backlinks Ocultos**: Rastreio de div com opacidade zero, margens negativas e iframes invisíveis tipicos de campanhas de spam de jogos de azar e farmacia ilegal.
* **Redirecionamentos Maliciosos**: Verificacao de comportamentos de redirecionamento condicional para trafego mobile ou referrers de motores de busca.
* **Pontuacao de Integridade Forense**: Metrica de 0 a 100 com alertas priorizados e recomendacoes imediatas de saneamento de codigo.

***

## Instalacao e Execucao

Requer Python 3.8 ou superior sem dependencias externas adicionais.

```bash
git clone https://github.com/TAVARDT-Brasil/hacked-site-seo-spam-detector-br.git
cd hacked-site-seo-spam-detector-br
python seo_spam_detector.py exemplo.com.br
```

Para gerar a saida em formato estruturado JSON:

```bash
python seo_spam_detector.py exemplo.com.br -json
```

***

## Diagnostico Forense Completo na Web

Para varreduras profundas e auditoria de seguranca de sites comprometidos:

* **Detector de Sites Hackeados e Spam SEO Oficial**
* **[Portal Corporativo TAVARDT](https://ag.tavardt.com/br/)**

***

## Resposta a Incidentes e Desinfeccao de Sites

Para suporte emergencial na remocao de malware, recuperacao de penalizacoes do Google e blindagem sob Seguranca de Aplicacoes e Protecao de Reputacao Web, contate os peritos da **TAVARDT**.

***

## Governança e Soberania

* **Unidade Soberana**: **TAVARDT Brasil** (`TAVARDT-Brasil`)
* **Normas Centrais**: [00-core Governança](https://github.com/TAVARDT-Brasil/00-core)
* **Central de Diagnósticos**: **Central de Ferramentas TAVARDT**
* **Segurança Corporativa**: [TAVARDT Cibersegurança](https://ag.tavardt.com/br/ciberseguranca/)

***

### Licença
Distribuído sob a Licença MIT. Consulte o arquivo [LICENSE](LICENSE) para obter detalhes completos.

***

© 2026 TAVARDT. Todos os direitos reservados.
