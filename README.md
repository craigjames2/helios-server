# Carleton Helios

This is part of the Voting machine comps of the 2020-21 Carleton CS comps. 

Advisor: Sneha Narayan 

Members: Harry, James, John, Judy, Kate, Matthew

This project is based off of [Helios Voting](https://vote.heliosvoting.org/), a web-based open-audit electronic voting system. In our implementation, we added three features:
1. A customizable verifiability features that allow administrators to customize the election's degree of verifiability/ballot secrecy.
2. The email server for private election is not working so we disabled private elections altogether.
3. We made some improvements to Helios usability and designs.

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

### Code changes

## Improvements on Helios usability

### Code changes
