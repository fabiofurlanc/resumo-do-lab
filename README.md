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


# Módulo 3 Gerenciamento e Governança na Azure
## Curso Gerenciamento de Custos na Azure
### Aula Fatores que Afetam os Custos
Gerenciamento de custos:
Calculadora de custos e preços
Gerenciamento de custos e marcas
TCO (Custo total de propriedade)

Fatores que afetam os custos:
1.	Tipo de recurso – Máquina virtual, pasta compartilhada, banco de dados.
2.	Consumo – conforme o modelo pode ser mais barato, exemplo pago conforme o uso(pay as you go) por horas tem um custo, com previsão de tempo de uso do recurso modalidade reserva por 3 meses tem outro custo.

Aula Fatores que Afetam os Custos e Azure Marketplace
3.	Manutenção - Monitorar seu volume no Azure e manter seu ambiente pode ajudá-lo a identificar e reduzir os custos não necessários, exemplos: como deligar máquinas virtuais subutilizadas, downgrade na máquina, etc.
4.	Área geográfica – O mesmo tipo de recurso tem custos diferentes dependendo da área geográfica.
5.	Tráfego de rede – Algumas transferências de dados são cobradas por volume e é afetado por zonas de cobrança.
6.	Assinatura – O tipo e a configuração da assinatura, por exemplo a avaliação gratuita permite explorar alguns recursos.

Marketplace – Permite que os clientes encontrem, experimentem, comprem e provisionem aplicativos e serviços de centenas de provedores de serviços, que são certificados para execução no Azure. Existem mais de 10.000 itens listados. Caso você use um recurso não nativo da Azure no caso de suporte não será com a Microsoft e sim com o Fornecedor/Desenvolvedor do recurso.


### Aula Calculando o Custo Total no Azure

Calculadora de preços – Faz estimativa de custos nem sempre será o valor exato que será cobrado quando criar o recurso de fato.
Gera um relatório.

Calculadora de custo total de propriedade (TCO) – Exemplo se a empresa quer ir para a nuvem, compara custos de infraestrutura local x nuvem, para estimular a economia de custos.

Gerenciamento de Custos do Azure – Monitorar, definir orçamento de gastos, colocar alertas de custo, recomendações de custo, Budget.

### Aula Marcas (Tags) no Azure

Fornecem metadados aos recursos.
Organizam os recursos em uma taxonomia de maneira lógica.  
Consiste em um par nome-valor.  
Úteis para reunir informações de cobrança.  
Facilitar a identificação na fatura, ajuda a filtrar na fatura.  
Não é obrigatório, se não informado o Azure adiciona um nome padrão.  
Não é herdável.  
Exemplos de marca:  
1)Nome Centro de custo  
    Valor Marketing  
  
2)Nome proprietário  
    Valor João  

### Aula Gerenciamento de Custos - Laboratório  
Simulações com a mesma máquina, alterando licenciamento, tipo de uso, modelo reserva, vimos que o custo muda muito.


## Curso Primeiros Passos com Governança e Conformidade na Azure
### Aula Blueprints, Políticas e Bloqueios de Recurso
Governança e conformidade:  
Azure policy – Impõe padrões para a organização de conformidade de recursos, exemplo determinar regiões permitidas ou não permitidas, regra acima de qualquer pemissionamento, inclusive owner será abrangido, pode ser relacionada com grupos de recursos, assinaturas.
Pode criar policy e deixar desativada.
Estados(Status) da policy:
* Non-compliant (não está dentro do compliance) - se tentar algo não permitido vai apresentar mensagem. Inclusive avalia recursos já criados antes da policy, portanto não permiti criar novos recursos mas os já existente funcionam mas ficam nesse estado.
* Remediation (remediação) – Permite efetuar alguma alteração para permitir algo, por exemplo criar tag em recurso.
* Compliant (Em compliance) – Significa que todos os recursos estão em conformidade com a policy do escopo aplicado.


