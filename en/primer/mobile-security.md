# Mobile Security Primer

Mobile security entails many of the challenges of Web security – a wide audience, rapid development, and continuous network connectivity – combined with the risks common to more traditional fat client applications such as buffer management, local encryption, and malware. One of the unique features to the mobile environment is the prevalence of installed applications coming from unknown developers who should be considered “untrusted.”

## The Mobile Attack Surface

As illustrated below, a mobile attack can involve the device layer, the network layer, the data center, or a combination of these. Inherent platform vulnerabilities and social engineering continue to pose major opportunities for cyber thieves and thus significant challenges for those looking protect user data. 

![Anatomy of a Mobile Attack](/assets/mobile-attack-surface.png)

### Attack Vectors

There are three points in the mobile technology chain where malicious parties may exploit vulnerabilities to launch malicious attacks:

 * The device
 * The network
 * The data center

## The Device

Mobile devices pose significant risks for sensitive corporate information (SCI); key risks include data loss and compromised security. Whether iPhone, Android or other smartphone, attackers targeting the device itself can use a variety of entry points:

 * Browser, mail, or other preloaded applications
 * Phone/SMS
 * Third-party applications (apps)
 * Operating system
 * RF such as Baseband, Bluetooth and other comm channels


### Browser-based attacks

Browser-based points of attack can include:

**Phishing** – Involves acquiring personal information such as usernames, passwords, and credit card details by masquerading as a trusted entity through e-mail spoofing. Research has shown that mobile users are three times more likely than desktop users to submit personal information to phishing websites. This is, in part, likely due to the scaled down environment a mobile browser runs in, which displays only small portions of URLs due to limited screen real-estate, limited warning dialogs, scaled down secure lock icons, and foregoes many user interface indicators such as large STOP icons, highlighted address bars, and other visual indicators.

**Framing** - Framing involves delivery of a Web/WAP site in an iFrame, which can enable “wrapper” site to execute clickjacking attacks.

**Clickjacking** – Also known as UI redressing, clickjacking involves tricking users into revealing confidential information or taking control of their device when a user clicks on a seemingly innocuous link or button. This attack takes the form of embedded code or scripts that execute without user knowledge. Clickjacking has been exploited on sites including Facebook to steal information or direct users to attack sites.

**Drive-by Downloading** – Android in particular has been vulnerable to this attack, where a Web site visit causes a download to occur without user knowledge, or by tricking the user with a deceptive prompt. The download can be a malicious app, and the user then may be prompted automatically by the device to install the app. When Android devices are set to allow apps from “unknown sources” the installation is allowed.

**Man-in-the-Mobile (MitMo)** – Allows malicious users to leverage malware placed on mobile devices to circumvent password verification systems that send codes via SMS text messages to users’ phones for identity confirmation.


### Phone/SMS-based attacks

Phone/SMS points of attack can include:

**Baseband attacks** – Attacks that exploit vulnerabilities found in a phone’s GSM/3GPP baseband processor, which is the hardware that sends and receives radio signals to cell towers.

**SMiShing** – Similar to phishing, but uses cell phone text messages in place of e-mail messages in order to prompt users to visit illegitimate websites and enter sensitive information such as usernames, passwords and credit card numbers.

**RF Attacks** – Bluejacking, NFC attacks and other RF exploits find vulnerabilities on various peripheral communication channels that are typically used in nearby device-to-device communications.


### Application-based attacks

App-based points of attack can include:

**Sensitive Data Storage** – A 2011 viaForensics study found 83% of popular apps sampled store data insecurely.

**No Encryption/weak encryption** – Apps that allow the transmission of unencrypted or weakly encrypted data are vulnerable to attack.

**Improper SSL validation** – Bugs in an app’s secure socket layer (SSL) validation process may allow data security breaches.

**Config manipulation** – Includes gaining unauthorized access to administration interfaces, configuration stores, and retrieval of clear text configuration data.

**Dynamic runtime injection** – Allows an attacker to manipulate and abuse the runtime of an application to bypass security locks, bypass logic checks, access privileged parts of an application, and even steal data stored in memory.

**Unintended permissions** – Misconfigured apps can sometimes open the door to attackers by granting unintended permissions.

**Escalated privileges** – Exploits a bug, design flaw or configuration oversight in order to gain access to resources normally protected from an application or user.


### OS-based attacks

Operating system-based points of attack can include:

**No passcode** – Many users choose not to set a passcode, or use a weak PIN, passcode or pattern lock.

**iOS jailbreaking** – “Jailbreaking” is a term for removing the security mechanisms put forth by the manufacturer and carrier that prevent unauthorized code from running on the device. Once these restrictions are removed the device can become a gateway for malware and other attacks.

**Android rooting** – Similar to jailbreaking, rooting allows Android users to alter or replace system applications and settings, run specialized apps that require administrator-level permissions. Like jailbreaking, it can result in the exposure of sensitive data.

**Passwords and data accessible** – Devices such as Apple’s line of iOS devices, have known vulnerabilities in their cryptographic mechanisms for storing encrypted passwords and data. An attacker with knowledge of these vulnerabilities can decrypt the device’s keychain, exposing user passwords, encryption keys, and other private data.

