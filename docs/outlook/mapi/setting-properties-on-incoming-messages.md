---
title: "Setting Properties on Incoming Messages"
manager: soliver
ms.date: 3/9/2015
ms.audience: Developer
localization_priority: Normal
api_type:
- COM
ms.assetid: cf4a0501-f42b-4652-a239-003022686475
description: "Last modified: March 09, 2015"
 
 
---

# Setting Properties on Incoming Messages

  
  
**Applies to**: Outlook 
  
The client applications within the MAPI subsystem expect a number of properties in any received message. When the transport provider brings a message into MAPI, it should set these properties, since it is either the only process with the necessary information to do so, or is at least the best source of the information.
  
Providers are encouraged to set the values for all of these properties in incoming messages.
  
|**Property name**|**Description**|
|:-----|:-----|
|**PR_SUBJECT** ([PidTagSubject](pidtagsubject-canonical-property.md))  <br/> |The subject of the message.  <br/> |
|**PR_BODY** ([PidTagBody](pidtagbody-canonical-property.md))  <br/> |Plain text message text.  <br/> |
|**PR_RTF_COMPRESSED** ([PidTagRtfCompressed](pidtagrtfcompressed-canonical-property.md))  <br/> |Compressed RTF message text.  <br/> |
|**PR_MESSAGE_DELIVERY_TIME** ([PidTagMessageDeliveryTime](pidtagmessagedeliverytime-canonical-property.md))  <br/> |The date and time the message was delivered.  <br/> |
|**PR_SENDER_NAME** ([PidTagSenderName](pidtagsendername-canonical-property.md))  <br/> |The display name of the message originator.  <br/> |
|**PR_SENDER_ENTRYID** ([PidTagSenderEntryId](pidtagsenderentryid-canonical-property.md))  <br/> |The address book entry of the message originator.  <br/> |
|**PR_SENDER_SEARCH_KEY** ([PidTagSenderSearchKey](pidtagsendersearchkey-canonical-property.md))  <br/> |The address book search key of the message originator.  <br/> |
|**PR_CLIENT_SUBMIT_TIME** ([PidTagClientSubmitTime](pidtagclientsubmittime-canonical-property.md))  <br/> |The time that the message was submitted to its messaging system by the sender's messaging client.  <br/> |
|**PR_SENT_REPRESENTING_NAME** ([PidTagSentRepresentingName](pidtagsentrepresentingname-canonical-property.md))  <br/> |The name of the representative delegate for sending.  <br/> |
|**PR_SENT_REPRESENTING_ENTRYID** ([PidTagSentRepresentingEntryId](pidtagsentrepresentingentryid-canonical-property.md))  <br/> |The address book entry of the sending delegate.  <br/> |
|**PR_SENT_REPRESENTING_SEARCH_KEY** ([PidTagSentRepresentingSearchKey](pidtagsentrepresentingsearchkey-canonical-property.md))  <br/> |The address book search key of the sending delegate.  <br/> |
|**PR_RCVD_REPRESENTING_NAME** ([PidTagReceivedRepresentingName](pidtagreceivedrepresentingname-canonical-property.md))  <br/> |The name of the representative delegate for receiving.  <br/> |
|**PR_RCVD_REPRESENTING_ENTRYID** ([PidTagReceivedRepresentingEntryId](pidtagreceivedrepresentingentryid-canonical-property.md))  <br/> |The address book entry of the receiving delegate.  <br/> |
|**PR_RCVD_REPRESENTING_SEARCH_KEY** ([PidTagReceivedRepresentingSearchKey](pidtagreceivedrepresentingsearchkey-canonical-property.md))  <br/> |The address book search key of the receiving delegate.  <br/> |
|**PR_REPLY_RECIPIENT_NAMES** ([PidTagReplyRecipientNames](pidtagreplyrecipientnames-canonical-property.md))  <br/> |The list of delegated recipient display names, separated by a semicolon and space ("; ").  <br/> |
|**PR_REPLY_RECIPIENT_ENTRIES** ([PidTagReplyRecipientEntries](pidtagreplyrecipiententries-canonical-property.md))  <br/> |The list of delegated recipients for a reply.  <br/> |
|**PR_MESSAGE_TO_ME** ([PidTagMessageToMe](pidtagmessagetome-canonical-property.md))  <br/> |Indicates that the recipient was specifically named as a "to" recipient (not in a group).  <br/> |
|**PR_MESSAGE_CC_ME** ([PidTagMessageCcMe](pidtagmessageccme-canonical-property.md))  <br/> |Indicates that the recipient was specifically named as a "cc" recipient (not in a group).  <br/> |
|**PR_MESSAGE_RECIP_ME** ([PidTagMessageRecipientMe](pidtagmessagerecipientme-canonical-property.md))  <br/> |Indicates that the recipient was specifically named as a "to", "cc" or "bcc" recipient (not in a group).  <br/> |
   
Providers that have no apparent mappings can set the **PR_SENT_REPRESENTING** group of properties to the same values as the **PR_SENDER** group, the **PR_RCVD_REPRESENTING** group of properties to the same values as the **PR_RECEIVED_BY** group, and can build the **PR_REPLY_RECIPIENT** group of properties based on the values of the **PR_SENDER** group. For example, **PR_SENT_REPRESENTING_NAME** can be set to the same value as **PR_SENDER_NAME**.
  
The **PR_ENTRYID** or **PR_ENTRYLIST** property can be generated, if necessary, by calling the [IMAPISupport::CreateOneOff](imapisupport-createoneoff.md) method. The **PR_SEARCH_KEY** group of properties can be generated by concatenating the **PR_ADDRTYPE** property associated with a user, a colon (:), and the **PR_EMAIL_ADDRESS** property associated with the user, then changing the result to uppercase. The Windows API function **CharUpperBuff** is a convenient function to use for this purpose. What is required of this process is to make a canonical form of the address that can be compared as a binary quantity. Note that this is not necessary if the transport provider is case-sensitive with respect to e-mail addresses. 
  
