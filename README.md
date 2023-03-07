# Índice
- [Criando um gateway para internet](#criando-um-gateway-para-internet)
- [Alterando tabela de rotas](#alterando-tabela-de-rotas)
- [Criando um grupo de Segurança para o Balanceador de Carga](#criando-um-grupo-de-segurança-para-o-balanceador-de-carga)
- [Alterando o grupo de Segurança default](#alterando-o-grupo-de-segurança-default)
- [Criando o grupo de Destino](#criando-o-grupo-de-destino)
- [Criando o Balanceador de Carga](#criando-o-balanceador-de-carga)
- [Criando uma Instância](#criando-uma-instância)
# Criando um gateway para internet
------------
1.Faça login na sua conta da AWS em [Amazon AWS](https://aws.amazon.com).</br>
2.Acesse a opção VPC [no console da AWS](https://console.aws.amazon.com/vpc/).</br>
3.Acesse a opção de Gateways da Internet no menu lateral esquerdo.</br>
4.Clique em Criar gateway da Internet.</br>
5.Preencha com as seguintes informações:
<dl>
  <dt>Tag de Nome</dt>
  <dd><code>my-internet-gateway</code></dd>
</dl>
6.Clique em criar Cria gateway

# Alterando tabela de rotas
------------
1.Acesse a opção VPC [no console da AWS](https://console.aws.amazon.com/vpc/).</br>
2.Clique em Security Group.</br>
3.Acesse a opção de Tabelas de Rotas no menu lateral esquerdo.</br>
4.Selecione a tabela de rotas relacionada a Sub-rede privada A.
5.Clique em Ações em seguida em Editar rotas.</br>
6.Adicione a seguinte entrada na tabela de rotas:
<dl>
  <dt>Destino</dt>
  <dd><code>0.0.0.0/0</code></dd>
  <dt>Alvo</dt>
  <dd><code>Internet Gateway criado anteriormente</code></dd>
</dl>
7.Clique em Salvar alterações</br>

# Criando um grupo de Segurança para o Balanceador de Carga
------------
1.Acesse a opção EC2 no [console da AWS](https://console.aws.amazon.com/ec2/).</br>
2.CLique em Security Groups no menu lateral esquerdo.</br>
3.Clique em Criar grupo de segurança.</br>
4.Preencha as seguintes informações:
<dl>
  <dt>Nome do grupo de segurança</dt>
  <dd><code>SG-Load-Balancer</code></dd>
  
  <dt>Descrição</dt>
  <dd><code>Grupo de seguranca do load balancer</code></dd>

  <dt>VPC</dt>
  <dd><code>Selecione uma VPC existente</code></dd>
</dl>
5.Adicione as seguintes regras de entradas:

| Name | ID da regra do Grupo de Segurança | Versão do IP | Tipo | Protocolo | Intervalo de portas | Origem | Descrição          |
|------|-----------------------------------|--------------|------|-----------|---------------------|--------|--------------------|
| | | IPv4         | HTTP              | TCP       | 80                  | 0.0.0.0/0      | Permite conexao HTTP na porta 80   |

# Alterando o grupo de Segurança default
-----------
1.Acesse a opção EC2 no [console da AWS](https://console.aws.amazon.com/ec2/).</br>
2.CLique em Security Groups no menu lateral esquerdo.</br>
3.Selecione o grupo de segurança default.
4.Clique em Editar regras de entrada.
5.Preencha as informações:
| Name | ID da regra do Grupo de Segurança | Versão do IP | Tipo | Protocolo | Intervalo de portas | Origem | Descrição          |
|------|-----------------------------------|--------------|------|-----------|---------------------|--------|--------------------|
| | | IPv4         | SSH              | TCP       | 22                  | Seu IP aqui    | Permite conexao HTTP na porta 80   |
| | | IPv4         | NFS              | TCP       | 2049                | SG do grupo de segurança default     | Permite conexao HTTP na porta 80   |
| | | IPv4         | HTTP              | TCP       | 80                  | SG do grupo de segurança do load balancer    | Permite conexao HTTP na porta 80   |

6.Clique em Salvar regras

# Criando o grupo de Destino
------------
1.Acesse a opção EC2 no [console da AWS](https://console.aws.amazon.com/ec2/).</br>
2.Acesse a opção de Grupos de destino no menu lateral esquerdo.
3.Clique em Create target group.
4.Preencha as seguinte informações:
<dl>
  <dt>Escolha um tipo de destino type</dt>
  <dd><code>Instâncias</code></dd>
  
  <dt>Nome do grupo de destino</dt>
  <dd><code>Nome que desejar</code></dd>

  <dt>Selecionar VPC</dt>
  <dd><code>Selecione a VPC existente</code></dd>
  
  <dt>Configurações avançadas de verificação de integridade</dt>
  <dd><code>Código de Sucesso:200,302</code></dd>
</dl>
5.Clique em Próximo.</br>
6.Clique em Criar grupo de destino.</br>

# Criando o Balanceador de Carga
------------
1.Acesse a opção EC2 no [console da AWS](https://console.aws.amazon.com/ec2/).</br>
2.Clique em Executar instância.
3.Clique em Create load balancer.
4.Selecione Application Load Balancer e Criar
5.Preencha as seguinte informações:
<dl>
  <dt>Nome do balanceador de cargatype</dt>
  <dd><code>Nome que desejar.</code></dd>
  
  <dt>Esquema</dt>
  <dd><code>Voltado para internet.</code></dd>

  <dt>Selecionar VPC</dt>
  <dd><code>Selecione a VPC existente.</code></dd>
  
  <dt>Mapeamento</dt>
  <dd><code>Zona de disponibilidade:us-east-1a (use1-az2).</code></dd>
  
  <dt>Grupo de segurança</dt>
  <dd><code>Selecione o grupo de segurança criado para o balanceador de carga.</code></dd>
  
  <dt>Listeners</dt>
  <dd><code>Protocol:HTTP; Porta:80; Ação Padrão: Grupo de destino criado</code></dd>
</dl>
6.Clique em criar balanceador de carga

# Criando uma Instância
------------
1.Acesse a opção EC2 no [console da AWS](https://console.aws.amazon.com/ec2/).</br>
2.Clique em Executar instâncias.
3.Preencha as seguintes informações:</br>
<dl>
  <dt>Nomes e Tags</dt>
  <dd><code>Name:Seunome Project:PB CosCenter:PBCompass</code></dd>
  
  <dt>Imagem da máquina da Amazon</dt>
  <dd><code>Amazon Linux</code></dd>

  <dt>Tipo de Instância</dt>
  <dd><code>t3.small</code></dd>
   
  <dt>Key pair</dt>
  <dd><code>atividade-key</code></dd>
   
  <dt>Configuração de rede-Editar</dt>
  <dd><code>VPC:Escolha a VPC existente; Sub-rede:Selecione a sub-rede privada A; Firewall:Selecionar o grupo de segurança default</code></dd>
   
  <dt>Configuração de Armazenamento</dt>
  <dd><code>1x 16gb GiB gp2</code></dd></br>
  
  </dl>
  4.Acesse a aba de Detalhes avançados.</br>
  
  5.Vá a área de Dados do usuário e copie o conteúdo `user_data.sh`para dentro do campo em branco.Esse script será responsável por fazer todas as configurações básicas da instância, incluindo instalação do `Docker` e `Docker Compose` e a montagem do sistema de arquivos `EFS`, ela também iniciará os containers contendo `WordPress` e `MySQL`.

## Para realizar alteração da URL do WordPress, siga esses passos:
1.Acesse a opção EC2 no [console da AWS](https://console.aws.amazon.com/ec2/).</br>
2.Clique em Load balancers no menu lateral esquerdo.</br>
3.Copie o endereço do Load balancer desejado.</br>
4.Acesse o [wp-config.php](https://github.com/luizz567/Compass.uol-Atividade-Docker/tree/main/nfs/LuizGustavo/wordpress) do seu wordpress e adicione as novas variáveis de ambiente(linhas 54,55), que serão responsáveis pela troca do URL do site, depois disso salve o arquivo.</br>
5.Acesse o [docker-compose.yml](https://github.com/luizz567/Compass.uol-Atividade-Docker/blob/main/docker-compose.yml) e adicione o seu novo LoadBalancer a variável de ambiente referente ao url do WordPress(linha 16), depois disso salve o arquivo.</br>
6.Suba os containers novamente com o novo endereço do WordPress.

