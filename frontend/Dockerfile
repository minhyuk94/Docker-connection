FROM node

WORKDIR /app

COPY package.json .

RUN npm install react-scripts@latest

COPY . .

EXPOSE 3000

CMD ["npm", "start"]