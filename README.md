# Explora-o-e-corre-o-de-vulnerabilidades-MQTT-Broker
# MQTT Project - Versão Segura
# Sobre o Projeto
Projeto MQTT original do repositório csai4cps/mqtt-project com correções de segurança implementadas para mitigar vulnerabilidades identificadas.

# Vulnerabilidades Corrigidas

1. Autenticação Ausente:

Problema: Broker aceitando conexões anônimas
Correção: Autenticação obrigatória implementada


2. Comunicação Não Criptografada:

Problema: Dados trafegando em texto claro (porta 1883)
Correção: Preparado para TLS na porta 8883


3. Tópicos Públicos sem ACL:

Problema: Acesso livre a todos os tópicos
Correção: Controle de acesso por tópico implementado


# Como Executar:
# Pré-requisitos

Docker
Docker Compose

# Execução com Segurança

# Clone o repositório
git clone https://github.com/seu-usuario/mqtt-project-secure.git
cd mqtt-project-secure

# Execute os containers
docker-compose up -d --build

# Verifique os logs
docker-compose logs -f mqtt-subscriber

# Credenciais para este Acesso:

Usuário: usuario1
Senha: P@ssw0rd123

# Configurações de Segurança Implementadas
# Broker MQTT Seguro

environment:
  - MOSQUITTO_ALLOW_ANONYMOUS=false
  - MOSQUITTO_PASSWORD_FILE=/mosquitto/config/passwd
volumes:
  - ./mosquitto/config/passwd:/mosquitto/config/passwd
  - ./mosquitto/config/aclfile:/mosquitto/config/aclfile

  # Arquivo de ACL

user usuario1
topic read sensor/temperatura
topic write comando/#

# Testando a Segurança
# Teste de Conexão Segura

# Conexão com autenticação (deve funcionar)
mosquitto_sub -h localhost -t "sensor/temperatura" -u "usuario1" -P "P@ssw0rd123"

# Conexão sem autenticação (deve falhar)
mosquitto_sub -h localhost -t "sensor/temperatura"


# Monitoramento

Logs de acesso disponíveis em: docker-compose logs mqtt-broker

Logs de dados dos sensores: docker-compose logs mqtt-subscriber

Logs do sensor de temperatura: docker-compose logs temperature-sensor-1

# Notas de Segurança
# Para Ambiente de Produção:

Alterar as credenciais padrão
Implementar certificados TLS
Configurar ACLs mais restritivas
Habilitar logging detalhado
Atualizar regularmente as imagens Docker

# Melhorias Implementadas:

Autenticação obrigatória
Controle de acesso por tópico
Preparação para TLS
Logs de acesso
Credenciais seguras