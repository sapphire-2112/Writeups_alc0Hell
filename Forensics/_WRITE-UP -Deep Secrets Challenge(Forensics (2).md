#  **WRITE\_UP \-Deep Secrets Challenge(**

I was given a file named `deep_secrets.zip`. At first glance, it looked like a simple archive… but this is a CTF, so there had to be a trick.

---

### **🔍 Step 1: Checking the File**

Instead of just assuming it’s a zip, I ran:

`file deep_secrets.zip`

The output showed that it’s actually an **audio file**. Definitely not a zip.

---

### **🎭 Step 2: Fixing the Extension**

Since it was audio, I renamed it properly:

`mv deep_secrets.zip deep_secrets.wav`

Now it could be opened in any audio software.

---

### **🎶 Step 3: Opening the Audio**

I loaded the file in **Sonic Visualizer** (Audacity would also work). Switching to spectrogram mode made it pretty clear what was going on — the signal looked like **Morse code**.

---

### **📡 Step 4: Reading the Code**

The audio pattern translated like this:

* Short beep (high pitch, small length) → Dot (`.`)

* Long beep (high pitch, long length) → Dash (`-`)

* Silence → Space between letters

Converting the Morse sequence revealed the hidden message.

---

### **🏁 Final Flag**

The decoded flag was:

`flag{s1gn4ls_fr0m_th3_d33p}`

