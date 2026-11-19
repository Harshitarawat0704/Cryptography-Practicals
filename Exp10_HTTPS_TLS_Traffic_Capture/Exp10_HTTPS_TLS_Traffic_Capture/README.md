# Experiment 10: Capturing HTTPS Traffic and Analyzing TLS Handshake, Certificates and Cipher Suites

## Aim
To capture HTTPS communication using Wireshark and analyze the TLS handshake process, digital certificates, and the cipher suite selected for secure data transmission.

## Software/Tools Required
- Wireshark
- Web Browser
- Internet Connection

## Learning Outcomes
1. Learn how to capture HTTPS packets using Wireshark.
2. Recognize and examine TLS handshake messages.
3. View and analyze digital certificate details.
4. Determine the cipher suite selected during the TLS handshake.

## Working Procedure

### Step 1: Launch Wireshark
1. Open the Wireshark application.
2. Choose the currently active network interface, such as Wi-Fi or Ethernet.
3. Click on **Start Capturing Packets** to begin monitoring network traffic.

### Step 2: Generate HTTPS Communication
1. Launch any web browser.
2. Navigate to [https://www.google.com](https://www.google.com).
3. Use the website for a few seconds to generate HTTPS traffic.
4. Go back to Wireshark and stop the packet capture.

### Step 3: Filter TLS Packets
Enter the following display filter in Wireshark:

```text
tls
```

Press Enter to view all packets related to TLS communication.

### Step 4: Analyze Client Hello Message
Apply the following filter:

```text
tls.handshake.type == 1
```

Choose a Client Hello packet and expand the following section:

Transport Layer Security → Handshake Protocol: Client Hello

Check the following details:
- TLS Version
- Random
- Available Cipher Suites
- Extensions
- Server Name

**Screenshots:**

![Client Hello 1](screenshots/Client_Hello(1).png)

![Client Hello 2](screenshots/Client_Hello(2).png)

### Step 5: Analyze Server Hello Message
Apply this display filter:

```text
tls.handshake.type == 2
```

Select the Server Hello packet and expand:

Transport Layer Security → Handshake Protocol: Server Hello

Find the cipher suite selected by the server.

Example: `TLS_AES_128_GCM_SHA256`

**Screenshots:**

![Server Hello 1](screenshots/Server_Hello(1).png)

![Server Hello 2](screenshots/Server_Hello(2).png)

### Step 6: Find the Digital Certificate
Enter the following filter:

```text
tls.handshake.type == 11
```

Select the Certificate packet and expand the following fields:

Transport Layer Security → Handshake Protocol: Certificate → Certificates → Certificate

Inspect the available X.509 digital certificate information.

### Step 7: Analyze Certificate Details
Check the certificate and note down these important attributes:

1. **Subject:** Represents the domain name or organization to which the certificate belongs.
2. **Issuer:** Indicates the Certificate Authority (CA) responsible for issuing the certificate.
3. **Validity:** Displays the certificate's starting date (Not Before) and expiration date (Not After).
4. **Public Key:** Under Subject Public Key Info, identify the algorithm used for the public key.
5. **Signature Algorithm:** Shows the cryptographic algorithm used to sign the digital certificate.

**Screenshots:**

![Certificate Details 1](screenshots/Certificate_Details(1).png)

![Certificate Details 2](screenshots/Certificate_Details(2).png)

### Step 8: Check the Selected Cipher Suite
Apply the following display filter:

```text
tls.handshake.type == 2
```

Open the Server Hello packet and navigate to:

Handshake Protocol: Server Hello → Cipher Suite

Identify and note the cipher suite chosen for establishing secure communication.

## Useful Wireshark Filters

| Purpose | Display Filter |
|---|---|
| TLS Packets | `tls` |
| Client Hello | `tls.handshake.type == 1` |
| Server Hello | `tls.handshake.type == 2` |
| Certificate | `tls.handshake.type == 11` |
| TLS Handshake | `tls.handshake` |
| HTTPS/TCP Packets | `tcp.port == 443` |

## Observation Table

| S. No. | Parameter | Observation |
|---|---|---|
| 1 | Website Visited | www.google.com |
| 2 | TLS Version | TLS 1.3 |
| 3 | Client Hello | Successfully Identified |
| 4 | Server Hello | Successfully Identified |
| 5 | Certificate Subject | CN=www.google.com |
| 6 | Certificate Issuer | Google Trust Services (WE2) |
| 7 | Certificate Valid From | 07 October 2026 |
| 8 | Certificate Valid To | 30 December 2026 |
| 9 | Public Key Algorithm | EC Public Key |
| 10 | Signature Algorithm | ecdsa-with-SHA256 |
| 11 | Selected Cipher Suite | TLS_AES_128_GCM_SHA256 |

## Result
HTTPS network communication was successfully captured and analyzed using Wireshark. The TLS handshake messages, digital certificate attributes, TLS version, and selected cipher suite were identified and examined.