# Allowed actions for accounts<a name="securityhub-accounts-allowed-actions"></a>

Master and member accounts have access to the following Security Hub actions\. In the table, the values have the following meanings:
+ **Any –** The account can perform the action for all of the accounts under the same Security Hub administrator or master account\.
+ **Self –** The account can only perform the action on their own account\.

A dash \(–\) indicates that the account cannot perform the action\.


|  Action  |  Security Hub administrator \(Organization\)  |  Master account \(Invitation\)  |  Member \(Organization\)  |  Member \(Invitation\)  | 
| --- | --- | --- | --- | --- | 
|  View accounts  |  Any  |  Any  |  \-  |  \-  | 
|  Disassociate member account  |  Any  |  Any  |  \-  |  Self  | 
|  Delete member account  |  Any non\-organization account  |  Any  |  \-  |  \-  | 
|  Disable Security Hub  |  \-  |  Self \- if there are no enabled member accounts  |  Self \- if disassociated from the Security Hub administrator account  |  Self \- if disassociated from the master account  | 
|  View findings  |  Any  |  Any  |  Self  |  Self  | 
|  Update findings  |  Any  |  Any  |  Self  |  Self  | 
|  View insight results  |  Any  |  Any  |  Self  |  Self  | 
|  View control details  |  Any  |  Any  |  Self  |  Self  | 
|  Enable and disable controls  |  Self  |  Self  |  Self  |  Self  | 
|  Enable and disable standards  |  Self  |  Self  |  Self  |  Self  | 
|  Enable and disable integrations  |  Self  |  Self  |  Self  |  Self  | 
|  Configure custom actions  |  Self  |  Self  |  Self  |  Self  | 