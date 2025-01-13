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

In order to fully understand the concepts developed in this document, you should have some basic knowledge of [[ref:trust registry]], [[ref: pubic trust registry]], [[ref:DIDComm]], [[ref:DTS]], ledger-based applications, and more generally, all terms present in the [Terminology](#terminology) section.

## Introduction

The Verana App provides:

- interaction with the verana network, by querying the ledger and post transactions;
- statistics (ecosystem, blockchain, DTSs).

## Terminology

[[def: account, accounts]]:
~ A [[ref: public trust registry]] account.

[[def: applicant, applicants]]:
~ A [[ref: controller]] that starts a [[ref: validation process]].

[[def: controller, controllers]]:
~ An [[ref: account]] which is the controller of a specific resource in an [[ref: PTR]].

[[def: credential schema, credential schemas]]:
~ An [[ref: PTR]] resource which represents a verifiable credential definition and the associated permissions and business rules for issuing, verifying or holding a credential linked to this credential schema.

[[def: decentralized identifier, DID, DIDs]]:
~ A decentralized identifier, as specified in [[spec-norm:DID-CORE]].

[[def: decentralized identifier communication, DIDComm]]:
~ [DIDComm](https://identity.foundation/didcomm-messaging/spec/) uses [[ref: DIDs]] to establish confidential, ongoing connections.

[[def: decentralized identifier document, DID Document, DID Documents]]:
~ A DID Document, as specified in [[spec-norm:DID-CORE]].

[[def: decentralized trust service, DTS, DTSs]]:
~ A service, usually provided using [[ref: DIDComm]], that can be deployed anywhere by its owner, and that is using the decentralized trust layer provided by an [[ref: PTR]], and has a resolvable [[ref: proof of trust]].

[[def: decentralized trust user agent, DTUA, DTUAs]]:
~ A user agent for accessing and using [[ref: DTSs]]. To be considered as a [[ref: DTUA]], a user agent must implement an [[ref: PTR]] trust layer and use a trust resolution using use the [[ref: essential credential schema]] of a given trust registry for providing a [[ref: proof of trust]] to users so that user clearly identifies [[ref: DTS]] and [[ref: DTUA]] providers and decides to connect or not.

[[def: DID Directory, DID directory]]:
~ A repository of DIDs in an PTR.

[[def: essential credential schema, essential credential schemas]]:
~ Default [[ref: credential schema]], owned by a [[ref: trust registry]], that provide the basis for a trust layer to exist in the ecosystem so that [[ref: DTUA]] can generate a [[ref: proof of trust]].

[[def: holder, holders]]:
~ A role an entity might perform by possessing one or more verifiable credentials and generating verifiable presentations from them. A holder is often, but not always, a [[ref: subject]] of the verifiable credentials they are holding. Holders store their credentials in credential repositories. Example holders include organizations, persons, things.

[[def: issuer, issuers]]:
~ A role an entity can perform by asserting claims about one or more [[ref: subjects]], creating a verifiable credential from these claims, and transmitting the verifiable credential to a [[ref: holder]]. Example issuers include corporations, non-profit organizations, trade associations, governments, and individuals.

[[def: json schema, json schemas]]:
~ A json schema as defined in [JSON-SCHEMA](https://json-schema.org).

[[def: json schema credential, json schema credentials]]:
~ A json schema credential as defined in [[spec-norm:VC-JSON-SCHEMA]].

[[def: linked-vp]]:
~ A presentation of a [[ref: verifiable credential]] as specified in [LINKED-VP](https://identity.foundation/linked-vp/).

[[def: participant, participants]]:
~ An entity that uses an [[ref: PTR]] and its trust layer to provide or use services.

[[def: proof of trust]]:
~ Visual representation using [[ref: essential credential schemas]] of a [[ref: trust resolution]] process of a [[ref: DTS]], for identifying the [[ref: DTS]], its owner, and the [[ref: issuer]] of the verifiable credential of its owner.

[[def: public trust registry, PTR]]:
~ a decentralized, ledger-based network, which provides: trust registry features that can be used by all its [[ref: participants]]; and a tokenized business model allows charging [[ref: participants]] for trust fees that are transferred to other [[ref: participants]], or locked into [[ref: trust deposits]].

[[def: subject, subjects]]:
~ A thing about which claims are made. Example subjects include human beings, animals, things, and organization, a [[ref: DID]]...

[[def: trust deposit, trust deposits]]:
~ A financial deposit that is used as a trust guarantee. For a given [[ref: controller]], its trust deposit is increased when running validation process (either as an [[ref: applicant]] or as a [[ref: validator]]), or when registering [[ref: DID]] in the DID directory.

[[def:trust registry, trust registries]]
~ An approved list of [[ref: issuers]] and [[ref: verifiers]] that are authorized to issue/verify certain credentials in an ecosystem.

[[def: trust resolution]]:
~ Process run by, for example a [[ref: DTUA]], which purpose is to recursively resolve [[ref: DID]] by digging into [[ref: DID Documents]] and look for [[ref: linked-vp]] entries and their [[ref: issuer]] [[ref: DIDs]], and [trust registry](https://trustoverip.github.io/tswg-trust-registry-protocol/) entries to gather whether the service provided by the [[ref: DID]] is trustable (and legitimate), or not.

[[def: validation process]]:
~ A process run by [[ref: applicants]] that want to, for a specific [[ref: credential schema]], be a [[ref: issuer]], be a [[ref: verifier]], or simply hold a verifiable credential linked to the [[ref: credential schema]].

[[def: validator]]:
~ A role an entity performs by participating in validation processes with [[ref: applicants]] in order to register them as [[ref: issuer]], or [[ref: verifier]] of a [[ref: credential schema]], or to deliver a verifiable credential to them.

[[def: verifier, verifiers]]:
~ A role an entity performs by receiving one or more verifiable credentials, optionally inside a verifiable presentation for processing. Example verifiers include service providers.

[[def: verifiable credential, verifiable credentials]]:
~ A verifiable credential as defined in [[spec-norm:VC-DATA-MODEL]].

## Specification

### [GENERAL] General

#### [GENERAL-ENV] General - Container Variables


| Type                           |Variable                               | Description                    | Default Value                    |
|--------------------------------|---------------------------------------|----------------------------------|----------------------------------|
| Network Configuration          | MAINNET_API_ENDPOINT                  |                                  | https://api.verana.network       |
|                                | MAINNET_RPC_ENDPOINT                  |                                  | https://rpc.verana.network       |
|                                | MAINNET_IDX_ENDPOINT                  |                                  | https://idx.verana.network       |
|                                | MAINNET_CHAIN_ID                      |                                  | vna-mainnet-1       |
|                                | TESTNET_API_ENDPOINT                  |                                  | https://api.testnet.verana.network       |
|                                | TESTNET_RPC_ENDPOINT                  |                                  | https://rpc.testnet.verana.network       |
|                                | TESTNET_IDX_ENDPOINT                  |                                  | https://idx.testnet.verana.network       |
|                                | TESTNET_CHAIN_ID                      |                                  | vna-testnet-1       |
|                                | DEVNET_API_ENDPOINT                   |                                  | https://api.vna-devnet-main.devnet.verana.network       |
|                                | DEVNET_RPC_ENDPOINT                   |                                  | https://rpc.vna-devnet-main.devnet.verana.network       |
|                                | DEVNET_IDX_ENDPOINT                   |                                  | https://idx.vna-devnet-main.devnet.verana.network       |
|                                | DEVNET_CHAIN_ID                       |                                  | vna-devnet-main       |
|                                | DEFAULT_NETWORK                       |                                  | vna-testnet-1       |
| Internationalization           | DEFAULT_LOCALE                        |                                  | en_US       |
| Internationalization           | SUPPORTED_LOCALES                        |                                  | en_US, fr_FR, en:en_US, fr:fr_FR       |

#### [GENERAL-SETTINGS] General - Settings

All settings MUST be persisted in browser session.

[GENERAL-SETTINGS-NETWORK-DEFAULT] When a new session is created, default selected network MUST be set to `DEFAULT_NETWORK`.

[GENERAL-SETTINGS-NETWORK-MANAGE] In Settings/Network, user can see pre-configured networks and their endpoints (Mainnet, Testnet, Devnet). Additionally, user CAN add custom networks and save. Custom networks MUST be persisted in session.

[GENERAL-SETTINGS-NETWORK-SELECT] User CAN select a network. Network list MUST show Mainnet, Testnet, Devnet, and custom networks.

[GENERAL-SETTINGS-NETWORK-SELECTED] If selected network is not Mainnet, its name MUST appear in App header.

[GENERAL-SETTINGS-LOCALE-SELECT] Default to user agent presented locale "Browser Default" which sets `settings.locale` to  NULL (undefined). User can force a locale here and store it to `settings.locale`. Locale list MUST contain all supported locales.

#### [GENERAL-I18N] General - Internationalization

[GENERAL-I18N-DEFAULT]

[GENERAL-I18N-LOCALE-DATA] All texts, labels, rollover texts, images with texts, videos, sounds, text icons MUST be centralized in a directory per locale

[GENERAL-I18N-CONTENT-KEY] Each content MUST be identified by its key, `content_key`.

[GENERAL-I18N-RENDER-CONTENT] Render content from `content_key`:

Get `locale` from `settings.locale` from user settings. If null, use `locale` from user agent.

- find content with its `content_key` for locale `locale`
- if not found, try to use the default locale for the same language. So if `locale` is equal to `en_GB`, use mapper to get default locale for `en`.
- else fallback to `DEFAULT_LOCALE` (usually `en_US`).

:::Note
At least the content of the default language MUST be provided by development/design team.
Default language for development MUST be english.
:::

:::Warn
Right to left text (like Arabic) MUST be supported.
:::

#### [GENERAL-I18N] General - Layout

[GENERAL-LAYOUT-RESPONSIVE] App MUST be usable from any device, layout MUST be responsive.

[GENERAL-LAYOUT-HEADER] Header MUST include the Verana App logo and name on the left, the setting icon, a dark/light mode, and an account zone.

### Crypto Wallet Integration

#### [CW-GENERAL]

Use a kit such as the [cosmos-kit repo](https://github.com/cosmology-tech/cosmos-kit) to easily integrate any wallet to the Verana App.

### [CW-CONNECT-WALLET]

![alt text](image.png)

#### [CW-KEPLR] Keplr Integration

- [CW-KEPLR-BW] The Verana App MUST integrate the [Keplr](https://keplr.app/) browser wallet for signing transactions.
- [CW-KEPLR-APP] The Verana App MUST integrate the [Keplr](https://keplr.app/) mobile app wallet for signing transactions.

#### [CW-LEAP] Leap Integration

- [CW-LEAP-BW] The Verana App MUST integrate the [Leap](https://www.leapwallet.io/) browser wallet for signing transactions.
- [CW-LEAP-APP] The Verana App MUST integrate the [Leap](https://www.leapwallet.io/) mobile app wallet for signing transactions.

### Trust Registry

#### List

#### 

### Credential Schemas

### DID Directory

#### List my entries

#### Add a DID

#### Renew a DID

#### Touch a DID

#### Remove a DID