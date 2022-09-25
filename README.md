# Best Node.js architecture 🛡️

It's meant for small startups or one-developer army projects.

I know if you start moving layers into another technology, you will end up with your business/domain logic into npm packages, your routing layer will be pure AWS Lambda functions and your data layer a combination of DynamoDB, Redis, maybe redshift, and Agolia.

Take a deep breath and go slowly, let the business grow and then scale up your product. You will need a team and talented developers anyway.

## Development

Use `node` version `14.9.0`

```
nvm install 14.9.0
```

```
nvm use 14.9.0
```

The first time, you will need to run

```
npm install
```

Then just start the server with

```
npm run start
```
It uses nodemon for livereloading :peace-fingers:

## Setup

- install the dependencies.
- run `cp .env.example .env`.
- run `npm run start`.

# API Validation

 By using [celebrate](https://github.com/arb/celebrate), the req.body schema becomes cleary defined at route level, so even frontend devs can read what an API endpoint expects without needing to write documentation that can get outdated quickly.

 ```js
 route.post('/signup',
  celebrate({
    body: Joi.object({
      name: Joi.string().required(),
      email: Joi.string().required(),
      password: Joi.string().required(),
    }),
  }),
  controller.signup)
 ```

 **Example error**

 ```json
 {
  "errors": {
    "message": "child \"email\" fails because [\"email\" is required]"
  }
 }
 ```

[Read more about celebrate here](https://github.com/arb/celebrate) and [the Joi validation API](https://github.com/hapijs/joi/blob/v15.0.1/API.md)

## API Documentation

To simplify documenting your API, use [Optic](https://useoptic.com). To use it, you will need to [install the CLI tool](https://useoptic.com/document/#add-an-optic-specification-to-your-api-project), and then you can use `api exec "npm start"` to start capturing your endpoints as you create them. Once you want to review and add them to your API specification run: `api status -- review`.