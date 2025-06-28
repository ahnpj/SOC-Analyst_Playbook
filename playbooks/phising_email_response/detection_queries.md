**Suspicious Email Subject (in Office365)**</br>
DeviceEvents</br>
| where ActionType == "MailReceived"</br>
| where Subject has "invoice" and Subject has_any("urgent", "payment", "overdue")</br>
| project Timestamp, SenderFromAddress, RecipientEmailAddress, Subject</br>
