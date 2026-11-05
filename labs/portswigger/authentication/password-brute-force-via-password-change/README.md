# Password brute-force via password change

> **Platform:** PortSwigger Web Security Academy<br>
> **Category:** Authentication<br>
> **Tooling:** Burp Suite

← [Back to Authentication labs](../README.md)

## Summary

I completed PortSwigger's [Password brute-force via password change](https://portswigger.net/web-security/authentication/other-mechanisms/lab-password-brute-force-via-password-change) lab. The weakness is not on the login screen: the password-change endpoint trusts a client-supplied username and reveals whether the current password is correct through distinct responses.

## Approach

Using the lab account, I inspected `POST /my-account/change-password` in Burp Suite. Its request body included `username`, `current-password`, `new-password-1`, and `new-password-2`. Because the username was supplied by the client, I replaced it with the lab's target account during the authorized exercise.

Before automating, I compared the form's behavior:

| Current password | New passwords | Response |
|---|---|---|
| Incorrect | Different | `Current password is incorrect` |
| Correct | Different | `New passwords do not match` |
| Incorrect | Matching | May trigger the account lockout |

Keeping the new-password fields intentionally different avoids changing the password and turns the differing response into a confirmation signal. I varied only the current-password field with the wordlist supplied by the lab, then used Burp Intruder's response matching to locate the successful candidate. I confirmed it through the lab's normal login flow.

The discovered password is intentionally omitted because it belongs only to the disposable lab instance and does not add technical value.

## Reference screenshots

The images below are from [siunam321's public writeup](https://github.com/siunam321/CTF-Writeups/tree/main/Portswigger-Labs/Authentication/Auth-12). They illustrate the same lab and are **not captures from my session**.

![Intercepted password-change request in Burp Suite, screenshot by siunam321](https://raw.githubusercontent.com/siunam321/CTF-Writeups/main/Portswigger-Labs/Authentication/Auth-12/images/Pasted%20image%2020221222061804.png)

![Incorrect-current-password response, screenshot by siunam321](https://raw.githubusercontent.com/siunam321/CTF-Writeups/main/Portswigger-Labs/Authentication/Auth-12/images/Pasted%20image%2020221222063542.png)

![Response that reveals a correct current password, screenshot by siunam321](https://raw.githubusercontent.com/siunam321/CTF-Writeups/main/Portswigger-Labs/Authentication/Auth-12/images/Pasted%20image%2020221222063736.png)

## Why it works

The application verifies the current password even when the new passwords do not match. It also trusts a request-controlled username and provides a different message for each condition. Together, those behaviors make the password-change route an oracle for another account's current password without using the normal login flow.

## Remediation

- Bind password changes to the authenticated server-side session, never a client-provided username.
- Apply attempt limits to password-change routes as well as login routes.
- Use responses that do not reveal whether the current password was correct.
- Record suspicious attempts and require fresh authentication before sensitive changes.

## References

- [PortSwigger — lab and official solution](https://portswigger.net/web-security/authentication/other-mechanisms/lab-password-brute-force-via-password-change)
- [PortSwigger — authentication vulnerabilities](https://portswigger.net/web-security/authentication/other-mechanisms)
- [PortSwigger — securing authentication](https://portswigger.net/web-security/authentication/securing)
- [siunam321 — source of illustrative screenshots](https://github.com/siunam321/CTF-Writeups/tree/main/Portswigger-Labs/Authentication/Auth-12)
