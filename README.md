# resumo-do-lab
Resumo do lab Microsoft Azure 

# Módulo 1 - Conceitos Iniciais de Cloud com Azure

## Curso Benefícios da Computação em Nuvem

### Aula Localizando Serviços por Categoria

Nessa aula aprendemos:
* Como mudar idioma do portal do Azure
* Mudar o tema(cor) do portal do Azure
* Como visualizar os recursos do Azure por Categoria.

Na Categoria - Rede
* Bastions - rede segura funciona como um Jump Server
* Firewall
* Armazenamento - Migração

* Quando constar como Versão Prévia (não é recomendado usar em base de produção)

### Aula Criando máquinas Virtuais na Azure
* SLA - existem diversos SLAs disponíveis conforme a redunância necessária, quando maior o SLA menor o tempo indisponível e mais caro o serviço
  
## Curso Tipos de Serviço de Nuvem na Azure
* IaaS – Infraestrutura como serviço, mais flexível, mais responsabilidades do contratante.
* PaaS – Plataforma como serviço, focado no desenvolvimento de apps, menos responsabilidades do contratante.
* SaaS – Software como serviço, pouca flexibilidade, poucas responsabilidades do contratante.

Modelo de responsabilidade compartilhada:

![image](https://github.com/user-attachments/assets/a2b6c1ba-1eb8-485c-9574-9a646fb44405)


# Módulo 2 - Arquitetura e Serviços Azure

## Curso Componentes de Arquitetura do Azure
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


### Aula – Configurando Recursos e Dimensionamentos em Máquinas Virtuais na Azure
### Laboratório - Máquinas virtuais:
* Cada Zona = 1 datacenter.
* Desconto Spot do Azure – Utilizar a carga de trabalho ociosa do Azure, pode desligar a máquina se o Azure precisar da capacidade computacional para cliente pagante preço normal, usar apenas em desenvolvimento.
* Para desligar e ligar automaticamente – tem que fazer conta de serviço, pois por padrão só tem o desligar automaticamente.
* Tipo de Host – Pessoal ou Em pool

## Curso Armazenamento no Azure

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

### Armazenamento no Azure - Laboratório
Compartilhamento de arquivos – protocolo SMB porta 445, observar que existem provedores que bloqueiam essa porta.
Migrações para Azure – tem opção para criar projeto de migração de dados para o Azure (Discovery and Assessment)
É possível simular para ver o custo, inclusive para grandes volumes de dados através do DataBox.

Para testes do AzCopy:
* Dentro do storage account – criar contêiner
* Token de acesso compartilhado – criar com permissões para Ler, Adicionar, Criar, Gravar, Excluir, Lista e Armazenamento imutável.
* Gerar Token SAS
* Copiar conteúdo gerado no campo URL de SAS do blob

Sintaxe do AzCopy, exemplo:  
c:\azcopy\azcopy.exe copy "c:\seusdados" "<URL de SAS do blob" --recursive=true  
Vai mostrar resumo no final, exemplo:  
![image](https://github.com/user-attachments/assets/4e0b3227-4401-4bd0-8035-8fec4844cc39)

 

Outra forma com sincronização de dados é através do:
Gerenciador de Armazenamento do Microsoft Azure (storage-explorer)
É possível baixar pelo site https://azure.microsoft.com/en-us/products/storage/storage-explorer
Ferramenta gráfica que usa AzCopy por trás.


## Curso Identidade - Acesso - Segurança

Serviços de diretórios – Entra ID, Entra Domain
Métodos de autenticação – Logon único SSO, MFA, sem senha(exemplo Windows Hello).
Modelos de segurança

Identidades Externas e acesso a convidado.
Acesso condicional do Entra – baseado em sinais.

Controle de Acesso baseado em função (RBAC)

Conceito de confiança zero.
Modelo de defesa em profundidade.
Microsoft Defender para nuvem.


### Aula Microsoft Entra ID e Domain Services
Serviço de gerenciamento de identidades e acesso baseado em nuvem do Azure.
Semelhante ao antigo Active Directory.
Domínio Gerenciado na nuvem – é possível replicar os novos usuários do AD Local para a Nuvem, mas usuários criados na nuvem não integram com AD Local, é possível integrar apenas alterações de senha.

### Aula Autenticação e Autorização
Autenticação – identifica a pessoa ou serviço buscando acesso a um recurso
Autorização – Determina o nível de acesso de uma pessoa ou serviço autenticado.
MFA – Autenticação multifator – algo que você sabe, algo que você possui e algo que você é.
B2B – ID externa do Microsoft Entra, parceiros, fornecedores outros colaboradores.
Azure AD B2C – Consumidores do seu aplicativo privado. Autenticação pelo ID do Facebook, Google por exemplo.

### Aula Acesso Condicional
Associação de usuário ou grupo
Local do IP, Dispositivo, Aplicativo, Detecção de risco.

Controle de acesso baseado em função - RBAC (rule base access control)
Gerenciamento de acesso de granularidade fina.
Definir tarefas dentro da equipe e permitir somente a quantidade necessária.
Habilitar acesso ao portal do Azure e o controle de acesso aos recursos.
Acesso herdável:
	Assinatura
		Grupo de recursos

Ou seja, se tive acesso a Assinatura, terá acesso a tudo que está abaixo dela.

Confiança Zero – Protege os ativos em qualquer lugar com uma política central, criar várias camadas de segurança.
Ataques contra uma camada são isolados das camadas subsequentes.
Defender para Cloud – aplicação cloud native, proteção contra ameaças nos datacenters Azure e locais. Analisa também AWS e GCP.
Faz recomendações de segurança;
Detectar e bloquear malware;
Analisar e identificar ataques potenciais;
Controle de acesso just-in-time para portas.


### Aula Laboratório Identidade - Acesso - Segurança
No Entra ID, depois de excluir um usuário, pode recuperar em até 30 dias.
Entra Connect – sincronismo on-premise(local) com azure cloud
Informar o domínio próprio da empresa em Custom domain names.
Health(Preview) – SLA
Access Control IAM – Permissões se dá por Grupo de Recursos ou direto no Recurso.
Defender for cloud – Cloud Native, visão geral de segurança, recomendações, multi-cloud, híbrido. DevOps Security

