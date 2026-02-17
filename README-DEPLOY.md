# Deploy Online - Enerflux Fit Coach

## 1) Requisitos do servidor
- Node.js 20+
- npm 10+
- (Opcional) PM2 e Nginx

## 2) Instalação
```bash
npm ci
```

## 3) Variáveis de ambiente
```bash
cp .env.production.example .env
```
Edite o arquivo `.env` e configure:
- `NEXTAUTH_URL` com seu domínio real
- `NEXTAUTH_SECRET` forte
- `DATABASE_URL`

## 4) Banco de dados
### Se usar SQLite
- Mantenha `DATABASE_URL="file:./prisma/dev.db"`
- Se quiser levar dados atuais, garanta que `prisma/dev.db` esteja no servidor

### Se usar PostgreSQL (recomendado)
```bash
npx prisma db push
npm run db:seed
```

## 5) Build e execução
```bash
npm run build
npm run start
```

## 6) Produção com PM2 (opcional)
```bash
npm i -g pm2
pm2 start npm --name enerflux-fit-coach -- start
pm2 save
pm2 startup
```

## 7) Publicação com domínio
- Configure Nginx como reverse proxy para `http://127.0.0.1:3000`
- Ative HTTPS com Let's Encrypt

## Observações importantes
- Não suba `node_modules` nem `.next` no repositório.
- Em produção, prefira PostgreSQL para estabilidade e backup.
- Se trocar `NEXTAUTH_URL`, reinicie a aplicação.
