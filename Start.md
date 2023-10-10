Getting started ​
Automatic (recommended) ​

husky-init is a one-time command to quickly initialize a project with husky.


npm

pnpm

yarn

bun
shell
npx husky-init && npm install
It will:

Add prepare script to package.json
Create a sample pre-commit hook that you can edit (by default, npm test will run when you commit)
Configure Git hooks path
To add another hook use husky add. For example:

shell
npx husky add .husky/commit-msg 'npx --no -- commitlint --edit "$1"'
INFO
For Windows users, if you see the help message when running npx husky add ..., try node node_modules/husky/lib/bin add ... instead. This isn't an issue with husky code.

Manual ​

Install ​
Install husky
shell
npm install husky --save-dev
Enable Git hooks
shell
npx husky install
To automatically have Git hooks enabled after install, edit package.json
shell
npm pkg set scripts.prepare="husky install"
You should have:


package.json
json
{
  "scripts": {
    "prepare": "husky install" 
  }
}
INFO
Yarn 2+ doesn't support prepare lifecycle script, so husky needs to be installed differently (this doesn't apply to Yarn 1 though). See Yarn 2+ install.

Create a hook ​

To add a command to a hook or create a new one, use husky add <file> [cmd] (don't forget to run husky install before).

shell
npx husky add .husky/pre-commit "npm test"
git add .husky/pre-commit
Try to make a commit

shell
git commit -m "Keep calm and commit"
If npm test command fails, your commit will be automatically aborted.

WARNING
Using Yarn to run commands? There's an issue on Windows with Git Bash, see Yarn on Windows.

For Windows users, if you see the help message when running npx husky add ..., try node node_modules/.bin/husky add ... instead. This isn't an issue with husky code and is fixed in recent versions of npm 8.

Uninstall ​
shell
npm uninstall husky && git config --unset core.hooksPath
Yarn 2 ​

Install ​
Install husky
shell
yarn add husky --dev
yarn add pinst --dev # ONLY if your package is not private
Enable Git hooks
shell
yarn husky install
To automatically have Git hooks enabled after install, edit package.json

package.json
js
{
  "private": true, // ← your package is private, you only need postinstall
  "scripts": {
    "postinstall": "husky install"
  }
}
TIP
if your package is not private and you're publishing it on a registry like npmjs.com, you need to disable postinstall script using pinst**. Otherwise, postinstall will run when someone installs your package and result in an error.


package.json
js
{
  "private": false, // ← your package is public
  "scripts": {
    "postinstall": "husky install",
    "prepack": "pinst --disable",
    "postpack": "pinst --enable"
  }
}
Uninstall ​
Remove "postinstall": "husky install" from package.json and run:

shell
yarn remove husky && git config --unset core.hooksPath
Previous page
Introduction
Next page
Guide
