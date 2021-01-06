# Claim Your Username

When new platforms launch, we rush to claim our monikers but sometimes find that they have been taken. We are giving as many people as possible the chance to claim their usernames before the MakeOS mainnet launches. 

We have created an easy to use utility that will allow you to reserve personal or organization usernames you own on Github, GitLab and Bitbucket. 

## How to Claim a Username

* Go to [https://makeos.org](https://makeos.org). You will see a widget that asks for your profile URL. It accepts personal or organization URLs from GitHub, GitLab and Bitbucket. 

![](../.gitbook/assets/screen-shot-2020-12-02-at-4.38.14-pm.png)

* After providing your profile URL, you must create an empty repository in the profile account with a name matching the unique 6 characters code generated for you.  This step allows us to verify that you own the account. 

![Example: Creating a repository with the unique code as its name](../.gitbook/assets/screen-shot-2020-12-02-at-4.43.06-pm.png)

* After creating the repository, click **"Verify & Claim"**. 
* Upon successful verification, a modal is displayed with a success message and a link to download your claim signature. Click the **"Download Signature"** button to download your claim signature. 

![](../.gitbook/assets/screen-shot-2020-12-04-at-4.30.39-pm%20%282%29.png)

* The claim signature gives you the power to claim the username when the mainnet launches. During a _claiming window_, you will be asked to provide the signature in other to claim the username.  

{% hint style="warning" %}
**Please keep your signature safely and never share it**. Anyone with the signature can claim the associated username.  
{% endhint %}

## Claim Public Key

This is the Ed25519 public key that will be used to verify all claim signatures. 

```text
9407311fef2336cc57044b44a55714a5b30b22b951e3b549704c12c39396067d
```

### Verify

The example below describes how to verify a signature:

```javascript
const publicKey = "9407311fef2336cc57044b44a55714a5b30b22b951e3b549704c12c39396067d"
const namespace = <check claim.sig>
const signature = <check claim.sig>
verifyEd25519(publicKey, namespace, signature)
```



