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



