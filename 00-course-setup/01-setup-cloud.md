# Configuração na Nuvem ☁️ – GitHub Codespaces

**Use este guia se você não quiser instalar nada localmente.**
O Codespaces fornece uma instância gratuita do VS Code no navegador com todas as dependências pré-instaladas.

---

## 1. Por que o Codespaces?

| Benefício | O que isso significa para você |
|-----------|------------------------------|
| ✅ Zero instalações | Funciona em Chromebook, iPad, computadores do laboratório da escola... |
| ✅ Container de desenvolvimento pré-construído | Python 3, Node.js, .NET, Java já inclusos |
| ✅ Cota gratuita | Contas pessoais recebem **120 core-hours / 60 GB-hours por mês** |

> 💡 **Dica**
> Mantenha sua cota saudável **parando** ou **excluindo** codespaces ociosos
> (Veja ▸ Command Palette ▸ *Codespaces: Stop Codespace*).

---

## 2. Crie um Codespace (um clique)

1. **Fork** deste repositório (botão **Fork** no canto superior direito).
2. No seu fork, clique em **Code ▸ Codespaces ▸ Create codespace on main**.
   ![ialog mostrando botões para criar um codespace](./images/who-will-pay.webp?WT.mc_id=academic-105485-koreyst)

✅ Uma janela do VS Code no navegador será aberta e o dev container começará a ser construído.
Isso leva **~2 minutos** na primeira vez.

## 3. Adicione sua chave de API (do jeito seguro)

### Opção A Secrets do Codespaces — Recomendado

1. ⚙️ Ícone de engrenagem -> Command Palette -> Codespaces : Manage user secret -> Add a new secret.
2. Nome: OPENAI_API_KEY
3. Valor: cole sua chave -> Add secret

Pronto — nosso código a reconhecerá automaticamente.

### Opção B arquivo .env (se realmente precisar)

```bash
cp .env.copy .env
code .env         # preencha OPENAI_API_KEY=seu_key_aqui
```
