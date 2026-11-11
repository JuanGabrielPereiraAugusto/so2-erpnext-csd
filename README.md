# Implantação de ERP de gestão de estoque com substituição do Windows por Linux

Trabalho final da disciplina de **Sistemas Operacionais II (SO2)**, do curso de Análise e Desenvolvimento de Sistemas da **FATEC Taquaritinga**.
Professor responsável: Prof. Marivaldo Aparecido Alcantara.

## Integrantes
- Juan Gabriel Pereira Augusto
- Carlos Eduardo Carvalho Gerônimo
- Vitor Gomes de Oliveira
- Daniel Freire Kim

## Sobre o projeto
Proposta de substituição do Windows pelo Ubuntu LTS nos computadores de uma pequena empresa fictícia, a **Central Sul Distribuidora (CSD)**, com instalação nativa do **ERPNext** (ERP de código aberto) pela ferramenta `bench`, para controle de estoque integrado à contabilidade.

A solução foi validada em laboratório com Ubuntu no **WSL 2** e os serviços do ERPNext em **containers Docker**, orquestrados pelo `pwd.yml` do repositório oficial [frappe_docker](https://github.com/frappe/frappe_docker). Os testes cobriram estoque, contabilidade, rede local, persistência após falha, backup, namespaces e cgroups.

## Conteúdo do repositório
- `documentacao_SO2.pdf`: documentação completa do trabalho.

O arquivo de orquestração `pwd.yml` usado no laboratório é o do repositório oficial [frappe_docker](https://github.com/frappe/frappe_docker), na versão consultada em outubro de 2026. O arquivo atual pode ter pequenas diferenças.

## Como reproduzir o ambiente de laboratório
Requisitos: Windows 10/11 com virtualização habilitada, WSL 2 e Docker Desktop com backend WSL 2.

Limite de recursos do WSL 2 usado nos testes (arquivo `%UserProfile%\.wslconfig`):

```ini
[wsl2]
memory=4GB
processors=2
```

Subida da pilha do ERPNext:

```powershell
git clone https://github.com/frappe/frappe_docker.git
cd frappe_docker
docker compose -f pwd.yml up -d
```

Aguarde a criação do site (`docker compose -f pwd.yml logs -f create-site`) e acesse `http://localhost:8080`. O usuário e a senha padrão são os definidos no `pwd.yml`.

> **Atenção:** o `pwd.yml` usa senhas padrão e HTTP sem criptografia. Serve apenas para testes e estudo, não para produção.

## Implantação proposta para a empresa
Ubuntu Desktop LTS instalado diretamente nos computadores, sem máquina virtual e sem containers, e ERPNext instalado de forma nativa com `bench` em modo de produção (Nginx e Supervisor). Detalhes na documentação, seções 3 e 4.

## Referências principais
- [ERPNext](https://docs.erpnext.com)
- [bench](https://github.com/frappe/bench)
- [frappe_docker](https://github.com/frappe/frappe_docker)
