# Índice
- [Criando sua VPC](#criando-sua-vpc)
- [Criando seu grupo de segurança](#configurando-seu-grupo-de-segurança)
- [Criando seu par de chaves pública e privada](#criando-seu-par-de-chaves-pública-e-privada)
- [Criando sua primeira instância](#criando-sua-primeira-instância)
- [Criando seu Ip elástico](#criando-seu-ip-elástico)
# Criando sua vpc
------------
1.Faça login na sua conta da AWS em [Amazon AWS](https://aws.amazon.com).</br>
2.Acesse a opção VPC [no console da AWS](https://console.aws.amazon.com/vpc/).</br>
3.Clique em Criar VPC.</br>
4.Em configurações de VPC seleciona Somente VPC.</br>
5.Preencha com as seguintes informações:
<dl>
  <dt>Tag de Nome</dt>
  <dd><code>VPC-AtividadePratica-01</code></dd>
  
  <dt>Bloco CIDR IPv4</dt>
  <dd><code>172.31.0.0/16</code></dd>

  <dt>Bloco CIDR IPv6</dt>
  <dd><code>Nenhum bloco CIDR IPv6</code></dd>
  
  <dt>Locação</dt>
  <dd><code>Padrão</code></dd>
</dl>
6.Clique em criar VPC

# Configurando seu grupo de segurança
------------
1.Acesse a opção EC2 no [console da AWS](https://console.aws.amazon.com/ec2/).</br>
2.Clique em Security Group.</br>
4.Clique no  grupo de segurança desejado</br>
5.Adicione uma tag de nome ao grupo default :
<dl>
  <dt>Nome do grupo de segurança</dt>
  <dd><code>SG-AtividadePratica-01</code></dd>
</dl>
6.Clique em Editar regras de entrada</br>
7.Adicione as seguintes informações:
<img src="https://user-images.githubusercontent.com/54165905/214590529-5a23468e-be0d-4da3-a4c1-370e34afda41.png">
8.Clique em salvar regras

# Criando seu par de chaves pública e privada
------------
1.Acesse a opção EC2 no [console da AWS](https://console.aws.amazon.com/ec2/).</br>
2.CLique em Pares de chaves.</br>
3.Clique em criar par de chaves.</br>
4.Preencha as seguintes informações:
<dl>
  <dt>Nome</dt>
  <dd><code>atividade-key</code></dd>
  
  <dt>Tipo de Par de chave</dt>
  <dd><code>RSA</code></dd>

  <dt>Formato de arquivo de chave privada</dt>
  <dd><code>.pem</code></dd>
</dl>
5.Clique em criar criar par de chaves

# Criando sua primeira instância
-----------
1.Acesse a opção EC2 no [console da AWS](https://console.aws.amazon.com/ec2/).</br>
2.Clique em Executar Instâncias</br>
3.Preencha as informações:
<dl>
  <dt>Nomes e Tags</dt>
  <dd><code>Name:Seunome Project:PB CosCenter:PBCompass</code></dd>
  
  <dt>Imagem da máquina da Amazon</dt>
  <dd><code>Amazon Linux</code></dd>

  
  <dt>Tipo de Instância</dt>
  <dd><code>t3.small</code></dd>
   
  <dt>Key pair</dt>
  <dd><code>atividade-key</code></dd>
   
  <dt>Configuração de rede</dt>
  <dd><code>Selecionar grupo de segurança existente</code></dd>
   
  <dt>Configuração de Armazenamento</dt>
  <dd><code>1x 16gb GIB gp2</code></dd></br>
  4.Clique em Executar Instância</br>


# Criando seu Ip elástico
------------
1.Acesse a opção EC2 no [console da AWS](https://console.aws.amazon.com/ec2/).</br>
2.Clique em IPs Elásticos
3.Alocar endereço Ip elástico
4.Preencha as seguinte informações:
<dl>
  <dt>Grupo de Borda de Rede</dt>
  <dd><code>us-east1</code></dd>
  
  <dt>Conjunto de endereços IPv4 públicos</dt>
  <dd><code>Conjunto de endereços IPv4 da Amazon</code></dd>

  <dt>Tags opcional</dt>
  <dd><code>Project:PB CosCenter:PB</code></dd>
</dl>
5.Clique em ALocar.</br>
6.Selecione o IP elástico, clique em ações e associar o enderço IP elástico.</br>
7.Preencha as seguinte informações:
<dl>
  <dt>Tipo de Recurso</dt>
  <dd><code>Instância</code></dd>
  
  <dt>Instância</dt>
  <dd><code>Selecione a instância desejada</code></dd>

  <dt>Endereço Privado</dt>
  <dd><code>Selecione o ip privado relacionado a instância</code></dd>
</dl>
8.Clique em associar.

