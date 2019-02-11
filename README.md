# finanger - mern stack app integrated with plaid api

[finanger app](https://finanger.herokuapp.com)

This project utilizes the following technologies:

- React and [React Router]
- Node.js and Express
- MongoDBfor the database
- Redux
- [Plaid](https://plaid.com) Banking API

## configuration

### mongo

Use [mLab](https://mlab.com) to connect your database in `config/keys.js`. Replace `MONGOURI` with your obtained information from mlab

```javascript
module.exports = {
  mongoURI: "YOUR_MONGO_URI_HERE",
  secretOrKey: "secret"
};
```

### plaid

Plaid API offers Sandbox and Development(100 live accounts) access for account retrieval. Since both are free, I got access for Development. Add your [Plaid API](https://plaid.com) keys (`PLAID_CLIENT_ID`, `PLAID_SECRET`, and `PLAID_PUBLIC_KEY`) in

1. `routes/api/plaid.js`

```
const PLAID_CLIENT_ID = "YOUR_CLIENT_ID";
const PLAID_SECRET = "YOUR_SECRET";
const PLAID_PUBLIC_KEY = "YOUR_PUBLIC_KEY";
```

2. `client/src/components/dashboard/Dashboard.js` and `client/src/components/dashboard/Accounts.js` - We are only retrieving transaction data hence 

``` 
product: ["transactions"] 
```

```
<PlaidLinkButton
                buttonProps={{
                  className:
                    "btn btn-large waves-effect waves-light hoverable blue accent-3 main-btn"
                }}
                plaidLinkProps={{
                  clientName: "YOUR_APP_NAME",
                  key: "YOUR_PUBLIC_KEY",
                  env: "development",
                  product: ["transactions"],
                  onSuccess: this.handleOnSuccess
                }}
                onScriptLoad={() => this.setState({ loaded: true })}
              >
                Link Account
              </PlaidLinkButton>
```

## quickstart

```javascript
// Install dependencies for server & client
npm install && npm run client-install

// Run client & server with concurrently(make sure to npm i concurrently - this enables us run the server and client at the same time)
npm run dev

// Server runs on http://localhost:5000 and client on http://localhost:3000
```