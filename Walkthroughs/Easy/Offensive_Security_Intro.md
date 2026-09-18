# Offensive Security Intro

- TryHackMe: [Offensive Security Intro](https://tryhackme.com/room/offensivesecurityintro)
- Difficulty: Easy
- Estimated time: 15 minutes
- Topics: `offensive security`, `web enumeration`, `gobuster`

> This walkthrough is for the authorized TryHackMe lab only. Do not scan or attack systems without explicit permission.

## Objective

This room introduces offensive security by simulating the work of an ethical hacker. The practical task is to enumerate a deliberately vulnerable banking website, find a hidden page, and demonstrate the impact of the exposed functionality.

## Offensive security

Offensive security focuses on identifying and safely exploiting weaknesses before a real attacker can use them. The results should be documented and reported so the owner can fix the vulnerability.

## Lab setup

Start the lab machine from the room and use the browser provided by TryHackMe. The target is the FakeBank application available at:

```text
http://fakebank.thm
```

All actions below stay inside the authorized lab environment.

## Reconnaissance

A website may contain pages that are not linked from its main navigation. Gobuster can test a list of common names and report paths that exist on the target.

```bash
gobuster dir -u http://fakebank.thm -w wordlist.txt
```

The important options are:

- `dir`: use directory and file enumeration mode
- `-u`: specify the target URL
- `-w`: specify the wordlist to test

The scan reveals a hidden endpoint named `/bank-transfer`. A successful HTTP response indicates that the page exists.

## Exploiting the exposed functionality

Open the discovered endpoint in the lab browser:

```text
http://fakebank.thm/bank-transfer
```

The page exposes a money transfer function that should not be publicly accessible. The room instructs you to transfer `$2000` from account `2276` to account `8881`.

After submitting the transfer, return to the account page and refresh the balance. The lab displays the room answer after the transfer succeeds. The answer is intentionally omitted here:

```text
THM{REDACTED}
```

## Findings

The main issue is an access-control failure: a sensitive administrative function is discoverable and usable without appropriate authentication or authorization controls.

A production application should:

- Require authentication for administrative actions.
- Enforce authorization on the server side for every transfer.
- Avoid exposing sensitive endpoints through predictable names.
- Log and monitor high-risk account activity.
- Validate transfer ownership and transaction limits.

## Conclusion

This room demonstrates a basic offensive-security workflow:

1. Identify the target in an authorized environment.
2. Enumerate hidden web content.
3. Investigate an exposed function.
4. Demonstrate the impact without attacking unrelated systems.
5. Report the vulnerability and recommend defensive controls.
