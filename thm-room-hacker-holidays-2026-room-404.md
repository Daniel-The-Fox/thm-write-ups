# TryHackMe Room Write-Up: Hacker Holidays 2026 - Room 404

<img src="https://tryhackme.com/_next/image?url=https%3A%2F%2Fcdn-images.tryhackme.com%2Froom-icons%2F5dbea226085ab6182a2ee0f7-1785087675274&w=256&q=75" width="100px" />

## Room Info
* **Name:** [Hacker Holidays 2026 - Room 404](https://tryhackme.com/room/hh-room404-804573bf)
* **Difficulty:** Easy

---

## Walkthrough

1. Start the room's Lab Machine & AttackBox or connect to the THM Room network via OpenVPN
2. Call `http://<machine IP address>:8080` in your web browser
3. Just in case, run a port scan on the machine IP address, but there's only SSH (22) and httpd at 8080
4. Don't waste time like me messing around with Kali pre-installed wordlists of gobuster and dirbuster! :joy:
5. `sudo apt install seclists` is your friend! :wink:
6. Run a quick web directory enumeration with the `quickhits.txt` list from the seclists collection via gobuster
7. You should discover a git repository which you could look at via web browser, but that won't get you far
8. Instead `wget -r <url>` is your quickest shot
9. cd into the downloaded git repo
10. Analyze the git repo with basic git commands (i.e. `git status`) to see the commit history (`git log`) and commit content (`git show <commit>`)
