# ArgoCD Repository

Este repositório contém as configurações Kubernetes para aplicações gerenciadas pelo ArgoCD.

## Estrutura do Repositório

```
ArgoCD/
├── apps/                     # Aplicações Kubernetes
│   └── minha-app/           # Aplicação principal
│       ├── deployment.yaml   # Deployment da aplicação
│       ├── service.yaml      # Service para exposição
│       ├── ingress.yaml      # Ingress para acesso externo
│       └── configmap.yaml    # Configurações da aplicação
├── argocd-app.yaml          # Manifest ArgoCD Application
└── README.md                # Esta documentação
```

## Aplicações

### minha-app

Uma aplicação web simples baseada em Nginx com as seguintes características:

- **Replicas**: 3 pods para alta disponibilidade
- **Imagem**: nginx:alpine
- **Porta**: 80
- **Recursos**: 
  - Requests: 64Mi RAM, 250m CPU
  - Limits: 128Mi RAM, 500m CPU
- **Health Checks**: Liveness e Readiness probes configurados
- **Configurações**: ConfigMap com variáveis de ambiente

## Como Usar

1. **Clone o repositório**:
   ```bash
   git clone https://github.com/gabrielscostaa/ArgoCD.git
   cd ArgoCD
   ```

2. **Aplique o ArgoCD Application**:
   ```bash
   kubectl apply -f argocd-app.yaml
   ```

3. **Verifique o status no ArgoCD UI**:
   - Acesse a interface web do ArgoCD
   - Verifique o status da aplicação "minha-app"

## Configuração do ArgoCD

O arquivo `argocd-app.yaml` está configurado com:

- **Sync Policy**: Automatizado com prune e self-heal habilitados
- **Source**: Aponta para este repositório GitHub
- **Path**: `apps/minha-app` (onde estão os manifests)
- **Destination**: Namespace `default` no cluster

## Personalização

Para adicionar uma nova aplicação:

1. Crie uma nova pasta em `apps/` (ex: `apps/nova-app/`)
2. Adicione os manifests Kubernetes necessários
3. Crie um novo `argocd-app.yaml` ou modifique o existente
4. Faça commit e push das alterações

## Troubleshooting

- **Aplicação não sincroniza**: Verifique se o repositório está acessível e o path está correto
- **Pods não iniciam**: Verifique os logs dos pods e as configurações de recursos
- **Service não funciona**: Verifique se os labels estão corretos entre deployment e service

## Contribuição

1. Faça um fork do repositório
2. Crie uma branch para sua feature
3. Faça commit das alterações
4. Abra um Pull Request

## Licença

Este projeto está sob a licença MIT. 