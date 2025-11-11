# Git Push Configuration

## By Steven Correa @stevencorrea
November 10th, 2025

### Goals
My goal was to push a new feature branch to the remote repository following a standard Git workflow. I expected this to be a quick operation that would allow me to share my work and create a pull request.

### Introduction
This video gives a brief introduction to `git` and provides some context around the workflow discussed in the interation section below.


https://github.com/user-attachments/assets/3e923e57-856d-4d0e-bb20-c2a746df35ee


### The Interaction
Working through my typical workflow: checkout a new branch, make changes, commit, and push, I encountered a common point of friction. After committing my changes, I executed git push and received an error message stating that no upstream branch was configured. The system required me to manually set the remote tracking branch using git push --set-upstream origin <branch-name>.
This interaction highlighted a significant issue with Git's **discoverability** (_the degree to which users can figure out what actions are possible and how to perform them_). The error message did provide the exact command needed, demonstrating good **feedback** (_information returned to the user about the results of their action_). However, this feedback only addresses the immediate problem, not the underlying workflow inefficiency.
The core issue relates to my **mental model** (_my understanding of how the system should work based on my goals and expectations_). My mental model assumes that when I push a new branch, Git should automatically create the corresponding remote branch. The system's actual behavior creates an **action gap** (_the gap between my intentions and the actions required to achieve them_), forcing an extra command for every new branch.


https://github.com/user-attachments/assets/56f94e7b-056c-435b-8f54-5aa607a1eeb2


### Outcome
While I could continue copying and pasting the command from the output, this represents poor efficiency and introduces unnecessary cognitive load. It is also inconsistant across Operating Systems and terminal emulators. The repeated need for this command suggests a misalignment between the system's default configuration and a _very_ common user workflow.

I implemented two configuration changes to resolve this:

```bash
git config --global push.default current
git config --global push.autoSetupRemote true
```
The first setting tells Git to push the current branch to a remote branch with the same name. The second automatically sets up remote tracking when pushing a new branch. Together, these configurations align Git's behavior with my mental model, eliminating the action gap.


https://github.com/user-attachments/assets/a682c7cc-632b-4e1f-8b1b-30291b95581e


### Assessment
Strengths: Git's error messages provide clear, actionable feedback with the exact command needed to resolve the issue. The system is highly configurable, allowing users to customize behavior to match their workflow.

Weaknesses: The default configuration creates unnecessary friction for such a common workflow. More critically, these configuration options have poor discoverability for a solution outside of the current working branch configuration.

Recommended Improvement: Git could improve this experience by detecting repeated use of --set-upstream and proactively suggesting the push.autoSetupRemote configuration option, similar to how it suggests adding files to .gitignore. This would transform a pain point into a learning opportunity, helping users discover configuration options that improve their workflow efficiency.
