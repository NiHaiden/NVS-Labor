---
title: NVS Email
author: Niklas Haiden, Marcel Denk - 5BHIF
date: 22.03.2022
tableofcontent: true
titlepage: true
titlepage-text-color: "000000"
logo: "logo.png"
logo-width: 100mm
toc-own-page: true
listings-disable-line-numbers: true
---

# Theory
## IMAP 
https://whatis.techtarget.com/definition/IMAP-Internet-Message-Access-Protocol

### What is IMAP (Internet Message Access Protocol)?

Internet Message Access Protocol, or IMAP, is a standard [email](https://whatis.techtarget.com/definition/e-mail-electronic-mail-or-email) retrieval (incoming) [protocol](https://www.techtarget.com/searchnetworking/definition/protocol). It stores email messages on a [mail server](https://whatis.techtarget.com/definition/mail-server-mail-transfer-transport-agent-MTA-mail-router-Internet-mailer) and enables the recipient to view and manipulate them as though they were stored locally on their device(s).

IMAP enables users to organize messages into folders, flag messages for urgency or follow-up, and save draft messages on the server. Users can also have multiple email [client](https://www.techtarget.com/searchenterprisedesktop/definition/client) applications that sync with the email server to consistently show which messages have been read or are still unread.

### How does IMAP work?

As an incoming email protocol, IMAP functions as the intermediary between the email server and email client. When users read an email using IMAP, they read them off the server. They don't actually download or store the email on their local device. This means that the email is not tied to a particular device, and users can access it from any location in the world using different devices, such as the following:

-   desktop PC
-   laptop
-   smartphone
-   tablet

These are the general steps and processes involved in an IMAP operation:

-   When a user signs into the email client -- e.g., [Microsoft Outlook](https://www.techtarget.com/searchwindowsserver/definition/Microsoft-Outlook) -- the client contacts the server using IMAP.
-   The connection is made on a specific port.
-   The headers of all emails are displayed by the email client.
-   IMAP only downloads a message to the client when the user clicks on it; attachments are not automatically downloaded.
-   Users can check their messages much more quickly with IMAP than with other email retrieval protocols, like Post Office Protocol 3 ([POP3](https://whatis.techtarget.com/definition/POP3-Post-Office-Protocol-3)).
-   Email messages remain on the server unless the user explicitly deletes them.

An IMAP server listens on [port number](https://www.techtarget.com/searchnetworking/definition/port-number) 143, while IMAP over Secure Sockets Layer ([SSL](https://www.techtarget.com/searchsecurity/definition/Secure-Sockets-Layer-SSL))/[Transport Layer Security](https://www.techtarget.com/searchsecurity/definition/Transport-Layer-Security-TLS) is assigned port number 993.

### Advantages and limitations of IMAP

#### Advantages

Most implementations of IMAP support multiple logins. This enables users to simultaneously connect to the email server from different devices. For example, users simultaneously could access their email with an Outlook app on an [iPhone](https://www.techtarget.com/searchmobilecomputing/definition/iPhone), as well as an Outlook desktop app.

Multiple accesses are not possible with POP3, where downloaded emails disappear from the server and, therefore, cannot be accessed from a different device later. So, POP3 is only suitable when users access their email from the same device every time.

IMAP provides greater access flexibility for users who travel often or need to check their email from different devices or locations. The details for how to handle multiple connections are not specified by the protocol, but are instead left to the developers of the mail client.

In brief, the advantages of IMAP are the following:

-   emails accessible from multiple devices;
-   fast and efficient access;
-   a single mailbox can be shared by multiple users;
-   users can organize emails on the server by creating folders and subfolders;
-   support for email functions, like search and sort;
-   IMAP server supports IDLE extensions (push mail) so the email is displayed in the inbox as unread, eliminating the need to set up a polling interval or requiring users to first click on **receive**; and
-   can be used offline.

#### Limitations

Even though IMAP has an [authentication](https://www.techtarget.com/searchsecurity/definition/authentication) mechanism, the authentication process can easily be circumvented by anyone who knows how to steal a password by using a [protocol analyzer](https://www.techtarget.com/searchnetworking/definition/network-analyzer) because the client's username and password are transmitted as cleartext.

In an [Exchange Server](https://www.techtarget.com/searchwindowsserver/definition/Microsoft-Exchange-Server) environment, administrators can work around this security flaw by using SSL encryption for IMAP.

In general, IMAP is a popular email retrieval protocol. Its popularity is growing due to the proliferation of mobile devices, such as smartphones and tablets. IMAP is ideal for those who need to access their email on the go or using different devices.

## SMTP
https://sendgrid.com/blog/what-is-an-smtp-server/

https://postmarkapp.com/guides/everything-you-need-to-know-about-smtp

## What is an SMTP server?

What does SMTP mean? We’re glad you asked. SMTP stands for Simple Mail Transfer Protocol, and it’s an application used by mail servers to send, receive, and/or relay outgoing mail between email senders and receivers. 

An SMTP email server will have an address (or addresses) that can be set by the mail client or application that you are using and is generally formatted as smtp.serveraddress.com. For example, the SMTP server Gmail uses is smtp.gmail.com, and Twilio SendGrid’s is smtp.sendgrid.com. You can generally find your SMTP email server address in the account or settings section of your mail client.

When you send an email, with SMTP host Gmail or AOL, the SMTP server processes your email, decides which server to send the message to, and relays the message to that server. The recipient’s inbox service provider, such as Gmail or AOL, then downloads the message and places it in the recipient’s inbox.



### Is an SMTP server the same as a normal server?

Technically, yes. Like most servers, the SMTP server processes data to send to another server, but it has the very specific purpose of processing data related to the sending, receiving, and relaying of email. An SMTP server is also not necessarily on a machine. It is an application that is constantly running in anticipation of sending new mail.

### Why are SMTP servers important?

Without an SMTP server, your email wouldn’t make it to its destination. Once you hit “send,” your email transforms into a string of code that is then sent to the SMTP server. The SMTP server is able to process that code and pass on the message. If the SMTP server wasn’t there to process the message, it would be lost in translation. 

Additionally, the SMTP server verifies that the outgoing email is from an active account, acting as the first safeguard in protecting your inbox from illegitimate email. It also will send the email back to the SMTP sender if it can’t be delivered. This informs the sender that they have the wrong email address or that their email is being blocked by the receiving server.

If you’re looking for more information on SMTP, check out our post, [SMTP Service Crash Course](http://sendgrid.com/blog/smtp-service-crash-course/).

### Basic SMTP commands

As we mentioned earlier, SMTP commands are a set of codes that power the transmission of email messages between servers. Here are the basic SMTP commands you should be aware of:

-   **HELO or EHLO (Hello):** This is a crucial command for beginning the entire email sending process. The email client is identifying itself to the SMTP server. It is the beginning of a conversation and usually involves the server sending a HELO command back complete with its domain name/IP address.

-   **MAIL FROM:** Following the identification command, the sender will share code that specifies who the mail is from. This outlines the email address and tells the SMTP server that a new transaction is about to start. From here, the server resets everything and is ready to accept the email address. Once accepted, it will reply with a 250 OK reply code.

-   **RCPT TO (Recipient To):** The next command follows the 250 OK reply code identifying who the email is being sent to. Again, the SMTP server responds with the same code, at which point another RCPT TO command can be sent with a different recipient’s email address. This can go back and forth as many times as required depending on how many people will receive the email.

-   **DATA:** This triggers the transfer of data between the client and the server. All of the message contents will be moved to the SMTP server, which will respond with a 345 reply code. The contents of the messages are transferred to the server, where a single dot is sent in a line by itself to signal the end of the message. If accepted and ready for delivery, the server sends another 250 OK code. At this point, the message is on its way to the recipients.

-   **QUIT:** When the email has been sent, the client sends the QUIT command to the server, severing the connection. If it has been successfully closed, the server will reply with a 221 code.

-   **RSET (Reset):** This command is sent to the server when the mail transaction needs to be aborted. It doesn’t close the connection, but it does reset everything and remove all previous data about the email and the parties involved. You will commonly use this when there has been an error, like inputting the wrong recipient information, and the process needs to be restarted.

### Understanding SMTP error codes

The email sending process doesn’t always go as smoothly as in the example chatter of our email servers above. [Bounces](https://postmarkapp.com/guides/email-bounces), blocks, or other issues might prevent an email from being sent. In this case, the receiving server can notify you of issues using [SMTP error codes](https://smtpfieldmanual.com/#codes), and knowing what they mean helps you diagnose and fix email delivery roadblocks.

For example, here are two groups of SMTP errors that crop up often:

-   **4.X.X Persistent Transient Failure:** These error codes start with the number “4” followed by two other numbers. They typically mean that there’s a temporary failure with the mail server. Repeating the command again could get rid of the error, but these codes are often used by servers to keep untrusted senders at bay.  
    

-   **5.X.X Permanent Error:** These error codes begin with the number “5” and are followed by two numbers. They typically signify that the SMTP connection has dropped. If you try to resend the email, it will likely still result in the same error.


## POP3
https://whatis.techtarget.com/definition/POP3-Post-Office-Protocol-3
### What is POP3 (Post Office Protocol 3)?

Post Office Protocol 3, or POP3, is the most commonly used protocol for receiving [email](https://whatis.techtarget.com/definition/e-mail-electronic-mail-or-email) over the internet. This standard protocol, which most email servers and their clients support, is used to receive emails from a remote server and send to a local client.

POP3 is a one-way [client-server](https://searchnetworking.techtarget.com/definition/client-server) [protocol](https://searchnetworking.techtarget.com/definition/protocol) in which email is received and held on the email server. The "3" refers to the third version of the original POP protocol.

A recipient or their email client can download mail periodically from the server using POP3. Thus, POP3 offers a means of downloading email from a [server](https://whatis.techtarget.com/definition/mail-server-mail-transfer-transport-agent-MTA-mail-router-Internet-mailer) to the client so the recipient can view the email offline. POP3 can be thought of as a "store-and-forward" service.

Once the email is on the client, POP3 then deletes it from the server. With some implementations, users or an administrator can specify that mail be saved for some time, allowing users to download email as many times as they wish within the specified period.

### POP3 and email applications

POP3 is built into most popular email clients, including  [Microsoft Outlook](https://www.techtarget.com/searchwindowsserver/definition/Microsoft-Outlook). The protocol will work provided that the email program is configured to host POP3. Each POP3 mail server has a different address that must be entered into the email program for it to connect with the protocol. Users must also enter their username and password to receive email successfully.

Additionally, since POP3 is built into standard internet browsers, including [Internet Explorer](https://www.techtarget.com/searchenterprisedesktop/definition/Internet-Explorer) and Mozilla Thunderbird, users can check their email even without an [email client.](https://www.techtarget.com/searchenterprisedesktop/photostory/252448032/4-enterprise-email-clients-to-consider-instead-of-Outlook/1/Get-to-know-alternatives-to-Outlook)

### Advantages and limitations of POP3

Although POP3 has been enhanced many times since it originated in the late 1980s, it remains popular because of its simplicity. Another reason for its ubiquity is that it enables email to be retrieved efficiently with minimal errors.

The protocol is ideal when users need to access their email offline and they use a designated device for retrieval. POP3 is also useful for sending and storing bulk email messages.

POP3 is not intended to support email manipulation or synchronization on the server, since the email is meant to be downloaded to the client and then deleted from the server. For these use cases, the more advanced and complex Internet Message Access Protocol ([IMAP](https://whatis.techtarget.com/definition/IMAP-Internet-Message-Access-Protocol)) is used.

IMAP can also poll an existing connection for newly arrived messages, and it supports multiple folders on the server. POP3 doesn't have these capabilities.
## Dovecot
https://www.interserver.net/tips/kb/dovecot-detailed-explanation/

Dovecot is an open source IMAP and POP3 email server for Linux/UNIX-like frameworks, created by demands for greater security. Dovecot is a fabulous decision for both little and vast establishments. It’s quick, easy to set up, requires no exceptional organization, and it utilizes almost no memory.

Dovecot can work with standard mbox, Maildir, and its own local elite dbox groups. It is completely compatible with UW IMAP and Courier IMAP servers’ execution of them, and also mail customers getting to the letter drops straightforwardly. Dovecot likewise incorporates a Mail Delivery Agent (called Local conveyance operator in Dovecot’s documentation) and a LMTP server, with discretionary Sieve sifting support. Dovecot bolsters an assortment of confirmation mappings for IMAP and POP access including CRAM-MD5 and the more secure DIGEST-MD5. With variant 2.2 some new elements have been added to Dovecot, e.g. extra IMAP order expansions, dsync has been changed or enhanced, and shared post boxes now bolster per-client flags.

By and large, a system which permits somebody to send and get email is known as a Mail User Agent or MUA. Examples of common MUAs include Mozilla Thunderbird and Microsoft Outlook Express. Whatever MUA was utilized, a message was made and sent to that client’s mail server. The mail server does not communicate with individuals specifically like the MUA does; rather, its occupation is to get email from another PC and either send it on to wherever it needs to go, or handle last conveyance of email. The “mail server” is known as a Mail Transfer Agent or MTA. The MTA then checks the message to decide the beneficiary, and inquiries the Domain Name System (DNS) servers to discover which other MTA is in charge of taking care of email for the beneficiary being referred to. It then sends the message to that MTA. Now, the message has gone from the remote client’s PC to their mail server, and has gone to the mail server which handles email for the beneficiary being referred to.

Contingent upon the system setup, it’s entirely conceivable that the message will be transferred to yet another MTA. Be that as it may, sooner or later, one MTA will assume liability for the message and get to be in charge of conveyance. As of now, the MTA will pass the message to a Mail Delivery Agent (MDA). At its center, a MDA is in charge of really putting away the message to plate. Some MDAs do different things also, for example, sifting mail or conveying to subfolders. Be that as it may, it is the MDA that stores the mail on the server.

Presently, it’s an ideal opportunity to check your mail. You start up your MUA, and it questions your mail server utilizing one of the standard protocols: IMAP or POP3. The mail server affirms your personality, then recovers the rundown of messages from the mail stockpiling territory and returns them to the MUA. Your MUA then shows those message to you, and you can now read your mail.

IMAP and POP3 are the two basic conventions utilized by MUAs to speak with mail stockpiling servers. POP3 is generally utilized by clients who do not have a fast association with the mail server. One of POP3’s fundamental standards is that MUAs downloads mail and stores it locally (on the client’s PC) and after that they erase the mail from the server. IMAP is designed for LANs and fast associations. The expectation of IMAP is to contact the server every time a given message should be perused (aside from MUA-particular reserving). Dovecot has various improvements for IMAP that make it an astoundingly decent entertainer for most IMAP situations.

Dovecot is not included with real gathering of email. That usefulness is given by a MTA such as Exim or Postfix. When email has been recieved by the MTA, then it can either be conveyed by MTA, or by another MDA. It can also be passed to the Dovecot LDA for conclusive conveyance. The decision relies on upon different variables particular to the establishment. As an IMAP and POP3 server, Dovecot gives an approach to Mail User Agents (MUAs) to get to their mail. When a client’s MUA contacts the mail server, the product which answers that solicitation is an IMAP or POP3 server. IMAP and POP3 servers take demands from MUAs and answer those solicitations by getting to email messages put away on the server and sending them out to the MUA utilizing IMAP or POP3. Dovecot is one system which can give that IMAP and POP3 server usefulness. Likewise, Dovecot gives usefulness to definite message conveyance with the Dovecot LDA (Local Delivery Agent). The LDA is in charge of putting away email messages into the message store. Nearby conveyance can be done by the MTA itself, by a different Mail Delivery Agent, or utilizing the Dovecot LDA. The decision is made by prerequisites of the specific server establishment.

Note that Dovecot is NOT in charge of accepting mail from different servers. Dovecot just handles email (a) messages leaving the neighborhood message store, going out to IMAP and POP3 customers, and (b) messages which have as of now been recieved by the MTA and are to be put away into the nearby message store. There are two essential stockpiling alternatives of mail in the *NIX world: mbox and Maildir. Mbox stores different messages – in some cases hundreds or a large number of messages – in a solitary record. Maildir stores every message a different document. Mbox and Maildir have wide backing crosswise over different email programming including MTAs and MDAs, and are both completely supported by Dovecot. Dovecot offers some mail stockpiling arrangements of its own: sdbox and mdbox.

## Postfix
https://www.plesk.com/wiki/postfix/

**Postfix** is a hugely-popular Mail Transfer Agent (**MTA**) designed to determine routes and send emails. This cross-platform server is open-source, free, and suitable for installation on the majority of UNIX-like operating systems.

Numerous client and server programs make up Postfix: the latter tend to run in the [backend](https://www.plesk.com/wiki/backend/), while user or administrator programs utilize the former. Postfix’s structure is modular: it comprises various small, independent executables. Different parameters, features, and options are available, too.

Another key aspect of Postfix is that it was created to overcome those drawbacks seen in [Sendmail](https://www.plesk.com/wiki/sendmail/). A solid configuration keeps Postfix user data secure from leakage, abuse, and spam.

Postfix includes a cutting-edge queue manager capable of handling queues in a faster, smoother way. That’s why a number of administrators cite Postfix’s higher efficiency compared to Sendmail, even with high loads.

With Postfix, you can expect a significant degree of flexibility and simple administration, which makes it easier for beginners to set up than alternative MTA options. On top of this, Postfix offers support for Sendmail’s command line interface. It’s also compatible with a variety of Sendmail’s mail filters.

### Advantages of Postfix

Here are the main advantages you can expect to find when you start using Postfix:

-   Includes highly-detailed documentation
-   Security was clearly a priority in Postfix’s design
-   Postfix offers impressive compatibility with Sendmail
-   High queuing operation is fundamental to Postfix’s functionality
-   Active development is part of the Postfix set-up
-   Easy configuration, according to parameters of configuration files

### Disadvantages of Postfix

-   Unfortunately, Postfix can be hard to customize in some cases, depending on your unique requirements

## SPF
# What is an SPF record?
https://www.dmarcanalyzer.com/spf/spf-record/

An SPF record (Sender Policy Framework record) is the core of an SPF implementation in which the SPF policy is defined. An SPF record is published in the DNS (Domain Name Service) and it contains a list of authorized email servers which can send email on behalf of your domain name. If an email sender isn’t listed in the record section and does send email on behalf of your domain this email may be considered as not legitimate and can be rejected by the email receiver.

Having a properly set up SPF record will improve email deliverability and will help to protect your domain against malicious emails sent on behalf of your domain. Though, in practice these goals are achieved more effectively if you use an SPF record together with DMARC. DMARC and DMARC Analyzer use both SPF and DKIM. Together they provide synergy and the best result for email security and deliverability.

## SPF record in practice

An SPF record consists of several parts. It should always start with a version number and should be authorized by one or more mechanisms which define valid senders.

**v=spf1**  
This part defines the record as SPF. An SPF record has to start with this section. These used to be a second version of SPF (SenderID) which was created by Microsoft, but this was discontinued.

**Mechanisms**  
An SPF record can contain multiple mechanisms.

**a  
a:somedomain.com  
a/prefix  
a:somedomain.com/prefix**  
Define the DNS A record of the current (or specified) domain as a valid sending source.

**mx  
mx:somedomain.com  
mx/prefix  
mx:somedomain.com/prefix**  
Define the DNS MX record of the current (or specified) domain as a valid sending source.

**ptr  
ptr:domain**  
Define the reverse hostname of the sending IP address as a valid sending source. (Not recommended)

**ip4:ip4-address  
ip4:ip4-address/prefix**  
Define this IPv4 address (or address range) as valid sending sources.

**ip6:ip6-address  
ip6:ip6-address/prefix**  
Define this IPv6 address (or address range) as valid sending sources.

**include:domain.com**  
Include the SPF record for this domain as valid sending sources.

**exists:domain**  
Check existence of an A record for a provided domain. You can use macros in this context to be able to do a ‘dynamic’ lookup of such a record.

**all**  
You can define a policy for ‘all other sources’ using the ‘all’ mechanism. You should place this at the end of your SPF record providing a ‘default’ for other sources. Use a qualifier to define the policy you want to apply.

**redirect=domain.com**  
When required, you can redirect the SPF record to another domain. There can only be one modifier in each SPF record. This cannot be combined with an ‘all’ mechanism as the redirect will only be followed if none of the mechanisms match.

**Maximum number of lookups**  
When using SPF you need to take note of a limitation in this technique. The number of DNS lookups which are allowed to take place is limited to 10.

A DNS lookup is done when you query for one of these mechanisms:

-   a
-   mx
-   ptr
-   include
-   exists

Please note that the ‘nested lookups’ will also count. If an ‘included’ domain does an A and MX lookup, these will both count as lookups for your domain as well.

## DKIM
https://postmarkapp.com/guides/dkim

### What is a DKIM record?

DKIM (DomainKeys Identified Mail) is an email security standard designed to make sure messages aren’t altered in transit between the sending and recipient servers. It uses public-key cryptography to sign email with a private key as it leaves a sending server. Recipient servers then use a public key published to a domain’s DNS to verify the source of the message, and that the body of the message hasn’t changed during transit. Once the signature is verified with the public key by the recipient server, the message passes DKIM and is considered authentic.

### Why is a DKIM record important? 
While DKIM isn't required, having emails that are signed with DKIM appear more legitimate to your recipients and are less likely to go to Junk or Spam folders. Spoofing email from trusted domains is a popular technique for malicious spam and phishing campaigns, and DKIM makes it harder to spoof email from domains that use it.

DKIM is compatible with existing email infrastructure and works with SPF and [DMARC](https://dmarcdigests.com) to create multiple layers of security for domains sending emails. Mail servers that don’t support DKIM signatures are still able to receive signed messages without any problems. It’s an optional security protocol, and DKIM is not a universally adopted standard.

Even though it’s not required, we recommend you add a DKIM record to your DNS whenever possible to authenticate mail from your domain. We use it to sign messages at Postmark, and ISPs like Yahoo, AOL, and Gmail use it to check incoming messages. We’ve done testing that proved messages are more likely [to be delivered](https://postmarkapp.com/blog/proof-dkim-and-senderid-improve-delivery) when they use these security protocols.

An additional benefit of DKIM is that ISPs use it to build a reputation on your domain over time. As you send email and improve your delivery practices (low spam and [bounces](https://postmarkapp.com/guides/email-bounces), high engagement), you help your domain build a good sending reputation with ISPs, which improves deliverability.

While it’s important to understand what DKIM does, it’s also important to be clear about what it doesn’t solve. Using DKIM will make sure your message hasn’t been altered, but it doesn’t encrypt the contents of your message. Many ESPs use opportunistic TLS to encrypt messages as they move between sender and recipients, but it’s still possible to send unencrypted messages if an email server refuses a TLS connection. Once a message has been delivered, the DKIM signature will remain in the email headers but won’t encrypt the content of the message in any way.

Now that we’ve described what DKIM does, let’s move on to how it protects your domain’s email.

### How do DKIM records work?

DKIM uses two actions to verify your messages. The first action takes place on a server sending DKIM signed emails, while the second happens on a recipient server checking DKIM signatures on incoming messages. The entire process is made possible by a private/public key pair. Your private key is kept secret and safe, either on your own server or with your ESP, and the public key is added to the DNS records for your domain to broadcast it to the world to help verify your messages. Let’s dive a little deeper into how DKIM works on servers that are sending and receiving email.

#### Sending a signed DKIM message

If you run your own mail server, you can generate this pair on your own. Any time you use a service like Google Apps, Campaign Monitor, Postmark, or other email providers that support DKIM they’ll normally generate the key for you.

To give you an idea of how DKIM works, let’s explain the process on Postmark. We keep your private key securely stored on our servers and sign each message as it is sent. When a message is sent we create a hash from the content of the message headers and then use your private key to sign the hash. This signature carries everything a recipient server needs to validate the message and looks like this:

```markup
DKIM-Signature: v=1; a=rsa-sha1; c=relaxed/relaxed; s=20130519032151pm; d=postmarkapp.com;
h=From:Date:Subject:MIME-Version:Content-Type:Content-Transfer-Encoding:To:Message-ID;
i=support@postmarkapp.com; bh=vYFvy46eesUDGJ45hyBTH30JfN4=;
b=iHeFQ+7rCiSQs3DPjR2eUSZSv4i/Kp+sipURfVH7BGf+SxcwOkX7X8R1RVObMQsFcbIxnrq7Ba2QCf0YZlL9iqJf32V+baDI8IykuDztuoNUF2Kk0pawZkbSPNHYRtLxV2CTOtc+x4eIeSeYptaiu7g7GupekLZ2DE1ODHhuP4I=
```

Here’s what each part of the header means:

-   `DKIM-Signature:` The header registered for DKIM signed messages.
-   `v=1;` The version of DKIM being used by the sending server.
-   `a=rsa-sha1;` The algorithm used to generate the hash for the private/public key. There are two officially supported signature algorithms for this hash, rsa-sha1 and rsa-sha256.
-   `c=relaxed/relaxed;` Sets the canonicalization posture for the sending domain. This regulates whitespace and text wrapping changes in a message. There are two canonicalized postures. `Simple` doesn’t allow any changes, and `relaxed` allows common changes to whitespace and header line-wrapping. Canonicalization in the header and body can be managed individually and uses a header/body format.
-   `s=20130519032151pm;` Used as a selector for the public DKIM key for verification. Domains can have multiple public DKIM keys, and the selector value makes sure recipient servers are using the correct public key.
-   `d=postmarkapp.com;` The email domain that signed the message. It’s important that your DKIM signature use your domain name here because this bolsters your domain’s reputation with ISPs as you send valid email, regardless of the Email Service Provider you use.
-   `From:Date:Subject:MIME-Version:Content-Type:Content-Transfer-Encoding:To:Message-ID;` The headers included with the message when it was cryptographically signed.
-   `i=support@postmarkapp.com;` The identity of the signer and is usually provided as an email address.
-   `bh=vYFvy46eesUDGJ45hyBTH30JfN4=;` The value of a body hash generated before the message headers are signed.
-   `b=iHeFQ+7rCiSQs3DPjR2eUSZSv4i/Kp+sipURfVH7BGf+SxcwOkX7X8R1RVObMQsFcbIxnrq7Ba2QCf0YZlL9iqJf32V+baDI8IykuDztuoNUF2Kk0pawZkbSPNHYRtLxV2CTOtc+x4eIeSeYptaiu7g7GupekLZ2DE1ODHhuP4I=`The cryptographic signature of all the preceding information from the DKIM-Signature field. This entry is treated as an empty string during the verification process.

This signature is computed and added to the outgoing email headers. The message is now ready for a recipient server to verify the message hasn’t been modified in transit.

### Verifying a signed DKIM message

Mail systems start DKIM verification by making sure the version number meets the DKIM specification, the identity of the sender’s domain matches the domain set in the signature, and the “h=“ tag contains the From header field.

Once the signature has been validated, the recipient server tries to retrieve the public key for the sending domain. The server uses the “d=“ tag to look up the DNS records for the sending domain, and the “s=“ tag to select the correct DKIM key.

The public key decrypts the encrypted hash sent. The receiving mail server then computes its own hash. If the two matches, the message is let through.

### How does DKIM prevent domain spoofing? 

DKIM alone does not prevent domain spoofing. It’s possible to sign a message using a DKIM key linked to a different domain than the one specified in the "From" header.

However, if you have a [DMARC policy set for your domain](https://postmarkapp.com/guides/dmarc), the receiving mail server will check that the DKIM key used to sign the message matches the From domain when determining DMARC compliance.

### How does DKIM improve deliverability? 
ISPs like Gmail, Yahoo, and AOL use DKIM as a signal when determining whether a message is legitimate or not. [Our testing has found](https://postmarkapp.com/blog/proof-dkim-and-senderid-improve-delivery) that using email authentication methods like SPF and DKIM is critical to good deliverability.

### What do SPF and DMARC have to do with DKIM? 

While DKIM ensures messages aren’t altered in transit between the sending and recipient servers, [SPF](https://postmarkapp.com/guides/spf) validates that the sending server is authorized to send messages using a domain in the first place.

[DMARC](https://postmarkapp.com/guides/dmarc) gives domain owners a mechanism for communicating how they’d like unauthenticated messages to be handled by receivers. It uses DKIM and SPF to determine if a message is legitimate and whether it should be delivered to the recipient or blocked.

## DMARC

## What is DMARC?

DMARC (Domain-based Message Authentication, Reporting & Conformance) is a standard that prevents spammers from using your domain to send email without your permission — also known as spoofing. Spammers can forge the “From” address on messages so the spam appears to come from a user in your domain. A good example of this is PayPal spoofing, where a spammer sends a fraudulent email to you pretending to be PayPal in an effort to obtain your account information. DMARC ensures these fraudulent emails get blocked before you even see them in your inbox. In addition, DMARC gives you great visibility and reports into who is sending email on behalf of your domain, ensuring only legitimate email is received.

The good news is that DMARC is open and free for anyone to use, allowing you to secure your domain’s emails and gain control of your email delivery. All you have to do is follow the implementation steps in this guide and choose an ESP who supports DMARC.

### What are the benefits of implementing DMARC? 

DMARC is a key component of a brand‘s email security and deliverability strategy as it enables:

-   **Visibility** - Monitor emails sent using your domain to ensure they are properly authenticated using SPF and/or DKIM.
-   **Brand Protection** - Block spoofed messages that might damage your brand‘s reputation with customers.
-   **Security** - Prevent users from falling victim to phishing scams that could compromise your organization‘s security.

#### Does DMARC improve deliverability?

DMARC allows you to see whether emails sent using your domain are properly authenticated using SPF and DKIM. This allows you to identify and fix any authentication issues that can affect the deliverability of your emails.

Preventing spoofed emails from reaching users can lower spam complaints and protect your domain‘s reputation with ISPs.

### How does DMARC work?

Before you understand the DMARC protocol, you first need to understand two email authentication standards called DKIM and SPF. DMARC is built on top of these standards, so let’s go over them first. If you already know about DKIM and SPF, skip to the DMARC section.


# Practice 

## DNS Configuration

### Create Master Zone 

We create a masterzone in which we will put the MX Record and other needed records. 

![Creating the masterzone](Pasted_image_1.png)

We define a Nameserver Entry in our DNS Zone. 

![Creating the Nameserver entry](Pasted_image_2.png)

We need to create an MX record so that our mailserver and the other mailservers know, where to send mails.

![Creating the MX Entry](Pasted_image_3.png)

To allow the MX Record to work, we need to point a domain name to the IP Address.

![Creating the A Record](Pasted_image_4.png)

### Create Entries 

We need to define our nameserver record in the nvslan masterzone so other servers can discover us.

![Create Entry for NS Server in the nvslan zone](Pasted_image_5.png)

Glue record to allow the Nameserver to function. 

![Glue record creation](Pasted_image_6.png)

## Installing Postfix

To send and receive mails in a basic CLI manner we need to install postfix and configure it with a few settings. The initial installation is done via apt and the CLI. 

```Bash
->  sudo apt install postfix

setting alias maps
setting alias database
changing /etc/mailname to niklasmail.nvs.lan
setting myorigin
setting destinations: $myhostname, niklasmail.nvs.lan, u2004-5bhif-6, localhost.localdomain, localhost
setting relayhost:
setting mynetworks: 127.0.0.0/8 [::ffff:127.0.0.0]/104 [::1]/128
setting mailbox_size_limit: 0
setting recipient_delimiter: +
setting inet_interfaces: all
setting inet_protocols: all
/etc/aliases does not exist, creating it.
WARNING: /etc/aliases exists, but does not have a root alias.

Postfix (main.cf) is now set up with a default configuration.  If you need to
make changes, edit /etc/postfix/main.cf (and others) as needed.  To view
Postfix configuration values, see postconf(1).

After modifying main.cf, be sure to run 'systemctl reload postfix'.

Running newaliases
Created symlink /etc/systemd/system/multi-user.target.wants/postfix.service → /lib/systemd/system/postfix.service.
Processing triggers for ufw (0.36-6) ...
Processing triggers for systemd (245.4-4ubuntu3.13) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for rsyslog (8.2001.0-1ubuntu1.1) ...
Processing triggers for libc-bin (2.31-0ubuntu9.2) ...
```

### Configuring postfix
We select the type `Internet Site` since it fits our needs just nicely and is the most used option.

![Selecting the type](Pasted_image_7.png)

We insert our FQDN in the system mail name which will be later used at the right side of our E-Mail address. (In my case `niklasmail.nvs.lan.`)

![Inputting Systemmailname](Pasted_image_8.png)


We need to define a user to which mails for root will be sent to.

![Defining the user to which ](Pasted_image_9.png)

We need issue a command to change a few more settings: 

```Bash
schueler in u2004-5bhif-6 in ~ took 1m55s
->  sudo dpkg-reconfigure postfix
```

Default: 

![Default Settings from before](Pasted_image_10.png)

![Sync Mail Queue](Pasted_image_11.png)


Angeben welche Netzwerke er sich zuständig fühlt? 10.128.0.0/13 (hier im 3. Stock ist das das netzwerk, alle mails aus diesem adressbereich 
dürfen mitspielen)

Allowed IPs

![Allowed IPs](Pasted_image_12.png)

No size limit: 

![The size limit for a single mailbox](Pasted_image_13.png)

Setting the Local Address Extension Character which is used when we create aliases (e.g. discord+niklas@haiden.ch).

![Local Address Extension Character](Pasted_image_14.png)

We restrict access to IPv4 only since it's only a testing area anyways.

![Restricting access to IPv4](Pasted_image_15.png)

## Mailx to send and receive mail
### Installing Mailx
Now we install mailx as a CLI tool to show us mails and send mails to other people on the same server and network. 
```
->  sudo apt install bsd-mailx

  liblockfile-bin liblockfile1
The following NEW packages will be installed:
  bsd-mailx liblockfile-bin liblockfile1
0 upgraded, 3 newly installed, 0 to remove and 98 not upgraded.
Need to get 85.6 kB of archives.
After this operation, 265 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://nova.clouds.archive.ubuntu.com/ubuntu focal/main amd64 liblockfile-bin amd64 1.16-1.1 [11.7 kB]
Get:2 http://nova.clouds.archive.ubuntu.com/ubuntu focal/main amd64 liblockfile1 amd64 1.16-1.1 [6680 B]
Get:3 http://nova.clouds.archive.ubuntu.com/ubuntu focal/main amd64 bsd-mailx amd64 8.1.2-0.20180807cvs-1 [67.2 kB]
Fetched 85.6 kB in 0s (366 kB/s)
[...]
```

### Sending and receiving

#### S&R on the same server

Sending a mail to myself:

```Bash
->  mailx -s "Marcel is waiting" schueler
Marcel is waiting like none other
Cc:
.
```

Viewing the sent email: 

```Bash
->  cat /var/mail/schueler
From schueler@niklasmail.nvs.lan  Wed Jan 26 14:22:56 2022
Return-Path: <schueler@niklasmail.nvs.lan>
X-Original-To: schueler
Delivered-To: schueler@niklasmail.nvs.lan
Received: by u2004-5bhif-6.openstacklocal (Postfix, from userid 1001)
        id 0DD32FC5A6; Wed, 26 Jan 2022 14:22:56 +0000 (UTC)
To: schueler@niklasmail.nvs.lan
Subject: Marcel is waiting
MIME-Version: 1.0
Content-Type: text/plain; charset="UTF-8"
Content-Transfer-Encoding: 8bit
Message-Id: <20220126142256.0DD32FC5A6@u2004-5bhif-6.openstacklocal>
Date: Wed, 26 Jan 2022 14:22:56 +0000 (UTC)
From: schueler@niklasmail.nvs.lan

Marcel is waiting like none other
Cc:
```

Adding my groupmate Marcel so I can send emails to him and the other way around: 

```
->  sudo adduser marcel
Adding user `marcel' ...
Adding new group `marcel' (1003) ...
Adding new user `marcel' (1002) with group `marcel' ...
Creating home directory `/home/marcel' ...
Copying files from `/etc/skel' ...
New password:
Retype new password:
passwd: password updated successfully
Changing the user information for marcel
Enter the new value, or press ENTER for the default
        Full Name []:
        Room Number []:
        Work Phone []:
        Home Phone []:
        Other []:
Is the information correct? [Y/n] y
```

Marcel logging in to see if his login works:

```Bash
PS C:\Users\denkp> ssh marcel@10.139.0.87 The authenticity of host '10.139.0.87 (10.139.0.87)' can't be established. ECDSA key fingerprint is SHA256:Jt5bWCa+IXwAVcr871KekYHr0HEJFeGVZGtK6X/Gz98. Are you sure you want to continue connecting (yes/no/[fingerprint])? yes Warning: Permanently added '10.139.0.87' (ECDSA) to the list of known hosts. marcel@10.139.0.87's password: Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.4.0-88-generic x86_64) 
[...]
marcel@u2004-5bhif-6:~$
```

Sending a message to Marcel: 

```Bash
schueler in u2004-5bhif-6 in ~ took 12s
->  mailx -s "Hallo Marcel" marcel
Hallo Marcel, ich hoffe es geht dir gut.
.
Cc:
```

Marcel checking his mails: 

```Bash
marcel@u2004-5bhif-6:/$ cat /var/mail/marcel
From schueler@niklasmail.nvs.lan  Wed Jan 26 14:28:54 2022
Return-Path: <schueler@niklasmail.nvs.lan>
X-Original-To: marcel
Delivered-To: marcel@niklasmail.nvs.lan
Received: by u2004-5bhif-6.openstacklocal (Postfix, from userid 1001)
        id 35CCAFC5B1; Wed, 26 Jan 2022 14:28:54 +0000 (UTC)
To: marcel@niklasmail.nvs.lan
Subject: Hallo Marcel
MIME-Version: 1.0
Content-Type: text/plain; charset="UTF-8"
Content-Transfer-Encoding: 8bit
Message-Id: <20220126142854.35CCAFC5B1@u2004-5bhif-6.openstacklocal>
Date: Wed, 26 Jan 2022 14:28:54 +0000 (UTC)
From: schueler@niklasmail.nvs.lan

Hallo Marcel, ich hoffe es geht dir gut.
```

Now Marcel sends an Email to me:

```Bash
    marcel@u2004-5bhif-6:/$ mailx -s "Sayonara Cabonara" schueler
    Egal ob Faul, egal ob Fleißig, ich mach Schluss um 15:30, Sayonara Cabonara
    .
    Cc:
```

Me looking at the newly sent mail from Marcel: 

```Bash
->  cat /var/mail/schueler

From marcel@niklasmail.nvs.lan  Wed Jan 26 14:31:36 2022
Return-Path: <marcel@niklasmail.nvs.lan>
X-Original-To: schueler
Delivered-To: schueler@niklasmail.nvs.lan
Received: by u2004-5bhif-6.openstacklocal (Postfix, from userid 1002)
        id 8FF5BFC5B1; Wed, 26 Jan 2022 14:31:36 +0000 (UTC)
To: schueler@niklasmail.nvs.lan
Subject: Sayonara Cabonara
MIME-Version: 1.0
Content-Type: text/plain; charset="UTF-8"
Content-Transfer-Encoding: 8bit
Message-Id: <20220126143136.8FF5BFC5B1@u2004-5bhif-6.openstacklocal>
Date: Wed, 26 Jan 2022 14:31:36 +0000 (UTC)
From: marcel@niklasmail.nvs.lan

Egal ob Faul, egal ob Fleißig, ich mach Schluss um 15:30, Sayonara Cabonara
```

#### S&R to a different server on the same network

Sending mail to Simon Wolffhardt on the same network, though on another server:

```Bash 
schueler in u2004-5bhif-6 in ~
->  mailx -s "Hallo Simon" simon@wolffhardtmail.nvs.lan
Hallo Simon :^)
.
Cc:
```

I received the following message back from Simon: 

```
Message 3:
From schueler@ransommail.nvs.lan  Wed Jan 26 14:44:40 2022
X-Original-To: schueler@niklasmail.nvs.lan
To: schueler@niklasmail.nvs.lan
Subject: Autobahnauffahrt
MIME-Version: 1.0
Content-Type: text/plain; charset="UTF-8"
Content-Transfer-Encoding: 8bit
Date: Wed, 26 Jan 2022 14:44:39 +0000 (UTC)
From: schueler@ransommail.nvs.lan

Hammerl im Himmel,
geheiligt werde dein Name,
Dein SQL Server komme,
dein JSON geschehe,
wie im Laptop so auch auf OLAP.
Unsere tägliche Query gib uns heute
Und vergib uns unsere Redundanz
wie auch wir vergeben des RAID Verbundes.
Und führe uns nicht in Datenverlust,
sondern erlöse uns von der Redundanz
Denn dein ist die MongoDB und die Kraft
und die Herrlichkeit in Ewigkeit.
Amen.
```

## Connecting via IMAP

The next task was to connect via an E-Mail Client to the server. For this we need a Server to handle this task, which is, in our case, Dovecot since it's the most popular and well documented solution. 

### Installing Dovecot

We install Dovecot via the usual method. 

```
schueler in u2004-5bhif-6 in ~
->  sudo apt install mail-stack-delivery
[sudo] password for schueler:
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following packages were automatically installed and are no longer required:
  linux-headers-5.4.0-84 linux-headers-5.4.0-84-generic linux-image-5.4.0-84-generic linux-modules-5.4.0-84-generic
  linux-modules-extra-5.4.0-84-generic
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  dovecot-core libexttextcat-2.0-0 libexttextcat-data liblua5.3-0
Suggested packages:
  dovecot-gssapi dovecot-imapd dovecot-ldap dovecot-lmtpd dovecot-lucene dovecot-managesieved dovecot-mysql
  dovecot-pgsql dovecot-pop3d dovecot-sieve dovecot-solr dovecot-sqlite dovecot-submissiond ntp
The following NEW packages will be installed:
  dovecot-core libexttextcat-2.0-0 libexttextcat-data liblua5.3-0 mail-stack-delivery
[...]
```

### Configuring Dovecot & Postfix to work with each other

This template was used for configuring the server: https://moodle.htlstp.ac.at/mod/page/view.php?id=15525

#### Configuring Postfix

Postfix was configured with the following options: 

`main.cf`
```

home_mailbox = Maildir/
smtpd_sasl_auth_enable = yes
smtpd_sasl_type = dovecot
smtpd_sasl_path = private/auth
smtpd_sasl_authenticated_header = yes
smtpd_sasl_security_options = noanonymous
smtpd_sasl_local_domain = $myhostname
broken_sasl_auth_clients = yes
smtpd_recipient_restrictions = reject_unknown_sender_domain, reject_unknown_>smtpd_sender_restrictions = reject_unknown_sender_domain
mailbox_command = /usr/lib/dovecot/deliver -m "${EXTENSION}"

```

#### Configuring Dovecot

`10-master.conf` In here we set the right values so that Dovecot can interact with the Postfix Server.

```

  # Postfix smtp-auth
  unix_listener /var/spool/postfix/private/auth {
    mode = 0660
     # Assuming the default Postfix user and group
    user = postfix
    group = postfix
  }


```

`10-mail.conf` In here we set the Maildir for each user.

```
#
mail_location = maildir:~/Maildir
```


### Enabling SMTP / IMAP Encryption
#### Creating keys

We first have to generate certificates that dovecot can use to 
encrypt traffic.

```
->  sudo openssl req -new -x509 -days 1000 -nodes -out "/etc/ssl/certs/dovecot.pem" -keyout "/etc/ssl/private/dovecot_key.pem"

Generating a RSA private key
............................+++++
....................................+++++
writing new private key to '/etc/ssl/private/dovecot_key.pem'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:AT
State or Province Name (full name) [Some-State]:Lower Austria
Locality Name (eg, city) []:St.Pölten
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Informatics Department
Organizational Unit Name (eg, section) []:IF
Common Name (e.g. server FQDN or YOUR name) []:niklasmail.nvs.lan
Email Address []:schueler@niklasmail.nvs.lan
```


`10-ssl.conf` In here we add the certificate paths for so that dovecot can use the files required for encryption.
```
##
## SSL settings
##

# SSL/TLS support: yes, no, required. <doc/wiki/SSL.txt>
ssl = yes

# PEM encoded X.509 SSL/TLS certificate and private key. They're opened befo>
# dropping root privileges, so keep the key file unreadable by anyone but
# root. Included doc/mkcert.sh can be used to easily generate self-signed
# certificate, just make sure to update the domains in dovecot-openssl.cnf
ssl_cert = </etc/ssl/certs/dovecot.pem
ssl_key = </etc/ssl/private/dovecot_key.pem
```

After that we connected with Thunderbird which worked beautifully.

### Sending a mail with OpenPGP
The next task was to send an encrypted E-Mail. For this we first have to create a PGP Key: 

![Creating a PGP Key](Pasted_image_16.png)


Then we can send mails with an PGP Key like so: 

![Setting Encryption to required](Pasted_image_17.png)

When I receive a Mail with a PGP Key attached, Thunderbird notifies me:

![Notification from Thunderbird](Pasted_image_18.png)

Then I click to import the key and get the following window: 

![Key Import successful](Pasted_image_19.png)

## Spam Prevention 

Spam is a really big problem nowadays. That's why we use Software like amavis to help us combat incoming spam messages. The following tutorial was used: 
https://help.ubuntu.com/community/PostfixAmavisNew

## Installing amavis 
Installing amavis via apt. 

```Bash
schueler in u2004-5bhif-6 in ~ took 7s
->  sudo apt-get install amavisd-new spamassassin clamav-daemon
[...]
Adding system user `debian-spamd' (UID 120) ...
Adding new group `debian-spamd' (GID 127) ...
Adding new user `debian-spamd' (UID 120) with group `debian-spamd' ...
Not creating home directory `/var/lib/spamassassin'.
spamassassin.service is a disabled or a static unit, not starting it.
Setting up sa-compile (3.4.4-1ubuntu1.1) ...
Running sa-compile (may take a long time)
Setting up amavisd-new (1:2.11.0-6.1ubuntu1) ...
Creating/updating amavis user account...
Job for amavis.service failed because the control process exited with error code.
See "systemctl status amavis.service" and "journalctl -xe" for details.
invoke-rc.d: initscript amavis, action "start" failed.
● amavis.service - LSB: Starts amavisd-new mailfilter
     Loaded: loaded (/etc/init.d/amavis; generated)
     Active: failed (Result: exit-code) since Wed 2022-02-16 12:45:41 UTC; 46ms ago
       Docs: man:systemd-sysv-generator(8)
    Process: 851644 ExecStart=/etc/init.d/amavis start (code=exited, status=1/FAILURE)

Feb 16 12:45:41 u2004-5bhif-6 amavis[851644]: Starting amavisd:
Feb 16 12:45:41 u2004-5bhif-6 amavis[851651]:   The value of variable $myhostname is "u2004-5bhif-6", but should have been
Feb 16 12:45:41 u2004-5bhif-6 amavis[851651]:   a fully qualified domain name; perhaps uname(3) did not provide such.
Feb 16 12:45:41 u2004-5bhif-6 amavis[851651]:   You must explicitly assign a FQDN of this host to variable $myhostname
Feb 16 12:45:41 u2004-5bhif-6 amavis[851651]:   in /etc/amavis/conf.d/05-node_id, or fix what uname(3) provides as a host's
Feb 16 12:45:41 u2004-5bhif-6 amavis[851651]:   network name!
Feb 16 12:45:41 u2004-5bhif-6 amavis[851644]: (failed).
Feb 16 12:45:41 u2004-5bhif-6 systemd[1]: amavis.service: Control process exited, code=exited, status=1/FAILURE
Feb 16 12:45:41 u2004-5bhif-6 systemd[1]: amavis.service: Failed with result 'exit-code'.
Feb 16 12:45:41 u2004-5bhif-6 systemd[1]: Failed to start LSB: Starts amavisd-new mailfilter.
dpkg: error processing package amavisd-new (--configure):
 installed amavisd-new package post-installation script subprocess returned error exit status 1
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for libc-bin (2.31-0ubuntu9.2) ...
Processing triggers for systemd (245.4-4ubuntu3.15) ...
Errors were encountered while processing:
 amavisd-new
E: Sub-process /usr/bin/dpkg returned an error code (1)
```

Installing packages for better spam detection: 

```Bash
schueler in u2004-5bhif-6 in ~ took 3m49s
->  sudo apt-get install libnet-dns-perl libmail-spf-perl pyzor razor

Reading package lists... Done
Building dependency tree
Reading state information... Done
libmail-spf-perl is already the newest version (2.9.0-4).
libmail-spf-perl set to manually installed.
libnet-dns-perl is already the newest version (1.22-1).
libnet-dns-perl set to manually installed.
The following packages were automatically installed and are no longer required:
  linux-headers-5.4.0-84 linux-headers-5.4.0-84-generic linux-image-5.4.0-84-generic linux-modules-5.4.0-84-generic
  linux-modules-extra-5.4.0-84-generic
Use 'sudo apt autoremove' to remove them.
Suggested packages:
  pyzor-doc
The following NEW packages will be installed:
  pyzor razor
0 upgraded, 2 newly installed, 0 to remove and 0 not upgraded.
1 not fully installed or removed.
Need to get 128 kB of archives.
After this operation, 514 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://nova.clouds.archive.ubuntu.com/ubuntu focal/universe amd64 pyzor all 1:1.0.0-3 [33.2 kB]
Get:2 http://nova.clouds.archive.ubuntu.com/ubuntu focal/universe amd64 razor amd64 1:2.85-4.2build5 [95.2 kB]
Fetched 128 kB in 1s (150 kB/s)
Selecting previously unselected package pyzor.
(Reading database ... 161040 files and directories currently installed.)
Preparing to unpack .../pyzor_1%3a1.0.0-3_all.deb ...
Unpacking pyzor (1:1.0.0-3) ...
Selecting previously unselected package razor.
Preparing to unpack .../razor_1%3a2.85-4.2build5_amd64.deb ...
Unpacking razor (1:2.85-4.2build5) ...
Setting up pyzor (1:1.0.0-3) ...
Setting up amavisd-new (1:2.11.0-6.1ubuntu1) ...
[...]
```

Add users to group vice-versa for scanning files:

```Bash
schueler in u2004-5bhif-6 in ~
->  sudo adduser clamav amavis
  sudo adduser amavis clamav
Adding user `clamav' to group `amavis' ...
Adding user clamav to group amavis
Done.
Adding user `amavis' to group `clamav' ...
Adding user amavis to group clamav
Done.

schueler in u2004-5bhif-6 in ~
-> 
```

Before we got an error starting the amavis dameon because our hostname is broke. Adjusting this in the `/etc/amavis/conf.d/05-node_id` file.

```Bash
root@u2004-5bhif-6:/home/schueler# cat /etc/amavis/conf.d/05-node_id
use strict;

# $myhostname is used by amavisd-new for node identification, and it is
# important to get it right (e.g. for ESMTP EHLO, loop detection, and so on).

chomp($myhostname = `hostname --fqdn`);

# To manually set $myhostname, edit the following line with the correct Fully
# Qualified Domain Name (FQDN) and remove the # at the beginning of the line.
#
$myhostname = "mail.niklasmail.nvs.lan";

1;  # ensure a defined retur
```

After running `sudo apt install -f`, which fixes the amavis installation and then restarting amavis: 

```Bash
root@u2004-5bhif-6:/home/schueler# sudo systemctl status  amavis
● amavis.service - LSB: Starts amavisd-new mailfilter
     Loaded: loaded (/etc/init.d/amavis; generated)
     Active: active (running) since Wed 2022-02-16 13:09:48 UTC; 19s ago
       Docs: man:systemd-sysv-generator(8)
    Process: 856946 ExecStart=/etc/init.d/amavis start (code=exited, status=0/SUCCESS)
      Tasks: 3 (limit: 2278)
     Memory: 75.4M
     CGroup: /system.slice/amavis.service
             ├─856976 /usr/sbin/amavisd-new (master)
             ├─856977 /usr/sbin/amavisd-new (virgin child)
             └─856978 /usr/sbin/amavisd-new (virgin child)

Feb 16 13:09:48 u2004-5bhif-6 amavis[856976]: No decoder for       .exe
[...]
```

### Configuring Amavis

Enabling Spam Filtering in the amavis config: 

```Bash
schueler in u2004-5bhif-6 in ~ took 45s
->  cat /etc/amavis/conf.d/15-content_filter_mode
use strict;

# You can modify this file to re-enable SPAM checking through spamassassin
# and to re-enable antivirus checking.

#
# Default antivirus checking mode
# Please note, that anti-virus checking is DISABLED by
# default.
# If You wish to enable it, please uncomment the following lines:


@bypass_virus_checks_maps = (
   \%bypass_virus_checks, \@bypass_virus_checks_acl, \$bypass_virus_checks_re);


#
# Default SPAM checking mode
# Please note, that anti-spam checking is DISABLED by
# default.
# If You wish to enable it, please uncomment the following lines:


@bypass_spam_checks_maps = (
   \%bypass_spam_checks, \@bypass_spam_checks_acl, \$bypass_spam_checks_re);

1;  # ensure a defined return
```

Restarting amavis results in no errors: 

```Bash
schueler in u2004-5bhif-6 in ~
->  sudo systemctl restart amavis

schueler in u2004-5bhif-6 in ~ took 9s
->  sudo systemctl status amavis
● amavis.service - LSB: Starts amavisd-new mailfilter
     Loaded: loaded (/etc/init.d/amavis; generated)
     Active: active (running) since Wed 2022-02-16 13:19:03 UTC; 8s ago
       Docs: man:systemd-sysv-generator(8)
    Process: 857881 ExecStart=/etc/init.d/amavis start (code=exited, status=0/SUCCESS)
      Tasks: 1 (limit: 2278)
     Memory: 147.6M
     CGroup: /system.slice/amavis.service
             └─857917 /usr/sbin/amavisd-new (master)

Feb 16 13:19:03 u2004-5bhif-6 amavis[857917]: No decoder for       .jar
Feb 16 13:19:03 u2004-5bhif-6 amavis[857917]: No decoder for       .lha
Feb 16 13:19:03 u2004-5bhif-6 amavis[857917]: No decoder for       .lrz
Feb 16 13:19:03 u2004-5bhif-6 amavis[857917]: No decoder for       .lzo
Feb 16 13:19:03 u2004-5bhif-6 amavis[857917]: No decoder for       .rar
Feb 16 13:19:03 u2004-5bhif-6 amavis[857917]: No decoder for       .rpm
Feb 16 13:19:03 u2004-5bhif-6 amavis[857917]: No decoder for       .swf
Feb 16 13:19:03 u2004-5bhif-6 amavis[857917]: No decoder for       .zoo
Feb 16 13:19:03 u2004-5bhif-6 amavis[857917]: Using primary internal av scanner code for ClamAV-clamd
Feb 16 13:19:03 u2004-5bhif-6 amavis[857917]: Found secondary av scanner ClamAV-clamscan at /usr/bin/clamscan
```

### Postfix Integration 

 To enable integration with Postfix, we need to add the following line to the `main.cf` file. 
 
```
content_filter = smtp-amavis:[127.0.0.1]:10024
```

Then we add the following to the `master.cf` file in the postfix config directory: 

```
smtp-amavis     unix    -       -       -       -       2       smtp
        -o smtp_data_done_timeout=1200
        -o smtp_send_xforward_command=yes
        -o disable_dns_lookups=yes
        -o max_use=20

127.0.0.1:10025 inet    n       -       -       -       -       smtpd
        -o content_filter=
        -o local_recipient_maps=
        -o relay_recipient_maps=
        -o smtpd_restriction_classes=
        -o smtpd_delay_reject=no
        -o smtpd_client_restrictions=permit_mynetworks,reject
        -o smtpd_helo_restrictions=
        -o smtpd_sender_restrictions=
        -o smtpd_recipient_restrictions=permit_mynetworks,reject
        -o smtpd_data_restrictions=reject_unauth_pipelining
        -o smtpd_end_of_data_restrictions=
        -o mynetworks=127.0.0.0/8
        -o smtpd_error_sleep_time=0
        -o smtpd_soft_error_limit=1001
        -o smtpd_hard_error_limit=1000
        -o smtpd_client_connection_count_limit=0
        -o smtpd_client_connection_rate_limit=0
        -o receive_override_options=no_header_body_checks,no_unknown_recipient_checks
        -o content_filter=
        -o receive_override_options=no_header_body_checks
```

To allow all users from the server to send mails and not be classified as spam, we need to add this to `/etc/amavis/conf.d/50-user` : 

```
[...]
         @whitelist_sender_acl = @local_domains_acl
[...]
```

Restarting postfix results in no errors: 

```Bash
schueler in u2004-5bhif-6 in ~
->  sudo systemctl restart postfix

schueler in u2004-5bhif-6 in ~ took 11s
->  sudo systemctl status postfix
● postfix.service - Postfix Mail Transport Agent
     Loaded: loaded (/lib/systemd/system/postfix.service; enabled; vendor preset: enabled)
     Active: active (exited) since Wed 2022-02-16 13:29:08 UTC; 9s ago
    Process: 859376 ExecStart=/bin/true (code=exited, status=0/SUCCESS)
   Main PID: 859376 (code=exited, status=0/SUCCESS)

Feb 16 13:29:06 u2004-5bhif-6 systemd[1]: Starting Postfix Mail Transport Agent...
Feb 16 13:29:08 u2004-5bhif-6 systemd[1]: Finished Postfix Mail Transport Agent.
```

Checking if amavis is ready: 

```Bash
schueler in u2004-5bhif-6 in ~ took 4s
->  telnet localhost 10024
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
220 [127.0.0.1] ESMTP amavisd-new service ready
```

When sending a Spam Mail to schueler@ransommail.nvs.lan, we get the following output in the mail.log:

```
Feb 16 13:44:53 u2004-5bhif-6 amavis[857967]: (857967-08) Blocked SPAM {DiscardedOpenRelay,Quarantined}, [10.129.4.106]:54792 <schueler@niklasmail.nvs.lan> -> <schueler@ransommail.nvs.lan>, quarantine: X/spam-Xrvh6PNOS14v.gz, Queue-ID: 0B45FFC519, Message-ID: <d4eef444-4ef5-11ca-7ff0-b403fa171686@niklasmail.nvs.lan>, mail_id: Xrvh6PNOS14v, Hits: 999.793, size: 9181, 17414 ms
```

## SPF Record 

The Sender Policy Framework (SPF) is a process designed to prevent the forgery of an email's sender address.

### Create SPF Records 

Creating the SPF record in Webmin: 

![Webmin SPF Record](Pasted_image_20.png)

## DKIM 

### Installing openDKIM

To generate DKIM Keys and use DKIM we need to install opendkim/-tools. 

```bash
schueler in u2004-5bhif-6 in ~
->  sudo apt install opendkim opendkim-tools
[sudo] password for schueler:
Sorry, try again.
[sudo] password for schueler:
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following packages were automatically installed and are no longer required:
  linux-headers-5.4.0-84 linux-headers-5.4.0-84-generic
  linux-image-5.4.0-84-generic linux-modules-5.4.0-84-generic
  linux-modules-extra-5.4.0-84-generic
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  liblua5.1-0 libmemcached11 libmilter1.0.1 libopendbx1
[...]
```

#### creating needed directories

We create the needed directories for OpenDKIM.

```Bash
schueler in u2004-5bhif-6 in ~
->  sudo mkdir /etc/opendkim /etc/opendkim/keys

schueler in u2004-5bhif-6 in ~
->  sudo chmod 700 /etc/opendkim/keys


schueler in u2004-5bhif-6 in ~
->  sudo chown -R opendkim:opendkim /etc/opendkim

```

#### creating the /trusted file 

In this file we define the trusted hostnames and domains for DKIM. 

```
127.0.0.1
::1
localhost
niklasmail.nvs
niklasmail.nvs.lan
mail.niklasmail.nvs.lan
```

#### Creating key files

```bash

schueler in u2004-5bhif-6 in /etc/opendkim🔒
->  sudo opendkim-genkey -d niklasmail.nvs.lan -b 2048 -r -s 202103


```

Moving keys to right location:

```Bash

schueler in u2004-5bhif-6 in /etc/opendkim🔒
->  sudo mv 202103.private keys/niklasmail.nvs.lan

schueler in u2004-5bhif-6 in /etc/opendkim🔒
->  mv 202103.txt keys/niklasmail.txt

mv: failed to access 'keys/niklasmail.txt': Permission denied

schueler in u2004-5bhif-6 in /etc/opendkim🔒
->  sudo mv 202103.txt keys/niklasmail.txt

```

Adjusting permissions:

```Bash

schueler@u2004-5bhif-6:/etc/opendkim$ sudo chmod 600 /etc/opendkim/keys/

schueler@u2004-5bhif-6:/etc/opendkim$ sudo chmod 600 /etc/opendkim/keys/niklasmail.txt
schueler@u2004-5bhif-6:/etc/opendkim$ sudo chmod 600 /etc/opendkim/keys/niklasmail.nvs.lan
schueler@u2004-5bhif-6:/etc/opendkim$ sudo chown -R opendkim:opend
kim /etc/opendkim

```


The key we sent to Mr. Weixlbaum because we he needs to add it to the DNS Masterzone: 

```Bash

niklasmail.nvs.lan  niklasmail.txt
root@u2004-5bhif-6 /e/o/keys# cat niklasmail.txt
202103._domainkey       IN      TXT     ( "v=DKIM1; h=sha256; k=rsa; s=email; "
          "p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzzXK61TnlCYIjcWoK/Iui1f6vlLkgerc7P5sXCGzO9SV4qiU8etsG+GkObRKR5iwV5ERuur1Tc9/rdS2q03y1TWylU30l49wZSI4TkIC1gUidYntn65IV5M6910jZIy+ZD8faWhwHnQRHGvGy2o1KW+rFK0AmdUL2clPPCeRxV7JydSlRwA3tPUufkn9KthxtBISSPAfJMQ93K"          "sgHjYXpIUYcMQAtUdOU+HBOaNVhQiNoJ5RgJzk6D2sRqtmYXgMQlNCk4FYYzTPWRZjqRjCID8JvMGrwU0cZpQzxf/jFAF6UjBjTu2okHO5xcyifj5RYebQDO1t5llyBZTSOKd0uwIDAQAB" )  ; ----- DKIM key 202103 for niklasmail.nvs.lan

```

Trying to test it yielded no results at that time: 

```Bash
root@u2004-5bhif-6 /e/o/keys# sudo systemctl restart opendkim
root@u2004-5bhif-6 /e/o/keys#
opendkim-testkey -d niklasmail.nvs.lan -s 202103 -vvv

opendkim-testkey: using default configfile /etc/opendkim.conf
opendkim-testkey: checking key '202103._domainkey.niklasmail.nvs.lan'
opendkim-testkey: '202103._domainkey.niklasmail.nvs.lan' record not found

```