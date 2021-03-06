<p align="center">
  <img src="https://user-images.githubusercontent.com/6391763/83290846-fa3b9880-a204-11ea-91d3-28afe7543d2c.png" alt="Logo"/>
</p>

<p align="center">
  <a href="https://twitter.com/nirmalyaghosh23">
    <img alt="Twitter: Nirmalya Ghosh" src="https://img.shields.io/twitter/follow/nirmalyaghosh23.svg?style=social" target="_blank" />
  </a>
</p>

This is a boilerplate for building applications using Hasura and Next.js. This boilerplate consists of the following:

1. [**frontend**](https://github.com/ghoshnirmalya/nextjs-hasura-boilerplate/tree/master/frontend): Next.js application
2. [**backend**](https://github.com/ghoshnirmalya/nextjs-hasura-boilerplate/tree/master/backend): Dockerized Hasura application

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Overview](#overview)
- [Requirements](#requirements)
- [Packages](#packages)
  - [1. **Frontend**: Next.js application](#1-frontend-nextjs-application)
  - [2. **Backend**: Dockerized Hasura application](#2-backend-dockerized-hasura-application)
- [Installation](#installation)
  - [1. **Clone the application**](#1-clone-the-application)
  - [2. **Install necessary dependencies for the frontend application**](#2-install-necessary-dependencies-for-the-frontend-application)
  - [3. **Create a .env file and copy the contents from .env.example (present in frontend directory)**](#3-create-a-env-file-and-copy-the-contents-from-envexample-present-in-frontend-directory)
  - [4. **Generate the RSA keys**](#4-generate-the-rsa-keys)
  - [5. **Print the keys in the escaped format**](#5-print-the-keys-in-the-escaped-format)
  - [6. **Copy the value of the key into the `AUTH_PRIVATE_KEY` key (in the .env file)**](#6-copy-the-value-of-the-key-into-the-auth_private_key-key-in-the-env-file)
  - [7. **Start the frontend application**](#7-start-the-frontend-application)
  - [8. **Go inside the directory of the backend package on another terminal window**](#8-go-inside-the-directory-of-the-backend-package-on-another-terminal-window)
  - [9. **Start docker-compose**](#9-start-docker-compose)
- [Deployment](#deployment)
  - [Frontend application](#frontend-application)
  - [Backend application](#backend-application)
- [Other interesting repositories](#other-interesting-repositories)
- [License](#license)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Overview

This boilerplate is built using the following technologies:

1. [Chakra UI](https://chakra-ui.com/)
2. [Emotion](https://emotion.sh/)
3. [GraphQL](https://graphql.org/)
4. [urql](https://formidable.com/open-source/urql/)
5. [NextAuth](https://next-auth.js.org/)
6. [TypeScript](https://www.typescriptlang.org/)

It supports GraphQL Query, Mutation and Subscription out of the box.

## Requirements

1. [Node.js](https://nodejs.org/)
2. [npm](https://www.npmjs.com/)
3. [Docker](https://www.docker.com/)

## Packages

### 1. [**Frontend**](https://github.com/ghoshnirmalya/nextjs-hasura-boilerplate/tree/master/frontend): Next.js application

This application is the primary user-facing application. Once it’s up and running (see Development section), it’s available on http://localhost:3000/.

![Home page before login](https://user-images.githubusercontent.com/6391763/91220100-4bdabd00-e739-11ea-861e-f4ede1f5f44c.png)

To create a new user, we’ll have to Sign Up using Google. [NextAuth](https://next-auth.js.org/) is being used to help us in authentication.
![Login page](https://user-images.githubusercontent.com/6391763/91220113-5006da80-e739-11ea-9580-9dacad898d9f.png)

![Home page after login](https://user-images.githubusercontent.com/6391763/91220117-509f7100-e739-11ea-9c5d-782185dc5a69.png)

![Feeds page](https://user-images.githubusercontent.com/6391763/91220121-51d09e00-e739-11ea-8960-ec335586d8af.png)

![My Profile page](https://user-images.githubusercontent.com/6391763/91220126-52693480-e739-11ea-87d0-5834617c9d96.png)

### 2. [**Backend**](https://github.com/ghoshnirmalya/nextjs-hasura-boilerplate/tree/master/backend): Dockerized Hasura application

[Hasura](https://hasura.io/) is an open source engine that connects to our databases & micro-services and auto-generates a production-ready GraphQL backend. It’s very easy to get Hasura up and running on our local system. All the migrations are set up in the [migrations](https://github.com/ghoshnirmalya/nextjs-hasura-trello-clone/tree/master/packages/backend/migrations) directory.

## Installation

### 1. **Clone the application**

```sh
git clone https://github.com/ghoshnirmalya/nextjs-hasura-boilerplate
```

### 2. **Install necessary dependencies for the frontend application**

```sh
cd frontend && yarn install
```

### 3. **Create a .env file and copy the contents from .env.example (present in frontend directory)**

### 4. **Generate the RSA keys**

```sh
openssl genrsa -out private.pem 2048
openssl rsa -in private.pem -pubout > public.pem
```

### 5. **Print the keys in the escaped format**

```sh
awk -v ORS='\\n' '1' private.pem
```

### 6. **Copy the value of the key into the AUTH_PRIVATE_KEY key (in the .env file)**

The **AUTH_PRIVATE_KEY** should look like the following:

```sh
AUTH_PRIVATE_KEY='{"type":"RS256", "key": "-----BEGIN RSA PRIVATE KEY-----\nMIIEowIBAAKCAQEA0U3NR0eyMehHBlx6DK5sJ+Pys9dTWf558kpKVeQvL2oIZEY3\nLvS3/jdrIm/dU4WrIGPki1r/AWXQAyBZ2FKnZROcUWN0IqdmxrC5zTDymuscqhKX\nqxjSwrwOVWHc+zWWmXCQGmDdoCokXd9ZW66nA0BN66MdMC2+d5GrZdKUF305dpzT\nUdzDE12/XwOEUalCM0703eGu8zFwutLYc3+vf2CFOQ1z+rvDQD4N2aZABKTxZRtE\nkMHljnoyKlF9rljNzT/5N8YQE7qn4pBh6CMa1zcSilk9nhgl55n/Kjn2xMieWdIa\nlaOEKw1LqqIjiT1ESkAKfPaIoSSnmTaYy78gbwIDAQABAoIBAF+3t+AYLqraMdj7\n46j2/2lCupR6LZkjYntmdBZRky6YzBunbMchjR9KEsmd5Na0c20NodAFHkdyWy2C\n1vOx4PG9hShHVi4e5kaJPX9UGi60xNgWRpwtbv01aUysw5VyjVvAeXZGxDPh8d2o\nLcJa3fADsV7IqqmE0ez2hi67nZQbkbEUbKs7aGfCE6srCfjCfOadfNnto9+7qDjJ\nnd4rK18H1rBSLTqj4T7wd1K8THgo25vjEuVRbGsEVrNB/B1Dz0pdOqhqukzixfcS\nVL/7uYDXehLasmUQu2VtMFsLqDpAbQgvpoNnzeZuB0WARvygSi/n4t+pCi84hXXe\na1m/01kCgYEA6+i5FwJAPxe2oCc0iignHjA20itTalyUhgJrLa8tTs721GJ3ku0A\n/EJVgmoNOLCQnZMldWvEDGmf6QuaWitq8ZWK/0BmHrEjbDA7m1fPdf3hrNx6eH/i\nazxjAoWA/u0yZg6QvUC7hSOO6WEpFYGuc2+/mHlnm5RLdL3QNIlHyyUCgYEA4yEI\n2deZ9MgmxbnFc76u7VhT1lc1MHpuAcDR3hqKT9xH2fTBaTDpVqeFbQJR5Hu+ZqgT\nL3+zV5kzIz3RaNMGN1IaxDEEx+tDnL9aw8sqawauWZtp7W2EeFvtP8uhHiBWpqVl\nvus6Gpl6hpNg6X96vHRcW+mB13I/h5YWA25EEwMCgYA5YbkrvJNuBVGZsQ+Zj1y8\nfhPHmVxH4c8KranuSc7mfXcSgAT/ywBTW7s65prisCfs/C6/WgAs2MBZykW4Kxlv\nO+W8Yqi0THgGR9En3vsKgz+ScWqkxs6HMQAQS/LtjzqUEnToY8d5AgYwBD8fCRUq\n5QKgjt9Bu5eDBOyQ6td4tQKBgBtDrOdRfTaoDBdyHGSvgBoXn0C8iTL/j1MAjXDG\n6NF7VNiyC8GP0ILJazfRrnjp7cou5Nav0pxyVHQniIq3wihD39irNbK16BDZ25Bj\nQ/1C+Qzing2VNvCnwEwHKpkOMrigZB1N6VSmFdIvwNNmrRoQMcIKvr5ZBY1GE/Bn\nfR53AoGBAIXaWIoDW5d9XwFa8HdxkgMPyLlizckZKyXASYEGWD2VU8P1NwA/bZ1t\nymioQPRJymTBfUL6E44Ebwx25DezjYEun1yqouZ+WZBlsEYtssffzTs2IocZ6aCN\nYfzt3orUEI/rWbRSqYFEuOntzzf3a7r3MtDU41e7iXcNkRSxCAIV\n-----END RSA PRIVATE KEY-----\n"}'
```

### 7. **Create and copy the Google client credentials**

Create a new [Google OAuth Client](https://console.developers.google.com/apis/credentials/oauthclient) and copy the credentials (Client ID and Client Secret) in your .env file.

### 8. **Start the frontend application**

From the frontend directory, we can run the following command to start our Next.js frontend application:

```sh
yarn dev
```

The above command will start the frontend application on [http://localhost:3000/](http://localhost:3000).

### 9. **Go inside the directory of the backend package on another terminal window**

```sh
cd packages/backend
```

### 10. **Add the necessary environment keys (in the docker-compose.yml file)**

```sh
awk -v ORS='\\n' '1' public.pem
```

The **HASURA_GRAPHQL_JWT_SECRET** should look like the following (in your docker-compose.yml file):

```sh
HASURA_GRAPHQL_JWT_SECRET='{"type":"RS256", "key": "-----BEGIN PUBLIC KEY-----\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA0U3NR0eyMehHBlx6DK5s\nJ+Pys9dTWf558kpKVeQvL2oIZEY3LvS3/jdrIm/dU4WrIGPki1r/AWXQAyBZ2FKn\nZROcUWN0IqdmxrC5zTDymuscqhKXqxjSwrwOVWHc+zWWmXCQGmDdoCokXd9ZW66n\nA0BN66MdMC2+d5GrZdKUF305dpzTUdzDE12/XwOEUalCM0703eGu8zFwutLYc3+v\nf2CFOQ1z+rvDQD4N2aZABKTxZRtEkMHljnoyKlF9rljNzT/5N8YQE7qn4pBh6CMa\n1zcSilk9nhgl55n/Kjn2xMieWdIalaOEKw1LqqIjiT1ESkAKfPaIoSSnmTaYy78g\nbwIDAQAB\n-----END PUBLIC KEY-----\n"}'
```

Also, the **HASURA_GRAPHQL_ADMIN_SECRET** value needs to be updated in the docker-compose.yml file:

```sh
HASURA_GRAPHQL_ADMIN_SECRET: secret
```

### 11. **Start docker-compose**

```sh
docker-compose up
```

We need to start Docker and then run the above command which will change the current directory to the backend package’s directory and then start the backend package. If everything goes well, it’ll be up and running on http://localhost:8080/v1/graphql.

## Deployment

### Frontend application

Click on the button below to deploy the frontend application on Vercel. You'll need to [sign up for a free Vercel account](https://vercel.com/signup/).

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/import/git?s=https%3A%2F%2Fgithub.com%2Fghoshnirmalya%2Fnextjs-hasura-boilerplate%2Ftree%2Fmaster%2Ffrontend&env=NEXT_PUBLIC_API_URL,NEXT_PUBLIC_WS_URL,DATABASE_URL,AUTH_PRIVATE_KEY,EMAIL_SERVER,EMAIL_FROM,NEXTAUTH_URL,GOOGLE_CLIENT_ID,GOOGLE_CLIENT_SECRET&project-name=nextjs-hasura-boilerplate&repo-name=nextjs-hasura-boilerplate)

### Backend application

Click on the button below to deploy the backend application on Heroku. You'll need to [sign up for a free Heroku account](https://signup.heroku.com/).

[![Deploy to
Heroku](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/ghoshnirmalya/nextjs-hasura-boilerplate)

## Other interesting repositories

1. [Hasura Next.js Boilerplate](https://github.com/ghoshnirmalya/nextjs-hasura-trello-clone)
2. [React Search Box](https://github.com/ghoshnirmalya/react-search-box)
3. [LinkedIn Clone using Create React App](https://github.com/ghoshnirmalya/linkedin-clone-react-frontend)

## License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT).
