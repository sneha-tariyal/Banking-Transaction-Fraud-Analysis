-- PROJECT: Banking Transaction & Fraud Analysis

/* Objective:
Analyze banking transactions using PostgreSQL to identify fraudulent transaction patterns,
high-risk transaction types,transaction-value patterns, and balance anomalies.
*/

Create Table transactions(step int,
     transaction_type varchar(20),
	 amount numeric(15,2),
	 sender varchar(50),
	 sender_balance_before numeric(15,2),
	 sender_balance_after numeric(15,2),
	 receiver_account varchar(50),
	 receiver_balance_before numeric(15,2),
	 receiver_balance_after numeric(15,2),
	 is_fraud int,
	 is_flagged_fraud int
	 );

-- Import Data into transactions Table
-- CSV file used: paysim.csv
-- Data imported using PostgreSQL COPY command.

-- Data Quality & Validation
select * from transactions limit(10);

-- Identify missing values in critical transaction fields?
select count(*) filter(where transaction_type is null) as missing_transaction_type,
 count(*) filter(where amount is null)as missing_amount,
 count(*) filter(where sender is null)as missing_sender,
 count(*) filter(where receiver_account is null)as missing_receiver
from transactions;

-- Identify transactions with invalid negative amounts?
select count(*)as negative_amount_transactions from transactions
where amount < 0;

-- Validate fraud indicators recorded using valid values?
select is_fraud,is_flagged_fraud,count(*)as transaction_count from transactions
group by is_fraud, is_flagged_fraud order by is_fraud, is_flagged_fraud;

--1 Identify the total number of transactions.	
select count(*) as total_transactions from  transactions;

--2 Which transaction types are used most frequently?
select transaction_type,count(*) as transaction_count from transactions
group by transaction_type;

--3 What is the total transaction value?
select sum(amount) as total_transaction_value from transactions;

--4 How many transactions are fraudulent and how many are normal?
select is_fraud,count(*) as transaction_count from transactions 
group by is_fraud;

--5 What percentage of all transactions are fraudulent?
select Round(100.0* sum(case when is_fraud = 1 Then 1 Else 0 End)/count(*),2) 
as fraud_rate_percentage from transactions;

--6 Which transaction types have the highest number of fraudulent transactions?
select transaction_type, count(*) as fraudulent_transaction from transactions
where is_Fraud =1 group by transaction_type order by fraudulent_transaction desc;

--7 What is the fraud rate for each transaction type?
select transaction_type,round(100.0*sum(case when is_fraud = 1 then 1 else 0 end)/count(*),2)
as fraud_rate_percentage from transactions group by transaction_type 
order by fraud_rate_percentage desc;

--8 What is the average transaction amount for fraudulent transactions compared with normal transactions?
select is_fraud,round(avg(amount),2) as average_transaction_amount from transactions group by is_Fraud
order by is_fraud;

--9 Which transaction types have the highest average transaction amount for fraudulent transactions?
select transaction_type,round(avg(amount),2)as average_fraud_amount from transactions 
where is_Fraud = 1 group by transaction_type order by average_fraud_Amount desc;

--10 Which time steps have the highest number of fraudulent transactions?
select step, count(*) as fraudulent_transactions from transactions where is_Fraud =1
group by step order by fraudulent_transactions desc;

--11 Which time steps have the highest total fraudulent transaction amount?
select step,sum(amount) as total_fraudulent_transaction from transactions where is_Fraud=1
group by step order by total_fraudulent_transaction desc;

--12 Which transaction types have the highest total fraudulent transaction amount?
select transaction_type,sum(amount)as total_fraudulent_amount from transactions where is_fraud=1
group by transaction_type order by total_fraudulent_amount desc;

--13 Which transaction types have the highest average amount for all transactions?
select transaction_type,round(avg(amount),2)as average_amount from transactions
group by transaction_type order by average_amount desc;

--14 Which transaction types have the highest total transaction value?
select transaction_type,sum(amount)as total_transaction_value from transactions group by transaction_type
order by total_transaction_value desc;

--15 Which fraudulent transactions occurred when the sender's balance was insufficient to cover the transaction amount?
select sender_balance_before,amount from transactions where is_fraud=1 and sender_balance_before<amount;

--16 Which transaction types have the highest number of fraudulent transactions with zero sender balance after the transaction?
select transaction_type,count(*)as zero_balance_transaction from transactions where is_fraud=1 and sender_balance_after=0
group by transaction_type order by zero_balance_transaction desc;

--17 Which fraudulent transactions involved the highest transaction amounts?
select step,transaction_type,amount,sender,receiver_account from transactions where is_Fraud=1 order by amount desc
limit 10;

--18 Which sender accounts are involved in the highest number of fraudulent transactions?
select sender,count(*) as fraudulent_transaction from transactions where is_fraud=1 group by sender
order by fraudulent_transaction desc;

--19 Which receiver accounts received the highest number of fraudulent transactions?
select receiver_account,count(*)as fraudulent_transaction from transactions where is_fraud=1 group by receiver_account
order by fraudulent_transaction desc;

--20 Which fraudulent transactions caused the receiver's balance to increase by more than the transaction amount?
select receiver_account,amount,receiver_balance_before,receiver_balance_after from transactions where is_Fraud=1
and(receiver_balance_after - receiver_balance_before)>amount
order by(receiver_balance_after - receiver_balance_before) desc;

--21 How many fraudulent transactions were not flagged by the system?
select count(*)as unflagged_fraudulent_transaction from transactions where is_fraud=1 and is_flagged_fraud=0;


/* Key Findings:
1. Total transactions analyzed:2,097,150
2. Fraudulent transactions:2,284
3. Overall fraud rate: 0.11%
4. Fraud was mainly concentrated in TRANSFER and CASH_OUT transactions.
5. Average Fraudulent transaction amount was approximately ₹11.93 lakh, 
   compared with ₹1.58 lakh for normal transactions.
*/


/* Business Recommendations:
1. Closely monitor TRANSFER and CASH-OUT transactions.
2. Use high transaction amounts as an additional fraud-monitoring factor.
3. Monitor unusual time-based spikes in fraudulent activity.
*/
