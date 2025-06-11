# 💸 Expense Splitter API

An API service for managing group expenses — inspired by Splitwise. It allows users to log expenses, split them among participants, track balances, and generate settlement summaries.

---

## 🚀 Local Setup

### 1. Clone the Repository

```bash
git clone https://github.com/HPrnav/split_app
cd backend
```
2. Install Dependencies
```bash
npm install
```
3. Start the Server
```bash
node index.js
```
## 🌍 Deployed URL
https://split-app-1-zsuk.onrender.com/api/v1/group

## 📬 Postman Collection
https://gist.githubusercontent.com/HPrnav/09861d1391ea7d166649cd7ecd7775f7/raw/e4339be0394512b7f08b13ddc6901d330df9178c/gistfile1.txt

## 📘 API Documentation
📌 Expense Management
GET /expenses — Fetch all expenses

POST /expenses — Add a new expense

PUT /expenses/:id — Update an existing expense

DELETE /expenses/:id — Remove an expense

### 👥 People & Balances
GET /people — Get list of all people

GET /balances — View net balance for each individual

GET /settlements — Get optimized settlement suggestions

GET /expenses/category-summary — Summary of expenses grouped by category

### ✍️ Example Requests
1. Equal Split
```json
{
  "amount": 600,
  "description": "Dinner at restaurant",
  "paid_by": "Shantanu",
  "split":{ { "user": "Shantanu" },
    { "user": "Sanket" },
    { "user": "Om" }
},
  "split_type": "equal",
  "category": "Food"
}
```
3. Percentage Split
```json
{
  "amount": 1000,
  "description": "Hotel Bill",
  "paid_by": "Shantanu",
  "split": {
    { "user": "Shantanu", "percent": 50 },
    { "user": "Sanket", "percent": 30 },
    { "user": "Om", "percent": 20 }
   },
  "category": "Travel"
}
```
4. Exact Share Split
``` json
{
  "amount": 900,
  "description": "Groceries",
  "paid_by": "Om",
  "split": {
    { "user": "Shantanu", "share": 300 },
    { "user": "Sanket", "share": 400 },
    { "user": "Om", "share": 200 }
   },
  "category": "Utilities"
}
```
✅ Sample Response
``` json
{
  "success": true,
  "data": {
    "_id": "123456",
    "amount": 900,
    "description": "Groceries",
    "paid_by": "Om",
    "split": {...},
    "category": "Utilities"
  },
  "message": "Expense added successfully"
}
```
## 🔄 Settlement Logic
This logic ensures the debts are settled with as few transactions as possible.

## 🔢 Process
Balance Calculation

Each participant’s net balance is calculated:

Total they paid minus total they owe.

Positive balance → they are owed money.

Negative balance → they owe money.

Transaction Optimization

Debtors are paired with creditors.

Payments are distributed so that all net balances reduce to zero.

The algorithm ensures the least number of transactions.

## 🧾 Example:
After all expenses:

Shantanu: +400

Sanket: -200

Om: -200

Settlements:

Sanket → Shantanu: ₹200

Om → Shantanu: ₹200

All balances settle to zero.

## 🧠 Why This Logic?
Promotes fairness by making sure everyone pays or receives their share.

Reduces financial clutter by minimizing transaction chains.

Scales well for group events, trips, or shared expenses.

## ⚠️ Limitations
$ no media upload option for uploading bill photos.
🌐 No frontend interface — API-only
⏱️ Real-time updates or notifications not included


