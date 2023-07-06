**DAML Fundamentals Capstone Project** 

** I.Project Overview **
The project's overall idea is to manage money in a particular facility, in this case
a bank. The amount would be a single storage element hence only one account.
Templates that are included in the project are - 
TotalBalance, AddBalanceRequest, WithdrawBalanceRequest, RejectRequest 

TotalBalance the contract will be holding the information about how much balance would be
deposited .

AddBalanceRequest a proposal/ request contract that will be have the information for the 
balance amount to be requested to supplier.

WithdrawBalanceRequest, a proposal/ request contract that will have the information for 
balance amount consumed.

RejectRequest, the contract holds information about any request / proposal being rejected 
including a description and the operation type.

Parties involved: 
* Bank, the party that is in the charge of the bank and accepts/ rejects proposals.
* Customer, the party that can propose a operation inside the bank and also has visibility 
on what is happening 
* Auditor, the party that only has visibility over the contracts but never participates
in any other way.

** II.Project Flow **

- The ledger is already started with TotalBalance contract with customer and auditor as 
observers, a balance amount and some other fields.

- In case that the customer sees fit to propose a request a more amount he can do so by exercising
the choice RequestAddBalance.
This choice takes a supplier field( this field is ust a text field that records a supplier name,
nothing else was implemented to not add up complexity and the amount that he sees fit and it 
creates a AddBalanceRequest that will create a RejectedRequest contract.
    - The request can be then approved by the bank by exercising AcceptAddBalanceRequest.
      This acceptance choice would be create a new TotalBalance contract with the new amount
      and archive the previous one.
    - Otherwise the bank can reject the Request by exercising the choice RejectAddBalanceRequest
      that will create a RejectedRequest Contract.

- When it's time to update log the balance consumption the customer can request the balance 
  consumption so that the manager can analyze it and accept/ reject it. The request is 
  done by the customer exercising the choice.
    - Be accepted by the bank by exercising AcceptBalanceConsumption. This acceptance 
      choice would create a new TotalBalance Contract with the new amount and consuming
      previous one.
    - Be rejected can also exercise straight forward the choice ConsumeWater that creates
      a new TotalBalance contract with the new amount and consumes previous one.

- The bank can also exercise straight forward the choice WithdrawBalance that creates a new
  TotalBalance and RevokeBalanceRequest, this exercise will consume the contract and end up
  revoking them.

** III How to run the system**

- DAML Studio - 
Daml Studio can be started by running command ==daml studio== when inside the project folder

- BUILD - 
The project can built by running command daml ==build==.

- CLEAN - 
The project build artifacts can be cleaned by running command ==daml clean==.

- DAML Sandbox
Daml Sandbox can be started by running command ==daml start==.
