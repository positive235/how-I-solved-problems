# How I Solved Problems

## Contents

1. [Create React App does NOT work](#1-create-react-app-does-not-work)
2. [GitHub Markdown Same Page Link](#2-github-markdown-same-page-link)
3. [virtualenv and django installation on Mac](#3-virtualenv-and-django-installation-on-mac)
4. [How to deploy react app to Github pages](#4-how-to-deploy-react-app-to-github-pages)
  
## 1. Create React App does NOT work

### Feb 28, 2021

- Problem: 
  - I have previously installed create-react-app globally via `npm install -g create-react-app`

- Suggested Solutions: 
  - To uninstall the package using `npm uninstall -g create-react-app` or `yarn global remove create-react-app` to ensure that npx always uses the latest version.
  - Or, If using npm 5.1 or earlier, you can't use npx. Instead, you can install create-react-app globally by `npm install -g create-react-app` and run by `create-react-app my-app`
    - Reference(https://gist.github.com/gaearon/4064d3c23a77c74a3614c498a8bb1c5f) 

- Results: Both did not work.
  - Errors in uninstalling the package using `npm uninstall -g create-react-app`
  - `create-react-app my-app` did NOT provide the templates. 

- **Solved the problem by `npx create-react-app@latest your-project-name --use-npm`**
  - Reference(https://stackoverflow.com/questions/64963796/create-react-app-is-not-working-since-version-4-0-1) 

## 2. GitHub Markdown Same Page Link

### Feb 28, 2021

```
## Title

### Place 1

Hello, this is some text to fill in this, [here](#place-2), is a link to the second place.

### Place 2

Place one has the fun times of linking here, but I can also link back [here](#place-1).

### Place's 3: other example

Place one has the fun times of linking here, but I can also link back [here](#places-3-other-example).

```
- Summary of the conversion rules:
  - Punctuation marks will be dropped
  - Leading White Spaces will be dropped
  - Upper Case will be converted to Lower
  - Spaces between letters will be converted to `-`

- Reference(https://stackoverflow.com/questions/27981247/github-markdown-same-page-link)

## 3. virtualenv and django installation on Mac

### Mar 26, 2021
 
### Problem: Error “virtualenv : command not found” but install location is in PYTHONPATH

 I installed virtualenv on my Macbook using `pip install virtualenv`. But when I try to create a new virtualenv using virtualenv venv, I get the error saying "virtualenv : command not found".

- Try 1: `python -m virtualenv venv` ----> this virtual env couldn't install django@3.1.7...

1. `python -m virtualenv venv`
2. `source venv/bin/activate`

- Reference
  - https://stackoverflow.com/questions/39964635/error-virtualenv-command-not-found-but-install-location-is-in-pythonpath/39977369
  - https://docs.python-guide.org/dev/virtualenvs/   

- **Solved the problem by `python3 -m venv environment_name`**  ---> This virtual env could install django@3.1.7 (By `pip install django==3.1.7`)

1. `python3 -m venv environment_name`
2. `source environment_name/bin/activate`

```
Instead of using brew you can simply use "venv".

To create a virtual environment you can run --> python3 -m venv environment_name

**Activation of Virtual Environment : source environment_name/bin/activate

**Deactivation : deactivate
```

(Reference: https://stackoverflow.com/questions/55482197/how-to-correctly-install-python3-and-virtualenv-on-macos-mojave)

## 4. How to deploy react app to Github pages

### May 2, 2021

- Reference 1: https://dev.to/yuribenjamin/how-to-deploy-react-app-in-github-pages-2a1f
- Reference 2: https://create-react-app.dev/docs/deployment/#github-pages

1. 
```
cd my-app
npm install gh-pages --save-dev
```
2. Add properties to `package.json` file. 
   The first property: `"homepage": "https://{username}.github.io/{repo-name}"`
   In the "scripts" property, add `"predeploy": "npm run build`, `"deploy": "gh-pages -d build"`
   
   For example,
```
{
  "homepage": "https://{username}.github.io/{repo-name}",
  "name":...
  "version": ...
  "private": ...
  "dependencies":...
  "scripts": {
    //...
    "predeploy": "npm run build",
    "deploy": "gh-pages -d build"
}
  
```

3. `npm run deploy`
