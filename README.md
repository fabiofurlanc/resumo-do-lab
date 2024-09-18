# resumo-do-lab
Resumo do lab Microsoft Azure 

# Módulo 1 - Conceitos Iniciais de Cloud com Azure

## Aula Localizando Serviços por Categoria

Nessa aula aprendemos:
* Como mudar idioma do portal do Azure
* Mudar o tema(cor) do portal do Azure
* Como visualizar os recursos do Azure por Categoria.

Na Categoria - Rede
* Bastions - rede segura funciona como um Jump Server
* Firewall
* Armazenamento - Migração

* Quando constar como Versão Prévia (não é recomendado usar em base de produção)

## Aula Criando máquinas Virtuais na Azure
* SLA - existem diversos SLAs disponíveis conforme a redunância necessária, quando maior o SLA menor o tempo indisponível e mais caro o serviço
  
## Aula Tipos de Serviço de Nuvem na Azure
* IaaS – Infraestrutura como serviço, mais flexível, mais responsabilidades do contratante.
* PaaS – Plataforma como serviço, focado no desenvolvimento de apps, menos responsabilidades do contratante.
* SaaS – Software como serviço, pouca flexibilidade, poucas responsabilidades do contratante.

Modelo de responsabilidade compartilhada:

![image](https://github.com/user-attachments/assets/a2b6c1ba-1eb8-485c-9574-9a646fb44405)


# Módulo 2 - Arquitetura e Serviços Azure

## Aula Componentes de Arquitetura do Azure
* Regiões – compostas por um ou mais datacenters próximos
Flexibilidade e escala para reduzir a latência.

* Zona de disponibilidade – redundância entre regiões e também no próprio datacenter.
* Datacenters – conectados entre fibras privadas.
* Pares de regiões – no mínimo 300 milhas(480 km) de separação entre pares
  https://learn.microsoft.com/pt-br/azure/reliability/cross-region-replication-azure
* Regiões soberanas - Serviços governamentais dos EUA e Azure China
* Grupos de Recursos - não se limita a tipo de recursos ou região.
* Assinaturas - recomendado separar por exemplo uma para cada cenário:
    * Assinatura de desenvolvimento
    * Assinatura de teste
    * Assinatura de produção
    Uma conta pode ter diversas assinaturas, mas uma assinatura só pode pertencer a uma conta. Para cada assinatura tem uma fatura.

* Hierarquia:  
  -- Grupos de Gerenciamento  
  --- Assinaturas  
  ---- Grupos de Recursos  
  ----- Recursos  

Assinaturas herdam as condições aplicadas ao grupo de gerenciamento.

Global Infrastructure | Microsoft Azure https://azure.microsoft.com/en-us/explore/global-infrastructure


## Aula – Configurando Recursos e Dimensionamentos em Máquinas Virtuais na Azure
### Laboratório - Máquinas virtuais:
* Cada Zona = 1 datacenter.
* Desconto Spot do Azure – Utilizar a carga de trabalho ociosa do Azure, pode desligar a máquina se o Azure precisar da capacidade computacional para cliente pagante preço normal, usar apenas em desenvolvimento.
* Para desligar e ligar automaticamente – tem que fazer conta de serviço, pois por padrão só tem o desligar automaticamente.
* Tipo de Host – Pessoal ou Em pool

## Aulas - Armazenamento no Azure

* Contas de armazenamento(storage acount)
Nome exclusivo global
Redundância  
LRS – Redundância local (3 cópias mesmo datacenter) – Durabilidade 11 noves
ZRS – Redundância de zona (3 cópias em datacenters diferentes) - Assíncrono Durabilidade 12 noves 
GRS – Redundância geográfica (cópia também fora da região) Durabilidade 16 noves
GZRS – Redundância de zona geográfica Durabilidade 16 noves

* Tipos de dados:
Blob – Dados não estruturados: texto ou dados binários.
Disco do Azure.
Fila do Azure – cada uma com até 64 kb.
Arquivos do Azure(files) – configura compartilhamento de arquivos de rede.
Tabelas do Azure – opção de chave/atributo armazenamento de dados estruturados não relacionais sem esquema.

* Pontos de Extremidades Públicos:
Para blob – https://<nome do storage account>.blob.core.windows.net
Data Lake Storage Gen2 – https://<nome do storage account>.dfs.core.windows.net
Arquivos – https://<nome do storage account>.file.core.windows.net
Armazenamento de filas – https://<nome do storage account>.queue.core.windows.net
Armazenamento de tabelas – https://<nome do storage account>.table.core.windows.net

* Camadas de acesso:
Frequente – Dados acessados com frequência.
Esporádico – Dados acessados com pouca frequência e armazenado por pelo menos 30 dias
Frio – Dados acessados com pouca frequência e armazenado por pelo menos 90 dias
Arquivo Morto – Dados acessados raramente e armazenado por pelo menos 180 dias com requisitos de latência flexíveis.

* Azure Data Box – Equipamento físico ajuda a levar grande quantidade de dados até 80 TB, usado para grandes volumes, locais remotos ou conectividade limitada.
Tipos: Data Box Disk, Data Box e Data Box Heavy.

* AzCopy – Utilitário de linha de comando, copiar blobs ou arquivos, sincronização em uma direção.

* Gerenciador de Armazenamento do Azure – Interface gráfica semelhante ao Windows Explorer, compatível com Windows, MacOS e Linux.

* Sincronização de Arquivos do Azure – Sincroniza arquivos e locais de forma bidirecional, a camada de nuvem mantém acessados com frequência no loca, e envia os demais para nuvem e manter um apontamento.
