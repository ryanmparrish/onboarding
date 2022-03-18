# Adobe Engineer Onboarding

 - AdobeId/SSO - Jennifer Funkhouser-Smith
	 - Okta Verify - https://adobe.okta.com/app/UserHome
	 - VPN - global protect
	 - iam.corp.adobe.com
	   - groups [confluence, consonant](https://wiki.corp.adobe.com/display/adobedotcom/Consonant+for+Adobe.com)
	 - [OneDrive/SharePoint](https://adobe.service-now.com/sc?id=kb_article&sysparm_article=kB0014372) 
	 - Slack
	   - add to channels. (#dexter-devs, #dexter-friends, #consonant_general, ...)
	 - Outlook
	 - Teams
	 - Jira
	 - Git:
		Dexter repo: Chris Millar / Ryan Clayton
		Adobe Consonant: Chris Millar / Ryan Clayton
Any git repo, go to the corresponding engineering manager. This info is listed on the team roster.

## Other useful Dexter links: 

https://wiki.corp.adobe.com/display/BaaP/Dexter+Home  
https://wiki.corp.adobe.com/display/BaaP/Dexter+Engineering

## WCMS Environments: 

Dexter and other env Dev, QA, etc. - Send a joint email to Audi and Jim Jones. 
https://wiki.corp.adobe.com/display/WCMSOps/WCMS+Ops+Home  
 
For all Con, Stage and Prod environments: Talk to Jim Jones. 
For Dev / QA: Talk to Audi
Or access the team roster wiki to talk to the right dev / qa person: 
https://wiki.corp.adobe.com/display/adobedotcom/Team+Roster  

## URL Access

 - get authorization and VPN group whitelisted for the following urls. https://auth.services.adobe.com/en_US/deeplink.html#/. Likely more...
 - https://dexter-author.lab02.corp.adobe.com/
 - https://dexter-author.qa01.corp.adobe.com/
 - https://dexter-author.dev01.corp.adobe.com/
 - https://cc-author.stage.corp.adobe.com/

### Terminal

- homebrew `3.5`
  - `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
- [node](https://nodejs.org/en/download/) `14`
  - `brew install node@14`
- [java JDK 8](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Fgeneral%2Fpublic%2Fazul-zulu-jdks%2F8u322%2Fzulu8.60.0.22-sa-jdk8.0.322-macosx_x64.zip)
- Maven
  - `brew install maven@3.5`
- ImageMagick
  - `brew install imagemagick`

building dexter •	https://git.corp.adobe.com/Dexter/dexter

### Tools
Harvest
Spectacle
Clipy

### GIT
Create your own https://git.corp.adobe.com/ user. 
Fork the dexter repo from https://git.corp.adobe.com/Dexter/dexter and set up your @username/dexter fork w/ develop and feature branches as needed. 

Add your work machine [SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) to your github corp and/or personal account.  

## Helix
Helix is a pretty easy set up. https://www.hlx.live/

Install the cli `sudo npm install -g @adobe/helix-cli` and run `hlx up` on a configured helix site. 
[See the tutorial for details](https://www.hlx.live/tutorial) 

FYI: I have helix work on my own personal github acct. for now. I need to follow up on best practice for contribution structure. 
aka. https://main--acom-kit--ryanmparrish.hlx.page/consonant-gallery

## AEM dev setup

Please read the [Dexter Engineering](https://wiki.corp.adobe.com/display/BaaP/Dexter+Engineering) documents

## Docs
https://spectrum.adobe.com/

https://consonant.adobe.com/

https://wiki.corp.adobe.com/


### System files for dev env.

`.m2/settings.xml`

Fill out <LDAP> with username && <Password> w/ artifactory API

---
`.npmrc`

In my project I have a few scoped internal repositories for NPM packages

@dexter:registry=https://artifactory.corp.adobe.com/artifactory/api/npm/npm-dexter-release/
@marketingtech:registry=https://artifactory.corp.adobe.com:443/artifactory/api/npm/npm-adobe-release/
@northstar:registry=https://artifactory.corp.adobe.com:443/artifactory/api/npm/npm-northstar-release/
@react:registry=https://artifactory.corp.adobe.com:443/artifactory/api/npm/npm-react-release/
@spectrum:registry=https://artifactory.corp.adobe.com:443/artifactory/api/npm/npm-spectrum-release/

As I came into work after the holiday I was getting 404’s on all of them.

Up to this point I had a simple ~/.npmrc:

_auth = {user:apiKey =>Base64}
always-auth = true
email = {email address}

I discovered through my adventure simple “LDAP based auth” is no longer supported. Something I would have probably known if I kept up better on my all the email I get.

Each scoped entry in your project .npmrc must have an entry in your ~/.npmrc file for authentication. This must be done with npm login. And, each repeated effort will append to the existing ~/.npmrc file.

e.g.

The project .npmrc entry
@dexter:registry=https://artifactory.corp.adobe.com/artifactory/api/npm/npm-dexter-release/

Requires that you run in in your “user” directory (~/):
npm login --registry=https://artifactory.corp.adobe.com/artifactory/api/npm/npm-dexter-release/ --always-auth

Which will ask you:

user: {your adobe username}
password: {your Artifactory Profile : Authentication Settings : API Key}
email: {your email address}

Rinse and repeat.

The outcome of this process, when successful, are entries in your ~/.npmrc file, which look something like

//artifactory.corp.adobe.com/artifactory/api/npm/npm-dexter-release/:_authToken={SUPER LONG HASH GENERATED BY npm login}
//artifactory.corp.adobe.com/artifactory/api/npm/npm-react-release/:_authToken={SUPER LONG HASH GENERATED BY npm login}

---

`.zshrc` ex.

```
# Path to your oh-my-zsh installation.
export ZSH="$HOME/.oh-my-zsh"



# Which plugins would you like to load?
# Standard plugins can be found in $ZSH/plugins/
# Custom plugins may be added to $ZSH_CUSTOM/plugins/
# Example format: plugins=(rails git textmate ruby lighthouse)
# Add wisely, as too many plugins slow down shell startup.
plugins=(
	git
	zsh-autosuggestions
	zsh-syntax-highlighting
)

source $ZSH/oh-my-zsh.sh

# User configuration

export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_311.jdk/Contents/Home/
export M2_HOME=/usr/local/share/maven
export M2=$M2_HOME/bin
export PATH=$M2:$PATH
export PATH="/opt/homebrew/opt/node@14/bin:$PATH"
export PATH="/opt/homebrew/opt/maven@3.5/bin:$PATH"

alias brewup="brew update; brew upgrade; brew cleanup; brew doctor"

alias aemstart='cd ~/Sites/AEM/6.5-dexter/crx-quickstart/bin && ./start'
alias aemstop='cd ~/Sites/AEM/6.5-dexter/crx-quickstart/bin && ./stop'
alias aemlog='tail -f ~/Sites/AEM/6.5-dexter/crx-quickstart/logs/error.log'
alias buildall='mvn clean install -Pmonolith,install-combined'
alias buildallfast='mvn clean install -Pmonolith,install-combined -DskipTests=true -Dskip.npm'
alias buildeverything='mvn clean install -Peverything,install-combined'
alias buildeverythingfast='mvn clean install -Peverything,install-combined -DskipTests=true -Dskip.npm'
alias buildui='mvn clean install -Pinstall-dexterUI-package'
alias builduifast='mvn clean install -Pinstall-dexterUI-package -DskipTests=true -Dskip.npm'

```


