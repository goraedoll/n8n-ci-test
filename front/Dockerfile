# ========================
# Stage 1 : Build
# ========================
FROM node:20-alpine AS builder
WORKDIR /app

# 1️⃣ 환경변수 (optional)
ARG NEXT_PUBLIC_API_URL
ENV NEXT_PUBLIC_API_URL=$NEXT_PUBLIC_API_URL

# 2️⃣ dependencies 설치
COPY package*.json ./
RUN npm ci

# 3️⃣ 소스 복사 및 빌드
COPY . .
RUN npm run build

# ========================
# Stage 2 : Run
# ========================
FROM node:20-alpine
WORKDIR /app

ENV NODE_ENV=production

# builder에서 빌드 결과만 복사
COPY --from=builder /app ./

EXPOSE 3000

CMD ["npm", "run", "start"]
