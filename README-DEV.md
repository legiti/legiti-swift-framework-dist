# Legiti Swift Distribution

This public repository contains the compiled Swift framework for the Legiti mobile antifraud. If you're reading this, either you're devving on this project (good) or something is broken and you're lost (bad!). Either way, chat with Pearson!

### Private Publishing
After compiling the Framework in the private repo, move over to this repo and follow these steps:
- `git add .`
- `git commit -m "<an informative message here>"`
- `git push origin master`
- `git tag -a <version> -m "<what changed?>"`
- `git push origin --tags`

Then, you will need to update the Podspec version (currently the podspec is listed in the private repo) and push the updated podspec to the Legiti podspec repo: `pod repo push legiti Legiti.podspec` **(Remeber to update the version number in th e Legiti.podspecs (located in the legiti-ios repo) before doing the pod repo push)** (If you have not already added the Legiti podspec repo to your local podspec repos, you can do so via `pod repo add legiti git@github.com:legiti/legiti-podspecs.git`)

### Public Publishing
To publish our Framework in the Cocoapods Specs repo you need to follow this steps:
- Do all the steps in the private publishing tutorial
- Update the Legiti.podspec to the new version
- `pod trunk push Legiti.podspec`
