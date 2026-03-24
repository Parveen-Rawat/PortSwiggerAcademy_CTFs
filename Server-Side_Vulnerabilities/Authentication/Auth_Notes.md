# Authentication Notes and Commands

Authentication vulnerabilities allows attacker to gain control of sensitive data by abusing the weak security system in place

## What is an Authentication?

--> Authentication is the process of verifying user's identity. There are three types of authentication:

  - `Knowledge Factor` --> Something you know
  - `Possession Factor` --> Something you have
  - `Inherence Factor` --> Something you are or do


## Difference between Authentication and Authoritzation?

--> Authentication --> Process of verifying identity of user

--> Authorization --> What can authenticated user do in the given environment

## Why authentication vulnerability exists?

1. Weak security mechnism in place to face brute force attacks
2. Insecure coding practices and logic flaws --> Broken Authentication

---

# Vulnerbilities in password-based authentication

## Brute Force Attacks
- A brute-force attack is when an attacker uses a system of trial and error to guess valid user credentials. 
- These attacks are typically automated using wordlists of usernames and passwords. 
- Automating this process, especially using dedicated tools, potentially enables an attacker to make vast numbers of login attempts at high speed.

### Username Enumeration

Username enumeration typically occurs either on the login page, for example, when you enter a valid username but an incorrect password, or on registration forms when you enter a username that is already taken. This greatly reduces the time and effort required to brute-force a login because the attacker is able to quickly generate a shortlist of valid usernames. 

==Things to observe==
- Status Codes
- Error Messages --> Password incorrect instead of username or password incorrect
- Response Times

# LAB 01 --> 

Let's first capture the request in burp and sent it to intruder

But before that see how the data is being handled --> on sending wrong username and password ==> response says  "Invalid Username"

<img width="1087" height="623" alt="image" src="https://github.com/user-attachments/assets/81b1c576-802c-4d4e-bb1f-574f4748c43c" />

Select sniper attack -> Copy username -> Paste payload --> attack

Look for the change in either in response received or length 

found change in length --> sent that response back to intruder --> this time select password param add to payload --> sniper attack --> paste password list --> attack

<img width="964" height="606" alt="image" src="https://github.com/user-attachments/assets/14feea97-3cb3-45db-a6df-bcfc1e7088dd" />

See for the change in response code as if the password is correct --> response code should be in 3xx

<img width="1454" height="870" alt="image" src="https://github.com/user-attachments/assets/e46a817e-cc5b-4a57-9c84-e4f3944249de" />

<img width="1209" height="516" alt="image" src="https://github.com/user-attachments/assets/1599f125-5ad8-4729-a4ea-c1c11dc6e04f" />

--Solved--

---

LAB 02 -->

Launch and capture the request --> sent it to intruder but before that see how the data is being handled

<img width="871" height="428" alt="image" src="https://github.com/user-attachments/assets/c0a37ee8-0616-4921-95d5-c55312cd25e6" />

![Uploading image.png…]()

Sniper attack --> paste the username list --> attack --> look for changes


