NeuroScope AVZ – Migração de Arquitetura Monolítica para Microsserviços (Cloudflare Workers)

Este repositório apresenta o projeto de migração do NeuroScope AVZ, originalmente desenvolvido como um sistema monolítico client-side, para uma arquitetura distribuída baseada em microsserviços, utilizando tecnologias ultraleves e processamento local, conforme solicitado pelo professor:

“Tecnologia ultraleve, sem servidores tradicionais e sem APIs pesadas, utilizando processamento local e serviços mínimos em nuvem.”

O repositório contém a versão original do sistema (monolítica), a proposta de migração, a documentação arquitetural e os serviços projetados.

Nota ao Professor Avaliador

Este README foi preparado especialmente para acompanhamento e avaliação deste Projeto Integrador da PUC Goiás – 2025.
A aplicação estará publicada via GitHub Pages, permitindo que o(a) professor(a) realize testes diretamente no navegador.

Para validação do fluxo completo (login → autenticação → acesso ao NeuroScope AVZ), seguem as credenciais de teste criadas apenas para fins acadêmicos durante o período de avaliação:

Usuário: professor_avaliador
Senha: 123456


Estas credenciais são fictícias e não permitem acesso a dados reais.
Servem somente para validar o funcionamento do Auth-Service, token e integração com o sistema.

1. Objetivo

Apresentar a migração do NeuroScope AVZ — anteriormente um único arquivo HTML/JS que acessava câmera e gravava vídeos — para uma arquitetura distribuída baseada em Cloudflare Workers, mantendo a filosofia dos sistemas desenvolvidos por mim:

local-first

serverless leve

segurança essencial

performance em edge computing

1.1 Objetivos Específicos

Criar microsserviços essenciais (Auth, Video, Patient, Pro, Notify)

Implementar login antes da gravação

Simplificar comunicação via fetch → Worker → JSON

Atender requisitos mínimos da ISO 27002

Estruturar uma arquitetura segura, clara e escalável

Integrar o Auth-Service ao NeuroScope AVZ

2. Desenvolvimento
2.1 Situação Inicial – Arquitetura Monolítica

O NeuroScope AVZ original era composto por:

Um único arquivo HTML/JS contendo toda a lógica

Acesso à câmera

Gravação WebM

Download local do vídeo

Sem login

Sem backend

Sem persistência

Nenhum controle de acesso

Limitações identificadas:

Nenhuma segurança

Nenhuma escalabilidade

Qualquer usuário acessava

Alterações exigiam editar o arquivo inteiro

Alto acoplamento do código

Esse arquivo representa o monolito inicial do projeto.

2.2 Proposta de Arquitetura Distribuída – Microsserviços

A migração foi planejada utilizando Cloudflare Workers, pois:

Não exigem servidor tradicional

Executam na borda (edge computing)

São ultraleves

Possuem latência mínima

São totalmente serverless

Atendem à exigência do professor

2.3 Microsserviços Desenhados
✔ Auth-Service (Cloudflare Worker)

Validação de usuário e senha

Geração de token

Controle de acesso ao sistema

✔ Video-Service

Gerencia gravação e possível envio

Independente do Auth-Service

✔ Patient-Service

Armazena dados mínimos do paciente

Histórico básico

✔ Pro-Service

Perfil do profissional

Acesso a vídeos e pacientes

RBAC (Role-Based Access Control)

✔ Notify-Service

Notificações simples via Worker

2.4 Comunicação Entre Serviços

Fluxo geral:

Frontend (HTML/JS)
      ↓
fetch()
      ↓
Cloudflare Worker
      ↓
Resposta JSON


Token armazenado no localStorage

Minimalista e eficiente

Sem servidores físicos

Sem APIs pesadas

2.5 Arquitetura Completa (Resumo)
[ Usuário / Paciente ]
          |
       Login Page
          |
        fetch()
          ↓
[ Auth-Service Worker ]
     valida token
          ↓
[ NeuroScope AVZ (vídeo) ]
          |
        fetch()
          ↓
[ Video-Service Worker ]
          |
[ Pro-Service → vídeos e pacientes ]

3. Metodologia

Estudo de caso: análise do monolito

Pesquisa aplicada: edge computing + serverless

Modelagem dos microsserviços

Planejamento da migração

Implementação mínima do Auth-Service

Documentação conforme o Projeto Integrador

4. Estratégia de Migração
Fase 1 – Identificação do monolito

Diagnóstico das limitações.

Fase 2 – Implementação do Auth-Service

Worker inicial criado.

Fase 3 – Redirecionamento seguro

Token obrigatório para acessar gravação.

Fase 4 – Separação conceitual dos demais serviços

Patient, Video, Pro e Notify.

Fase 5 – Documentação e diagrama

Consolidação para entrega.

5. Segurança da Informação (CID)
Confidencialidade

Autenticação no Worker

Token com expiração

HTTPS Cloudflare

Integridade

Logs no Worker

Hash opcional do vídeo

Verificação do token

Disponibilidade

Execução na borda

Escalabilidade natural

Latência reduzida

Sem servidor físico

6. Referências Bibliográficas

ISO/IEC 27002 – Segurança da Informação
International Organization for Standardization. ISO/IEC 27002:2022.

Edge Computing
Shi, W. et al. “Edge Computing: Vision and Challenges.” IEEE IoT Journal, 2016.

Cloudflare Workers
Cloudflare – Workers Documentation
Cloudflare – Serverless on the Edge

 Estrutura do Repositório
/
 ├── NeuroScope AVZ Official.html   → versão monolítica adaptada para o PI
 ├── README.md                      → documentação principal
 └── /workers/                      → microsserviços (em construção para o Projeto)

Como Executar o Projeto

Disponibilizado com login de teste para o professor conhecer o sistema simplificado e funcional.

Toda a gravação ocorre localmente, preservando privacidade e segurança.

Exemplo de execução:

Acessar o link do GitHub Pages

Inserir as credenciais de teste

Acessar o NeuroScope AVZ

Testar gravação/fluxo

Tecnologias Utilizadas

HTML5 / CSS3 / JavaScript

MediaDevices + MediaRecorder API

Cloudflare Workers

Edge Computing

Arquitetura Serverless

ISO 27002

RBAC (Role-Based Access Control)

Licença

Uso acadêmico conforme instruções da PUC Goiás – 2025.
Propriedade intelectual da autora Viviane B., reservada para aprimoramentos futuros.
Este material será removido após o período de avaliação do Projeto Integrador (2025).
