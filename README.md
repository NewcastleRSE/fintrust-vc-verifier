# Fintrust Verifiable Credentials Verifier Website

[![Docker Builds](https://github.com/NewcastleRSE/fintrust-vc-verifier/actions/workflows/docker.yml/badge.svg)](https://github.com/NewcastleRSE/fintrust-vc-verifier/actions/workflows/docker.yml)

This repository contains a sample website written in NodeJS that verifies a verifiable credential. All code for the website is contained in `app.js`. Essentially, this website does three things:

1. It generates a QR code and displays it in a browser.
2. It generates a credential presentation request, which is sent to Microsoft Authenticator after the QR code is scanned.
3. It receives the requested credential from Authenticator and validates it.

See the Microsoft Azure [documentation](https://aka.ms/didfordevs) for a more detailed explanation of the credential presentation and verification process.

## Using Verifiable Credentials to identify vulnerable customers in finance

This app is part of the implementation of the [Software Design Specification (SDS) Document](https://docs.google.com/document/d/1j2QFLKuDnUsdsmZphjdF2znI3LH5KEEPMwucwEcefUw/edit?usp=sharing) for the Trustworthy Digital Infrastructure for Identity Systems project, led by the Turing Institute and funded through a grant from the Bill & Melinda Gates Foundation. 

## Running the app 

Follow these steps to run the app using the pre-configured Verified Credential 'Fairness for All' card on your local machine.

1. Clone this repository and `cd` to this `verifier` directory.
2. Run `npm install` to install all dependencies for the verifier website.
3. Proceed with each step below to configure and run the website.

### Installing Microsoft Authenticator.

To run this sample, you'll need Microsoft Authenticator installed on an android device. Please follow [the instructions on our documentation](https://didproject.azurewebsites.net/docs/authenticator.html) to install Microsoft Authenticator.

### Issue a verifiable credential.

Before you can use the verifier sample, you'll first need to issue a verifiable credential to Authenticator. If you haven't done so already, head on over to the  [fintrust-vc-issuer](https://github.com/NewcastleRSE/fintrust-vc-issuer) app first, and then return to this verifier sample.

### Connect Authenticator to your local Node server

When you run the sample website, your android device will need to be able to communicate with your Node server via HTTPS requests. Setting this up can be a bit tricky - you have a few options to choose from:

1. You can deploy the Node server to the cloud, so that Authenticator can communicate with it over the public internet.
2. You can connect your android device to your machine via USB and configure the network settings appropriately.
3. You can connect your android device to the same wifi network as your machine, and communicate over the LAN.
4. You can expose your local machine over the public internet using a tool like ngrok.

We recommend the last option. Here are the steps we used to do so:

1. Go to [ngrok.com/](https://ngrok.com/) and create an account.
2. Follow the instructions to install and configure ngrok.
3. Start ngrok, exposing your server, which uses port 8082 by default:

```
ngrok http 8082
```

### Run the website

Finally, you're ready to run the website on your local machine:

```bash
node ./app.js
```

Once the site is up and running, navigate to the site in a browser using the secure ngrok URL.

### Using the website

To request and validate a verifiable credential, run the website and navigate to the homepage. Then:

1. Click the button to display a QR code (or a deep link on mobile browsers).
2. In Authenticator, open the QR scanner.
3. Approve the request in Authenticator.    

## Modifying the code to use a different issuer and/or verifier

To switch the issuer (i.e. if you've created a new issuer service or want to verify a new credential type):

1. In `app.js`, update the `credentialType` value for your verifiable credential.
2. In `app.js`, update the `issuerDid` value to the expected DID of the issuer of the verifiable credential you expect.
3. In `app.js`, optionally update the `client` values to reflect your verifier website.
4. In `didconfig.json`, update all values to use your Azure Key Vault.

## Image credit links

* [Handshake Icon](https://icon-icons.com/icon/handshake/78379)
* [Bank Icon](https://icon-icons.com/icon/bank/78392)


## Project Team
Dave Horsfall, Newcastle University ([dave.horsfall@newcastle.ac.uk](mailto:dave.horsfall@newcastle.ac.uk)) - Developer  
Dr Samantha Finnigan, Newcastle University ([samantha.finnigan@newcastle.ac.uk](samantha.finnigan@newcastle.ac.uk)) – Maintainer  
Dr Kovila Coopamootoo, Newcastle University ([kovila.coopamootoo@newcastle.ac.uk](kovila.coopamootoo@newcastle.ac.uk)) - Project Co-Investigator  
Prof. Aad van Moorsel, Newcastle University ([aad.vanmoorsel@newcastle.ac.uk](aad.vanmoorsel@newcastle.ac.uk)) – Project Principal Investigator  

### RSE Contact
Dr Samantha Finnigan  
RSE Team  
Newcastle University  
([samantha.finnigan@newcastle.ac.uk](samantha.finnigan@newcastle.ac.uk))


## License
Released under MIT License  
Copyright © 2022 Newcastle University  


## Citation

Please cite the associated papers for this work if you use this code:

```
@misc{spiliotopoulos2021identifying,
      title={Identifying and Supporting Financially Vulnerable Consumers in a Privacy-Preserving Manner: A Use Case Using Decentralised Identifiers and Verifiable Credentials}, 
      author={Tasos Spiliotopoulos and Dave Horsfall and Magdalene Ng and Kovila Coopamootoo and Aad van Moorsel and Karen Elliott},
      year={2021},
      eprint={2106.06053},
      archivePrefix={arXiv},
      primaryClass={cs.CY}
}
```

## Acknowledgements

This app is part of the implementation of the [Software Design Specification (SDS) Document](https://docs.google.com/document/d/1j2QFLKuDnUsdsmZphjdF2znI3LH5KEEPMwucwEcefUw/edit?usp=sharing) for the Trustworthy Digital Infrastructure for Identity Systems project, led by the Turing Institute and funded through a grant from the Bill & Melinda Gates Foundation [INV-001309](https://www.gatesfoundation.org/about/committed-grants/2019/12/INV001309). 
