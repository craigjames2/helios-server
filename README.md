# Carleton Helios

This is part of the Electronic Voting Machine project of the 2020-21 Carleton CS comps. 

Advisor: Sneha Narayan 

Members: James Craig, John Sherer, Judy Bush, Kate Sweeney, Matthew Stritzel, Harry Tian

Our project dug into electronic voting machines (EVMs) and what must be done to ensure that they are secure, usable, and trustworthy. A major component of the project is to explore EVM issues through the framework of an existing EVM, Helios. [Helios Voting](https://vote.heliosvoting.org/) is a web-based open-audit electronic voting system. After analyzin Helios and the issues behind it using our threat model, we modified Helios in several ways:

1. A customizable verifiability features that allow administrators to customize the election's degree of verifiability/ballot secrecy.
2. The email server for private election is not working so we disabled private elections altogether.
3. We made some improvements to Helios usability and designs.

Details about our threat model and analyze can be find on our [website](https://cs.carleton.edu/cs_comps/2021/votingmachines/final-results/index.html)

Special thanks to our advisor Sneha for guiding us through this project and to Mike Tie for helping us troubleshoot Helios on our remote server.

## Customizable verifiability

A key feature of Helios is its open-audit, ["true-verifiable"](https://vote.heliosvoting.org/faq) nature. That is, anyone can verify *anyone's* votes *at any time*. We implemented a customizable version of this where the when creating an election, users can choose how much verifiability or ballot secrecy they want. The idea behind this can be found in our website. As parameters, the adminstrator can modify the following options, where the options are in brackets:

When the election is open: 
* anyone can audit votes belonging to **\[anyone, themselves, nobody\]**

When the election is closed: 
* anyone can audit votes belonging to **\[anyone, themselves, nobody\]**

### Code changes

We added fields `admin_perm_open` and `admin_perm_close` to Helios' Django forms and models by modifying `helios/models.py`,  `helios/views.py`, `helios/forms.py`, `helios/migrattions/0001_initial.py`, although we are unsure if all of those changes are necessary. To distinguish if the election is open or closes, we used the Helios parameter `election.voting_has_stopped`.

To the implement the verifiability options, we enabled or disabled access to voters' encrypted ballot, which can be used to verify votes. Changes were made to `templates/voters_list.html` and `templates/castvote.html`. 

## Disabling private elections

Helios allows private elections, where the administrator provides a list of eliglible voters and their emails and Helios sends to those voters passwords to vote. However, the emails are never sent due to Helios' email server issues. In other words, private elections are not working. Thus, we've decided to disable the feature altogether.

### Code changes

Files that we changed to implement this include `helios/forms.py` and `templates/voters_list.html`. Code related to private elections were commented out.

## Improvements on Helios usability

Following feedback from independent studies (including our own), we made some modifications to the layout of the site. These are mostly cosmetic and helps ease the process for unfamiliar users. These include repositioning the login button, providing a notice of login status above the voting button on the main page, reformatting the next/previous/proceed buttons, repositioning the audit button, and various updates to language for precision, comprehensibility and removing redundancy.

### Code changes

We made changes in in the following files.
- heliosbooth/templates/audit.html
- heliosbooth/templates/question.html
- heliosbooth/templates/seal.html
- heliosbooth/vote.html
- server_ui/templates/base.html
