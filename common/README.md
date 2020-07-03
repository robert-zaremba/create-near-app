near-blank-project
==================

This [NEAR] app was initialized with [create-near-app]


Quick Start
===========

To run this project locally:

1. Prerequisites: Make sure you have [Node.js] ≥ 12 installed
2. Install dependencies: `npm install`
3. Run the local development server: `npm run dev` (see `package.json` for a
   full list of `scripts` you can run with `npm`)

Now you'll have a local development environment backed by the NEAR TestNet! This is a test network that operates just like the main NEAR blockchain, but the tokens are just for testing and cannot be exchanged for other currencies.

Running `npm run dev` will tell you the URL you can visit in your browser to see the app.


Exploring The Code
==================

1. The backend code lives in the `/assembly` folder. This code gets deployed to
   the NEAR blockchain when you run `npm run deploy:contract`. This sort of
   code-that-runs-on-a-blockchain is called a "smart contract" – [learn more
   about NEAR smart contracts][smart contract docs].
2. The frontend code lives in the `/src` folder. `/src/index.html` is a great
   place to start exploring. Note that it loads in `/src/index.js`, where you
   can learn how the frontend connects to the NEAR blockchain.
3. Tests: there are different kinds of tests for the frontend and the smart
   contract. The smart contract code gets tested with the [asp] command, and
   the frontend code gets tested with [jest]. You can run both of these at once
   with `npm run test`.

Both contract and client-side code will auto-reload as you change source files.


Deploy
======

Every smart contract in NEAR has its [own associated account][NEAR accounts]. When you run `npm run dev`, your smart contracts get deployed to the live NEAR TestNet with a throwaway account. When you're ready to make it permanent, here's how.


Step 0: Install near-shell
--------------------------

You need [near-shell] installed globally:

    npm install --global near-shell

This will give you the `near` [CLI] tool, a command-line interface for interacting with the NEAR blockchain. Ensure that it's installed with:

    near --version


Step 1: Create an account for the contract
------------------------------------------

Each account on NEAR can have at most one contract deployed to it. If you've already created an account such as `your-name.testnet`, you can deploy your contract to `near-blank-project.your-name.testnet`. Assuming you've already created an account on [NEAR Wallet], here's how to create `near-blank-project.your-name.testnet`:

1. Authorize NEAR shell, following the commands it gives you:

      near login

2. Create a subaccount (replace `YOUR-NAME` below with your actual account name):

      near create-account near-blank-project.YOUR-NAME.testnet --masterAccount YOUR-NAME.testnet


Step 2: set contract name in code
---------------------------------

Modify the line in `src/config.js` that sets the account name of the contract. Set it to the account id you used above.

    const CONTRACT_NAME = process.env.CONTRACT_NAME || 'near-blank-project.YOUR-NAME.testnet'


Step 3: deploy!
---------------

One command:

    npm run deploy

As you can see in `package.json`, this does two things:

1. builds & deploys smart contracts to NEAR TestNet
2. builds & deploys frontend code to GitHub using [gh-pages]. This will only work if the project already has a repository set up on GitHub. Feel free to modify the `deploy` script in `package.json` to deploy elsewhere.


Troubleshooting
===============

On Windows, if you're seeing an error containing `EPERM` it may be related to spaces in your path. Please see [this issue](https://github.com/zkat/npx/issues/209) for more details.


  [NEAR]: https://near.org/
  [create-near-app]: https://github.com/near/create-near-app
  [Node.js]: https://nodejs.org
  [AssemblyScript]: https://docs.assemblyscript.org/
  [React]: https://reactjs.org
  [smart contract docs]: https://docs.near.org/docs/roles/developer/contracts/intro
  [asp]: https://www.npmjs.com/package/@as-pect/cli
  [jest]: https://jestjs.io/
  [NEAR accounts]: https://docs.near.org/docs/concepts/account
  [NEAR Wallet]: https://wallet.testnet.near.org/
  [near-shell]: https://github.com/near/near-shell
  [CLI]: https://techterms.com/definition/command_line_interface
  [gh-pages]: https://github.com/tschaub/gh-pages
