## Bitbucket to Github Migration - forked

This repository copies ALL of your personal/organizational Bitbucket repositories to your Github account or organization while maintaining its privacy status.

### Changes made in the fork

1. Improved logging for clearer visibility into what's happening during the process.

- Including the start and stopping of the main functions within index.js.
- Outputting the non-sensitive dotenv vars as they are processed to notify the engineer if variables are not instantiating. (My experience.)
- Summary for each step in the process along with a final summary at the end. As a bonus, any failed bitbucket repositories will be listed at the end with links back to them in bitbucket.
- Normalized all the verbiage and naming to be very consistent. IE: repos is now repository (for increased visibility)
- Prefixed each status log with either BITBUCKET or GITHUB so the engineer knows where it is originating.

2. Optional dotenv variables for organization (Bitbucket Organization and Github Teams) Eventually this will be created into a setting (PR's welcome!! ;-).

3. Yarn usage instead of npm -i instruction.
4. Testing dotenv flag to only test a subset of repos.
5. Pragmatic improvement to the github repo creation. This script now checks first if a repo has already been created and will not try to create it again.

### Requirements

1. Node
2. Yarn
3. `yarn install`
4. Create bitbucket app password: https://confluence.atlassian.com/bitbucket/app-passwords-828781300.html _TIP: Bitbucket 2.0 api does not work well with two factor authentication so turn this off temporarily and use the app password with full rights. ('write' on all functions)_
5. Create github access token for your account: `https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/`
6. Save the .env.sample as a new file named: .env (\$ cp .env.sample .env) and then follow the instructions next to each variable.

### General Process Explained

The steps below is how each sequential repository gets processed individually.

#### Duplicating a Bitbucket repository to Github a Single Time

1. `cd repositories/ && mkdir archive-client_admin && cd archive-client_admin/`
2. `git clone --mirror https://bitbucket.com/amu_technology/archive-client_admin.git`
3. `cd archive-client_admin.git`
4. `git push --mirror https://abarrows:$GITHUB_TOKEN@github.com/abarrows/archive-client_admin.git`

5. OPTIONAL CLEANUP:`cd ../../ && rm -rf archive-client_admin`

#### Mirroring a Bitbucket repository to Github

1. `git clone --mirror https://bitbucket.com/amu_technology/repository-to-mirror.git`
2. `cd repository-to-mirror.git`
3. `git remote set-url --push origin https://github.com/Andrews-McMeel-Universal/mirrored`
4. `git fetch -p origin`
5. `git push --mirror`

##### Run the script

```javascript
`node index.js`;
```

## TODOS

1. Wrap all console logs into a verbose flag.
2. Add optional flag for "mirroring/syncing" a repo to both bitbucket and github.
3. Improve the failsafes for operations that have already occurred.
4. Potentially use GM's node service worker prototype to visually represent this utility.
5. Add back in the dotenv.config() so variables are not required during the command line script.
6. Add functionality to cleanup repos after processing.

## Resources

1. Github Instructions on this topic: https://help.github.com/en/github/importing-your-projects-to-github/importing-a-git-repository-using-the-command-line
2. GUI Importer for failed repositories: https://help.github.com/en/github/importing-your-projects-to-github/importing-a-repository-with-github-importer
