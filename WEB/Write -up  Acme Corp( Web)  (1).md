# **Write \-up  Acme Corp( Web)** 

We were given an old Acme Corp website to explore and told the flag was broken into five parts hidden around the site. The goal was to track down each piece and put them back together.

### **Step 1: Checking the Page Source**

The first thing I did was open the page source. Inside an HTML comment, I found the first clue:

`Part 1/5 = S3GM`

### **Step 2: Looking at the CSS**

Next, I checked the stylesheet (`style.css`). At the bottom, there was a developer’s note:

`[2/5]-3NT_`

That gave us the second part: **3NT\_**.

### **Step 3: Digging in JavaScript**

The site also loaded a `app.js` file. It had some fake hints, but one comment stood out. It said the fragment was written backwards:

`'3R0F' reversed`

Flipping it gave the third piece: **F0R3**.

### **Step 4: Robots.txt**

Then I opened `/robots.txt`. Along with the usual disallowed directories, there was another note:

`[4/5]-NS1C`

That’s the fourth piece: **NS1C**.

### **Step 5: Finding Legacy Files**

Since the challenge mentioned “old website stuff,” I tried directory brute-forcing with **ffuf**. This uncovered a hidden `.htaccess` file, which contained:

`[5/5]-S`

That gave us the final part: **S**.

### **Final Flag**

Putting all the parts together in order:

`S3GM + 3NT_ + F0R3 + NS1C + S`

The final flag is:

**flag{S3GM3NT\_F0R3NS1CS}**

### **What I Learned**

* Always check the page source — comments can hide useful info.

* CSS and JavaScript files sometimes contain leftover dev notes.

* Robots.txt can point to interesting paths.

* Directory brute-forcing is key to finding hidden files like `.htaccess`.

* Not every hint in the code is real — look for the ones that make sense.

