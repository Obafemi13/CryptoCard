```markdown
# 🪙 CryptoCard Smart Contract

CryptoCard is a Clarity smart contract for the Stacks blockchain that enables users to create, manage, and claim on-chain gift cards using STX. It supports advanced features such as expiry, cancellation, transfer, and sender gift tracking.

---

## 🚀 Features

- **Create Gift Cards:** Lock STX with a unique hash code, amount, and expiry block.
- **Claim Gifts:** Anyone with the hash code can claim the gift before expiry.
- **Extend Expiry:** Senders can extend the expiry of unclaimed gifts.
- **Increase Amount:** Senders can add more STX to an existing, unclaimed gift.
- **Cancel Gifts:** Senders can cancel unclaimed gifts and reclaim their STX.
- **Transfer Gifts:** Senders can transfer ownership of a gift to another principal.
- **Sender Gift Tracking:** Efficiently tracks up to 100 active gifts per sender.
- **On-chain Validation:** All actions are validated for authorization, expiry, and claim status.

---

## 📄 Contract Interface

### Public Functions

| Function | Description |
|----------|-------------|
| `create-gift (hash-code, amount, expiry-block)` | Create a new gift card. |
| `claim-gift (hash-code)` | Claim a gift if you have the hash code. |
| `extend-expiry (hash-code, new-expiry-block)` | Extend the expiry of your unclaimed gift. |
| `update-amount (hash-code, additional-amount)` | Add more STX to your unclaimed gift. |
| `cancel-gift (hash-code)` | Cancel your unclaimed gift and reclaim funds. |
| `transfer-gift (hash-code, new-sender)` | Transfer gift ownership to another principal. |

### Read-Only Functions

| Function | Description |
|----------|-------------|
| `get-sender-gifts (sender)` | Get a list of all gift hash-codes created by a sender. |
| `is-claimable (hash-code)` | Check if a gift is claimable (not claimed and not expired). |
| `get-gift-details (hash-code)` | Get all details for a specific gift. |

---

## 🛡️ Error Codes

| Constant                | Code | Description                                 |
|-------------------------|------|---------------------------------------------|
| `ERR_UNAUTHORIZED`      | u1   | Caller is not authorized for this action    |
| `ERR_ALREADY_CLAIMED`   | u2   | Gift has already been claimed               |
| `ERR_INVALID_EXPIRY`    | u3   | Expiry block is invalid                     |
| `ERR_NOT_FOUND`         | u4   | Gift not found                              |
| `ERR_INVALID_AMOUNT`    | u5   | Amount is zero or invalid                   |
| `ERR_INSUFFICIENT_FUNDS`| u6   | Not enough STX sent                         |
| `ERR_GIFT_EXPIRED`      | u7   | Gift has expired                            |
| `ERR_LIST_FULL`         | u8   | Sender's gift list is full                  |

---

## 🧑‍💻 Example Usage

```clarity
;; Create a gift
(create-gift 0x1234... u100 u5000)

;; Claim a gift
(claim-gift 0x1234...)

;; Extend expiry
(extend-expiry 0x1234... u6000)

;; Add more STX to a gift
(update-amount 0x1234... u50)

;; Cancel a gift
(cancel-gift 0x1234...)

;; Transfer a gift
(transfer-gift 0x1234... 'SP...NEWOWNER)
```

---

## 🏗️ Data Structures

- **gifts:**  
  `{ hash-code: (buff 32) } => { sender, amount, expiry-block, claimed }`
- **sender-gift-keys:**  
  `{ sender: principal } => (list 100 (buff 32))`

---
---


