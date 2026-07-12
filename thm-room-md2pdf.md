# TryHackMe Room Write-Up: Neighbour

<img src="https://cdn-images.tryhackme.com/room-icons/c53da808dba7b45a03b79dacf587ebb6.png" width="100px" />

## Room Info
* **Name:** [MD2PDF](https://tryhackme.com/room/md2pdf)
* **Difficulty:** Easy

---

## Walkthrough

1. Start the room's Lab Machine & AttackBox or connect to the THM Room network via OpenVPN
2. Call `http://<machine IP address>` in your web browser
3. Test the webapp with some dummy text to understand how it works
4. Look at the source code of the MD2PDF webapp in order to see how the entered Markdown text is processed and passed onto the MD2PDF webapp to generate the PDF file
5. Now that you know the endpoint of the webapp data converter, you can switch to the Shell and just use curl to save time
6. You will feel the urge to try different embeds (Markdown image reference, Inline HTML object, embed and iframe tags), but none of them will work, or in the best case, an empty PDF will be returned
7. Change of perspective: Run a port scan on the Lab Machine!
8. You will discover that the same webapp is running also on port 5000!
9. So now, an idea could be to repeat all the injection attempts on the webapp on port 5000, but this will also fail or lead to the same results as previously
10. Is there maybe a sort of admin panel for the MD2PDF webapp? You should use dirbuster or Gobuster to check that...
11. Accessing the admin panel via your browser will be blocked. However, the 403 response gives you the final hint!
12. With this final hint, you can come up with an iframe embed to the admin panel, which you can either send via the webapp in your browser, or via curl, to obtain the flag needed to finish the MD2PDF room.
