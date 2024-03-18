# Forum API

The Forum API is a RESTful backend developed in Node.js using NestJS framework. It follows the principles of Clean Architecture and DDD (Domain-Driven Design).
This API allows users to create questions, provide answers, attach files, comment on questions, answers, and more, facilitating discussion and interaction within a forum environment.

## Relevant technologies
- NestJS: Nest (NestJS) is a framework for building efficient and scalable Node.js server-side applications.
- Zod: Zod is a data validation library for TypeScript.
- Passport: Passport is a server-side user authentication library.
- Passport JWT: A Passport strategy for authenticating with a JSON Web Token, this module allows authenticating endpoints using a JSON web token.
- Prisma: Prisma is a database persistence library for Node.js.
- Cloudflare: Cloudflare is a network data storage platform.

## Installation

Make sure you have Node.js in the version 16.20.2 and npm installed on your machine.

1. Clone this repository:
   `git clone https://github.com/gbrogni/forum-api.git`
  
2. Install dependencies
   `cd nestjs-api`
   
   `npm install`

## Configuration

1. Rename the .env.example file to .env and configure the environment variables as needed.
2. The authentication strategy used is JWT with RSA-256 algorithm. Therefore, you should generate the public and private keys of the algorithm and convert them to Base64.
   `openssl genrsa -out private.pem 2048`
   
   `openssl rsa -in private.pem -pubout -out public.pem`
   
   `base64 private.pem`
   
   `base64 public.pem`
3.Additionally, we use Cloudflare R2 for storing question and answer attachments. The interesting aspect is that it uses the same AWS S3 API, which facilitates switching if necessary.
 Given this, for end-to-end (e2e) testing, simply create the bucket in Cloudflare with a 1-day lifecycle to prevent test attachments from accumulating.

To override environment variables for testing, use the .env.test file, replacing what is needed, for example:
`AWS_BUCKET_NAME="forum-test"`
4. Do not forget to run the migrations
`npx migrate dev`
5. Using Docker Compose, start the necessary services to run the application:
`docker-compose up -d`
6. After that, simply start the application (development):
`npm run start:dev`


To test the application requests, I'm using the VSCode extension called Rest Client. I've created a file named client.http in the root of the project where all the application routes are listed.

## Tests

In this project, I'm using unit tests and end-to-end (e2e) tests. To execute them, simply run the commands:

### Unit Tests
`npm run test`

### End-To-End Tests
`npm run test:e2e`
