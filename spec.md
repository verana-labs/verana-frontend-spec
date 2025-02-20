# Verana App Specification

**Specification Status:** Pre-Draft

**Latest Draft:** [verana-labs/verana-app-spec](https://github.com/verana-labs/verana-app-spec)

**Editors:**

~ [Fabrice Rochette](https://www.linkedin.com/in/fabricerochette) (The Verana Foundation, 2060.io)

<!-- -->

**Participate:**

~ [GitHub repo](https://github.com/verana-labs/verana-app-spec)

~ [File a bug](https://github.com/verana-labs/verana-app-spec/issues)

~ [Commit history](https://github.com/verana-labs/verana-app-spec/commits/main)

---

## About this Document

This specification is for the Verana Network frontend, a container-based App easily deployable locally, or in any modern cloud infrastructure.

## Introduction

*This section is non-normative.*

### What is Verana?

Verana is the Zero Trust layer that makes the Internet verifiable.

Like the DNS (Domain Name System) provides a way of resolving domain names, Verana provides a way of resolving, verifying, and proving trust.

- DNS: Resolve domain names
- Verana: Resolve Proof of Trust

Verana is a public, decentralized ecosystem run by volunteers around the world. Anyone can participate and contribute to the ecosystem.

Participants build a Proof-of-Trust reputation over time, and are financially rewarded by the network for their trustworthiness.

### Based on Verifiable Credentials and GDPR compliant

### The Verana Foundation

As a non-profit organization, the Verana Foundation's mission is to provide the required bricks for enabling a Zero Trust layer: governance and leadership, open source software, and a verifiable trust registry of essential credential schemas.

#### Governance and Leadership

The Verana Foundation is governed and leaded by its contributors, participants, and ambassadors.


#### Software

Open source software and modules that implement the [Verifiable Trust specification](https://verana-labs.github.io/verifiable-trust-spec/)

#### Essential Credential Schemas (ECS) Trust Registry

a Trust Registry of Essential Credential Schemas:

- Organization,
- Person,
- Service,
- User Agent.

These credential schemas provide the required basic features of the Zero Trust layer, that can be queried by users, organizations, user agents...:

- who is the organization or person running this service?
- what is the name of this service? What is the minimum required age for connecting to this service?
- is this user agent compliant with the Verifiable Trust specification?

A trust registry governance framework defines the rules for participating in the ECSs as credential Issuer. Provided that they comply with the Governance Framework, any organization can join the ECS Trust Registry.

### Benefits

Fraud and Identity theft are eradicated.

#### For the End User

- identify, verify, and get a proof of who is the provider of a service before connecting to it.
- collect verifiable credentials from verified service providers.
- use your credentials to prove your identity, age, address, diplomas, avatar ownership. Use selective disclosure to only share essential information and protect your data.
- anonymously register and connect to services, without revealing public identifier(s) such as email or phone number, and without a password.
- stop using public identifiers and control who can contact you. Revoke connections at will.

#### For Service Providers

- get your organization or person verifiable credential and link all your services to your credential so that users can clearly identify you and know they are connecting to the right service.
- ease user onboarding by removing registration forms and passwords.
- fast verify user's identity (and other claims) with no hassle.
- create hubs, meeting rooms, or other services protected by identity: users must present an identity credential to enter.
- issue Verifiable Credentials to your users and get paid when other organizations request presentation of the credential.
- build a verifiable trust reputation and be recognized.
- be searchable: add your services to the verifiable service directory

### The Verana App provides:

- interaction with the verana network, by querying the ledger and post transactions;
- statistics: ecosystem, blockchain, Verifiable Services (aka VSs).

## Terminology

TBW

## Specification

### [GENERAL] General

The Verana App MUST be delivered as a container.

#### [GENERAL-DEPLOYMENT] General - Deployment

- [GENERAL-DEPLOYMENT-HUB] Container MUST be versioned and deployed to docker hub.
- [GENERAL-DEPLOYMENT-DOCKER] Documentation for running the container with docker MUST be provided.
- [GENERAL-DEPLOYMENT-KUBE] Documentation for deploying the container in Kubernetes MUST be provided.
- [GENERAL-DEPLOYMENT-HELM] Verana App MUST be installable in Kubernetes by using helm install. Documentation MUST be provided.
- [GENERAL-DEPLOYMENT-LAMBDA] Verana App MUST be runnable in Amazon Lambda. Documentation MUST be provided.

#### [GENERAL-ENV] General - Container Variables

| Type                           |Variable                               | Description                    | Default Value (if unspecified)                    |
|--------------------------------|---------------------------------------|----------------------------------|----------------------------------|
| General                        | APP_NAME                              |                                  | Veranito                         |
|                                | APP_LOGO                              |                                  | logo.svg                        |
|                                | ADDRESS_EXPLORER                      |                                  | https://www.mintscan.io/verana/address/VERANA_ADDRESS   |
| Network Configuration          | MAINNET_API_ENDPOINT                  |                                  | https://api.verana.network       |
|                                | MAINNET_RPC_ENDPOINT                  |                                  | https://rpc.verana.network       |
|                                | MAINNET_IDX_ENDPOINT                  |                                  | https://idx.verana.network       |
|                                | MAINNET_CHAIN_ID                      |                                  | vna-mainnet-1       |
|                                | MAINNET_NAME                          |                                  | Mainnet       |
|                                | MAINNET_TOPUP_VS                      |   List of VSs for top-up       | did:example:123, did:example:456       |
|                                | TESTNET_API_ENDPOINT                  |                                  | https://api.testnet.verana.network       |
|                                | TESTNET_RPC_ENDPOINT                  |                                  | https://rpc.testnet.verana.network       |
|                                | TESTNET_IDX_ENDPOINT                  |                                  | https://idx.testnet.verana.network       |
|                                | TESTNET_CHAIN_ID                      |                                  | vna-testnet-1       |
|                                | TESTNET_NAME                          |                                  | Testnet       |
|                                | TESTNET_TOPUP_VS                      |   List of VSs for top-up       | did:example:123, did:example:456       |
|                                | DEVNETS__VNA-DEVNET_MAIN__API_ENDPOINT|                                  | https://api.vna-devnet-main.devnet.verana.network       |
|                                | DEVNETS__VNA-DEVNET_MAIN__RPC_ENDPOINT|                                  | https://rpc.vna-devnet-main.devnet.verana.network       |
|                                | DEVNETS__VNA-DEVNET_MAIN__IDX_ENDPOINT|                                  | https://idx.vna-devnet-main.devnet.verana.network       |
|                                | DEVNETS__VNA-DEVNET_MAIN__NAME        |                                  | Vna Devnet Main       |
|                                | DEVNETS__VNA-DEVNET_MAIN__TOPUP_VS    |   List of VSs for top-up       | did:example:123, did:example:456       |
|                                | DEFAULT_NETWORK                       |   Default selected network in App    | vna-mainnet-1       |
| Internationalization           | DEFAULT_LOCALE                        |   Failover locale | en_US       |
|                                | SUPPORTED_LOCALES                     |                                  | en_US, fr_FR, en:en_US, fr:fr_FR       |

#### General - Networks

[GENERAL-NETWORKS] All network declarations are optionals. Container MUST be configured with at least one network, else it cannot start and MUST log an error. Declared `DEFAULT_NETWORK` MUST exist else container startup MUST fail and log error. There can be only one Mainnet and one Testnet. An unlimited number of devnets can be configured. Add a devnet by creating a `DEVNETS__DEVNET_ID__*` env vars by replacing DEVNET_ID by the devnet id.

Example: to declare 2 devnets with id mydevnet-1 and mydevnet-2, declare:

- for mydevnet-1:

DEVNETS__MYDEVNET_1__API_ENDPOINT=...
DEVNETS__MYDEVNET_1__RPC_ENDPOINT=...
DEVNETS__MYDEVNET_1__IDX_ENDPOINT=...
DEVNETS__MYDEVNET_1__NAME=...
DEVNETS__MYDEVNET_1__TOPUP_VS=...

- for mydevnet-2:

DEVNETS__MYDEVNET_2__API_ENDPOINT=...
DEVNETS__MYDEVNET_2__RPC_ENDPOINT=...
DEVNETS__MYDEVNET_2__IDX_ENDPOINT=...
DEVNETS__MYDEVNET_2__NAME=...
DEVNETS__MYDEVNET_2__TOPUP_VS=...


#### General - Internationalization

[GENERAL-I18N-DEFAULT]

[GENERAL-I18N-LOCALE-DATA] All texts, labels, rollover texts, images with texts, videos, sounds, text icons MUST be centralized in a directory per locale

[GENERAL-I18N-CONTENT-KEY] Each content MUST be identified by its key, `content_key`.

[GENERAL-I18N-RENDER-CONTENT] Render content from `content_key`:

Get `locale` from `settings.locale` from user settings. If null, use `locale` from user agent.

- find content with its `content_key` for locale `locale`
- if not found, try to use the default locale for the same language. So if `locale` is equal to `en_GB`, look for entry en:... in `SUPPORTED_LOCALES` to get default locale for `en`.
- else fallback to `DEFAULT_LOCALE` (normally `en_US`).

:::note
At least the content of the default locale MUST be provided by development/design team.
Default locale for development MUST be en_US.
:::

:::warn
Right to left text (like Arabic) MUST be supported.
:::

#### [GENERAL-LAYOUT] General - Layout

[GENERAL-LAYOUT-RESPONSIVE] App MUST be usable from any device, layout MUST be responsive.

[GENERAL-LAYOUT-HEADER] Header MUST include a squared App logo and App name on the left side, and on the right side the setting icon, a dark/light mode, and a crypto account zone. Optionally, if layout is very small, a Menu hamburger icon CAN appear on te left side of the header, and the App name MAY disappear.

##### Header - Not Connected

![layout-header-not-connected](assets/layout-header-not-connected.png)

##### Header - Connected

![layout-header-connected](assets/layout-header-connected.png)

##### Header - Crypto account details

![layout-header-crypto-account](assets/layout-header-crypto-account.png)

[GENERAL-LAYOUT-MENU] On the left size, a menu. When size of window is small, menu is hidden and a hamburger icon appears for showing the menu.

[GENERAL-LAYOUT-MENU-NORMAL]

![normal menu](assets/layout-menu-normal.png)

[GENERAL-LAYOUT-MENU-SMALL]

![small menu](assets/layout-menu-small.png)

[GENERAL-LAYOUT-MENU-SMALL-OPENED]

![small menu - opened](assets/layout-menu-small-opened.png)

[GENERAL-LAYOUT-CONTENT] The content zone.

![content zone](assets/layout-content-zone.png)

### Menu

[MENU] Menu entries:

- Dashboard (default page): go to Dashboard  => [DASHBOARD]
- Account (user MUST be connected to see this menu entry) => [ACCOUNT-MAIN]
- DID Directory (user MUST be connected to see this menu entry) => [DIDS-LIST-DIDS-I-CONTROL]

### Crypto Wallet Integration

#### Crypto Wallet Integration - General

[CW-GENERAL-KIT]  Use a kit such as the [cosmos-kit repo](https://github.com/cosmology-tech/cosmos-kit) to easily integrate any wallet to the Verana App.

[CW-CONNECT-WALLET]

If user reaches the App through any URL of the App, and if a detected installed wallet is found and it has been already granted, App MUST connect to it immediately with no user intervention. (same will happen if I am connected and I reload the page in my browser).

- read the doc of cosmos-kit or any other library you want to use
- detect any installed wallet extension, and put them in the "Detected Installed Wallets" section.
- show available mobile wallets, in the "Mobile Wallets" section
- show available non mobile wallets not detected, in the "Other Wallets" section

![connect wallet](assets/cw-main.png)

#### Crypto Wallet - Browser Extension

[CW-CONNECT-WALLET-EXT]

Follow kit instructions and be inventive. Example mockup:

![connect wallet ext](assets/cw-connect-ext.png)

#### Crypto Wallet - Connect with Mobile

[CW-CONNECT-WALLET-MOB]

Follow kit instructions and be inventive. Example mockup:

![connect wallet mobile](assets/cw-connect-mobile.png)

#### Crypto Wallet - Connected

[CW-CONNECT-WALLET-CONNECTED]

Redirect user to where he was before connecting.

![just connected](assets/cw-justconnected.png)

### Dashboard

[DASHBOARD]

- show the network I am connect to (as selected in settings)
- show the block height
- If user is not connected, show a button "connect wallet"

![dashboard-not connected](assets/dashboard-notconnected.png)

![dashboard-not connected](assets/dashboard-connected.png)

### Crypto Transaction execution

[CRYPTO-TRANSACTIONS-DISPLAY-ZONE]

When a transaction is executed, it MUST be always shown as a popup. Transaction info (a text, _renew DID did:example:abc_ in the example below) MUST be passed as a description so that the display text can be shown in the popup.

![display zone](assets/transaction-display-zone.png)

[CRYPTO-TRANSACTIONS-EXEC] When executing a transaction:

- `Transaction in progress` MUST be shown with message "Your transaction _renew DID did:example:abc_ is being broadcasted to the network".
- when transaction ID is known, message should change to "Your transaction _renew DID did:example:abc_ is being processed [link](https://mintscan.com)" with a link to the transaction explorer.

![pending](assets/transaction-pending.png)

[CRYPTO-TRANSACTIONS-SUCCESS] when transaction is successful:

![success](assets/transaction-success.png)

[CRYPTO-TRANSACTIONS-ERROR] when error:

![error](assets/transaction-error.png)

### Account

[ACCOUNT-MAIN]

Account shows balances:

- Main balance
- Trust Deposit balance

and 3 use cases:

- Main Balance > get VNA: to top-up crypto account main balance.
- Trust Deposit > claim interests: to collect my Trust Deposit interests and receive them in my main balance. Use [MOD-TD-MSG-2] from verifiable-trust-vpr-spec.
- Trust Deposit > reclaim deposit: to get back claimable deposit, if any. Use [MOD-TD-MSG-3] from verifiable-trust-vpr-spec.

![account](assets/account.png)

Header Actions

- [ACCOUNT-HEADER-ACTIONS-QR] show QR of my account address
- [ACCOUNT-HEADER-ACTIONS-COPY] copy my account address
- [ACCOUNT-HEADER-ACTIONS-EXPLORE] show in configured explorer (`ADDRESS_EXPLORER`) (opens in new window)
- [ACCOUNT-HEADER-ACTIONS-LOGOUT] disconnect wallet

#### Account - Get VNA

Present a list of services to top-up my verana account.

The list of the services is configurable in variables `*TOPUP-VS` which depends on network. Use this list of service to generate a radio button type select. 

- [ACCOUNT-GET-VNA-RESOLVE-VS] Selected Verifiable Service MUST be trust resolved to get service name (service credential) and organization name (organization credential) shown in service description text, and get supported payment methods to show related icons.

- [ACCOUNT-GET-VNA-QR] MUST show a QR code for connecting to it and passing the vna account address as a parameter. User then scans the service with Hologram and follow instructions to top-up his/her account.

![account](assets/account-get-vna.png)

#### Account - Claim Interests

[ACCOUNT-TD-CLAIM-INTERESTS] If interests are available, user sees the text and the cancel / confirm buttons like in mockup. Else, show text "You do not have interests to claim yet." with no buttons.

![account](assets/account-claim.png)

#### Account - reclaim TD

[ACCOUNT-TD-RECLAIM] If reclaimable trust deposit is not equal to 0, user sees the text, confirm check, and the cancel / confirm buttons like in mockup. Else, show text "You do not have reclaimable trust deposit." with no check box and no buttons.

![account](assets/account-reclaim.png)

### Settings

All customized settings MUST be persisted in browser session.

[SETTINGS-MAIN] The Settings page MUST be shown when user hits the settings icon in header. Settings include 2 sections: General and Networks. Settings MUST work even if user is not connected.

![settings](assets/settings.png)

#### Settings - General

[SETTINGS-GENERAL-LOCALE-SELECT] Default to user agent presented locale "Browser Default" which sets `settings.locale` to  NULL (undefined). User can force a locale here and store it to `settings.locale`. Locale list MUST contain all supported locales. Changing locale does not require any confirmation and is immediate.

![alt text](assets/settings-general.png)

#### Network Selection

When a new session is created, default selected network MUST be set to `DEFAULT_NETWORK`.

[SETTINGS-NETWORKS-LIST] Show the list of existing networks, as defined in container env variables. UI MUST order the networks that way: first, mainnet, if declared, second, testnet, if declared, then devnet(s) ordered by id, if declared, then custom networks, ordered by creation date (newer first).

[SETTINGS-NETWORKS-BOOT-ERROR] If configured default network does not exist (not declared), container SHOULD NOT start and SHOULD log error message.

![network selection](assets/settings-network-selection.png)

#### Network Selection - Add Network

[SETTINGS-NETWORKS-ADD] user MAY add/remove custom networks that are persisted in browser session.

![add network](assets/settings-network-selection-add.png)

#### Network Selection - Added Network

![added network](assets/settings-network-selection-added.png)

#### Network Selection - Delete Network

[SETTINGS-NETWORKS-REMOVE] User CAN remove a network only if network is not currently selected.

![delete network](assets/settings-network-selection-delete.png)

#### Network Selection - Non mainnet - Header

[SETTINGS-NETWORKS-HEADER] when selected network is not mainnet, network name and its id MUST be shown in header.

![no mainnet](assets/settings-network-selection-no-mainnet-selected.png)

### DID Directory

#### List

[DIDS-LIST-RESULTS]

- search results are clickable and lead to DID info use case.
- search result pagination MUST be managed by frontend, as we can assume a given account will not have tons of DIDs, and because we want to be able to order result by clicking columns.

When screen size is reduced, column are progressively eliminated, in this order:

- created
- deposit
- controller
- modified

DID and expire MUST be shown always.

[DIDS-LIST-QUERY-PERSISTENCE]

By default, Did query option is preselected with "Show DIDs I control / All DIDs". When user customizes the query, query is persisted in user session. If user go to DID Info by clicking a result row, and go back to list using the browser "back" or clicks "back to directory" from other DID screens, query is loaded from session. If user hits the "DID Directory" menu, query session is cleared.  

[DIDS-LIST-DIDS-I-CONTROL]

- filters are self-explained (see [MOD-DD-QRY-1] List DIDs in VPR spec)

![list I control](assets/dids-search-list-i-control.png)

[DIDS-LIST-SEARCH-DID]

- User MUST write the full DID in order to do a search. Due to backend limitations, only the full DID name can be specified, subtext search is not supported. A better version will be specified when idx endpoint will be available.
- If a result is returned, save this DID in session so that we can use auto-completion when user wants to search again the same DID
- If a DID is in session but a new search doesn't return anything (removed DID), remove it from session.

![alt text](assets/dids-search-did.png)

[DIDS-LIST-FOR-CONTROLLER]

- controller is mandatory
- other filters are self-explained (see [MOD-DD-QRY-1] List DIDs in VPR spec)

![list for controller](assets/dids-search-list-for-controller.png)

#### DID Infos

[DIDS-DID-INFOS] Show DID infos and Action use cases:

- renew
- touch
- remove

![did infos](assets/dids-did-info.png)

#### Add a DID

[DIDS-DID-ADD] Adds a DID to the Directory. Use [MOD-DD-MSG-1-2-2] from VPR spec to estimate approx transaction cost.

- CANCEL: go back to where I was, with the same search filters
- CONFIRM: execute transaction, show transaction status until successful. If successful, go to DID Info.
- back to directory: return to DID directory, with current search filter (stored in session)

![add a DID](assets/dids-add.png)

#### Renew a DID

[DIDS-DID-RENEW] Renew a DID. Use [MOD-DD-MSG-2-2-2] from VPR spec to estimate approx transaction cost.

- CANCEL: close renew section
- CONFIRM: execute transaction, show transaction status until successful. If successful, refresh DID info data (without reloading page).
- back to directory: return to DID directory, with current search filter (stored in session)

![renew a DID](assets/dids-did-renew.png)

#### Touch a DID

[DIDS-DID-TOUCH] Renew a DID. Use [MOD-DD-MSG-4-2-2] from VPR spec to estimate approx transaction cost.

- CANCEL: close touch section
- CONFIRM: execute transaction, show transaction status until successful. If successful, refresh DID info data (without reloading page).
- back to directory: return to DID directory, with current search filter (stored in session)

![touch a DID](assets/dids-did-touch.png)

#### Remove a DID

[DIDS-DID-REMOVE] Renew a DID. Use [MOD-DD-MSG-3-2-2] from VPR spec to estimate approx transaction cost.

- CANCEL: close remove section
- CONFIRM: execute transaction, show transaction status until successful. If successful, return to DID directory, with previous search filter stored in session.
- back to directory: return to DID directory, with current search filter (stored in session)

![remove a DID](assets/dids-did-remove.png)