Always start by ensuring that your system has the correct timezone and time set.

There are two important things:
- Proxy category (number)
- Port number (always `3128`)

The proxy category number can be found in the table below.

### Proxy Table (also available in HPC-IITD supercomputing website)

Users can check their authorized proxy from the table below and use it accordingly while accessing the internet on HPC.

| Category | faculty | retfaculty | phd | mtech | btech | dual | integrated | staff | irdstaff | mba | mdes | msc | msr | pgdip | diit | research |
|----------|---------|------------|-----|-------|-------|------|------------|-------|----------|-----|------|-----|-----|--------|------|----------|
| Proxy    | 82      | 82         | 61  | 62    | 22    | 21   | 21         | 21    | 21       | 21  | 21   | 21  | 21  | xen03  |      |          |


---
The following will work for everyone. Just need to use appropriate Proxy category (number).
## 1. System-wide Proxy (GUI)

There are three ways to configure this (pick **one**):

### Option 1: Manual configuration
1. Go to **Settings → Network → Network Proxy**
2. Turn on **Network Proxy**
3. Choose **Manual** from the *Configuration* panel
4. Set the following:
   - **HTTP Proxy**: `proxy61.iitd.ac.in`  
     **Port**: `3128`
   - **HTTPS Proxy**: `proxy61.iitd.ac.in`  
     **Port**: `3128`
   - **Ignore hosts**: `localhost,127.0.0.1`

### Option 2: Automatic configuration
1. Go to **Settings → Network → Network Proxy**
2. Turn on **Network Proxy**
3. Choose **Automatic** from the *Configuration* panel
4. Enter:
http://www.cc.iitd.ac.in/cgi-bin/proxy.phd

### Option 3: Browser-based configuration: so you can access internet in your browser
1. Open your preferred browser
2. Go to **Settings** and search for **proxy**
3. Open the system proxy settings window
4. Choose one of the following:
- Use system proxy settings
- Automatic proxy configuration URL: proxy61.iitd.ac.in/cgi-bin/proxy.cgi
- You could also select Manual proxy configuration. Just enter HTTP and HTTPS details and port in this case

Once done, go to `https://proxy61.iitd.ac.in/cgi-bin/proxy.cgi` enter your kerberos id (not your entery number), password, and login. Leave this page open and browse the internet on other tabs or browsers. Once done browsing, logout. 

---

## 2. Terminal Proxy (for  wget etc.): so that you can install external libraries/packages etc through your terminal 

Append the following lines to your `~/.bashrc` file:

```bash
export http_proxy=http://proxy61.iitd.ac.in:3128
export https_proxy=http://proxy61.iitd.ac.in:3128
export HTTP_PROXY=http://proxy61.iitd.ac.in:3128
export HTTPS_PROXY=http://proxy61.iitd.ac.in:3128
export no_proxy=localhost,127.0.0.1
```
### why my `sudo apt update` won't work?
That's because sudo doesn't pass the environment variables by default. Need to configure apt to use the proxy. 
```bash
sudo nano /etc/apt/apt.conf.d/95IIT-Delhi-apt-Proxy
```
Don't think too much about the filename `95IIT-Delhi-apt-Proxy`. Just choose any file name ensure to have a number as a prefix. You can name it 95-my-proxy or whatever you like.

Then
Add these lines:
```bash
Acquire::http::Proxy "http://proxy61.iitd.ac.in:3128";
Acquire::https::Proxy "http://proxy61.iitd.ac.in:3128";
```