### Aula Gerenciando Bloqueios de Recursos
Bloqueios de recurso – Permite por exemplo proteger um grupo de recursos de exclusão ou modificação acidental. Manter o estado do recurso, usar com cautela, por exemplo se existem scripts que criam e excluem recursos, pode ser usado em nível de assinatura, grupo de recursos e em recursos.  
![image](https://github.com/user-attachments/assets/0f8f320f-20ee-43f0-bfb5-d855df540dc6)
  
 
Se atribuir bloqueio de recurso direto no recurso ao mover esse recurso para outro grupo de recursos o bloqueio também vai.

Portal de confiança do serviço – Local onde a Microsoft publica as informações relacionadas a quais as estratégias a Microsoft segue por exemplo para proteção de dados, validação de conteúdos de IA, protocolos e leis relativos a informações de seus clientes, portanto pode ser utilizado inclusive para auditorias.
https://servicetrust.microsoft.com

Microsoft Purview – Família de soluções de governança, risco e conformidade. Exemplo identificar em um banco de dados, quem tem acesso a uma tabela, campos, quem pode alterar. Reúne insights sobre seus dados locais, multinuvem e de software como serviço.
Descoberta de dados  
Classificação dos dados  
Linhagem de ponta a ponta (Ciclo de vida dos dados) 

### Aula Gerenciando Políticas em Acessos Azure - Laboratório  
Foi testado bloqueio de recursos.  
Foi demonstrado Microsoft Purview – Inclusive tem ferramentas adicionais como Microsoft Priva que pode ser usado por exemplo para LGPD. Ferramentas de auditoria. Ajuda a identificar pontos de segurança e compliance.  
Policy – Habilitada/Desabilitada.  


## Curso Ferramentas de Gerenciamento e Implantação Azure
### Aula Ferramentas de Gerenciamento e Implantação
Portal do Azure  
Azure Cloud Shell / Azure PowerShell - Usa comandos do PowerShell.
CLI (Interface de linha de comando) - Usa comandos Bash.
Azure Arc - Multicloud, permite fazer gestão de máquinas on-premise e que estão hospedadas em outro cloud AWS(Amazon), GCP(Google), permite criar, atualizar e excluir recursos na assinatura do Azure.
ARM (Azure Resource Manager) Template - Camada de gerenciamento.

Infraestrutura como código – Consistência na implantação, configuração em escala.  Provisionar rapidamente ambientes com base em configuração.

Modelos de ARM – são arquivos JSON(Javascript Object Notation) que podem usados para criar e implantar a infraestrutura no Azure sem a necessidade de escrever comandos de programação.  

Azure Bicep – Linguagem nativa Microsoft, comandos não aceitos para outras nuvens.

### Aula Ferramentas de Implantação na Azure - Laboratório
Para entrar no Azure Shell tem que ter storage account na assinatura.


## Curso Ferramentas de Monitoramento do Azure  
### Aula Ferramentas de Monitoramento do Azure

Assistente do Azure – Cloud Native analisa recursos implantados e faz recomendações para otimizar implantações do Azure, principais pontos analisados:    
	Confiabilidade  
	Segurança  
	Desempenho
	Custo  
	Excelência Operacional

Integridade do Serviço do Azure – Possibilidade de degradação status de serviços que podem afetar você, exibição focada nos serviços e regiões que você está usando.  
	Resource Helth – exibição personalizada dos recursos reais do Azure. Fornece informações sobre a integridade de seus serviços em nuvem individuais.  

Azure Monitor – Maximiza a disponibilidade e desempenho de aplicativos e serviços coletando, analisando e tomando decisões com base na telemetria da nuvem e de ambientes locais.  Azure Log Analytics, Alertas e Application Insights.


### Aula Ferramentas de Monitoramento do Azure – Laboratório
Advisor – Centro de recomendações e insights.



