-- Suspicious Email Subject (in Office365)
DeviceEvents
| where ActionType == "MailReceived"
| where Subject has "invoice" and Subject has_any("urgent", "payment", "overdue")
| project Timestamp, SenderFromAddress, RecipientEmailAddress, Subject

