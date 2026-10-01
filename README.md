# Dashboard EFT/EPO

Pacote estático para publicação no GitHub Pages. O dashboard preserva as análises, filtros, hierarquias, validações, área Administrador e exportações do `index.html` concluído.

## Estrutura

```text
.
├── index.html
├── dados/
│   ├── dashboard-config.json
│   ├── EFT-AA-MM.json
│   ├── eft-schema.json
│   └── README.md
├── .github/workflows/pages.yml
├── .gitignore
└── .nojekyll
```

## Publicar no GitHub Pages

1. Crie um repositório e envie todos os arquivos desta pasta para a branch `main`.
2. Em **Settings → Pages**, mantenha **Source: GitHub Actions**.
3. O workflow `pages.yml` publicará o conteúdo estático automaticamente.
4. Aguarde a execução em **Actions** e abra a URL informada pelo GitHub Pages.

## Ativar os dados operacionais

O arquivo `dados/EFT-AA-MM.json` é apenas um modelo vazio, pois nenhuma base operacional foi incluída no material de origem. Para ativar o painel:

1. Abra a aba **Administrador** no dashboard.
2. Selecione uma base `.xlsx`, `.csv` ou `.tsv`.
3. Baixe o JSON gerado, cujo nome segue `EFT-AA-MM.json` (por exemplo, `EFT-26-09.json`).
4. Coloque-o em `dados/`.
5. Atualize `dados/dashboard-config.json` com o nome exato do arquivo.
6. Faça commit e push.

## Teste local

Como o navegador bloqueia `fetch()` de arquivos locais em páginas abertas por `file://`, execute um servidor HTTP simples na raiz do projeto:

```bash
python3 -m http.server 8000
```

Depois abra `http://localhost:8000/`.

## Contrato do JSON

- `schemaVersion`: `1`
- `operationalYear`: `2026`
- `data`: array não vazio
- cada registro deve conter `subcluster`, `un`, `type`, `value`, `month`, `day` e `dateKey`
- `type`: `liquid` ou `non`
- `dateKey`: mês e dia no formato numérico `MMDD`

O esquema completo de referência está em `dados/eft-schema.json`.

## Segurança e privacidade

O pacote não inclui a planilha original, credenciais, tokens ou segredos. O processamento da base na área Administrador ocorre no navegador. Revise o JSON operacional antes de publicá-lo conforme as regras internas de acesso à informação.
