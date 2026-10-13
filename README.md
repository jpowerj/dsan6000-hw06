# DSAN 6000 Homework 6: Serverless S3 Bucket Queries with AWS Athena

**Due Sunday, October 18, 11:59pm EDT**

> [!WARNING]
> If you have cloned the repository **template** from the `https://github.com/jpowerj/dsan6000-hw06` URL, you are **not starting the assignment correctly!** That is, if the command you used to clone the repo onto EC2 looks like:
> 
> `git clone https://github.com/jpowerj/dsan6000-hw06`
> 
> This will **not work** for assignments in this course, since you **will not be able to push your changes** back to this repository! (Notice how the above code purposefully has *no copy button!*) Instead, you need to create your **own *private* version of the template** (shared with instructors only), as described in the next section.

### Creating Your Own *Private* Repo From the Template

Click the **green "Use this template" button** in the upper-right corner of the template repo on GitHub, then choose the "Create a new repository" option. On the next page, you will be able to create a **new repository** in **your own GitHub account**. Follow these steps to set up your new private repository:

1.  Within the **"1. General"** section, call it **`dsan6000-hw06`** (the same name as the template), and
1.  Within the **"2. Configuration"** section, choose **Private**
1.  Click the green **Create Repository** button
1.  Once the repository has been created, open the **Settings** page linked at the top of the GitHub interface
1.  In the menu on the left side of the Settings page, within the **"Access"** section, click **"Collaborators"**
1.  Use the **"Manage access"** portion of this Collaborators page to add the course instructors via our GitHub usernames, given in the following table:

<table>
<thead>
</thead>
<tbody>
<tr>
<td>Jeff</td>
<td>
  
```
jpowerj
```

</td>
</tr>
<tr>
<td>Samyu</td>
<td>

```
samyu-vakkalanka
```

</td>
</tr>
<tr>
<td>Fangzhou</td>
<td>

```
fangzhou-wang
```

</td>
</tr>
<tr>
<td>Siru</td>
<td>

```
siruwuu
```

</td>
</tr>
</tbody>
</table>

Once this **derived** private repository has been set up on **your GitHub account**, and you have added the instructors as collaborators, you are all set up to **submit the URL for your newly-created repository on Canvas!** Please submit the URL immediately after creating the repo: this is what will allow us to see your progress and check any issues between distribution and submission.

Then, once you have submitted the URL on Canvas, **clone *your* newly-created repository (*not* the template owned by `jpowerj`) to your EC2 instance to begin working!** In other words, the command you run on EC2 should look as follows (with your GitHub username in place of `YOUR_GH_USERNAME`):

```bash
git clone https://github.com/YOUR_GH_USERNAME/dsan6000-hw06
```

Note that this and other `git` commands interacting with your GitHub repository will likely require you to use a GitHub **Access Token** in place of your password (despite the fact that `git` will ask you for your password, the password you use to log into your GitHub account in your browser typically will *not* work within the `git` command-line interface).

To create this Access Token, **follow the instructions [here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-personal-access-token-classic)**: you can just check off all permissions (since this is a case of you "granting" permissions to yourself – you would need to worry about specific permissions if you were granting access to a coworker on a project, for example!), and you don't need to choose an expiration date for this Access Token (though you can for extra account security).

## HW6 Task: Direct Queries on an S3-Based Data Lake

### Background

The dataset you'll be working with for this assignment is the global "High-Resolution Settlement Layer", a dataset constructed by Columbia's [Center for Integrated Earth Systems Information (CIESIN)](https://ciesin.columbia.edu/) where each row represents a tiny (30m-by-30m) "grid cell" on the surface of the earth, and the columns represent some statistically-inferred demographic information about that grid cell: for this assignment, we're focusing on the estimated **population** for various subgroups (men, women, youth under age 5, elderly over age 60, etc.) within this cell.

There are lots of important social-scientific reasons for utilizing these grid-based estimates, as a complement to the "standard" ways of chopping up territories that you might expect as the default choice: countries, states, provinces, etc... Since this isn't a social science course, however, I'll just quickly highlight two core factors that motivate the analyses in this assignment.

### (1) Rapid Movement Across Political Boundaries

The first factor is just that, with [117.8 million forcibly-displaced people](https://www.unhcr.org/refugee-statistics) in the world as of 2026 (and with this number growing each year), population groups shift rapidly on a day-to-day basis *across* the "standardized" geographic boundaries of countries and provinces.
  
With these population movements happening far too rapidly for a census to track (think of how, e.g., the US Census is only conducted once every 10 years), modern approaches to refugee aid provision instead use [remote sensing](https://en.wikipedia.org/wiki/Remote_sensing) – especially photos taken from satellites – to detect collections of pixels in these photos that might be indicative of new human activity (hence the "Settlement Layer" in the name of the dataset).

### (2) Insufficiency of Census Data

The second factor is that, on the topic of **censuses**, there are also major conflicts in the world (producing large proportions of the 117.8 million forcibly-displaced) in countries which **purposefully do *not* conduct censuses**, for avowedly political reasons.
  
One famous example is **Lebanon**, the country whose political events (in ACLED) you analyzed at the end of HW5! The last "official" census ever conducted in Lebanon took place in 1932, when it was still a French mandate, and its results were used to construct a quota-based presidential-parliamentary system striking a "delicate balance" among Lebanon's... dizzying array of [ethnic and religious populations](https://en.wikipedia.org/wiki/Demographics_of_Lebanon#/media/File:Lebanon_religious_groups_distribution.jpg).

Since that time [crunching an entire country's history into one sentence], no administration since its 1943 independence from France has found it wise to "upset" this "delicate balance" by conducting a new census. Thus, for aid-delivery purposes, data derived from grid cells via satellite imagery is crucial for understanding the population landscape of Lebanon.

Thinking counterfactually, and striving to find comparisons to test claims like *"we shouldn't conduct another census since it would spark a civil war"*, we can also look at Nigeria, where a history book like Eghosa Osaghae's [*Crippled Giant: Nigeria Since Independence*](https://www.dropbox.com/scl/fi/4e2kxfhpfks4j25obamaj/Crippled-giant-_-Nigeria-since-independence.pdf?rlkey=m4pjscx0t8v78vbfyfniu3xco&dl=1) has a section on "The Census Crisis" of 1963 as an early catalyst for [Civil War](https://en.wikipedia.org/wiki/Nigerian_Civil_War) 4 years later.

### The Data Lake Infrastructure

With the choice of this particular data motivated in the previous section, here the link with the DSAN 6000 material comes from **how this data is stored**: CEISIN updates the data each month,  **Data Lake pattern**

## HW6 Submission

Since you submitted your GitHub URL all the way up at the top of the instructions, all that is left is for you to **push your work from EC2 to GitHub**. If you push a commit with the commit message **"Final submission"** (by running `git commit -m "Final submission"` and then `git push`), we will consider your repo ready to grade – otherwise, if no commit with this message is found, we will consider the **most recent commit when the due date is reached** to be your final submission.

---

Assignment hash (SHA-256): `856ca8e65743d5d34d76c8d7022624c0037ae5ffab8c943af0aeb631dfea8187`
