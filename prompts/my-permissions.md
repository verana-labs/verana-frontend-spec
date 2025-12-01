# Permission Management

## Participants

Build the "Participants" page.

This view must show on the top a breadcrumbs indicating:

- ecosystem name
- the credential schema title

Show:

- a select called "show" with the options: My Permissions, Full Permission Tree, Search => default to My Permissions. When search is selected, user can input text to filter per did or grantee account
- a select called "filter permissions" with the options: All, Pending Actions, Active Permissions, Slashed not Repaid, Expired Permissions, Expired Validation Process => default All.
- a list of my permissions as cards (one card per row, ideally horizontal content, if window width is reduced (mobile), then content of card can switch to vertical), with pagination support.
On the right side, three vertical dots for showing a small menu, with the following entries: "Renew a Permission", "Repay Slash Deposit". Both option trigger a transaction. Make sure the three dot menu is always on the top right side of the card, and the state label on the top left, no matter the width of the screen, and that they are aligned horizontally. Make sure that both the ID and the DID are each one always on their own row (full width of the card), below the state label.
Use state labels, exactly one per card, green for "active", yellow for "expire in 2 weeks", grey for "expired", red for "slashed", light red for "repaid". Do not use background color for cards. Make sure all card content is fully visible depending on window width.

  id: uint64
  did: string => id of the service linked to this permission
  created: timestamp => date of creation of the permission
  modified: timestamp => date the permission was last modified
  extended: timestamp => date the permission was last extended
  slashed: timestamp => date the permission was last slashed
  repaid: timestamp => date the permission was last repaid
  revoked: timestamp => date the permission was revoked
  effective_from: timestamp => date the permission is effective from
  effective_until: timestamp => date the permission expires
  validation_fees: number => fees that must pay applicants that want to run a validation process
  issuance_fees: number => fees charged by this participant when a child permission issues a credential
  verification_fees: number => fees charged by this participant when a child permission verifies a credential of this schema
  deposit: number => deposit managed by this permission (trust value of the permission)
  slashed_deposit: number => amount of deposit that has been slashed
  repaid_deposit: number => amount of deposit that has been repaid
  country: string => country this permission applies to
  +vp_exp: timestamp => date the validation process of this permission will expire
  +vp_last_state_change: timestamp => date the validation process of this permission last changed state
  +vp_validator_deposit: number => deposit managed by this validation process
  +vp_current_fees: number => validation process escrowed fees
  +vp_current_deposit: number => deposit managed by this validation process 
  +vp_summary_digest_sri: digest_sri => checksum of the documentation linked to this permission

additionally, each permission card must show the number of grantees (sub-permission on the permission tree for which my permission is acting as a validator) example: 123, clearly visible with a nice icon, and a number in a colored disc on the top right side corresponding to the number of grantee permissions that require an action from my side, example: 12. A click to this icon/link leads to a new view (of the same page, managed in the same html) called "Grantees of #type permission #id" where #type is the permission type (ISSUER, ISSUER_GRANTOR, VERIFIER, VERIFIER_GRANTOR, ECOSYSTEM) and #id the id of the permission. Number of grantee must be on the left side of the three dot menu.


**View of "Grantees of #type permission #id:**

This view must show on the top a breadcrumbs (items must all be clickable) indicating:

- ecosystem name
- the credential schema title
- the history of permissions clicks since the initial page, each permission named "#type permission #id"

below, show:

- title: "Grantees of #type permission #id" (the permission that were clicked to arrive here)
- a select called "filter permissions" with the options: All, Pending Actions, Active Permissions, Slashed not Repaid, Expired Permissions, Expired Validation Process => default All.
- a search field with an input that accept filtering per did or grantee account
- a list of permission card (same design and features as in previous page), with pagination support (same design than above).