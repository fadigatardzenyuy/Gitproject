# How the Internet Works
### A Complete Lesson Guide for Web Development Students
**By Fadidev Studio**

---

## Table of Contents

1. [What Is the Internet?](#1-what-is-the-internet)
2. [How Data Travels — Packets & Routers](#2-how-data-travels--packets--routers)
3. [IP Addresses](#3-ip-addresses)
4. [DNS — The Internet's Phonebook](#4-dns--the-internets-phonebook)
5. [Clients and Servers](#5-clients-and-servers)
6. [HTTP and HTTPS](#6-http-and-https)
7. [How a Browser Renders a Page](#7-how-a-browser-renders-a-page)
8. [The Full Journey — Putting It All Together](#9-the-full-journey--putting-it-all-together)
9. [Recap Questions](#9-recap-questions)
10. [Homework Task](#10-homework-task)

---

## 1. What Is the Internet?

The internet is a **massive global network of computers connected together**. It is not a cloud floating somewhere in the sky — it is real, physical infrastructure: cables running under the ocean, towers transmitting wireless signals, and millions of servers sitting in large buildings called **data centers**.

### The Internet vs The Web

Many people think the internet and the World Wide Web (WWW) are the same thing. They are not.

| Term | What It Is |
|------|------------|
| **The Internet** | The physical network of connected computers (the infrastructure) |
| **The Web** | A service that runs *on top of* the internet, made of websites and web pages |
| **Email** | Another service that runs on the internet |
| **Video calls** | Another service that runs on the internet |

> **Analogy:** The internet is the road network. The web is the cars driving on it. Email is a delivery truck. Online games are taxis. They all use the same roads but are different services.

### A Brief History

- The internet began as **ARPANET** in the late 1960s — a US military project to connect computers across universities
- In 1989, **Tim Berners-Lee** invented the World Wide Web — a system of linked documents accessible via the internet
- Today, over **5 billion people** use the internet every day

---

## 2. How Data Travels — Packets & Routers

When you send a message or load a website, your data does not travel as one big block. It gets **broken into small pieces called packets**.

### What Is a Packet?

A packet is a small chunk of data. Every piece of information sent over the internet — a photo, a message, a web page — is broken into many packets before it travels.

Each packet contains:
- A piece of the actual data (the payload)
- The **sender's address** (where it came from)
- The **receiver's address** (where it is going)
- A sequence number (so packets can be reassembled in the right order)

> **Analogy:** Imagine writing a 10-page letter and tearing each page apart. You mail each page in a separate envelope through different post offices. When all envelopes arrive, the receiver staples them back together in order. That is exactly how packets work.

### What Is a Router?

A **router** is a device that reads the address on each packet and decides the best path to send it forward. There are millions of routers across the internet, forming a huge relay system.

```
Your Computer
     |
  Home Router
     |
  ISP Router  (ISP = Internet Service Provider, e.g. MTN, Orange)
     |
  Backbone Router  (high-speed cables connecting countries)
     |
  Destination Server
```

### Why Break Data Into Packets?

- If one packet fails, only that piece needs to be resent — not the entire file
- Different packets can travel different routes and arrive faster
- Many users can share the same network at the same time without waiting

---

## 3. IP Addresses

Every device connected to the internet has a unique identifier called an **IP address** (Internet Protocol address).

Think of it like a home address. Just as every house has a unique address so that letters can be delivered correctly, every device on the internet has a unique IP address so that packets can be delivered to the right place.

### What Does an IP Address Look Like?

**IPv4 example:**
```
192.168.1.1
```
This is four numbers separated by dots, each between 0 and 255.

**IPv6 example:**
```
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

### IPv4 vs IPv6

| | IPv4 | IPv6 |
|--|------|------|
| Format | 4 numbers (e.g. 192.168.1.1) | 8 groups of hex (longer) |
| Total addresses | ~4.3 billion | 340 undecillion (virtually unlimited) |
| Problem | Running out of addresses | Designed to replace IPv4 |

> **Why IPv6?** The internet grew so fast that we ran out of IPv4 addresses. IPv6 was created to provide enough addresses for every device on earth — and far beyond.

### Public vs Private IP

- **Public IP** — the address your internet provider gives your home/office network (visible to the internet)
- **Private IP** — the address given to each device inside your home network (e.g. your phone gets `192.168.1.5`, your laptop gets `192.168.1.6`)

> **Try it yourself:** Open your terminal and type `curl ifconfig.me` to see your public IP address.

---

## 4. DNS — The Internet's Phonebook

Humans remember names like `google.com`. Computers communicate using IP addresses like `142.250.200.46`. **DNS (Domain Name System)** is the system that translates one into the other.

### How DNS Works — Step by Step

When you type `www.google.com` into your browser, this is what happens:

```
Step 1 — Browser Cache Check
  Browser checks if it already knows the IP for google.com
  (from a recent visit). If yes, skip to Step 5.

Step 2 — OS Cache Check
  Browser asks the operating system (Windows/Mac/Linux).
  If the OS has it cached, skip to Step 5.

Step 3 — Recursive Resolver
  Your ISP has a DNS resolver that handles the lookup on your behalf.

Step 4 — Root & TLD Name Servers
  The resolver asks the Root server → directed to .com server →
  directed to Google's name server → gets the IP address.

Step 5 — IP Returned
  The browser now has the IP address: 142.250.200.46

Step 6 — Connection Made
  Browser connects to that IP and loads the page.
```

> **Analogy:** DNS is like a phonebook. You know your friend's name (google.com), the phonebook gives you their phone number (142.250.200.46), and then you call them.

### What Is a Domain Name?

A domain name is the human-readable address of a website. It has parts:

```
https://www.google.com
        |   |      |
        |   |      +-- TLD (Top-Level Domain): .com, .org, .net, .cm
        |   +--------- Second-Level Domain: google
        +------------- Subdomain: www
```

> **Try it yourself:** Open your terminal and type `nslookup google.com` or `ping google.com`. You will see the real IP address that DNS returns.

---

## 5. Clients and Servers

The internet runs on a simple model: **clients ask, servers answer**.

### What Is a Client?

A **client** is any device or software that sends a request for data.

Examples:
- Your web browser (Chrome, Firefox, Edge)
- A mobile app on your phone
- A desktop application

### What Is a Server?

A **server** is a powerful computer that stores resources (files, databases, media) and responds to requests from clients.

- Servers run 24 hours a day, 7 days a week
- A single server can handle thousands of requests at the same time
- Servers are stored in large buildings called **data centers**

### The Request-Response Cycle

```
Client                          Server
  |                               |
  |------- HTTP Request --------> |
  |        "Give me google.com"   |
  |                               |
  |<------ HTTP Response -------- |
  |        HTML + CSS + JS files  |
  |                               |
Browser renders the page
```

> **Analogy:** You (client) walk into a restaurant and order jollof rice. The kitchen (server) prepares it and sends it to your table. The waiter is the network carrying messages back and forth.

---

## 6. HTTP and HTTPS

**HTTP (HyperText Transfer Protocol)** is the language clients and servers use to communicate. It is a set of rules that define how requests and responses are formatted and transmitted.

### An HTTP Request

When your browser wants a web page, it sends an HTTP request that looks something like this:

```
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0 (Chrome)
Accept: text/html
```

- `GET` — the method (what kind of action we want)
- `/index.html` — the resource we are asking for
- `Host` — the server we are talking to

### An HTTP Response

The server replies with a response:

```
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 1234

<!DOCTYPE html>
<html>
  <head>...</head>
  <body>...</body>
</html>
```

### HTTP Methods

| Method | Purpose | Example Use |
|--------|---------|-------------|
| `GET` | Fetch/retrieve data | Load a web page |
| `POST` | Send/submit data | Submit a login form |
| `PUT` | Update existing data | Edit a profile |
| `DELETE` | Remove data | Delete a post |

### HTTP Status Codes

The server always responds with a **status code** — a 3-digit number that tells you what happened.

| Code | Meaning | What It Means in Plain English |
|------|---------|-------------------------------|
| `200` | OK | Everything worked fine |
| `201` | Created | Data was successfully created |
| `301` | Moved Permanently | Page has moved to a new URL |
| `400` | Bad Request | Your request had an error |
| `401` | Unauthorized | You need to log in first |
| `403` | Forbidden | You do not have permission |
| `404` | Not Found | The page does not exist |
| `500` | Internal Server Error | Something broke on the server |

> **Remember this:** 2xx = Success. 3xx = Redirect. 4xx = Client error (your fault). 5xx = Server error (their fault).

### HTTP vs HTTPS

The **S** in HTTPS stands for **Secure**.

| HTTP | HTTPS |
|------|-------|
| Data travels in plain text | Data is encrypted before travelling |
| Anyone on the network can read it | Only the sender and receiver can read it |
| No padlock in browser | Shows a padlock icon in the browser |
| Not safe for passwords or payments | Safe for sensitive information |

HTTPS uses a system called **TLS (Transport Layer Security)** to encrypt data. When you see the padlock icon in your browser, it means:
1. You are talking to the real server (not a fake one)
2. Everything you send is encrypted and private

> **Rule:** Never enter a password, credit card number, or personal information on a website that uses HTTP instead of HTTPS.

---

## 7. How a Browser Renders a Page

Once the browser receives the files from the server (HTML, CSS, JavaScript), it goes through a process called **rendering** to turn those files into the visual page you see.

### Step-by-Step Rendering Process

```
1. HTML Parsing
   Browser reads the HTML file and builds the DOM
   (Document Object Model) — a tree structure of all elements

2. CSS Parsing
   Browser reads the CSS and builds the CSSOM
   (CSS Object Model) — the styling rules for each element

3. Render Tree
   Browser combines the DOM + CSSOM to create the render tree
   (only visible elements are included)

4. Layout
   Browser calculates the exact position and size of every element
   on the screen

5. Paint
   Browser fills in pixels — colors, borders, images, text

6. JavaScript Execution
   JavaScript runs and can update the DOM dynamically,
   changing what you see without reloading the page
```

### What Is the DOM?

The **DOM (Document Object Model)** is how the browser represents your HTML as a tree of objects in memory. JavaScript can read and change the DOM to make pages interactive.

```html
<!-- This HTML... -->
<html>
  <body>
    <h1>Hello</h1>
    <p>World</p>
  </body>
</html>
```

```
...becomes this DOM tree:
html
 └── body
      ├── h1 → "Hello"
      └── p  → "World"
```

---

## 8. The Full Journey — Putting It All Together

Here is the complete journey from typing a URL to seeing a web page:

```
You type: https://www.google.com

  Step 1 — DNS Lookup
    Browser checks cache → asks DNS resolver →
    DNS returns IP: 142.250.200.46

  Step 2 — TCP Connection
    Browser establishes a connection to the server
    at that IP address (via TCP — Transmission Control Protocol)

  Step 3 — TLS Handshake (HTTPS only)
    Browser and server verify each other's identity
    and agree on an encryption key

  Step 4 — HTTP Request
    Browser sends: GET / HTTP/1.1 Host: www.google.com

  Step 5 — Server Responds
    Server sends back: 200 OK + HTML file

  Step 6 — Browser Requests More Files
    Browser reads HTML and finds links to CSS and JS files
    It sends more GET requests for each file

  Step 7 — Rendering
    Browser parses HTML → builds DOM
    Browser parses CSS → builds CSSOM
    Browser runs JavaScript
    Page is displayed on your screen

Total time: Usually under 1 second
```

---

## 9. Recap Questions

Test your understanding by answering these questions:

1. What is the difference between the internet and the World Wide Web?
2. What is a packet, and why is data broken into packets?
3. What does DNS do, and why do we need it?
4. What is the difference between a client and a server?
5. What does HTTP status code 404 mean?
6. Why should you always use HTTPS instead of HTTP?
7. What does the browser do after it receives the HTML from the server?
8. What is the DOM?

---

## 10. Homework Task

**Task:** Use your browser's DevTools to inspect real HTTP traffic.

**Instructions:**
1. Open any website (e.g. `https://github.com`)
2. Press `F12` to open DevTools
3. Click the **Network** tab
4. Reload the page (`Ctrl + R` or `Cmd + R`)
5. Look at the list of requests that appear

**Write down the following:**
- 3 different files that were requested (HTML, CSS, JS, images, etc.)
- The HTTP method used for each (GET, POST, etc.)
- The status code for each request
- Approximately how long each request took (in milliseconds)

**Bonus:** Find one request that returned a status code other than 200 and explain what it means.

---

*Fadidev Studio — Front-End Web Development Training*