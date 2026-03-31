# Análise do Bug - Erro ao Gerar QR Code PIX

## Problema Identificado
O usuário recebe o erro: **"Resposta inválida do servidor: <!DOCTYPE html> <html lang="en">..."**

Isso significa que o servidor está retornando uma página HTML (provavelmente a página de erro do Manus Sandbox) em vez de um JSON com os dados do PIX.

## Causa Raiz
A rota `/api/gerar-pix` não está sendo encontrada corretamente. Possíveis causas:

1. **Proxy não configurado no Vite**: Durante o desenvolvimento, o Vite (frontend) não sabe encaminhar requisições `/api` para o Express backend
2. **Backend não está rodando**: O servidor Express precisa estar rodando na porta 3000
3. **CORS ou headers incorretos**: O servidor pode estar bloqueando as requisições

## Solução
Implementar um proxy no Vite que encaminhe todas as requisições `/api` para o backend Express.

## Arquivos Afetados
- `vite.config.ts` - Precisa adicionar configuração de proxy
- `server/index.ts` - Backend está correto, apenas precisa estar rodando
- `client/src/hooks/useSigiloPay.ts` - Código está correto

## Status
✅ Problema identificado
⏳ Solução em implementação
