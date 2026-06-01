# ⚓ OffshoreJobs BR — App React Native / Expo

Rastreador de vagas offshore para o mercado brasileiro.  
Pronto para publicar na **Google Play Store** e **Apple App Store**.

---

## 📁 Estrutura do Projeto

```
OffshoreJobsBR/
├── App.js                    ← Ponto de entrada + navegação
├── app.json                  ← Configuração Expo
├── eas.json                  ← Configuração de build (Play Store)
├── package.json
├── babel.config.js
└── src/
    ├── data/
    │   ├── constants.js      ← Cores, fontes, dados fixos
    │   └── jobs.js           ← Gerador de vagas
    ├── hooks/
    │   └── useJobs.js        ← Estado global + AsyncStorage
    ├── components/
    │   ├── UI.js             ← Componentes reutilizáveis
    │   ├── JobCard.js        ← Card de vaga
    │   └── JobDetailModal.js ← Modal de detalhes
    └── screens/
        ├── ExplorerScreen.js ← Tela principal com filtros
        ├── SavedScreen.js    ← Vagas salvas
        ├── AnalyticsScreen.js← Gráficos e estatísticas
        └── AIScreen.js       ← Chat com IA (Claude API)
```

---

## 🚀 Passo a Passo — Rodar no Celular

### 1. Instalar Node.js
Baixe em: https://nodejs.org (versão LTS)

### 2. Instalar Expo CLI
```bash
npm install -g expo-cli eas-cli
```

### 3. Instalar dependências do projeto
```bash
cd OffshoreJobsBR
npm install
```

### 4. Rodar no celular (sem cabo)
```bash
npx expo start
```
- Baixe o app **Expo Go** no seu celular (Play Store / App Store)
- Escaneie o QR code que aparecer no terminal

### 5. Rodar em emulador Android
```bash
npx expo start --android
```
*(Precisa ter Android Studio instalado com um emulador configurado)*

---

## 📦 Publicar na Google Play Store

### Pré-requisitos
- Conta no **Google Play Console**: https://play.google.com/console ($25 USD, taxa única)
- Conta no **Expo EAS**: https://expo.dev (gratuito)

### Passo a Passo

**1. Criar conta Expo e fazer login:**
```bash
eas login
```

**2. Configurar o projeto:**
```bash
eas build:configure
```

**3. Gerar o bundle Android (AAB) para produção:**
```bash
eas build --platform android --profile production
```
Aguarde ~10 minutos. Você receberá um link para baixar o arquivo `.aab`.

**4. Enviar para o Google Play:**
- Acesse o Google Play Console
- Crie um novo app: "OffshoreJobs BR"
- Em "Versões" → "Produção" → "Criar nova versão"
- Faça upload do arquivo `.aab`
- Preencha: descrição, screenshots, categoria ("Emprego")
- Envie para revisão (leva 3-7 dias)

**5. Alternativa — Gerar APK direto (para testes):**
```bash
eas build --platform android --profile preview
```
Instala direto no celular sem precisar da Play Store.

---

## 🍎 Publicar na Apple App Store

```bash
eas build --platform ios --profile production
eas submit --platform ios
```
*(Requer conta Apple Developer: $99 USD/ano)*

---

## 🔑 Configurar Chave da API Claude (IA)

O assistente IA usa a API da Anthropic. Para funcionar em produção:

1. Crie uma conta em: https://console.anthropic.com
2. Gere uma API Key
3. Crie um arquivo `.env` na raiz:
```
EXPO_PUBLIC_ANTHROPIC_KEY=sk-ant-...sua-chave...
```
4. No `AIScreen.js`, adicione o header de autenticação:
```js
headers: {
  'Content-Type': 'application/json',
  'x-api-key': process.env.EXPO_PUBLIC_ANTHROPIC_KEY,
  'anthropic-version': '2023-06-01',
}
```

> ⚠️ **Nunca coloque a API key diretamente no código!**  
> Para produção, use um backend (ex: Supabase Edge Functions) como proxy.

---

## ✨ Funcionalidades do App

| Funcionalidade | Status |
|---|---|
| 🗺 Explorar 48 vagas offshore | ✅ |
| 🔍 Busca por cargo/empresa/local | ✅ |
| 🌐 Filtro por 6 fontes (LinkedIn, Google, etc.) | ✅ |
| 📂 Filtro por 9 categorias | ✅ |
| 🎯 Filtro por nível (Júnior → Gerência) | ✅ |
| ⭐ Salvar vagas favoritas | ✅ |
| ✅ Marcar candidaturas | ✅ |
| 💾 Persistência local (AsyncStorage) | ✅ |
| 📊 Analytics e gráficos | ✅ |
| 🤖 IA Assistente (Claude API) | ✅ |
| 🔗 Links diretos para candidatura | ✅ |
| 🔄 Atualizar vagas com pull-to-refresh | ✅ |

---

## 📱 Próximas Melhorias Sugeridas

- [ ] Notificações push para novas vagas
- [ ] Login com Google / LinkedIn  
- [ ] Alertas de vaga por e-mail
- [ ] Integração real com APIs das plataformas
- [ ] Perfil do candidato + currículo
- [ ] Mapa de vagas por estado

---

Desenvolvido com ❤️ para o mercado offshore brasileiro.
