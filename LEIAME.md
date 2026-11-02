# Calculadora C.A.T.S – Líder e Membro (PWA)

## Como funciona
- **Líder**: edita a calculadora (todos veem ao vivo), edita nomes e carros na aba Ataques, zera as marcações e cadastra acessos na aba **Membros** (inclusive outros líderes).
- **Membro**: vê a calculadora em tempo real com contagem regressiva, marca "atacou" (✓) ou "indisponível" (✕) **só na própria linha** e usa o chat.
- Login por **código** (ex.: `MAV9287`). Senha é opcional e definida pelo líder. O código é gerado sozinho (nome + 4 números).

## Configuração (uma vez só)

### 1. Ativar o login anônimo
Firebase Console > **Authentication** > Começar > **Sign-in method** > **Anônimo** > Ativar.
(Ninguém precisa de e-mail. O app usa isso por trás para o servidor saber quem é quem.)

### 2. Colar as regras de segurança
Firebase Console > **Realtime Database** > aba **Regras** > apague tudo, cole o conteúdo de `database.rules.json` > **Publicar**.
Isso também resolve o aviso de "modo de teste expira em 30 dias".

### 3. Criar o primeiro líder (você)
Realtime Database > aba **Dados**. Passe o mouse na raiz do banco, clique no **+** e crie:
- Nome: `users`  → dentro dele, clique no **+** e crie o nome com o SEU código (ex.: `NITRO8902`)
- Dentro do seu código, crie dois itens: `name` = `NITRO` e `role` = `leader`

Depois de entrar, vá em Membros > 🔑 e coloque uma senha em você mesmo (recomendado, porque líder tem poder alto).

### 4. Publicar o PWA (link para os membros)
**Opção A – GitHub Pages (já usa GitHub):**
1. Envie todos estes arquivos para o repositório (inclusive a pasta oculta `.github`).
2. No repositório: Settings > Pages > Source: **GitHub Actions**.
3. Aba Actions > "Publicar PWA" roda sozinho a cada push. O link aparece em Settings > Pages.
   (Em conta grátis, Pages exige repositório público. O app continua protegido pelas regras do Firebase.)

**Opção B – Firebase Hosting:** no computador, `npm i -g firebase-tools`, `firebase login`, `firebase init` (escolha o projeto existente) e `firebase deploy`.

### 5. Convidar os membros
Aba Membros > Cadastrar > **Copiar convite** e mande no WhatsApp. O membro abre o link e digita o código.
Para ficar como app: no Android, menu do Chrome > "Instalar app" / "Adicionar à tela inicial"; no iPhone, Safari > Compartilhar > "Adicionar à Tela de Início".

## APK (opcional, para o líder)
O workflow `build-apk.yml` continua funcionando. O APK avisa o fim da batalha **mesmo com o app fechado**; o PWA só avisa com o app aberto.

## Segurança (resumo honesto)
- As **permissões são aplicadas no servidor** (regras do Firebase): mesmo mexendo no código, um membro não consegue editar a calculadora, nomes ou cadastros.
- Quem não tem senha entra só com o código. Por isso o código tem números aleatórios. Use senha em todo líder.
- Remover um acesso desconecta a pessoa. Mudar a senha só vale para os próximos logins.
