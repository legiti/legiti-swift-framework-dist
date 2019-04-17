# Inspetor Swift Distribution

This public repository contains the compiled Swift framework for the Inspetor mobile antifraud. If you're reading this, either you're devving on this project (good) or something is broken and you're lost (bad!). Either way, chat with Pearson!

### Publishing
After compiling the Framework in the private repo, move over to this repo and follow these steps:
- `git add .`
- `git commit -m '<an informative message here>'
- `git push origin master`
- `git tag -a <version> -m "<what changed?>"`
- `git push origin --tags`

Then, you will need to update the Podspec version (currently the podspec is listed in the private repo) and push the updated podspec to the Inspetor podspec repo: `pod repo push inspetor InspetorSwiftFramework.podspec` (If you have not already added the Inspetor podspec repo to your local podspec repos, you can do so via `pod repo add inspetor git@github.com:inspetor/inspetor-podspecs.git`)
