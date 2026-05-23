FROM node:20

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

RUN addgroup --system appgroup && adduser --system appuser --ingroup appgroup

RUN chown -R appuser:appgroup /app

USER appuser

EXPOSE 5173

CMD ["npm", "run", "dev", "--", "--host"]