**Carrier-loaded software** – Software pre-installed on devices can contain security flaws. Recently, some pre-loaded apps on Android handsets were found to contain security vulnerabilities that could be used to wipe the handset, steal data, and even eavesdrop on calls.

**Zero-day exploits** – Attacks often occur during the window between when a vulnerability is first exploited and when software developers are able to issue a release addressing the issue.


## The Network

Network-based points of attack can include:

**Wi-Fi (weak encryption/no encryption)** – Applications failing to implement encryption, when used across a Wi-Fi network run the risk of data being intercepted by a malicious attacker eavesdropping on the wireless connection. Many applications utilize SSL/TLS, which provides some level of protection; however some attacks against SSL/TLS have also been proven to expose critical user data to an attacker.

**Rogue access points** – Involves physically installing an unauthorized wireless access point that grants parties access to a secure network.

**Packet sniffing** – Allows a malicious intruder to capture and analyze network traffic, which typically includes username and password information transmitted in clear text.

**Man-in-the-Middle (MITM)** – Involves eavesdropping on an existing network connection, intruding into that connection, intercepting messages, and modifying select data.

**SSLStrip** – A form of the man-in-the-middle attack that exploits weakness in the SSL/TLS implementation on Web sites, which can rely on the user verifying that an HTTPS connection is present. The attack invisibly downgrades connections to HTTP, without encryption, and is difficult for users to detect in mobile browsers.

**Session hijacking** – Involves exploitation of a session key to gain unauthorized access to user and network information.

**DNS poisoning** – Exploiting network DNS can be used to direct users of a website to another site of the attacker’s choosing. In some cases attacks can also inject content through apps.

**Fake SSL certificates** – Another man-in-the-middle attack that involves issuing fake SSL certificates that allow a malicious user to intercept traffic on a supposedly secure HTTPS connection.


## The Data Center

Attackers targeting the data center use two main points of entry:

 * Web server
 * Database


### Web server-based attacks

Web server-based attacks and vulnerabilities include:

**Platform vulnerabilities** – Vulnerabilities in the operating system, server software, or application modules running on the web server can be exploited by an attacker. Vulnerabilities can sometimes be uncovered by monitoring the communication between a mobile device and the web server to find weaknesses in the protocol or access controls.

**Server misconfiguration** – A poorly configured web server may allow unauthorized access to resources that normally would be protected.

**Cross-site scripting (XSS)** – Cross-site scripting is an attack that involves injecting malicious JavaScript code into a website. Pages that are vulnerable to this type of attack return user input to the browser without properly sanitizing it. This attack is often used to run code automatically when a user visits a page, taking control of a user’s browser. After control of the browser has been established, the attacker can leverage that control into a variety of attacks, such as content injection or malware propagation.

**Cross-site Request Forgery (CSRF)** – Cross-site request forgery involves an attacker creating HTTP (Web) requests based on knowledge of how a particular web application functions, and tricking a user or browser into submitting these requests. If a Web app is vulnerable, the attack can execute transactions or submissions that appear to come from the user. CSRF is normally used after an attacker has already gained control of a user’s session, either through XSS, social engineering, or other methods.

**Weak input validation** – Many Web services overly trust the input coming from mobile applications, relying on the application to validate data provided by the end user. However, attackers can forge their own communication to the web server or bypass the application’s logic checks entirely, allowing them to take advantage of missing validation logic on the server to perform unauthorized actions.

**Brute-force attacks** – A brute-force attack simply tries to guess the valid inputs to a field, often using a high rate of attempts and dictionaries of possible values. The most common usage of a brute-force attack is on authentication, but it can also be used to discover other valid values in a Web app. 


### Database attacks

Database attacks and vulnerabilities include:

**QL injection** – Interfaces that don’t properly validate user input can result in SQL being injected into an otherwise innocuous application query, causing the database to expose or otherwise manipulate data that should normally be restricted from the user or application.

**OS command execution** – Similar to SQL injection, certain database systems provide a means of executing OS-level commands. An attacker can inject such commands into a query, causing the database to execute these commands on the server, providing the attacker with additional privileges, up to and including root level system access.

**Privilege escalation** – This occurs when an attack leverages some exploit to gain greater access. On databases this can lead to theft of sensitive data.
Data dumping – An attacker causes the database to dump some or all data within a database, exposing sensitive records.


## Types of Mobile Apps

Mobile applications typically fall under three operational categories:

**Web**** – Apps that operate via a general purpose web browser. Sometimes referred to as WAP or Mobile Sites, these are the mobile equivalent to functional web applications that have proliferated in the past decade offering many capabilities such as online banking and shopping. Although regular web sites can be used in mobile web browsers, many companies now create a separate mobile web app to optimize for mobile attributes, such as smaller screen size, touch-based navigation and availability of GPS location.

**Native** – Installed apps that operate off the native mobile device operating system, compiled for the specific mobile platform and leveraging its APIs. These are typically (though not always) downloaded and installed via an app market.

**Wrapper** – Apps that operate by leveraging web pages inside a dedicated native application wrapper, also sometimes referred to as “shell apps” or “hybrid apps.” While appearing as a native app to the end user, the web-based functionality can result in different vulnerabilities than are found in fully native coded apps.

